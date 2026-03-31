# Omnifill

Unified fulfillment abstraction layer across warehouse management systems.

## Git Workflow — MANDATORY

**Every task completion MUST push to remote.** No exceptions.

```bash
# Before signaling done:
git add <changed-files>
git commit -m "<type>: <description>"
git push -u origin HEAD
```

If push fails, resolve and retry. Work is NOT complete until `git push` succeeds
and `git status` shows up-to-date with remote.

**Branch strategy:**
- `main` — stable, merged work only
- `crew/<name>` — crew feature branches (push here, refinery merges to main)

## Project Structure

```
research/           # API research and competitive analysis
docs/               # Architecture, API specs, data models
src/                # Source code
  adapters/         # Per-WMS connector implementations
  core/             # Shared types, interfaces, utilities
  api/              # Unified API surface
tests/              # Test suites
```

## Supported Systems (by priority)

1. ShipBob (REST, full docs, sandbox available)
2. ShipHero (GraphQL, full docs)
3. Extensiv/3PL Central (REST, 8 sub-APIs, full docs)
4. Logiwa (REST/Swagger, full docs)
5. Oracle WMS Cloud (REST, full docs)
6. SAP EWM (OData, partial docs)
7. Deposco (REST, partial docs)
8. Manhattan Associates (gated — requires partnership)
9. Blue Yonder (gated)
10. Korber/Infios (gated)

## Crew Roles

See `CREW.md` for detailed role descriptions:
- **architect** — API design, data model, adapter interface
- **integrator** — Connector implementations per WMS
- **ops** — Infrastructure, CI/CD, deployment

## Research

See `research/wms-api-landscape.md` for full API documentation on all 10 systems.
