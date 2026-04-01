# Middle Mile SaaS Systems — Research Index

Research date: 2026-03-31
Covers: Inbound receiving, sortation, cross-docking, routing decisions (FC vs store allocation), yard management, dock scheduling, and inbound logistics platforms.

## System Files

| System | File | Category | API Access | Middle Mile Strength |
|--------|------|----------|-----------|---------------------|
| [Manhattan Associates](manhattan-associates.md) | manhattan-associates.md | Enterprise WMS+YMS+DOM | GATED (20k REST endpoints, OAuth 2.0) | Very Strong |
| [Blue Yonder](blue-yonder.md) | blue-yonder.md | Enterprise WMS+YMS+DOM | GATED (MOCA/REST, OAuth) | Very Strong |
| [Korber/Infios](korber-infios.md) | korber-infios.md | Enterprise WMS+YMS+TMS | GATED (SFTP/SQL/EDI) | Strong |
| [Made4net](made4net.md) | made4net.md | Mid-Enterprise WMS+YMS | SEMI-OPEN (MIS middleware, LDAP/SAML) | Strong |
| [Softeon](softeon.md) | softeon.md | Enterprise WMS+WES+DOM | SEMI-GATED (REST, SAML SSO) | Strong |
| [Synergy/SnapFulfil](synergy-logistics-snapfulfil.md) | synergy-logistics-snapfulfil.md | Cloud WMS+MAO | OPEN (REST+Swagger, free dev accounts) | Moderate |
| [Datex](datex.md) | datex.md | Mid-Market WMS+YMS | SEMI-OPEN (Open API, EDI) | Moderate |
| [Deposco](deposco.md) | deposco.md | Mid-Market WMS+DOM | PARTIALLY OPEN (REST, Basic Auth, GitHub client) | Strong (DOM) |
| [Extensiv/3PL Central](extensiv-3pl-central.md) | extensiv-3pl-central.md | SMB WMS+Dock | OPEN (REST, OAuth 2.0, webhooks) | Weak |
| [Logiwa](logiwa.md) | logiwa.md | SMB FMS | OPEN (REST+Swagger, webhooks) | Moderate |
| [Additional Systems](additional-systems.md) | additional-systems.md | YMS, DOM, Visibility | Varies | Varies |

## Capability Matrix

| System | Yard Mgmt | Cross-Dock | Sortation | Dock Sched | Order Routing/DOM | Decision Engine |
|--------|-----------|-----------|-----------|-----------|-------------------|-----------------|
| Manhattan | Native (3 strategies) | Advanced | MHE integration | Native | AI/ML allocation | Multi-layer AI+ML |
| Blue Yonder | CV/ML-based | AI-driven | Robotics Hub | Constraint-based | 4-step solver | Cost-to-serve solver |
| Korber/Infios | Full YMS | Native | Automation integ. | Constraint-based | Via MercuryGate TMS | Rules-based+AI slotting |
| Made4net | YardExpert | Native | WCS integration | AppointmentExpert | RoutingExpert | Rules engine + AI agents (dev) |
| Softeon | Graphical tool | Advanced | WES integration | Native | DOM rules engine | Multi-attribute DOM |
| SnapFulfil | Basic | Not prominent | SnapControl MAO | Basic | Workflow rules | Rules-based |
| Datex | Dock scheduling | Native | NOS routing | Native | Sub-order splitting | Workflow engine |
| Deposco | Via Conduit partner | Native | Automation integ. | Via OpenDock | AI-powered DOM | Cloud AI + DOM |
| Extensiv | None | None | None | DataDocks | None | None |
| Logiwa | None | Native | API-driven | None | Rules-based putaway | Rules-based |

## Integration Difficulty Ranking (easiest to hardest)

