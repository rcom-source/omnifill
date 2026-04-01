# Korber / Infios (HighJump) — Middle Mile Capabilities

Research date: 2026-03-31

## Company Overview

**Brand History:** HighJump -> acquired by Korber AG -> Korber Supply Chain Software -> rebranded as **Infios** in March 2025, after acquiring MercuryGate (TMS) in 2024. Infios is a joint venture between Korber AG and KKR. Serves 5,000+ customers across 70 countries.

[Source: https://www.infios.com/en/knowledge-center/news/koerber-supply-chain-software-rebrands-as-infios]

**Product Lines:**
- **K.Motion Warehouse Edge** — Small/mid warehouses, RF and voice-directed
- **K.Motion Warehouse Advantage** — Large, highly automated DCs, first full HTML5 UI in WMS
- **K.Motion Enterprise 3PL** — Multi-client operations, flexible per-customer configuration
- **Yard Management System (YMS)** — Standalone yard/dock solution
- **Labor Management, Slotting, Event Management** — Part of Korber Supply Chain Advantage suite

[Source: https://koerber-supplychain.com/supply-chain-solutions/supply-chain-software/warehouse-management/]

## Middle Mile Capabilities

### Yard Management

- Full YMS with dock and slot management, inflow control, constraint-based appointing
- Carrier reliability tracking, arrival/departure appointment management
- Automated and manual yard process control
- Peripheral integration: display panels, traffic lights, gate technology, transponder systems
- Multi-yard, multi-client support for medium-to-large facilities and complex container parks
- Mobile and desktop UI

[Source: https://koerber-supplychain.com/supply-chain-solutions/supply-chain-software/yard-management-system/]

### Cross-Docking

- Native support — inbound goods bypass storage and move directly to outbound shipments
- Back-to-back functionality: stock can be immediately picked on receipt
- Replenishment directed straight from receipt

### Sortation

- Integration with sortation equipment and conveyors via automation solutions
- Automated receiving systems for high-volume inbound processing

[Source: https://koerber-supplychain.com/supply-chain-solutions/supply-chain-automation-solutions/receiving/]

### Inbound Receiving

- System-driven QC and quarantine procedures on inbound stock
- Properties (size, weight) captured on receipt via measurement systems for cartonization
- Directed putaway by: size/dimension, velocity, sales volume, consolidation, FIFO, custom rules
- Multiple picking strategies: batch, wave, e-commerce, pallet, case

### Routing

- With MercuryGate acquisition (now part of Infios), full TMS capabilities including transportation management and routing
- Previously limited to warehouse-level routing (pick paths, replenishment routing)

## Technical Integration

| Method | Details |
|--------|---------|
| SFTP | Confirmed; used by integration partners |
| SQL Stored Procedures | MS SQL Server stored procs paired with REST endpoints |
| ERP Integration | Microsoft Dynamics, Sage, SAP, NetSuite, Infor |
| EDI | Built-in EDI connectivity |
| REST | Being developed but not publicly documented |

Third-party connectors available via Makini, Extensiv, Takt.

[Source: https://www.makini.io/integrations/k-motion-warehouse-advantage]

### Developer Portal

**None public.** Integration is partner/consultant-mediated. Gated integration model — requires Korber/Infios professional services or certified partners.

### Authentication

No public API authentication details. Customer portal at https://www.koerber.com/en/portals.

### Documentation

| Resource | URL | Access |
|----------|-----|--------|
| Customer Portal | https://www.koerber.com/en/portals | Gated |
| Downloads | https://koerber-supplychain.com/downloads/ | Public |
| Support | Phone + online | Customer only |

## User Reviews

### Ratings

| Platform | Rating | Reviews |
|----------|--------|---------|
| G2 | 3.9/5 | 40 verified |
| Capterra | ~80% satisfaction | 9 |

### Pros
- Ease of use, strong reporting, end-user friendly
- 99.9% accuracy claims, real-time order tracking
- Comprehensive WMS/TMS/LMS/YMS providing end-to-end visibility
- First-rate implementation teams

### Cons
- "Built on a lot of old programs pieced together" — legacy feel
- Customer support and after-sales technical expertise concerns
- Limited number of strong implementation partners
- Steep learning curve for advanced configuration

[Source: https://www.g2.com/products/korber-k-motion-warehouse-advantage/reviews]
[Source: https://www.capterra.com/p/154104/Koerber-WMS/reviews/]
[Source: https://www.trustradius.com/products/korber-warehouse-management-system/reviews]

## Pricing

- **Entry-level:** ~$5,000/month for up to 5 users and 100 orders/day
- **Enterprise:** Custom pricing, quote-based
- **Deployment:** Cloud (Korber Cloud) or on-premise
- No public pricing page

[Source: https://www.capterra.com/p/154104/Koerber-WMS/]

## Decision Engine

- No standalone decision engine product
- Rules-based decision-making integrated throughout WMS
- AI-enabled functionalities for planning and execution optimization
- Slotting Solution uses data science for optimal inventory placement
- Wave planning, task interleaving, directed putaway use configurable rules

## Integration Assessment

**Classification: GATED**

| Dimension | Assessment |
|-----------|------------|
| API Surface | Limited — SFTP, SQL stored procs, emerging REST |
| Public Access | No public API docs or developer portal |
| Sandbox | None |
| Integration Effort | HIGH — partner-mediated |
| Middle Mile Strength | Strong YMS, native cross-docking, TMS via MercuryGate |
| Decision Engine | Rules-based + AI-enabled slotting |

## Sources

- https://koerber-supplychain.com/supply-chain-solutions/supply-chain-software/warehouse-management/
- https://koerber-supplychain.com/supply-chain-solutions/supply-chain-software/yard-management-system/
- https://koerber-supplychain.com/supply-chain-solutions/supply-chain-automation-solutions/receiving/
- https://www.infios.com/en/knowledge-center/news/koerber-supply-chain-software-rebrands-as-infios
- https://www.explorewms.com/infios-wms-software-profile.html
- https://www.makini.io/integrations/k-motion-warehouse-advantage
- https://www.koerber.com/en/portals
- https://koerber-supplychain.com/downloads/
- https://www.g2.com/products/korber-k-motion-warehouse-advantage/reviews
- https://www.capterra.com/p/154104/Koerber-WMS/reviews/
- https://www.trustradius.com/products/korber-warehouse-management-system/reviews
- https://softwareconnect.com/reviews/korber-wms/
