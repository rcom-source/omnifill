# Deposco — Middle Mile Capabilities

Research date: 2026-03-31

## Company Overview

- **Product:** Deposco Bright Suite — unified platform on single codebase
- **Target:** Mid-market ($50M-$1B annual revenue), e-commerce, 3PL, retail
- **Implementation:** 90-day timeline advertised
- **Not recommended for:** Companies under $25M annual revenue

[Source: https://deposco.com/resources/product-brochures/bright-suite/]

## Products

| Product | Description |
|---------|-------------|
| Bright Suite | Unified platform (all solutions on one codebase) |
| Bright Warehouse | WMS module |
| Bright Order | OMS/DOM module |
| Supply Chain Planning | Planning module |
| Conduit | Dock and yard management (partner/module) |

## Middle Mile Capabilities

### Yard Management

- Via **Conduit** partnership — all-in-one dock and yard manager
- Scheduling, driver check-in, yard management
- Can standalone or integrate with WMS/TMS
- Also integrates with **OpenDock** for dock scheduling
- Predictive dock scheduling functionality

[Source: https://lp.opendock.com/opendock-deposco]

### Cross-Docking

- Native WMS feature in Bright Warehouse
- Barcoding, labeling, cross-docking, returns all supported

[Source: https://deposco.com/solutions/supply-chain-execution/warehouse-management/]

### Sortation

- Seamless real-time integration with automation: fulfillment robotics, pick-to-light, print-and-apply, sortation systems

### Order Routing / Allocation (Bright Order — DOM)

**Key middle-mile decision engine:**
- Automated intelligent order routing
- Distributed Order Management (DOM) allocates to most optimal location
- Routes based on real-time inventory, demand, and location
- Fulfillment from warehouses, 3PLs, and retail stores
- DOM escalates hierarchy to fulfill by planned ship date
- Drop shipping support
- **Cloud-native AI:** Network-level intelligence learns from operations to optimize routing
- Predicts bottlenecks before they hit
- Carrier rate shopping for automated best-rate selection
- Multi-node fulfillment across warehouses, 3PLs, and retail stores
- Pre-ordering/pre-selling: inventory available before physical receipt

[Source: https://deposco.com/solutions/supply-chain-execution/order-management-dom/]

## Technical Integration

### REST API

- **Developer Portal:** https://developer.deposco.com/
- **Documentation:** https://doc.deposco.com/docs/login/home (login required)
- **GitHub TypeScript wrapper:** https://github.com/launched-la/deposco-api

**Known Endpoints:**
- `GET /integration/{code}/inventory/{businessUnit}/facility/{facilityNumber}/location/{locationNumber}`
- `PUT /integration/{code}/import/{businessUnit}/customerOrder/{orderNumber}`

[Source: https://developer.deposco.com/]
[Source: https://github.com/launched-la/deposco-api]

### Pre-built Integrations

- 150+ pre-built integrations
- NetSuite, Shopify, Amazon, UPS, FedEx, QuickBooks
- Hundreds of shipping carriers, online marketplaces, ERPs
- Patchworks connector available

[Source: https://doc.wearepatchworks.com/product-documentation/connectors-and-instances/patchworks-connectors/deposco-prebuilt-connector]

### Authentication

- **Basic Authentication** (username/password)
- Required credentials: Tenant Code, API Username, API Password, Business Unit
- Deposco URL (base URL per tenant)
- Credentials obtained from Deposco account manager
- User Acceptance Mode (test environment) toggle available

### Documentation

| Resource | URL | Access |
|----------|-----|--------|
| Developer Portal | https://developer.deposco.com/ | Public (partial) |
| Full Docs | https://doc.deposco.com/ | Gated (login required) |
| GitHub Client | https://github.com/launched-la/deposco-api | Public |

## User Reviews

### Ratings

| Platform | Rating | Reviews |
|----------|--------|---------|
| SoftwareConnect | 5/5 | 3 |
| SelectHub | 84/100 sentiment | 21 |
| Capterra | Available | Multiple |
| G2 | Available | 5 |
| Gartner Peer Insights | Listed | Available |

### Pros
- Fast onboarding (weeks), scalable, real-time visibility
- Cloud-native, modern interface
- "Night and day from pre-Deposco" — near-perfect uptime
- Enabled Amazon Seller Fulfilled Prime, doubling Amazon sales
- Customer experience teams praised

### Cons
- Put-away logic is hardcoded, limiting customization
- Potential surprise bills for support/customizations post-setup
- Lacks some advanced features of leading WMS platforms
- NetSuite integration difficulties reported

[Source: https://softwareconnect.com/reviews/deposco-bright-warehouse/]
[Source: https://www.capterra.com/p/89269/Bright-Warehouse/reviews/]
[Source: https://www.selecthub.com/p/warehouse-management-software/deposco/]

## Pricing

- **Custom/subscription-based** — per-facility (site) model
- **Unlimited users** included
- Based on modules and advanced features selected
- "No black box pricing" — transparent, single bottom-line price
- Not recommended for companies under $25M annual revenue

## Decision Engine

- **DOM:** Advanced allocation engine selecting optimal fulfillment location
- **Cloud-Native AI:** Learns from hundreds of operations to optimize routing and predict bottlenecks
- **Intelligent pathfinding:** Optimizes every decision from receiving to delivery
- **Carrier rate shopping:** Automated best-rate selection

## Integration Assessment

**Classification: PARTIALLY OPEN**

| Dimension | Assessment |
|-----------|------------|
| API Surface | REST API with developer portal and GitHub client |
| Public Access | Partial — developer portal public, full docs gated |
| Sandbox | User Acceptance Mode available (via account manager) |
| Integration Effort | LOW-MEDIUM — Basic Auth, known endpoints, TS wrapper |
| Middle Mile Strength | Strong DOM with AI routing, cross-docking, yard via partners |
| Decision Engine | AI-powered DOM with multi-node optimization |

## Sources

- https://developer.deposco.com/
- https://doc.deposco.com/docs/login/home
- https://deposco.com/solutions/supply-chain-execution/warehouse-management/
- https://deposco.com/solutions/supply-chain-execution/order-management-dom/
- https://deposco.com/resources/product-brochures/bright-suite/
- https://github.com/launched-la/deposco-api
- https://lp.opendock.com/opendock-deposco
- https://doc.wearepatchworks.com/product-documentation/connectors-and-instances/patchworks-connectors/deposco-prebuilt-connector
- https://help.extensiv.com/366939-deposco/1624749-setting-up-deposco
- https://www.capterra.com/p/89269/Bright-Warehouse/reviews/
- https://www.g2.com/products/bright-suite/reviews
- https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/deposco
- https://softwareconnect.com/reviews/deposco-bright-warehouse/
- https://www.selecthub.com/p/warehouse-management-software/deposco/