1. **Extensiv** — Fully public REST API, OAuth 2.0, webhooks, well-documented
2. **Logiwa** — Public Swagger/OpenAPI, webhooks with HMAC, client credentials
3. **SnapFulfil** — Public REST API, free dev accounts, test environment
4. **Deposco** — Developer portal, Basic Auth, GitHub TypeScript wrapper
5. **Datex** — Open API architecture, but no public docs
6. **Made4net** — MIS middleware, but no self-service
7. **Softeon** — REST+EIW tooling, via support team only
8. **Korber/Infios** — SFTP/SQL/EDI, partner-mediated
9. **Manhattan** — 20k endpoints but gated ecosystem, requires partnership
10. **Blue Yonder** — Proprietary MOCA, enterprise contract required

## Best-in-Class by Capability

### Yard Management
1. **Blue Yonder** — CV/ML trailer identification, 3D mapping, no infrastructure required
2. **Manhattan** — 3 intelligent prioritization strategies, WMS-YMS unification
3. **Made4net** — YardExpert with RFID/kiosk check-in, 47% dock utilization improvement

### Cross-Docking
1. **Blue Yonder** — AI-driven bypass identification during receiving
2. **Manhattan** — Cross-dock optimization matching trailer contents to outbound allocations
3. **Softeon** — Advanced cross-docking integrated with complex inventory management

### Order Routing / Allocation (FC vs Store)
1. **Blue Yonder** — 4-step constraint solver, real-time cost-to-serve, ML-powered
2. **Manhattan** — Multi-layer AI/ML allocation with size optimization and store clustering
3. **Softeon** — DOM with multi-attribute allocation, capacity-aware, store overflow routing
4. **Deposco** — Cloud AI DOM learning from operations, multi-node fulfillment

### Sortation
1. **Blue Yonder** — Robotics Hub, vendor-agnostic, mixed AMR/AGV fleet management
2. **SnapFulfil** — SnapControl MAO, device-agnostic, MQTT, works with any WMS
3. **Made4net** — Built-in WCS, Level 5 automation orchestration

### Dock Scheduling
1. **Made4net** — AppointmentExpert with carrier portals and performance analytics
2. **Extensiv** — DataDocks with self-serve portal, workload balancing
3. **Manhattan** — Integrated with YMS, transportation ETA overlay

## Specialized Systems Worth Noting

| System | What | Why It Matters |
|--------|------|---------------|
| Fluent Commerce | Cloud-native DOM | Best pure-play order routing engine, REST API, OAuth 2.0 |
| Kibo Commerce | Unified commerce DOM | Strong retail DOM with developer portal |
| project44 | Visibility platform | Real-time inbound ETAs feed dock/yard decisions |
| FourKites | Visibility platform | Inbound visibility, yard management coordination |
| C3 Solutions | Standalone YMS | Leading pure-play yard management |
| OpenDock | Dock scheduling | Cloud dock scheduling, integrates with Deposco |

## Integration Strategy Recommendations

### Tier 1: Integrate First (public APIs, high value)
- **Extensiv** — Easy API, but limited middle-mile value
- **Logiwa** — Easy API, cross-docking support
- **Deposco** — Good API + strong DOM for routing decisions
- **Fluent Commerce** — Best pure-play DOM with open APIs

### Tier 2: Integrate with Effort (partial APIs, high value)
- **Made4net** — Strong middle-mile suite, needs MIS middleware
- **Softeon** — Strong DOM+WES, needs vendor engagement
- **SnapFulfil** — Public API, moderate middle-mile

### Tier 3: Partnership Required (gated, highest value)
- **Manhattan Associates** — Deepest middle-mile capabilities, 20k endpoints, but gated
- **Blue Yonder** — Best decision engine, but proprietary MOCA + enterprise-only
- **Korber/Infios** — Strong YMS+TMS, but partner-mediated integration

### Tier 4: Visibility Layer (complement any WMS)
- **project44** — Inbound shipment visibility + predictive ETAs
- **FourKites** — Yard visibility + dock coordination

## Sources

All source URLs are documented within individual system files. Each file contains a Sources section listing all URLs consulted during research.
