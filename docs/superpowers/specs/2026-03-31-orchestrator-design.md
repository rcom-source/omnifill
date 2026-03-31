# Omnifill Orchestrator — Design Spec

Date: 2026-03-31

## Problem

7 omnifill rigs with 36 crew workspaces share a single Anthropic API capacity.
Work needs to be dispatched efficiently, respecting throttle signals, DAG-based
role dependencies within each rig, and surviving rig restarts.

## Overview

A Dolt-backed, beads-driven orchestrator that dispatches work across omnifill
rigs. It uses adaptive concurrency control with automatic ceiling discovery to
maximize throughput, and supports per-rig DAG-based role pipelines.

## Architecture

Three components:

### 1. Queue Manager

Watches for new beads tagged with rig/role assignments. Resolves DAG
dependencies to determine which tasks are dispatchable.

- Polls Dolt for beads with `status=open` and an assigned rig+role
- Checks the rig's pipeline DAG to see if upstream dependencies are complete
- Marks dispatchable tasks as `ready`

### 2. Dispatcher

Pulls dispatchable tasks and calls `gt sling` to spawn polecats. Tracks
active sessions.

- Dispatches up to `current_max_concurrency` tasks at once
- Records `dispatched_at` timestamp for each task
- Monitors active polecat sessions via `gt polecat list`

### 3. Backpressure Controller (Auto-Scaling)

Automatically discovers and maintains optimal concurrency.

**Startup probe:**
1. Start with 1 concurrent task
2. Double concurrency each cycle (1 → 2 → 4 → 8 → 16...) as long as tasks
   complete within normal duration
3. When first slowdown detected (task duration > 1.5x baseline), record that
   as the **ceiling**
4. Set operating concurrency to `ceiling * 0.8` (headroom)

**Steady-state adaptation:**
- Every N completions, probe by adding +1 above current max
- If probe task completes normally → raise ceiling, increase operating concurrency
- If probe task is slow → ceiling holds, back off to `current * 0.8`
- Baseline duration recalculated as rolling average (last 20 completions),
  adapts to changing task complexity

**Crash recovery:**
- Last known ceiling stored in Dolt (`orchestrator_state` table)
- On restart, start at `last_ceiling * 0.5` (conservative) and re-probe upward

## State Schema (Dolt)

### orchestrator_queue

| Column | Type | Description |
|--------|------|-------------|
| id | VARCHAR(36) | Primary key (UUID) |
| bead_id | VARCHAR(64) | Reference to the beads issue |
| rig | VARCHAR(64) | Target rig (e.g., omnifill_first_mile) |
| role | VARCHAR(32) | Target crew role (e.g., researcher) |
| status | ENUM | pending, ready, dispatched, complete, failed |
| depends_on | JSON | Array of role names this task depends on (within same rig) |
| polecat_id | VARCHAR(64) | Polecat identifier once dispatched |
| created_at | TIMESTAMP | When queued |
| dispatched_at | TIMESTAMP | When sent to polecat |
| completed_at | TIMESTAMP | When finished |
| duration_ms | BIGINT | Completion time in milliseconds |

### orchestrator_config

| Column | Type | Description |
|--------|------|-------------|
| rig | VARCHAR(64) | Primary key |
| pipeline_dag | JSON | Role dependency graph |
| max_concurrency_override | INT | Per-rig ceiling override (nullable) |
| enabled | BOOLEAN | Whether orchestrator manages this rig |

### orchestrator_metrics

| Column | Type | Description |
|--------|------|-------------|
| id | VARCHAR(36) | Primary key |
| rig | VARCHAR(64) | Rig name |
| role | VARCHAR(32) | Role name |
| start_time | TIMESTAMP | Dispatch time |
| end_time | TIMESTAMP | Completion time |
| duration_ms | BIGINT | Task duration |
| tokens_used | BIGINT | Tokens consumed (if detectable) |
| was_probe | BOOLEAN | Whether this was a concurrency probe task |

### orchestrator_state

| Column | Type | Description |
|--------|------|-------------|
| key | VARCHAR(64) | Primary key |
| value | TEXT | JSON-encoded value |

Singleton keys:
- `current_max_concurrency` — Current operating concurrency
- `discovered_ceiling` — Last discovered ceiling
- `last_probe_at` — Timestamp of last concurrency probe
- `completions_since_probe` — Counter for probe interval
- `rolling_avg_duration_ms` — Current baseline
- `paused` — Whether dispatching is paused

## Pipeline DAG Configuration

