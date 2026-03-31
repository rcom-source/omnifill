# Omnifill Crew

## Project Vision

Omnifill is a unified fulfillment abstraction layer that normalizes across
warehouse management and fulfillment systems, providing a single API surface
for multi-system orchestration.

## Crew Roles

### architect — System Design Lead

**Focus:** Design the unified Omnifill API schema, adapter pattern, and data model.

**Responsibilities:**
- Define the canonical Omnifill data model (orders, inventory, shipments, returns)
- Design the adapter/provider interface that each WMS connector implements
- Establish API conventions (REST endpoints, error handling, pagination, webhooks)
- Define the authentication abstraction (each WMS has different auth — PAT, OAuth, JWT, BasicAuth)
- Document integration patterns (sync vs async, polling vs webhooks, retry/backoff)

**Key inputs:**
- `research/wms-api-landscape.md` — API capabilities and auth methods for each system
- Start with the 5 publicly documented systems (ShipBob, ShipHero, Extensiv, Oracle WMS, Logiwa)

**Deliverables:**
- `docs/architecture.md` — System design document
- `docs/api-spec.md` — Unified API specification
- `docs/data-model.md` — Canonical data model

---

### integrator — Connector Builder

**Focus:** Build adapters/connectors for each WMS/fulfillment system.

**Responsibilities:**
- Implement the adapter interface defined by the architect for each supported system
- Handle auth flows (OAuth token refresh, JWT rotation, API key management)
- Map each system's data model to the canonical Omnifill model
- Implement rate limiting and retry logic per provider
- Write integration tests against sandboxes where available (ShipBob sandbox)

**Priority order (by API accessibility):**
1. ShipBob (REST, full docs, free sandbox)
2. ShipHero (GraphQL, full docs)
3. Extensiv/3PL Central (REST, full docs, 8 sub-APIs)
4. Logiwa (REST/Swagger, full docs)
5. Oracle WMS Cloud (REST, full docs)
6. SAP EWM (OData, partial docs)
7. Deposco (REST, partial docs)
8. Manhattan Associates (gated — requires partnership)
9. Blue Yonder (gated)
10. Korber/Infios (gated)

**Key inputs:**
- `research/wms-api-landscape.md` — Auth methods, endpoints, rate limits
- Architect's adapter interface specification

**Deliverables:**
- One adapter module per supported system
- Integration test suite per adapter
- Auth flow implementations

---

### ops — Infrastructure & DevOps

**Focus:** Build the runtime infrastructure, CI/CD, and operational tooling.

**Responsibilities:**
- Set up the project scaffolding (language, framework, build system)
- Configure CI/CD pipeline (tests, linting, builds)
- Set up credential/secret management for WMS API keys
- Implement observability (logging, metrics, health checks)
- Design deployment strategy (containerization, cloud deployment)
- Manage environment configs (dev, staging, production)

**Deliverables:**
- Project scaffolding and build configuration
- CI/CD pipeline
- Docker/container setup
- Secrets management approach
- Monitoring and alerting setup
