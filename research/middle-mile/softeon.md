# Softeon (now IFS Softeon) — Middle Mile Capabilities

Research date: 2026-03-31

## Company Overview

- **Headquarters:** 11700 Plaza America Drive Suite 910, Reston, VA 20190
- **Founded:** 20+ years ago
- **Key customers:** Brooks, Casey's, Denso, Sears Home Services, Sony, UPS
- **Operations:** 30 countries, millions of orders/month
- **ACQUISITION:** IFS (Swedish ERP vendor) completed acquisition March 2, 2026. Now operates as "IFS Softeon."
- **Gartner:** Visionary in 2025 MQ for WMS (14th consecutive year). Top 5 scoring vendor for Level 3-5 Warehouse Operations use cases.

[Source: https://www.ifs.com/en/insights/news/ifs-completes-acquistion-of-softeon]
[Source: https://www.softeon.com/2025-gartner-magic-quadrant-for-warehouse-management-systems-wms/]

## Products

| Product | Description |
|---------|-------------|
| Softeon WMS | Core warehouse management — receiving, putaway, inventory, picking, loading, shipping |
| Softeon WES | Warehouse Execution System — "central nervous system of the warehouse," can run standalone with any WMS |
| Softeon DOM | Distributed Order Management — intelligent order sourcing, allocation, multi-node fulfillment |

## Middle Mile Capabilities

### Yard Management

- Extends warehouse to dock and yard
- Graphical viewing tool for complete yard visibility
- Flexible appointment scheduling for yard moves (deliveries, pickups)
- Dock door scheduling optimization
- Real-time trailer/vehicle/inventory tracking
- Visibility into trailer contents, associated documents, inventory status

[Source: https://www.softeon.com/solutions/warehouse-management-system-wms/yard-management/]

### Cross-Docking

- Advanced cross-docking functionality within WMS
- Integrated with complex inventory management capabilities

### Sortation

- Carton sortation support
- Complex sortation integration through WES
- Manages picking sub-systems: Voice, smart carts, pick-to-light, put walls, mobile robots

[Source: https://www.softeon.com/solutions/warehouse-execution-system-wes/]

### Warehouse Execution System (WES)

- Can run integrated with Softeon WMS or standalone with any other WMS
- Real-time visibility to throughput and bottlenecks
- Automated order release based on priorities and service commitments
- Wave, waveless, or dual order release optimization
- Configurable optimization by picking area or technology
- Advanced labor planning using simulation
- Automation/robotics integration: AGVs, robotic arms, ASRS, put walls, conveyor systems, goods-to-person

### Inbound Receiving

- Flexible options: ASN receiving, blind receiving, blanket purchase orders
- Appointment scheduling for inbound/outbound
- Quality checking during receiving
- Putaway operations and location management

### Routing / Allocation (DOM)

Softeon DOM is the **key middle-mile decision engine:**
- Intelligent order sourcing and allocation via rules engine
- Real-time visibility of inventory and orders across channels
- Multi-node fulfillment: DCs, stores, suppliers
- Evaluates: inventory levels, transit times, shipping costs
- Inventory allocation at multiple levels/attributes: forecast, history, actual orders, marketing allocation
- In-transit and planned inventory allocation
- Mortgage inventory by channels and channel clusters
- Capacity-aware: limits orders per fulfillment node (e.g., store capacity limits)
- Omnichannel: curbside pickup, BOPIS, ship-from-store, vendor drop ship
- Centralized "Order Hub" for B2C and B2B

[Source: https://www.softeon.com/solutions/distributed-order-management-system-dom/]
[Source: https://www.softeon.com/our-solutions/product-solutions/order-management]

## Technical Integration

### Data Formats

- XML, REST APIs, Webhooks, Flat files, EDI

### Enterprise Integration Workbench (EIW)

- Integration configurator and mapping tool
- Integration simulator
- Real-time Interface Monitor — continuously tracks all WMS-enterprise/MHE communications

[Source: https://www.softeon.com/blog/wms-integration-what-you-need-know/]

### Authentication

- **SAML SSO** (SP and IDP initiated)
- **Microsoft Entra ID** (Azure AD) integration
- Just In Time user provisioning supported
- URL pattern: `https://<companyname>.softeon.com/<instancename>`
- Certificate (Base64) exchange with Softeon support for SSO setup

[Source: https://learn.microsoft.com/en-us/entra/identity/saas-apps/softeon-tutorial]

### Developer Portal

**None public.** No public API documentation. Integration via support team and EIW tooling.

## User Reviews

### Ratings

| Platform | Rating | Reviews |
|----------|--------|---------|
| G2 | Leader (Summer 2025, Winter 2026) | Multiple |
| Gartner Peer Insights | Available | Multiple |
| SelectHub | 87% satisfaction | 61 reviews aggregated |

### Pros
- Ease of use, customization, customer support
- Flexibility and reliability
- Real-time dashboards
- Strong receiving and pick-and-pack

### Cons
- Customization can be costly/complex
- Steep learning curve
- Rigid workflow enforcement makes exception handling difficult

[Source: https://www.g2.com/products/softeon-warehouse-management-system/reviews]
[Source: https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/softeon/product/softeon-warehouse-management-system]

## Pricing

- **Not publicly disclosed** — custom quotes only
- Enterprise-focused, supports subscription-based and perpetual licensing
- Additional costs for modules, support, implementation
- Cloud and on-premises options

[Source: https://www.getapp.com/operations-management-software/a/softeon-warehouse-management-system-wms/pricing/]

## Decision Engine

- Rules engine governs order routing decisions
- Considers: cost to ship, item margin, fulfillment node capacity, service-level commitments, network constraints
- Dynamic order sourcing across fulfillment network
- Sophisticated allocation with multiple levels, attributes, parallel formulas
- Store capacity limits with automatic overflow routing

## Integration Assessment

**Classification: SEMI-GATED**

| Dimension | Assessment |
|-----------|------------|
| API Surface | REST APIs + EIW integration tooling |
| Public Access | No public API docs |
| Sandbox | None |
| Integration Effort | MEDIUM-HIGH — via support team |
| Middle Mile Strength | Strong DOM (order routing), YMS, WES, cross-docking |
| Decision Engine | Sophisticated rules-based DOM with multi-attribute allocation |
| IFS Acquisition Impact | May improve integration options as part of IFS platform |

## Sources

- https://www.softeon.com/solutions/warehouse-management-system-wms/yard-management/
- https://www.softeon.com/solutions/warehouse-execution-system-wes/
- https://www.softeon.com/solutions/distributed-order-management-system-dom/
- https://www.softeon.com/our-solutions/product-solutions/order-management
- https://www.softeon.com/blog/wms-integration-what-you-need-know/
- https://www.softeon.com/2025-gartner-magic-quadrant-for-warehouse-management-systems-wms/
- https://www.ifs.com/en/insights/news/ifs-completes-acquistion-of-softeon
- https://learn.microsoft.com/en-us/entra/identity/saas-apps/softeon-tutorial
- https://www.g2.com/products/softeon-warehouse-management-system/reviews
- https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/softeon
- https://www.getapp.com/operations-management-software/a/softeon-warehouse-management-system-wms/pricing/
- https://www.selecthub.com/p/warehouse-management-software/softeon/
- https://www.explorewms.com/softeon-wms.html
- https://www.capterra.com/p/162155/WMS-Cloud/
