# OMS / Promising / Sourcing Systems Research

> Research date: 2026-03-31

---

## Table of Contents

1. [Kibo Commerce](#1-kibo-commerce)
2. [Fabric OMS](#2-fabric-oms)
3. [Deposco OMS](#3-deposco-oms)
4. [Deck Commerce](#4-deck-commerce)
5. [Comparative Summary](#5-comparative-summary)

---

## 1. Kibo Commerce

**Website:** https://kibocommerce.com/
**Docs:** https://docs.kibocommerce.com/
**API Tracker:** https://apitracker.io/a/kibo

### What It Does

Kibo Commerce is a unified commerce platform offering a composable, MACH-compliant OMS with deep promising, sourcing, and inventory visibility capabilities. Core modules include Order Management, Real-Time Inventory, Order Routing/Orchestration, and Store Fulfillment.

#### Promising Algorithms

- **Available-to-Promise (ATP):** Real-time ATP calculation across the entire fulfillment network. The inventory service tracks `onHand`, `available`, `allocated`, and `pending` quantities per location.
- **Future Inventory / CTP:** Supports `futureInventory` arrays that track incoming stock with associated fulfillment dates, enabling capable-to-promise beyond current on-hand levels.
- **Delivery Date Promising:** Provides fulfillment date calculations per location and fulfillment type (BOPIS, STH, transfer), factoring in processing time hours.

#### Sourcing Logic

- **Cost-Based Routing:** Explicit cost-based order routing feature (announced as a headline capability). Routes orders to minimize fulfillment cost.
- **Proximity-Based Routing:** Distance calculations between customer and fulfillment locations are built into the inventory API responses.
- **Inventory-Level Routing:** Routes based on real-time stock availability with support for split-shipment optimization (Shipium integration to reduce splits).
- **SLA-Based:** Balances service levels against cost; configurable rules for routing priority.
- **Split Shipment Logic:** Intelligent splitting with configurable preferences (minimize splits vs. minimize cost vs. fastest delivery).

#### Multi-Node Inventory Visibility

- Aggregates inventory across warehouses, DCs, stores, and dropship vendors.
- Single source of truth published to all order capture channels (synchronous or asynchronous).
- Supports tagged inventory segmentation by OrderType, Channel, etc.
- Location-specific fulfillment flags: `directShip`, `transferEnabled`, `pickup`.
- Search modes: `ALL` (full quantity), `PARTIAL`, `ANY`, `ALL_STORES`.

### Technical Documentation

#### API Surface

**REST + GraphQL dual API:**

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/commerce/realtime-inventory/graphql` | POST | GraphQL inventory queries |
| `/api/commerce/realtime-inventory/v5/inventory` | POST | Bulk inventory retrieval |
| `/api/commerce/realtime-inventory/api/storefront/site/availability` | POST/GET | Site-level availability |
| `/api/commerce/realtime-inventory/api/storefront/availability/locations/product` | GET | Single-product location availability |
| `/api/commerce/realtime-inventory/api/storefront/availability/locations/products` | GET | Multi-product location availability |
| `/api/commerce/realtime-inventory/api/storefront/locations` | POST | Available locations query |
| `/commerce/orders` (with `isImport=true`) | POST | Order import for OMS-only implementations |

Full OpenAPI specs available at `/api-overviews/openapi_overview_overview`.

- **Developer Portal:** https://docs.kibocommerce.com/developer-guides/commerce
- **Orders API Overview:** https://docs.kibocommerce.com/help/orders-api-overview
- **Inventory API:** https://docs.kibocommerce.com/help/real-time-inventory
- **API Overviews:** https://docs.kibocommerce.com/help/api-overviews

#### SDKs

Kibo provides SDKs that expose full REST API functionality. The SDK manages OAuth authentication automatically via a Configuration object containing Client ID and Shared Secret.

#### Webhooks

Extensive webhook model with Managed API Extensions that allow adding or overriding behavior while preserving core performance and upgrade paths.

### Authentication

- **OAuth 2.0** token exchange managed by SDK.
- Required headers for REST: `x-vol-tenant` (tenant ID) and `x-vol-site` (site ID).
- Credentials: Client ID + Shared Secret, passed via Configuration object.

### Integration Patterns

- API-first, 100% API coverage (REST and GraphQL).
- Composable / MACH-compliant architecture.
- Managed API Extensions for custom logic injection.
- Supports OMS-only mode (headless, with external ecommerce front-end).

### Help Centers & Community

- **Kibo Help Center / Docs:** https://docs.kibocommerce.com/
- **Resource Center:** https://kibocommerce.com/resources/
- **Gartner Peer Insights:** https://gartner.com/reviews/market/digital-commerce/vendor/kibo/product/kibo-composable-commerce-platform
- **G2:** https://www.g2.com/products/kibo-commerce/reviews

### User Reviews (Pros & Cons)

**Pros:**
- Intuitive, robust platform with solid performance and security
- Strong promotions engine; plentiful out-of-the-box integrations
- Stays current with industry best practices and cutting-edge technology
- Real-time inventory visibility rated highly by implementers
- 167% ROI and $8M NPV reported in Forrester TEI study; payback under 6 months

**Cons:**
- Customizations can be expensive and time-consuming
- Support quality has degraded; Tier-1 support is slow and cannot help with technical issues
- API documentation sometimes outdated; needs sample code and required field specifications
- Costs escalate quickly depending on module count
- Complex setup for teams new to ecommerce platforms

**Sources:** [G2](https://www.g2.com/products/kibo-commerce/reviews), [TrustRadius](https://www.trustradius.com/products/kibo-ecommerce/reviews?qs=pros-and-cons), [Capterra](https://www.capterra.com/p/245050/Kibo-eCommerce/), [Gartner](https://gartner.com/reviews/market/digital-commerce/vendor/kibo/product/kibo-composable-commerce-platform)

### Pricing Model

- Custom pricing with tiers: Starter, Essentials, Advanced, Complete.
- Annual subscription based on number of order lines.
- Agentic Commerce add-on uses conversation-volume-based pricing.
- No public price list; contact sales for quote.

---

## 2. Fabric OMS

**Website:** https://fabric.inc/
**Developer Portal:** https://developer.fabric.inc/
**Knowledge Base:** https://knowledgebase.fabric.inc/
**Full Docs Index:** https://developer.fabric.inc/llms.txt

### What It Does

Fabric OMS (formerly CommonSense Robotics / fabric inc) is a distributed order management platform with two core modules: Inventory and Orders. It provides order orchestration, fulfillment logic, and real-time inventory visibility across retail networks.

#### Promising & Sourcing Logic

- **Order Fulfillment Logic (OFL):** Rules-based engine for routing decisions. Retailers create fulfillment rule sets that direct orders based on:
  - Geo-location / warehouse proximity
  - Warehouse capacity and inventory levels
  - Item price and order attribute type
  - Available services at each location
  - Shipping costs and last-mile logistics efficiency
- **Dynamic Reallocation:** Automatic reallocation when inventory shortages occur at the originally assigned location.
- **Geographic Banding:** Within a geographic band, rules select the optimal location based on capacity, inventory, and available services.
- **No-code Configuration:** Order routing rules configurable without writing code.

#### Multi-Node Inventory Visibility

- **Inventory Aggregation Engine:** Calculates availability across multiple locations using product and location attributes as aggregation criteria.
- **Network Endpoints:** Aggregate SKU quantities for "On Hand" and "Reserved" counters across specified location sets (warehouses or stores).
- **Real-Time Snapshots:** Live inventory visibility across the entire network at any given time.
- Legacy systems had no concept of cross-network availability; fabric explicitly addresses this gap.

### Technical Documentation

#### API Surface (v2 and v3)

- **v2 Orders API:** High-performance endpoints on scalable architecture with configurable data model.
- **v3 Orders API:** Latest version with expanded developer guides.
- **Inventory API:** `GET /inventories` endpoint for retrieving inventory data.
- **Postman Collection:** Available on GitHub for v2 orders API.

Key API areas:
- Order creation and lifecycle management
- Invoicing, tracking, returns, exchanges, cancellations
- Appeasements, backorders, shipments
- Webhook configuration and event subscription

**Developer Portal:** https://developer.fabric.inc/
**v2 API Reference:** https://developer.fabric.inc/v2/api-reference/orders-v2/order-management-system
**v3 API Reference:** https://developer.fabric.inc/v3/api-reference/orders/developer-guide/overview
**Knowledge Base:** https://knowledgebase.fabric.inc/docs/developer-portal/oms-developer-guide/oms-overview/

#### Webhooks

- Self-service pub/sub webhook system.
- Subscribe to supported order event types.
- Specify target URL to receive notifications.
- Throttled at up to 10 events per second.
- Configure via: `POST /webhooks` endpoint.
- Event list: https://developer.fabric.inc/reference/oms-developer-guide-webhook-events

### Authentication

- Access token required for all API requests.
- Supports **Identity v1** and **Identity v2** approaches for obtaining tokens.
- Token-based (Bearer) authentication pattern.

### Integration Patterns

- Modular, API-first platform.
- Two independent data orchestration modules (Inventory + Orders).
- Integrates with Shopify, major ecommerce platforms.
- Supports BOPIS, curbside pickup, ship-from-store.
- Location management with capacity and outage planning.

### Help Centers & Community

- **Developer Portal:** https://developer.fabric.inc/
- **Knowledge Base:** https://knowledgebase.fabric.inc/
- **Release Notes:** https://knowledgebase.fabric.inc/knowledgebase/oms/release-notes
- **G2:** https://www.g2.com/products/fabric/reviews
- **PeerSpot:** https://www.peerspot.com/products/fabric-commerce-platform-reviews
- **TrustRadius:** https://www.trustradius.com/products/fabric/reviews

### User Reviews (Pros & Cons)

**Pros:**
- Strong PIM, CMS, and storefront capabilities alongside OMS
- No-code order routing configuration is a differentiator
- Real-time inventory aggregation across network
- Self-service webhooks for integration flexibility
- Growing market share (0.3% to 0.9% in Order Management Hubs category)

**Cons:**
- Runtime reliability can be challenging
- Not all organizations use enough of its functionality to justify cost
- Better value proposition for B2C than B2B models
- Relatively newer entrant; smaller community than established players
- Limited detailed user reviews available publicly

**Sources:** [G2](https://www.g2.com/products/fabric/reviews), [TrustRadius](https://www.trustradius.com/products/fabric/reviews?qs=pros-and-cons), [PeerSpot](https://www.peerspot.com/products/fabric-commerce-platform-reviews)

### Pricing Model

- Not publicly listed; contact sales for custom quote.
- Broader fabric Commerce Platform includes PIM, OMS, Offers modules (modular pricing likely).

---

## 3. Deposco OMS

**Website:** https://deposco.com/
**Developer Portal:** https://developer.deposco.com/
**Documentation:** https://doc.deposco.com/
**Product:** Bright Suite (Bright Order, Bright Warehouse, Bright Socket)

### What It Does

Deposco provides an end-to-end WMS + OMS platform (Bright Suite) with integrated Distributed Order Management (DOM). The key differentiator is that OMS and WMS run on the same platform, eliminating the "integration tax" between separate systems.

#### Promising & Sourcing Logic

- **Distributed Order Management (DOM):** Allocates order fulfillment to the most optimal location using AI and real-time transparency.
- **Intelligent Routing:** Split-second decisions about inventory allocation based on:
  - Real-time inventory levels across all nodes
  - Customer location / proximity
  - Demand signals
  - Cost optimization (reported 2-20% shipping cost reduction)
  - Speed / SLA requirements
- **Multi-Item Order Splitting:** Automatically divides orders among stores, DCs, warehouses, or suppliers.
- **Drop Shipping:** Connects and compares drop shipping options across suppliers.
- **Pre-ordering / Pre-selling:** Supports orders against future inventory.
- **Rate Shopping:** Carrier rate comparison for cost-optimized shipping.
- **Peak Season Resilience:** DOM routing continues to optimize during supply chain disruptions.

#### Multi-Node Inventory Visibility

- Unified view across warehouses, 3PL providers, retail stores, and suppliers.
- Real-time inventory, demand, and location data.
- Right-inventory-by-channel allocation.
- Same-platform WMS integration means zero latency between warehouse and order data.

### Technical Documentation

#### API & Integration

- **Developer Portal:** https://developer.deposco.com/
- **Documentation Portal:** https://doc.deposco.com/
- **Bright Socket:** Integration module supporting:
  - REST API integrations
  - Socket integrations
  - Data imports/exports via Data Exchange
- **150+ Pre-Built Connectors:** Shopify, marketplaces, ERPs, carriers -- built and maintained by Deposco (not third parties).
- **GitHub Community SDK:** https://github.com/launched-la/deposco-api (community-maintained)

#### Authentication

- Basic authentication with credentials:
  - Tenant Code / ID (from account manager)
  - Username / Password (dashboard credentials)
  - Instance URL
- Parameters: Tenant Code, Deposco URL, API Username, warehouse company code, facility/location values.
- Contact account manager for API credential provisioning.

### Integration Patterns

- Cloud-native SaaS platform.
- Pre-built connectors for major platforms (Shopify, marketplaces, ERPs, carriers).
- Extensiv integration available.
- Rithum partnership for marketplace connectivity.
- Patchworks pre-built connector available.

### Help Centers & Community

- **Developer Portal:** https://developer.deposco.com/
- **Documentation:** https://doc.deposco.com/
- **Support (Techdinamics):** https://support.techdinamics.com/
- **G2 (as Bright Suite):** https://www.g2.com/products/bright-suite/reviews
- **Capterra:** https://www.capterra.com/p/89269/Bright-Warehouse/reviews/
- **Gartner Peer Insights:** https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/deposco
- **GetApp:** https://www.getapp.com/operations-management-software/a/shipforce/

### User Reviews (Pros & Cons)

**Pros:**
- Very robust and customizable without exorbitant cost
- Scales flawlessly with rapid growth
- Exceptional customer support and development teams; genuinely solve operational roadblocks
- 99%+ order accuracy rate achievable
- System-directed workflows improve productivity 30-50%, reduce labor costs
- Easy onboarding; user-friendly interface shortens training
- Affordable relative to larger WMS/OMS vendors for mid-market

**Cons:**
- UI is disorganized and clunky in places
- Software has limitations; labor management reports need improvement
- Mobile app does not auto-update on Zebra MC3300 devices
- API documentation is behind a login wall; less open than competitors
- Requires contacting account manager for API credentials (not self-service)

**Sources:** [Capterra](https://www.capterra.com/p/89269/Bright-Warehouse/reviews/), [G2](https://www.g2.com/products/bright-suite/reviews), [Gartner](https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/deposco), [SoftwareConnect](https://softwareconnect.com/reviews/deposco-bright-warehouse/)

### Pricing Model

- Custom pricing; not publicly listed.
- **Per-facility (site) model** with unlimited users.
- Factors: modules selected, advanced features enabled.
- Starting range: ~$1,000+/month (varies significantly).
- Target market: mid-market companies ($50M-$1B revenue), 3PLs, retailers, CPGs.
- SaaS subscription; pay only for modules needed.

---

## 4. Deck Commerce

**Website:** https://www.deckcommerce.com/
**Founded:** 2015, St. Louis, Missouri
**Formerly:** Magento Order Management (Deck acquired/evolved the platform after Adobe archived it)

### What It Does

Deck Commerce is a purpose-built OMS for D2C and omnichannel brands. It focuses on order lifecycle automation, smart fulfillment routing, and real-time inventory visibility. Processes 1M+ orders/day with 99.999% uptime SLA.

#### Promising & Sourcing Logic

- **Smart Fulfillment Routing:** Business-defined rules that balance margin, efficiency, and delivery speed.
- **AI-Powered Delivery Estimates:** Predictive fulfillment logic at checkout to enhance conversion and minimize post-purchase costs.
- **Rule-Based Order Orchestration:** Automated routing across DCs, stores, 3PLs, and drop-ship vendors.
- **Omnichannel Fulfillment:** BOPIS, curbside pickup, ship-from-store, returns-in-store.
- **Exception Management:** Real-time data surfacing for manage-by-exception workflows.

#### Multi-Node Inventory Visibility

- **Channel-Aware Inventory:** Real-time visibility across the entire fulfillment network (DCs, stores, 3PLs).
- **Prevents Stockouts & Overselling:** Centralized inventory with channel-specific allocation.
- **Inventory Optimization:** Shows inventory where it performs best across sales channels.

### Technical Documentation

#### API Surface

- **API-First Architecture:** All functionality exposed via APIs.
- **Sub-250ms API Response Times:** Performance-optimized endpoints.
- **75+ Pre-Built Connectors:** Integrations with ERPs, ecommerce platforms (Shopify, BigCommerce, Salesforce Commerce Cloud), 3PLs, POS systems.
- **Shopify App:** https://apps.shopify.com/deckcommerce
- **BigCommerce Integration:** https://go.deckcommerce.com/oms-installation-for-big-commerce
- **Microsoft AppSource:** https://appsource.microsoft.com/en-us/product/web-apps/deckinternetsolutions1613054850423.deckcommerce

#### Documentation Access

- API documentation referenced but behind partner/customer access.
- Help Center and Knowledge Base available to customers.
- Product Updates & Release Notes published.
- No public developer portal found; integration likely requires partnership engagement.

**Archived Magento OMS Docs (historical reference):** https://commerce-docs.github.io/oms-documentation-archive/

### Authentication

- Not publicly documented. Likely token-based given API-first architecture.
- Integration setup requires working with Deck Commerce implementation team.

### Integration Patterns

- Modular, composable architecture (start with what you need, expand over time).
- Cloud-native SaaS.
- Pre-built connectors for major platforms.
- 90-day typical implementation timeline (vs. 9 months for competitors).
- Four modular "Centers": Order Center, Inventory Center, Fulfillment Center, Store Center.

### Help Centers & Community

- **Website:** https://www.deckcommerce.com/
- **G2:** https://www.g2.com/products/deck-commerce/reviews
- **Capterra:** https://www.capterra.com/p/201869/Deck-Commerce/
- **Gartner:** https://www.gartner.com/reviews/vendor/deck-commerce
- **Shopify App Reviews:** https://apps.shopify.com/deckcommerce/reviews

### User Reviews (Pros & Cons)

**Pros:**
- High reliability: 99.999% uptime, confidence that orders flow without issues even during traffic spikes
- Strong returns management and omnichannel support (buy online, pick up in store)
- 96.9% order automation rate reported by customers
- 43.9% reduction in fulfillment errors
- Notable customers: New Balance, NETGEAR, Build-A-Bear, Newell Brands
- Fast implementation (~90 days)
- Sub-250ms API response times

**Cons:**
- User interface could be more user-friendly
- Limited public API documentation (behind customer login)
- Smaller market presence compared to Kibo or fabric
- No public developer portal or self-service API access
- Pricing not transparent

**Sources:** [G2](https://www.g2.com/products/deck-commerce/reviews?qs=pros-and-cons), [Gartner](https://www.gartner.com/reviews/vendor/deck-commerce), [Shopify App Store](https://apps.shopify.com/deckcommerce/reviews)

### Pricing Model

- Not publicly listed; custom quote required.
- SaaS subscription model.
- Positioned for growth-stage and enterprise D2C brands.
- Case studies cite: $10M+ savings (global footwear retailer over 20+ years), $50K+ savings per brand (Newell), 10% revenue boost (Build-A-Bear).

---

## 5. Comparative Summary

| Dimension | Kibo Commerce | Fabric OMS | Deposco OMS | Deck Commerce |
|-----------|--------------|------------|-------------|---------------|
| **Primary Focus** | Unified commerce + OMS | Distributed OMS | End-to-end WMS + OMS | D2C order lifecycle |
| **Architecture** | MACH-compliant, composable | API-first, modular | Cloud SaaS, integrated suite | API-first, modular centers |
| **API Quality** | REST + GraphQL, full OpenAPI specs | REST, v2/v3 APIs, Postman collection | REST, behind login wall | API-first but docs not public |
| **Auth Method** | OAuth 2.0 (Client ID + Secret) | Bearer token (Identity v1/v2) | Basic auth (tenant + credentials) | Not publicly documented |
| **Promising** | ATP + future inventory (CTP) | Rules-based OFL | AI-powered DOM | AI delivery estimates |
| **Sourcing Logic** | Cost, proximity, inventory, SLA | Geo, capacity, inventory, cost | Real-time inv, proximity, cost, demand | Margin, efficiency, speed rules |
| **Inventory Aggregation** | Real-time multi-node, tagged inventory | Aggregation Engine across locations | Unified WMS+OMS (zero latency) | Channel-aware centralized |
| **Webhooks** | Extensive model + API extensions | Self-service, 10 events/sec | Via Bright Socket | Not documented publicly |
| **Pre-Built Integrations** | Extensive (not quantified) | Growing library | 150+ owned connectors | 75+ connectors |
| **Developer Experience** | Public docs, SDKs, OpenAPI | Public dev portal + KB | Dev portal behind login | No public dev portal |
| **Target Market** | Mid-market to enterprise | Enterprise retail | Mid-market ($50M-$1B) | Growth-stage to enterprise D2C |
| **Pricing** | Custom (order-line based) | Custom (contact sales) | Custom (per-facility, ~$1K+/mo) | Custom (contact sales) |
| **Uptime SLA** | Not specified | Not specified | Not specified | 99.999% |
| **Throughput** | Not specified | Not specified | Not specified | 1M+ orders/day |
| **Implementation** | Not specified | Not specified | Straightforward (per reviews) | ~90 days |
| **Strongest For** | Complex omnichannel with deep promising | No-code routing + inventory aggregation | Unified WMS+OMS on one platform | High-volume D2C automation |

### Key Takeaways for Omnifill Integration

1. **Kibo** has the most mature and well-documented promising/ATP capabilities with public REST+GraphQL APIs and full OpenAPI specs. Best candidate for deep inventory promising integration.

2. **Fabric** offers the most accessible developer experience with public docs, no-code routing, and a self-service webhook system. Good fit for order routing abstraction.

3. **Deposco** is unique in combining WMS+OMS on one platform (zero-latency inventory data). The 150+ owned connectors and DOM capabilities are strong, but API access is gated behind account management.

4. **Deck Commerce** excels at D2C automation with impressive performance metrics (sub-250ms APIs, 99.999% uptime) but has the least publicly accessible technical documentation.

---

### URLs Referenced

**Kibo Commerce:**
- https://kibocommerce.com/
- https://docs.kibocommerce.com/
- https://docs.kibocommerce.com/developer-guides/commerce
- https://docs.kibocommerce.com/help/orders-api-overview
- https://docs.kibocommerce.com/help/real-time-inventory
- https://docs.kibocommerce.com/help/api-overviews
- https://kibocommerce.com/platform/order-management/
- https://kibocommerce.com/use-cases/order-orchestration-and-routing/
- https://kibocommerce.com/use-cases/fulfillment-optimization/
- https://kibocommerce.com/use-cases/real-time-inventory-visibility/
- https://kibocommerce.com/technology/
- https://apitracker.io/a/kibo

**Fabric OMS:**
- https://fabric.inc/
- https://developer.fabric.inc/
- https://knowledgebase.fabric.inc/
- https://developer.fabric.inc/v2/api-reference/orders-v2/order-management-system
- https://developer.fabric.inc/v3/api-reference/orders/developer-guide/overview
- https://developer.fabric.inc/reference/oms-developer-guide-webhook-events
- https://developer.fabric.inc/v3/api-reference/orders/webhooks/configure-new-webhook
- https://developer.fabric.inc/v2/api-reference/orders-v2/inventory/get-inventories
- https://fabric.inc/products/order-management/features
- https://fabric.inc/blog/product/order-routing

**Deposco:**
- https://deposco.com/
- https://developer.deposco.com/
- https://doc.deposco.com/
- https://deposco.com/solutions/supply-chain-execution/order-management-dom/
- https://deposco.com/resources/product-brochures/bright-order/
- https://github.com/launched-la/deposco-api

**Deck Commerce:**
- https://www.deckcommerce.com/
- https://www.deckcommerce.com/order-management-platform
- https://www.deckcommerce.com/dtc-solutions/for-omnichannel-and-ecommerce
- https://www.deckcommerce.com/integrations
- https://apps.shopify.com/deckcommerce
- https://commerce-docs.github.io/oms-documentation-archive/
