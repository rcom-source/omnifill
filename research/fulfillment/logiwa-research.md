# Logiwa (Logiwa IO)

## Overview & History

Logiwa is a cloud-native warehouse management and fulfillment management system (FMS) designed for high-volume direct-to-consumer (DTC) and ecommerce fulfillment. The platform targets 3PLs, brands, and online sellers who need to process large order volumes with carrier integration and multi-channel connectivity.

- **Headquarters**: Chicago, IL (US) and Istanbul, Turkey
- **Founded**: 2017
- **Platform evolution**: Launched **Logiwa IO** in December 2023, replacing the legacy WMS with a "headless" microservice architecture focused on fulfillment management rather than pure warehousing
- **Architecture**: Cloud-native, built on .NET framework, serverless/microservice design
- **Target market**: SMB to mid-market 3PLs, DTC brands, ecommerce fulfillment operations
- **Analyst rating**: 92% (SelectHub); 4.6/5 (Capterra, 93 reviews); listed on G2 and Gartner Peer Insights

## What It Does

### Pick Methods

Logiwa supports multiple picking strategies running simultaneously within a single warehouse:

- **Discrete (single-order) picking**: One picker, one order at a time
- **Batch picking**: Groups multiple orders together so pickers collect items for several orders in one trip; reduces walking time for warehouses with many small items or overlapping SKUs
- **Wave picking**: Schedules picking in timed waves, grouping orders to be picked simultaneously and dispatched together; improves coordination with packing and shipping
- **Zone picking (pick-and-pass)**: Divides the warehouse into specific zones where pickers specialize in their designated area; items pass between zones
- **Cluster picking**: Multiple orders picked concurrently with a cart/tote system
- **Put-to-wall (put wall) operations**: Saves thousands of picking hours compared to manual/cluster picking; Logiwa allows building put wall cells, defining bin/tote capacity, and automating order picking batches based on put wall cell capacity

Smart algorithms and job batching speed up fulfillment by ~50% according to Logiwa, with walking path optimization built in.

### Pack Optimization

- Mobile scanning at pack stations eliminates picking errors; every order verified 100% accurate
- Automated packing slip, return form, and shipping label pre-printing
- Smart box size recommendations
- Digital scale integration
- Automatic dimensioning system connections
- Rule-based labeling for different scenarios (real-time rate shopping, batch label printing, on-demand printing)

### Shipping / Carrier Selection

- **Automated rate shopping** across preferred carriers to find the lowest rate
- **Carrier rate grouping** for best pricing per provider
- **Batch label printing** and on-demand printing at packing stations
- **Shipment tracking number management** with real-time package visibility
- **Markup capabilities** for third-party carrier accounts (3PL billing)
- Automatic sync of tracking information with sales channels
- Plug-and-play carrier connections

### Carrier Integrations

**Direct carrier integrations:**
- UPS, USPS, FedEx, DHL Express

**Shipping platform integrations:**
- Shippo (natively embedded), EasyPost, Easyship, eHub, ShipStation, Endicia, ShipWise

### Labor Management

- **Labor standards**: Estimate how much work teams can accomplish; compare productivity between teams and individual workers
- **AI and predictive analytics** for labor planning and demand forecasting
- **Smart job allocation** and resource management to reduce labor costs
- **Performance benchmarking** across warehouse teams

### Robotics Integration

Logiwa supports hybrid human-robot warehouse models:

- **Locus Robotics**: Integration with Locus's autonomous mobile robots (AMRs) for goods-to-person picking
- **Dematic**: Integration with Dematic's automation software for autonomous robotic systems (reduces space requirements, operational costs, process duration)
- **inVia Robotics**: Picking robot integration
- General support for emerging robotics platforms via low-code integration framework

### Additional Features

- **Multi-warehouse operations**: Manage multiple facilities from a single platform
- **Multi-client support**: Configurable client portals with real-time visibility (critical for 3PLs)
- **Directed putaway**: Smart location suggestions for incoming goods
- **Real-time inventory management**: Cross all locations and channels
- **Order orchestration**: Rule engine for complex fulfillment strategies
- **Analytics and reporting**: Operational dashboards and performance metrics
- **EDI support**: Standards 850, 856, 940, 945, 753, 754, 810, 846, 855, 128
- **Returns management**: Process and restock returns

