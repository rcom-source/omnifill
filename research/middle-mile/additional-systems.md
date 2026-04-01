# Additional Middle Mile Systems

Research date: 2026-03-31

Beyond the primary WMS vendors, several specialized systems focus on specific middle-mile functions: yard management, dock scheduling, order routing/allocation, and inbound logistics visibility.

---

## Standalone Yard Management Systems (YMS)

### C3 Solutions (C3 Reservations / C3 Yard)

- **What:** Leading standalone YMS and dock scheduling platform
- **Capabilities:** Dock appointment scheduling, yard management, gate automation, trailer tracking, dock door optimization
- **Integration:** REST API available, integrates with WMS/TMS/ERP systems
- **Auth:** Vendor-managed, no public API docs
- **Reviews:** Well-regarded in 3PL and manufacturing verticals
- **Pricing:** Quote-based SaaS
- **Website:** https://www.c3solutions.com/

[Source: https://www.c3solutions.com/ — company website]

### Exotrac (YardTMS)

- **What:** Cloud-based yard management and dock scheduling
- **Capabilities:** Trailer tracking, dock scheduling, gate management, yard visibility, carrier appointment management
- **Integration:** API-based integrations with WMS/TMS platforms
- **Reviews:** Used by large retailers and manufacturers
- **Pricing:** Quote-based
- **Website:** https://www.exotrac.com/

[Source: https://www.exotrac.com/ — company website]

### 4sight / YardView

- **What:** YMS solutions for trailer and dock management
- **Capabilities:** Real-time trailer tracking, RFID/GPS integration, dock scheduling, yard workflow automation
- **Integration:** ERP and WMS connectors
- **Target:** Large distribution centers, manufacturing facilities

---

## Dock Scheduling Platforms

### OpenDock

- **What:** Cloud-based dock scheduling platform for warehouses and carriers
- **Capabilities:** Self-serve carrier booking portal, multi-location scheduling, automated slot management, carrier performance tracking
- **Integration:** Integrates with Deposco, multiple WMS platforms
- **API:** REST API available
- **Pricing:** SaaS subscription, contact for pricing
- **Website:** https://www.opendock.com/

[Source: https://lp.opendock.com/opendock-deposco — Deposco partnership page]

### DataDocks (Extensiv)

- **What:** Dock scheduling built into Extensiv 3PL Warehouse Manager
- See: [extensiv-3pl-central.md](extensiv-3pl-central.md) for details

---

## Order Routing / Allocation Engines (Distributed Order Management)

### Fluent Commerce

- **What:** Cloud-native Distributed Order Management (DOM) platform
- **Capabilities:**
  - Real-time order orchestration across all fulfillment nodes (DC, store, 3PL, drop-ship)
  - Dynamic inventory availability computation
  - Rules-based and ML-assisted order routing
  - Configurable fulfillment logic via "Rubik" rules engine
  - BOPIS, ship-from-store, click-and-collect orchestration
  - Pre-order and backorder management
- **Integration:** REST APIs, webhooks, event-driven architecture
- **Auth:** OAuth 2.0
- **Documentation:** Developer docs at https://docs.fluentcommerce.com/
- **Reviews:** Strong G2 presence, known for flexibility and speed of implementation
- **Pricing:** SaaS subscription, volume-based
- **Decision Engine:** Configurable rules engine + ML for optimal node selection considering cost, proximity, inventory levels, capacity

[Source: https://fluentcommerce.com/ — company website]
[Source: https://docs.fluentcommerce.com/ — developer documentation portal]

### Kibo Commerce (Order Management)

- **What:** Unified commerce platform with DOM capabilities
- **Capabilities:**
  - Distributed order management and routing
  - Real-time inventory aggregation across all nodes
  - Intelligent order splitting and fulfillment optimization
  - Store fulfillment, ship-from-store, BOPIS
  - Carrier selection optimization
- **Integration:** REST APIs, comprehensive developer documentation
- **Auth:** OAuth 2.0
- **Documentation:** https://developer.kibocommerce.com/
- **Reviews:** Strong in retail/commerce verticals
- **Pricing:** Enterprise, quote-based

[Source: https://kibocommerce.com/ — company website]
[Source: https://developer.kibocommerce.com/ — developer portal]

### Fabric (formerly CommonSense Robotics)

- **What:** Modular commerce platform with OMS/DOM
- **Capabilities:**
  - Order management and fulfillment orchestration
  - Distributed inventory management
  - Intelligent order routing
  - Multi-node fulfillment optimization
- **Integration:** REST APIs
- **Target:** DTC brands, e-commerce retailers
- **Pricing:** Modular SaaS

[Source: https://fabric.inc/ — company website]

### Orderful

- **What:** EDI-as-a-service platform (note: NOT an order routing engine)
- **Capabilities:** Modern EDI connectivity via API, cloud-based EDI translation, partner onboarding
- **Integration:** REST API for EDI document exchange
- **Relevance:** Enables middle-mile data exchange between systems but is not itself a routing engine
- **Website:** https://www.orderful.com/

[Source: https://www.orderful.com/ — company website]

---

## Inbound Logistics / Visibility Platforms

### project44 (Movement by project44)

- **What:** Supply chain visibility platform — leader in real-time transportation visibility
- **Capabilities:**
  - Real-time shipment tracking across all modes (ocean, air, rail, truck, parcel)
  - Predictive ETAs using ML
  - Exception management and alerting
  - Inbound visibility for receiving/dock scheduling coordination
  - Carbon emissions tracking
  - Inventory in-transit visibility
- **Integration:** REST APIs, webhooks, EDI
- **Auth:** API key authentication
- **Documentation:** Developer portal available
- **Reviews:** Gartner Leader in Real-Time Transportation Visibility Platforms
- **Pricing:** Enterprise SaaS, volume-based
- **Decision Engine:** Predictive ETA algorithms help inform dock scheduling and receiving decisions

[Source: https://www.project44.com/ — company website]

### FourKites

- **What:** End-to-end supply chain visibility platform
- **Capabilities:**
  - Real-time freight tracking (all modes)
  - Predictive ETAs and exception management
  - Yard management visibility
  - Dock scheduling coordination
  - Dynamic ETA for inbound planning
  - Temperature and condition monitoring
  - Carrier performance analytics
- **Integration:** REST APIs, webhooks, 1000+ carrier integrations
- **Auth:** API key / OAuth
- **Reviews:** Gartner Leader alongside project44
- **Pricing:** Enterprise SaaS
- **Relevance:** Provides inbound visibility that feeds into YMS and dock scheduling decisions

[Source: https://www.fourkites.com/ — company website]

### Uber Freight (Transplace, now part of Uber Freight)

- **What:** TMS and managed transportation services (Transplace acquired by Uber Freight 2021)
- **Capabilities:**
  - Transportation management (full TMS)
  - Inbound freight management and optimization
  - Carrier management and procurement
  - Real-time visibility and tracking
  - Network optimization
- **Integration:** REST APIs, EDI
- **Relevance:** Covers inbound freight management piece of middle mile

[Source: https://www.uberfreight.com/ — company website]

---

## Comparison: Specialized Middle Mile Systems

| System | Category | API Access | Middle Mile Focus | Integration Effort |
|--------|----------|-----------|-------------------|-------------------|
| C3 Solutions | YMS/Dock | Vendor-managed | Yard + Dock scheduling | MEDIUM |
| Exotrac | YMS | API-based | Yard + Dock | MEDIUM |
| OpenDock | Dock Scheduling | REST API | Dock scheduling | LOW |
| Fluent Commerce | DOM | REST + OAuth | Order routing/allocation | LOW-MEDIUM |
| Kibo Commerce | DOM | REST + OAuth | Order routing/allocation | MEDIUM |
| Fabric | DOM | REST | Order routing | LOW-MEDIUM |
| project44 | Visibility | REST + Webhooks | Inbound tracking/ETA | LOW |
| FourKites | Visibility | REST + Webhooks | Inbound tracking/ETA | LOW |
| Uber Freight | TMS | REST + EDI | Inbound freight mgmt | MEDIUM |

## Sources

- https://www.c3solutions.com/
- https://www.exotrac.com/
- https://www.opendock.com/
- https://lp.opendock.com/opendock-deposco
- https://fluentcommerce.com/
- https://docs.fluentcommerce.com/
- https://kibocommerce.com/
- https://developer.kibocommerce.com/
- https://fabric.inc/
- https://www.orderful.com/
- https://www.project44.com/
- https://www.fourkites.com/
- https://www.uberfreight.com/
