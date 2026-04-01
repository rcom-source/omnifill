# Synergy Logistics (SnapFulfil) — Middle Mile Capabilities

Research date: 2026-03-31

## Company Overview

- **Headquarters:** Castle Donington, UK
- **US Offices:** Charleston, SC and Chicago, IL
- **Founded:** 1972
- **Website:** https://snapfulfil.com
- **Gartner:** Recognized in 2025 MQ for WMS (13th consecutive year) — Niche Player, closest to Visionary axis
- **QKS Group:** Named Leader in SPARK Matrix for WMS (Q2 2025)
- **Key distinction:** Cloud-native WMS architected for the web in 2007

[Source: https://snapfulfil.com/news/synergy-logistics-recognized-in-2025-gartner-magic-quadrant-for-warehouse-management-systems-for-the-13th-year]

## Products

| Product | Description |
|---------|-------------|
| SnapFulfil | Cloud-based Tier 1 WMS with rules-based config engine (no-code, point-and-click) |
| SnapCart | Autonomous mobile robot for small parts picking and e-commerce fulfillment |
| SnapControl | Device-agnostic Multi-Agent Orchestration (MAO) platform |

**SnapFulfil Tiers:**
- Starter — E-commerce focused
- Pro — SMB
- Enterprise — Large warehouse

**Key differentiator:** Deployable in ~45 days (much faster than typical Tier 1 WMS).

[Source: https://snapfulfil.com/about-synergy-logistics]

## Middle Mile Capabilities

### Yard Management

- Integrated yard and load management
- Coordinates trailers and dock schedules
- Out-of-the-box yard and dock management

### Sortation (via SnapControl)

SnapControl is the **Multi-Agent Orchestration (MAO) platform:**
- Device-agnostic orchestration of robotics, conveyors, sortation, PLCs, AGVs, voice, handhelds
- Bi-directional MQTT messaging between WMS and warehouse devices
- Conversational decision-making between WMS and devices
- Automatically allocates tasks and workflows
- Evaluates which devices best match specific operations
- Works with SnapFulfil or any other WMS/OMS/e-commerce system
- Implementation: 60-90 days
- Robotics partners: 6 River Systems, HAI Robotics, Hikrobot, Jungheinrich, Cartesian Kinetics, Lowpad

[Source: https://snapfulfil.com/about-snapcontrol]

### Cross-Docking

- Not prominently documented as a specific feature
- General warehouse flow management capabilities present

### Routing / Allocation

- Workflow Rules Engine automates task prioritization, product put-away, replenishment
- Can allocate work to AMRs and route to carton right-sizing equipment
- Rules set to prioritize orders based on customer demand
- Allocate tasks based on worker availability and skill set
- Self-service configuration (no-code)

[Source: https://snapfulfil.com/news/maximizing-warehouse-efficiency-with-snapfulfils-workflow-rules-engine]

### Inbound / Receiving

- Inbound product quality assurance protocols configurable via rules engine
- Replenishment automation

## Technical Integration

### API

- **RESTful API** available with v1 and v2/Swagger documentation
- API endpoints: `lintliveapi.snapfulfil.net` (production), `treltestapi.snapfulfil.net` (testing)
- **Free developer account** available (no credit card required)
- Custom integration development via API

[Source: https://lintliveapi.snapfulfil.net/]

### Authentication

- Username/password for API access
- HOST_API permission must be enabled for API users
- Credentials configured in Users > Detail section
- No public SSO documentation

### Integration Partners (40+)

| Category | Partners |
|----------|---------|
| ERP | NetSuite (Built For NetSuite certified) |
| iPaaS | Celigo, Jitterbit, Blue Moon, MindCloud |
| Shipping (40+) | UPS, FedEx, USPS, DPD, Parcelforce, Royal Mail, Purolator, OnTrac |
| Robotics/MHE | 6 River Systems, HAI Robotics, Hikrobot, Jungheinrich |
| Other | Extensiv, ShipEngine/ShipStation, Metapack, SAP (via Stacksync) |

[Source: https://snapfulfil.com/integrations-and-partners/]

### Communication Protocol

- SnapControl uses **MQTT** (MQ Telemetry Transport) for device communication
- Bi-directional messaging with small code footprint and minimal bandwidth

### Documentation

| Resource | URL |
|----------|-----|
| Celigo Connection Docs | https://docs.celigo.com/hc/en-us/articles/360038937331-Set-up-a-connection-to-Snapfulfil |
| Extensiv Integration | https://help.extensiv.com/en_US/366980-snapfulfil/1624860-snapfulfil-integration-overview |

## User Reviews

### Ratings

| Platform | Rating | Notes |
|----------|--------|-------|
| Capterra | Listed | Starts $4,000/mo per feature |
| Gartner Peer Insights | Available | 13th year in MQ |
| G2 | Listed | Limited review volume |

### Pros
- Scalable, affordable for Tier 1 WMS
- User-friendly, easy to train
- Some users cut staff by half
- Fast deployment (~45 days)

### Cons
- Can feel complicated due to many features
- May not suit single-brand retail/B2C well

[Source: https://www.capterra.com/p/90869/Snapfulfil-WMS/reviews/]
[Source: https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/synergy-logistics/product/snapfulfil]

## Pricing

- Subscription-based SaaS (monthly or annual)
- Three tiers: Starter, Pro, Enterprise
- Based on: number of users, warehouses, functionality
- Capterra lists starting at **$4,000/month** per feature
- Transparent pricing (no hidden costs claimed)
- Bespoke packages for fixed-cost periods available
- Fast deployment reduces implementation cost vs. typical Tier 1 WMS

[Source: https://www.getapp.com/operations-management-software/a/snapfulfil/]

## Integration Assessment

**Classification: OPEN**

| Dimension | Assessment |
|-----------|------------|
| API Surface | RESTful API with Swagger docs, free dev accounts |
| Public Access | Yes — API endpoints publicly accessible |
| Sandbox | Test API available (treltestapi.snapfulfil.net) |
| Integration Effort | LOW-MEDIUM — public API, free dev accounts |
| Middle Mile Strength | Moderate — YMS, SnapControl sortation orchestration |
| Decision Engine | Rules-based workflow engine (warehouse-level, not DOM) |

## Sources

- https://snapfulfil.com
- https://snapfulfil.com/about-synergy-logistics
- https://snapfulfil.com/about-snapcontrol
- https://snapfulfil.com/integrations-and-partners/
- https://snapfulfil.com/news/maximizing-warehouse-efficiency-with-snapfulfils-workflow-rules-engine
- https://lintliveapi.snapfulfil.net/
- https://docs.celigo.com/hc/en-us/articles/360038937331-Set-up-a-connection-to-Snapfulfil
- https://help.extensiv.com/en_US/366980-snapfulfil/1624860-snapfulfil-integration-overview
- https://snapfulfil.com/news/synergy-logistics-recognized-in-2025-gartner-magic-quadrant-for-warehouse-management-systems-for-the-13th-year
- https://www.capterra.com/p/90869/Snapfulfil-WMS/reviews/
- https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/synergy-logistics/product/snapfulfil
- https://www.g2.com/products/snapfulfil-wms/competitors/alternatives
- https://www.getapp.com/operations-management-software/a/snapfulfil/
- https://www.snapfulfil.com/news/snapfulfil-announces-autonomous-fulfilment-cart-snapcart/