## Technical Documentation

### API Overview

Logiwa provides an open **REST API** for integration with stores, marketplaces, websites, warehouses, vendors, ERPs, BI tools, and more.

- **API style**: REST (JSON)
- **Documentation**: Swagger UI at `https://myapi.logiwa.com/swagger/index.html`
- **Help center article**: `https://logiwa.my.site.com/logiwahelp/s/article/Logiwa-Open-API`
- **Webhook docs**: `https://webhook.logiwa.com/`

### API Endpoint Categories

Based on available documentation, the API covers these domain areas:

| Category | Key Endpoints | Description |
|----------|--------------|-------------|
| **Authentication** | `GetAuthenticationToken` | Token-based auth via username/password |
| **Inventory** | Inventory Property Update, Location Search, Location Update | Manage inventory levels and warehouse locations |
| **Orders** | Order Detail Operations (Insert, Update, Delete, Search) | Full CRUD on shipment order details |
| **Warehouse Tasks** | Warehouse Task Processing | Search picking, sorting, packing tasks; replenishment task details |
| **Shipments** | List Shipment Info, Update Shipment Info | Tracking number, carrier, shipment method, rate management |
| **Pick & Ship** | Pick and Ship with Tracking Number | Execute picking and shipping simultaneously with multiple tracking numbers |
| **Receipts** | Receipt Report with Serial Numbers, Put Away Suggestion | Inbound receiving, serial number tracking, directed putaway |
| **Products** | Product Information | Product data management |

### Authentication

Logiwa uses **JWT (JSON Web Token)** bearer authentication:

1. **Obtain token**: `POST /v1/auth/login` with username and password credentials
2. **Use token**: Include `Authorization: Bearer <token>` header in all subsequent requests
3. **Credential source**: API User (Client ID) and API Key (Client Secret) configured in Entity > Store Management within Logiwa
4. **Legacy endpoint**: `wms.logiwa.com/en/api/IntegrationApi/GetAuthenticationToken` (older auth flow)

Webhook payloads include a **signature in message headers** containing account, warehouse, and webhook subscription details for security verification.

### Rate Limits

| Tier | Rate | Requests/Minute |
|------|------|-----------------|
| **Standard API** | 1 request per 1 second | 60 RPM |
| **Enterprise API** | 1 request per 113 ms | 530 RPM |

### Webhooks

Logiwa offers **7 webhook event types** delivered as JSON via HTTP POST:

| Webhook Event | Trigger |
|---------------|---------|
| **Order Status Update** | Shipment, purchase, or receipt order status changes |
| **Inventory Change** | Stock level modifications |
| **Location Update / Movement Info** | Warehouse location changes or inventory movement |
| **Order Shipment Info** | Shipment details available for an order |
| **Shipment Tracking Info** | Tracking number updates |
| **Receipt Info** | Inbound receiving events |
| **Order Consolidated Shipment Info** | Consolidated shipment data for multi-package orders |
| **Product Information Updated** | Product data changes |

**Webhook technical specs:**
- **Format**: JSON via HTTP POST
- **Endpoint requirement**: Must respond within 10 seconds
- **Retry policy**: Up to 3 retries on failure
- **Activation delay**: Up to 5 minutes after creation/update
- **Error notifications**: Optional email alerts when delivery fails
- **Security**: Signature in headers with account, warehouse, and subscription details
- **Timestamps**: Each event includes unique date stamp for troubleshooting

### Integration Patterns

- **200+ pre-built integrations** with ecommerce, marketplace, and order management systems
- **iPaaS-level integration framework**: Low-code environment for rapid deployment and scaling
- **EDI support**: Full range of standard logistics EDI documents
- **Open API + Webhooks**: Use webhooks for real-time push notifications, API calls for data validation and pull operations
- **No official SDKs**: API is consumed directly via REST calls

### Developer Resources

- **Swagger UI**: Interactive API exploration at `myapi.logiwa.com`
- **Webhook documentation portal**: `webhook.logiwa.com`
- **Help center**: `logiwa.my.site.com/logiwahelp`
- **No public Postman collections** confirmed
- **No public GraphQL endpoint**