Per-rig config stored in `orchestrator_config.pipeline_dag` and also loadable
from JSON files at `config/pipelines/<rig>.json`.

Example for `omnifill_first_mile`:

```json
{
  "researcher": [],
  "architect": ["researcher"],
  "product_manager": ["researcher"],
  "ml_engineer": ["architect"],
  "developer": ["architect", "ml_engineer"],
  "validation_engineer": ["developer"]
}
```

A role is dispatchable when ALL of its listed dependencies have completed for
that rig's current work cycle.

### DAG Validation

On config load, validate:
- No cycles (topological sort must succeed)
- All referenced roles exist as crew members in the rig
- No orphan roles (every role in the rig appears in the DAG)

## Bead Tagging Convention

The orchestrator identifies work by two fields on a bead:
- **Rig:** The `--rig` flag on `bd create` (routes to the correct beads database)
- **Role:** The `--assignee` field, set to the crew role name (e.g., `researcher`, `architect`)

The orchestrator scans for beads where `assignee` matches a known crew role
and `status=open`. This is the trigger for queuing.

## Workflow

1. User files a bead: `bd create --rig omnifill_first_mile "Research multi-modal freight APIs" --assignee=researcher`
2. Queue Manager detects new bead with assignee matching a crew role
3. Checks DAG — researcher has no deps → status set to `ready`
4. Dispatcher checks capacity — active sessions < max_concurrency → dispatches via `gt sling`
5. Backpressure controller records dispatch time
6. On completion, marks task complete, records duration in metrics
7. Queue Manager checks if downstream roles (architect, product_manager) are now unblocked
8. Newly unblocked roles marked `ready`, dispatcher picks them up if capacity allows

## CLI Commands

```bash
omnifill-orch status                          # Queue depth, active sessions, concurrency level, ceiling
omnifill-orch pause                           # Stop dispatching (active tasks drain)
omnifill-orch resume                          # Resume dispatching
omnifill-orch pipeline show <rig>             # Show DAG config for a rig
omnifill-orch pipeline set <rig> <file.json>  # Update DAG from file
omnifill-orch pipeline validate <rig>         # Validate DAG (cycle detection, role existence)
omnifill-orch history [--rig <rig>]           # Recent completions with duration
omnifill-orch metrics                         # Concurrency trends, avg durations, probe history
omnifill-orch reset-ceiling                   # Force re-probe of concurrency ceiling
```

## Runtime

Cron-based, runs every 30 seconds:

1. Read queue from Dolt
2. Detect completed/failed tasks (cross-reference `gt polecat list`)
3. Record metrics for completed tasks
4. Update backpressure controller (adjust concurrency if needed)
5. Resolve DAG dependencies → mark newly ready tasks
6. Dispatch ready tasks up to concurrency limit
7. Write all state changes back to Dolt

### Orphan Detection

On each cycle, cross-reference `orchestrator_queue` (status=dispatched) with
`gt polecat list`. If a dispatched task has no running polecat:
- If polecat completed (branch merged or closed) → mark complete
- If polecat gone with no result → mark failed, re-queue

## Recovery

On startup after crash/restart:
1. Read all state from Dolt
2. Set concurrency to `last_ceiling * 0.5`
3. Detect orphaned dispatches → re-queue or mark complete
4. Resume normal dispatch cycle
5. Re-probe upward to rediscover ceiling

## Technology

- **Language:** Python (faster iteration, good Dolt/MySQL client support)
- **State:** Dolt via MySQL protocol (port 3307, already running)
- **Scheduling:** System cron or systemd timer (30-second interval)
- **Dependencies:** `pymysql` for Dolt, `subprocess` for `gt`/`bd` CLI calls

## File Structure

```
src/orchestrator/
  __init__.py
  main.py              # Entry point (cron invocation)
  queue_manager.py     # Bead watching, DAG resolution
  dispatcher.py        # gt sling calls, session tracking
  backpressure.py      # Adaptive concurrency controller
  db.py                # Dolt connection and table operations
  cli.py               # CLI commands (omnifill-orch)
  models.py            # Data classes for queue items, config, metrics
config/
  pipelines/           # Per-rig DAG JSON files
    omnifill_first_mile.json
    omnifill_middle_mile.json
    omnifill_promise_sourcing.json
    omnifill_fulfillment.json
    omnifill_last_mile.json
    omnifill_planning.json
```

## Non-Goals

- Token budget enforcement (unlimited plan)
- Multi-project orchestration (omnifill only, for now)
- Web UI (CLI is sufficient)
- Custom task prioritization beyond DAG ordering (equal priority for now)
