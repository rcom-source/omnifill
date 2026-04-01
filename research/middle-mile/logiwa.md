# Logiwa — Middle Mile Capabilities

Research date: 2026-03-31

## Company Overview

Logiwa IO is positioned as a **Fulfillment Management System (FMS)** rather than traditional WMS. Cloud-native, .NET framework. Focuses on processing and shipping orders fast for high-volume DTC/ecommerce fulfillment.

- 200+ pre-built integrations (Amazon, Shopify, Walmart, UPS, etc.)
- AI-powered automation
- Best suited for small-to-medium DTC/ecommerce businesses
- Implementation: 2-3 weeks reported

[Source: https://www.logiwa.com/blog/logiwa-io-next-generation-warehouse-management-system]

## Products

| Product | Description |
|---------|-------------|
| Logiwa WMS | Cloud-based warehouse management (legacy branding) |
| Logiwa IO | Next-generation FMS — the current product |

## Middle Mile Capabilities

### Sortation

- API-first, headless architecture enables orchestration with automation partners (AMRs, Goods-to-Person, sortation)
- Warehouse task processing API supports picking, sorting, packing tasks

[Source: https://www.logiwa.com/blog/automated-sortation-systems-for-3pls]

### Cross-Docking

- **Native cross-docking** support in Logiwa IO
- Direct transfer from receiving to shipping, bypassing storage
- Software flags items for cross-docking during goods receipt
- Cross-docking and putaway suggestions during receiving
- Reduces handling times and storage costs

[Source: https://www.logiwa.com/blog/warehouse-cross-docking]

### Routing / Allocation

- Rules-based location suggestion algorithms for putaway
- Directed putaway configurable by: velocity, volume, fragility, temperature, cross-dock, zone, or custom criteria
- Smart inventory management with customizable rules
- Multi-channel order routing across fulfillment network

[Source: https://www.logiwa.com/blog/directed-putaway-algorithm-warehouse]

### Receiving

- Barcode scanners, smartphones, tablets, PCs supported
- Rules-based location suggestion during receiving
- Cross-docking flagging at receipt
- Putaway suggestions at point of receipt
- Backorder handling, pre-optimized inventory storage algorithms

[Source: https://www.logiwa.com/solutions/logistics-software-inbound-operations]

### Yard Management

**Not offered.** No dedicated yard management module.

### Dock Scheduling

**Not offered.** No dedicated dock scheduling module.

## Technical Integration

### REST API

- **Swagger/OpenAPI:** https://myapi.logiwa.com/swagger/index.html
- API-first, headless architecture
- Open REST API for websites, stores, ERPs, BI tools, vendors, warehouses

[Source: https://logiwa.my.site.com/logiwahelp/s/article/Logiwa-Open-API]

### Webhook API

- Dedicated webhook system with 7 event types:
  1. Shipment/Purchase/Receipt Order Status Updates
  2. Inventory Change notifications
  3. Location Update and Movement Information
  4. Order Shipment Details
  5. Shipment Tracking Information
  6. Receipt Information
  7. Order Consolidated Shipment Details
- **HMAC-SHA256** cryptographic signatures for delivery verification
- Auto-scaling up to 1000x capacity
- 1000ms timeout per request
- 99.9% uptime SLA
- Automatic retry with backoff on failures (including 429 rate limiting)

[Source: https://www.logiwa.com/blog/logiwa-webhooks]
[Source: https://webhook.logiwa.com/]

### Authentication

- **Client ID / Client Secret** authentication for REST API
- **JWT** for webhook authentication
- Rate Limiting:
  - Standard: 1 req/sec (60 req/min)
  - Enterprise: 1 req per 113ms (530 req/min)
  - 429 on rate limit exceeded

### Documentation

| Resource | URL |
|----------|-----|
| Swagger UI | https://myapi.logiwa.com/swagger/index.html |
| Open API Guide | https://logiwa.my.site.com/logiwahelp/s/article/Logiwa-Open-API |
| Webhook API | https://webhook.logiwa.com/ |
| Ecosystem | https://www.logiwa.com/ecosystem |

## User Reviews

### Ratings

| Platform | Rating | Reviews |
|----------|--------|---------|
| Capterra | 4.6/5 | 95 |
| G2 | 4.0+ | 20+ (Users Love Us badge) |
| Gartner Peer Insights | Available | Multiple |

### Pros
- Automation capabilities
- Patient/responsive support during implementation
- Affordable pricing
- User-friendly, seamless implementation
- Can handle exponential volume jumps

### Cons
- No documentation/tutorials
- Confusing UI in some areas
- No customer service phone number
- Billing glitches
- Performance issues with frequent slowdowns
- Constraining for growing businesses with duplicate-entry workflows

[Source: https://www.capterra.com/p/149744/Logiwa/reviews/]
[Source: https://www.g2.com/products/logiwa-corp-logiwa/reviews]

## Pricing

- **Starting price:** $300/month (quote-based)
- **Volume-based pricing** (not per-seat)
- **Unlimited users** included at all tiers
- Core functionality ungated
- Discovery call required for specifics

[Source: https://www.logiwa.com/pricing]

## Decision Engine

- Rules-based putaway with configurable algorithms
- Smart inventory management for optimized storage
- Multi-warehouse fulfillment network operations
- AI-powered job batching and automation rules
- No dedicated middle-mile transportation routing
- No explicit freight routing or carrier selection optimization

## Integration Assessment

**Classification: OPEN**

| Dimension | Assessment |
|-----------|------------|
| API Surface | REST API with Swagger/OpenAPI, webhook API |
| Public Access | Yes — Swagger UI public, webhook docs public |
| Sandbox | None dedicated |
| Integration Effort | LOW — standard REST with Swagger, well-documented |
| Middle Mile Strength | MODERATE — native cross-docking, sortation integration, no YMS/dock scheduling |
| Decision Engine | Rules-based putaway, no DOM-level routing |

## Sources

- https://myapi.logiwa.com/swagger/index.html
- https://logiwa.my.site.com/logiwahelp/s/article/Logiwa-Open-API
- https://apitracker.io/a/logiwa
- https://www.logiwa.com/solutions/logistics-software-inbound-operations
- https://www.logiwa.com/blog/warehouse-cross-docking
- https://www.logiwa.com/blog/directed-putaway-algorithm-warehouse
- https://www.logiwa.com/blog/automated-sortation-systems-for-3pls
- https://www.logiwa.com/blog/logiwa-webhooks
- https://webhook.logiwa.com/
- https://www.logiwa.com/blog/logiwa-io-next-generation-warehouse-management-system
- https://www.logiwa.com/ecosystem
- https://www.logiwa.com/pricing
- https://www.capterra.com/p/149744/Logiwa/reviews/
- https://www.g2.com/products/logiwa-corp-logiwa/reviews
- https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/logiwa/product/logiwa-io
- https://softwareconnect.com/reviews/logiwa-wms/