## Help Centers, Knowledge Bases & Community

| Resource | URL | Description |
|----------|-----|-------------|
| **Help Center** | `logiwa.my.site.com/logiwahelp/s/` | Salesforce-based knowledge base with articles and guides |
| **Support Portal** | `support.logiwa.com` | Authenticated support portal for registered customers |
| **API Docs** | `myapi.logiwa.com/swagger/index.html` | Swagger UI for REST API exploration |
| **Webhook Docs** | `webhook.logiwa.com` | Webhook event documentation and configuration guide |
| **Resources Hub** | `logiwa.com/resources` | Blog posts, guides, and educational content |
| **Contact/Support** | `logiwa.com/contact-us` | Contact form for support inquiries |

**Community forums**: No dedicated community forum found. Support is primarily ticket-based through the support portal.

**Third-party documentation**: Extensiv (formerly 3PL Central) maintains integration setup guides for Logiwa at `help.extensiv.com`.

## Pros and Cons from Real Users

### Pros (from G2, Capterra, Software Advice, Research.com)

| Category | Details |
|----------|---------|
| **Cost-effective** | "Literally fractions of what" users paid for previous solutions; pricing far below competitors for comparable features |
| **Feature-rich** | Comprehensive API connections to Amazon, Walmart, Shopify; direct carrier integrations save time on label generation |
| **Ease of use** | Intuitive interface; new warehouse workers trained and productive in 3-4 hours; smooth onboarding |
| **Stability** | System described as "very stable" and reliable; never crashed for some users |
| **Customer support** | Support team consistently described as responsive, thorough, and timely; excellent onboarding assistance |
| **Scalability** | Cloud-native architecture handles volume spikes well; unlimited users included |
| **Multi-channel** | Strong marketplace integrations; real-time sync across channels |

### Cons (from G2, Capterra, Software Advice, Research.com)

| Category | Details |
|----------|---------|
| **UI/UX complexity** | Interface described as "a bit clunky"; always an extra click or two; confusing terminology |
| **Learning curve** | Complex for management teams; longer training required for admin-level users (not floor workers) |
| **Performance** | Reported slowdowns throughout the day; some latency issues |
| **Customization** | Can be constraining as businesses grow; tedious workflows with duplicate entries; requires technical expertise |
| **Feature gaps** | No payment processing; cannot track partial units for manufacturing; some IMS limitations |
| **Integration promises** | Some users reported being promised comprehensive WMS+IMS but features required additional contracts |
| **Documentation gaps** | Some users report insufficient tutorials and documentation |

### Reddit Presence

Minimal Reddit discussion found. Logiwa does not have an active Reddit community or subreddit. Most user reviews are concentrated on G2, Capterra, and Software Advice.

## Pricing Model

Logiwa uses **volume-based pricing** (not per-user/per-seat):

| Aspect | Details |
|--------|---------|
| **Pricing model** | Based on fulfillment volume and complexity, not number of users |
| **Users** | **Unlimited** — all plans include unlimited users |
| **Starting price** | ~$300-$500/month for up to 1,000 orders |
| **Mid-volume** | ~$2,000-$3,000/month for ~10,000 orders |
| **Implementation** | SMB: $2,000-$5,000; Enterprise: $10,000-$20,000 |
| **Core functionality** | All plans include complete suite of core features and standard integrations |
| **Free trial** | Demo available; no public free trial |
| **Contract** | Custom quotes; contact sales for pricing |

All plans include ungated core functionality. Pricing scales with order volume rather than adding per-seat fees.

## Integration Ecosystem (200+ Partners)

### Ecommerce Platforms
Amazon, Shopify, WooCommerce, eBay, Walmart, BigCommerce

### Shipping Carriers (Direct)
UPS, USPS, FedEx, DHL Express

### Shipping Platforms
Shippo (natively embedded), EasyPost, Easyship, eHub, ShipStation, Endicia, ShipWise

### ERP / Business Systems
NetSuite, custom ERP via API/EDI

### Robotics
Locus Robotics, Dematic, inVia Robotics

### Payment / Finance
PayPal

### Other
Order Desk, Pipe17, Extensiv, custom integrations via Open API and EDI

