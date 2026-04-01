# Extensiv (3PL Central / Skubana) — Comprehensive Research

> Multi-product fulfillment platform for 3PLs and brands. 8 separate REST APIs.
> Research date: 2026-03-31

---

## 1. Overview & History

Extensiv is a fulfillment technology company formed through acquisitions:
- **3PL Central** — Core WMS for 3PLs (founded 2006)
- **Skubana** — Multi-channel order management (acquired 2021)
- **Scout/TopShelf** — Warehouse management for brands
- **CartRover** — Integration middleware for ecommerce
- **Rebranded to Extensiv** in 2022

**Market position:** Mid-market, focused on 3PL operators and D2C brands. Powers 1,500+ warehouses globally. [Source: https://www.extensiv.com/about]

---

## 2. What It Does: Core Fulfillment Capabilities

### Pick Methods
- **Wave picking** — Group orders into waves by priority, carrier, zone
- **Batch picking** — Multi-order batch with sort-after-pick
- **Discrete picking** — Single order pick for priority/special orders
- **Zone picking** — Zone-based with consolidation
- **Directed picking** — System-directed pick paths with barcode scanning
- **Mobile RF picking** — Android/iOS scanner-based pick workflows
[Source: https://www.extensiv.com/3pl-warehouse-manager]

### Pack Optimization
- Pack verification with barcode scanning
- Directed packing (system suggests box size)
- Multi-item consolidation
- Packing slip and insert management
- Custom packaging rules per customer
- Kitting and assembly workflows
[Source: https://www.extensiv.com/3pl-warehouse-manager/features]

### Shipping & Carrier Selection
- **Extensiv Parcel** — Native multi-carrier shipping
- Rate shopping across carriers (UPS, FedEx, USPS, DHL, regional)
- Label generation (thermal ZPL, PDF)
- Batch label printing
- International shipping support
- Integration with Shippo, ShipStation, EasyPost for expanded carrier access
[Source: https://developer.extensiv.com/ — Parcel API documentation]

### Labor Management
- Basic labor tracking (task completion, productivity metrics)
- Not as deep as enterprise WMS (Manhattan, Blue Yonder)
- Time-on-task reporting
- Employee performance dashboards
[Source: https://www.extensiv.com/3pl-warehouse-manager/features]

### Robotics Integration
- Limited native robotics integration
- Partner integrations with AMR providers via API
- Focused more on software workflows than automation hardware
[Source: https://www.extensiv.com/integrations]

---

## 3. Technical Documentation

### API Architecture — 8 Separate REST APIs

1. **3PL Warehouse Manager API** — Core WMS operations (orders, inventory, receiving, shipping)
   - Base: `https://secure-wms.com/`
   - Docs: https://developer.3plcentral.com/

2. **Order Manager API (Skubana)** — Multi-channel order management
   - Docs: https://documentation.skubana.com/

3. **Hub API** — Cross-product data aggregation
   - Docs: https://developer.extensiv.com/

4. **Billing API** — 3PL billing and invoicing
   - Docs: https://developer.extensiv.com/

5. **Fulfillment Marketplace API** — Connect brands to 3PLs
   - Docs: https://developer.extensiv.com/

6. **Parcel API** — Multi-carrier parcel shipping
   - Docs: https://developer.extensiv.com/

7. **Integration Manager API (CartRover)** — eCommerce channel connectors
   - Docs: https://developer.extensiv.com/

8. **Warehouse Manager API (Scout/TopShelf)** — Brand-side WMS
   - Docs: https://developer.extensiv.com/

### Key 3PL Warehouse Manager API Endpoints
- `POST /orders` — Create/update orders
- `GET /orders/{id}` — Get order details
- `GET /inventory` — Inventory inquiry
- `POST /receivers` — Create receiving orders (ASNs)
- `GET /stockdetails` — Location-level stock
- `POST /customers` — Manage customer (brand) accounts
- `GET /packages` — Shipment/package details
- Supports pagination, filtering, and sorting
[Source: https://developer.3plcentral.com/]

### Developer Portal
- **Public** — https://developer.extensiv.com/ (hub for all APIs)
- **3PL Central API** — https://developer.3plcentral.com/ (most mature docs)
- **Skubana API** — https://documentation.skubana.com/
- API reference with try-it-out functionality
- Postman collections available for some APIs
[Source: https://developer.extensiv.com/]

### Webhooks
- Available on 3PL Warehouse Manager
- Events: order status changes, inventory updates, shipment confirmations
- HTTP POST callbacks to configured URLs
- JSON payload format
[Source: https://developer.3plcentral.com/ — webhook documentation]

---

## 4. Authentication & Integration Patterns

### OAuth 2.0 Client Credentials Flow
- **Token endpoint:** `https://secure-wms.com/AuthServer/api/Token`
- **Credentials:** Client ID + Client Secret (Base64-encoded in Authorization header)
- **Token lifetime:** 30-60 minutes (varies by API)
- **Refresh:** Request new token before expiry
- **Scopes:** Not granular — token grants access to all authorized resources

### Integration Setup
1. Request API access from Extensiv account manager
2. Receive Client ID and Client Secret
3. Exchange credentials for bearer token
4. Include `Authorization: Bearer {token}` in all API calls

### Rate Limits
- Not publicly documented per-API
- General guidance: 60 requests/minute for standard accounts
- Higher limits available for enterprise plans
- 429 Too Many Requests response when exceeded
[Source: https://help.extensiv.com/rest-api/providing-rest-api-access]

### Common Integration Patterns
- **eCommerce → CartRover → 3PL WM** — Orders flow from Shopify/Amazon/etc. through CartRover middleware into WMS
- **3PL WM → Parcel** — Orders fulfilled in WMS, shipped via Parcel API
- **Hub** — Aggregates data across all Extensiv products for reporting
- **Skubana** — Sits on top as order management / demand planning layer

---

## 5. Help Centers, Knowledge Bases & Community

- **Help center:** https://help.extensiv.com/ (public, comprehensive) [Source: https://help.extensiv.com/]
- **3PL Central knowledge base:** https://help.extensiv.com/3pl-warehouse-manager
- **API access guide:** https://help.extensiv.com/rest-api/providing-rest-api-access
- **Extensiv Academy** — Training courses and certifications
- **Support:** Email, phone, chat (business hours). Enterprise gets dedicated CSM.
- **Community:** No public developer forum. Support via help desk tickets.
- **YouTube channel:** Product demos and tutorials [Source: https://www.youtube.com/@extensiv]
- **Blog:** Industry content at https://www.extensiv.com/blog

---

## 6. Carrier Integration Capabilities

### Via Extensiv Parcel
- **Major carriers:** UPS, FedEx, USPS, DHL Express, DHL eCommerce
- **Regional carriers:** OnTrac, LSO, Spee-Dee, CDL Last Mile
- **International:** DHL, FedEx International, UPS International
- **Rate shopping:** Automated carrier/service selection based on rules (cost, speed, destination)
- **Label generation:** ZPL thermal labels, PDF labels
- **Tracking:** Real-time tracking updates via carrier APIs
- **Manifest:** End-of-day manifesting
- **Returns:** Return label generation

### Via 3rd-Party Integrations
- ShipStation connector
- Shippo connector
- EasyPost connector
- ShipEngine connector
[Source: https://www.extensiv.com/integrations]

---

## 7. Pricing Model

- **Not publicly listed.** Requires quote from sales.
- **3PL Warehouse Manager:** SaaS subscription, priced per warehouse/user
  - Estimated: $500–$2,000/month per warehouse (industry estimates)
  - Per-user fees on top of base
- **Order Manager (Skubana):** Per-order pricing + base platform fee
  - Estimated: $1,000–$5,000/month depending on volume
- **Parcel:** Per-label fee
- **CartRover:** Per-integration connector fees
- **Bundle discounts** for multi-product adoption
- Free trials available for some products
[Source: https://www.g2.com/products/extensiv-3pl-warehouse-manager/reviews — pricing discussions in reviews]

---

## 8. Pros & Cons from Real Users

### Pros
- **Purpose-built for 3PLs** — Billing, multi-client management, customer portals built in [Source: https://www.g2.com/products/extensiv-3pl-warehouse-manager/reviews]
- **Strong eCommerce integrations** — CartRover connects 80+ channels (Shopify, Amazon, WooCommerce, etc.)
- **Public API** — Well-documented, accessible without enterprise sales process
- **Reasonable price point** — Accessible for mid-market 3PLs (vs. Manhattan/Blue Yonder)
- **Cloud-native** — No on-prem infrastructure needed
- **Multi-product suite** — WMS + OMS + shipping in one platform
- **Good for scaling 3PLs** — Grows from 1 to many warehouses

### Cons
- **8 separate APIs is confusing** — Product acquisitions resulted in fragmented API surface [Source: https://www.g2.com/products/extensiv-3pl-warehouse-manager/reviews]
- **Integration complexity** — CartRover middleware adds a layer between channel and WMS
- **Limited advanced WMS features** — Not as deep as Manhattan/Blue Yonder for complex warehouse ops
- **Reporting limitations** — Users report needing external BI tools for advanced analytics
- **API rate limits** — Can be restrictive for high-volume operations
- **Customer support** — Mixed reviews; response times vary [Source: https://www.capterra.com/p/137981/3PL-Warehouse-Manager/reviews/]
- **Skubana integration still maturing** — Post-acquisition product integration is ongoing
- **Mobile app limitations** — RF/scanner app UX could be improved

[Source: https://www.g2.com/products/extensiv-3pl-warehouse-manager/reviews]
[Source: https://www.capterra.com/p/137981/3PL-Warehouse-Manager/reviews/]
[Source: Reddit r/ecommerce — "3PL Central / Extensiv" experience threads]

---

## 9. Implications for Omnifill Integration

### Integration Feasibility: HIGH
- Public REST APIs with documentation
- OAuth 2.0 standard auth flow
- Well-documented 3PL Warehouse Manager API covers core WMS operations
- No partnership or licensing required for API access (just an account)

### Recommended Approach
1. Start with **3PL Warehouse Manager API** — covers orders, inventory, receiving, shipping
2. Add **Parcel API** for carrier/shipping operations
3. Use **CartRover** patterns as reference for channel integration design
4. **Hub API** for cross-product data if needed

### Key Challenges
- 8 APIs with different conventions and maturity levels
- Token management across multiple API endpoints
- Rate limits may constrain high-frequency polling (prefer webhooks)
- Skubana API may be deprecated/consolidated in future

---

## Sources

- https://developer.extensiv.com/
- https://developer.3plcentral.com/
- https://documentation.skubana.com/
- https://help.extensiv.com/rest-api/providing-rest-api-access
- https://help.extensiv.com/
- https://www.extensiv.com/about
- https://www.extensiv.com/3pl-warehouse-manager
- https://www.extensiv.com/integrations
- https://www.g2.com/products/extensiv-3pl-warehouse-manager/reviews
- https://www.capterra.com/p/137981/3PL-Warehouse-Manager/reviews/
- Reddit r/ecommerce — Extensiv/3PL Central discussion threads