## Key Differentiators for Omnifill Integration

1. **REST API with Swagger**: Well-documented REST API with interactive Swagger UI; straightforward to build an adapter
2. **JWT auth**: Standard bearer token authentication pattern; easy to implement
3. **Webhook support**: 7 event types covering orders, shipments, inventory, and receipts; useful for real-time sync
4. **Rate limits are modest**: 60 RPM standard, 530 RPM enterprise; need to implement request throttling
5. **Volume-based pricing**: Good for high-volume fulfillment scenarios; no per-user costs
6. **Strong carrier integration**: Rate shopping and label generation built in; may overlap with Omnifill shipping features
7. **Multi-tenant 3PL support**: Client portals and multi-warehouse; relevant for multi-tenant fulfillment scenarios
8. **EDI support**: Important for B2B fulfillment and retail distribution channels

### Integration Considerations

- **No official SDK**: Must consume REST API directly; build adapter from Swagger spec
- **Rate limiting**: Standard tier is quite restrictive at 1 req/sec; batch operations and caching important
- **Webhook reliability**: 3 retries with 10-second timeout; need idempotent webhook handlers
- **Auth token management**: JWT tokens need refresh logic; token lifecycle not fully documented publicly
- **Two API generations**: Legacy (`wms.logiwa.com`) vs new (`myapi.logiwa.com`); ensure targeting correct API version
- **5-minute webhook activation delay**: Account for this in integration setup flows

## Sources

- [Logiwa - Batch Picking vs Wave Picking](https://www.logiwa.com/blog/batch-picking-vs-wave-picking)
- [Logiwa - Wave Picking](https://www.logiwa.com/blog/warehouse-wave-picking)
- [Logiwa - Zone Picking](https://www.logiwa.com/blog/zone-picking-pick-and-pass)
- [Logiwa - Outbound Operations](https://www.logiwa.com/solutions/fulfillment-of-orders-outbound-operations)
- [Logiwa - Ecommerce Shipping Software](https://www.logiwa.com/solutions/ecommerce-shipping-software)
- [Logiwa - Webhooks Blog](https://www.logiwa.com/blog/logiwa-webhooks)
- [Logiwa - Integrations](https://www.logiwa.com/integrations)
- [Logiwa - Pricing](https://www.logiwa.com/pricing)
- [Logiwa Open API (Help Center)](https://logiwa.my.site.com/logiwahelp/s/article/Logiwa-Open-API)
- [Logiwa Swagger UI](https://myapi.logiwa.com/swagger/index.html)
- [Logiwa Webhook Documentation](https://webhook.logiwa.com/)
- [Logiwa - Locus Robotics Integration](https://www.logiwa.com/integrations/locus-warehouse-robotics-solution)
- [Logiwa - Dematic Integration](https://www.logiwa.com/integrations/dematic-warehouse-robotics-solution)
- [Logiwa - Labor Planning with AI](https://www.logiwa.com/blog/warehouse-labor-planning-with-ai-and-predictive-analytics)
- [Logiwa Reviews - Capterra](https://www.capterra.com/p/149744/Logiwa/reviews/)
- [Logiwa Reviews - G2](https://www.g2.com/products/logiwa-corp-logiwa/reviews)
- [Logiwa Pros & Cons - G2](https://www.g2.com/products/logiwa-corp-logiwa/reviews?qs=pros-and-cons)
- [Logiwa Review - SoftwareConnect](https://softwareconnect.com/reviews/logiwa-wms/)
- [Logiwa Review - Research.com](https://research.com/software/reviews/logiwa-wms)
- [Logiwa - Software Advice](https://www.softwareadvice.com/scm/la-wms-profile/)
- [Logiwa IO - SelectHub](https://www.selecthub.com/p/warehouse-management-software/logiwa-io/)
- [Logiwa API - API Tracker](https://apitracker.io/a/logiwa)
- [Shippo + Logiwa Integration](https://goshippo.com/blog/streamlined-shipping-inside-your-wms-introducing-the-shippo-logiwa-integration)
- [Logiwa IO Next Generation WMS](https://www.logiwa.com/blog/logiwa-io-next-generation-warehouse-management-system)
