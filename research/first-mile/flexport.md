# Flexport - First-Mile Transportation SaaS Research

Research date: 2026-03-31

## 1. Overview

**Company:** Flexport, Inc.
**Founded:** 2013 (San Francisco, CA)
**Revenue:** $2.1B (2024, +30% YoY)
**Website:** https://www.flexport.com/
**Category:** Digital freight forwarder / supply chain platform

Flexport is a technology-first freight forwarder that combines software with logistics
services. It positions itself as a full-stack supply chain platform providing visibility
from factory floor to customer door. Unlike pure-software TMS/WMS vendors, Flexport
operates as a licensed customs broker and freight forwarder — it moves goods and provides
the software to manage that movement.

## 2. Capabilities & Modules

### Transportation Modes Supported

| Mode | Capabilities |
|------|-------------|
| **Ocean (FCL/LCL)** | Full container load, less-than-container load, ocean consolidation services |
| **Air** | Air freight forwarding, charter services, live shipment updates |
| **Truck** | Drayage, cartage, FTL (full truckload), LTL (less-than-truckload) |
| **Rail** | Intermodal rail services |

### Core Platform Modules

- **Freight Forwarding** — Ocean, air, truck, rail booking and management
- **Customs Brokerage** — Licensed brokerage with AI-powered compliance audits; claims 10x lower error rates than competitors
- **Fulfillment (D2C + B2B)** — Warehousing, pick/pack/ship, omni-channel fulfillment
- **Supply Chain Visibility** — SKU-level tracking from PO creation through delivery
- **Trade Finance** — Cargo insurance, financing options
- **Analytics & Reporting** — Shipment analytics, spend analysis, carbon calculation
- **AI/ML Features** — Routing optimization, freight consolidation suggestions, predictive ETAs

### Platform Features

- Satellite-powered shipment visibility across all modes (including non-Flexport shipments)
- Real-time milestone tracking and notifications
- Collaborative portal replacing phone/email workflows
- Shipment-level carbon emissions calculation (4PL feature)
- Integration with 80+ ERP and TMS systems

## 3. Technical Documentation & APIs

### API Portfolio

Flexport exposes **two distinct API surfaces**:

#### A. Flexport API v2 (Freight Forwarding / Trade)

- **Type:** REST, JSON request/response
- **Base docs:** https://apidocs.flexport.com/
- **Developer portal:** https://developers.flexport.com/
- **Versioning:** v2 current (v1, v3 also available); date-versioned (2023-07-01)
- **License:** Apache 2.0
- **Spec:** Not confirmed OpenAPI; JSON in both directions

**Endpoint categories:**

| Resource | Operations |
|----------|-----------|
| Shipments | List, retrieve, update, shareable URLs |
| Shipment Legs | Route segment details |
| Containers | List, retrieve |
| Container Legs | Ocean container movement |
| Bookings | Create, list, retrieve, amend (with line items) |
| Purchase Orders | CRUD + line items |
| Products | Create, retrieve, update, delete |
| Commercial Invoices | Create, update, retrieve (for customs/landed cost) |
| Customs Entries | Retrieve detailed customs datasets |
| Documents | Post/retrieve 35+ logistics document types |
| Freight Invoices | Retrieve with filtering (status, shipment, date range) |
| Companies | CRUD + self-retrieval |
| Company Entities | Organizational units |
| Contacts | Contact management |
| Locations | Location directory |
| Ports | Port directory |
| Carbon Calculation | Emissions data (4PL feature) |
| Webhook Endpoints | Register/manage webhook subscriptions |

#### B. Logistics API (Fulfillment / E-commerce)

- **Type:** REST, OpenAPI 3.0 compliant
- **Base URL:** https://logistics-api.flexport.com
- **Docs:** https://docs.logistics-api.flexport.com/2023-10/
- **Versioning:** Date-based (`yyyy-mm` format); quarterly stable releases; `unstable` branch for experimental features
- **License:** Apache 2.0
- **Error format:** RFC 7807 (problem+json)

**Endpoint categories:**

| Resource | Operations |
|----------|-----------|
| Orders | Fulfillment order creation, status tracking |
| Inbounds | Inventory shipments, quotes |
| Parcels | Label creation, tracking, cancellation |
| Products | Catalog + inventory management |
| Bundles | Bundle definitions |
| Returns | Return order processing |
| Reports | Fulfillment report generation |
| Events | 12+ event types |
| Webhooks | Event subscriptions |
| OAuth | Multi-merchant partner authorization |

**Custom headers:**

| Header | Direction | Purpose |
|--------|-----------|---------|
| `x-correlation-id` | Response | UUID v4 request correlation |
| `idempotency-key` | Request | POST/PATCH idempotency |
| `idempotent-replayed` | Response | Indicates cached response |

### EDI Support

- **Standard:** ANSI X12 4010
- **Developer docs:** https://developers.flexport.com/edi/

| Transaction Set | Description |
|----------------|-------------|
| EDI 850 | Purchase Order |
| EDI 300 | Booking Request |
| EDI 214 | Air Shipment Status |
| EDI 315 | Ocean Shipment Status |
| EDI 310 | Ocean Freight Invoice |
| EDI 110 | Air Freight Invoice |
| EDI 856 | Ship Notice/Manifest (ASN) |

**Note:** EDIFACT is not documented. Communication protocols (AS2, SFTP, VAN) are not
publicly specified — likely requires onboarding to configure. SPS Commerce partnership
provides mapped EDI connections to 115,000+ retail trading partners.

### SDKs

No official SDKs were found. The API is REST/JSON so any HTTP client works. Third-party
tracking integrations exist (e.g., TrackingMore provides a Flexport tracking wrapper).

## 4. Authentication & Security

### OAuth 2.0 (API Credentials) — Recommended

- **Flow:** Client credentials grant (`grant_type=client_credentials`)
- **Token endpoint:** `https://api.flexport.com/oauth/token`
- **Parameters:** `client_id`, `client_secret`, `audience=https://api.flexport.com`
- **Token type:** JWT bearer token
- **Token lifespan:** 24 hours (Forwarding API); 1 year with 1-year grace period (Logistics API merchant tokens)
- **Partner tokens:** Do not expire (Logistics API)
- **Rate limit on token requests:** 10 per day (Forwarding API)
- **Granular scopes:** Credentials can be restricted to specific endpoint sets
- **Management:** Seller Portal > Settings > API Credentials

### API Keys — Legacy

- **Format:** Bearer token (`Authorization: Bearer API_KEY`)
- **Scope:** Unrestricted access to all endpoints (no granular permissions)
- **Management:** Seller Portal > Settings > API Keys; instant revocation available
- **Status:** Still functional but not recommended for new integrations

### Webhook Security

- **Verification:** HMAC signature validation
- **Headers:** `X-Hub-Signature` (SHA-1), `X-Hub-Signature-256` (SHA-256, recommended)
- **Secret token:** Required per endpoint registration

## 5. Webhooks & Events

### Forwarding API Webhook Events

| Event Category | Description |
|---------------|-------------|
| Milestones | Shipment milestone changes |
| Estimated Transit Events | Predicted arrival/departure updates |
| Actual Transit Events | Confirmed arrival/departure events |
| Administrative Events | Booking/shipment admin changes |
| Invoice Events | Invoice creation/updates |
| Document Events | Document uploads/changes |
| PurchaseOrder Events | PO status changes |
| Container Load Result Events | Container loading outcomes |

### Logistics API Events

| Event | Description |
|-------|-------------|
| `EventInbound.ShipmentStatusChanged` | Inbound shipment status update |
| `EventParcel.TrackingUpdated` | Parcel tracking milestone |
| `EventFreight.TrackingUpdated` | Freight tracking update |
| `EventOrder.Cancelled` | Order cancellation |
| `EventOrder.Shipped` | Order shipped |
| `EventOrder.Held` | Order placed on hold |

**Retry policy:** Failed deliveries are retried multiple times over at least 24 hours.

## 6. Data Exposed

| Data Category | Details |
|---------------|---------|
| **Tracking** | SKU-level, container-level, shipment-level; milestone events; satellite-powered visibility |
| **Rates/Quotes** | Quote retrieval, inbound shipment quotes (Logistics API) |
| **Documents** | 35+ document types: BOL, commercial invoices, packing lists, customs docs |
| **ETAs** | Estimated transit events, predictive arrival dates |
| **Events** | 12+ event types via webhooks; milestone-driven notifications |
| **Customs** | Customs entries, HTS classifications, duties, compliance data |
| **Invoices** | Freight invoices with filtering by status, date, shipment |
| **Carbon** | Per-shipment carbon emissions calculations |
| **Network** | Companies, contacts, locations, ports directory |
| **Products** | Product catalog with inventory levels |
| **Purchase Orders** | Full PO lifecycle data |

## 7. Help Centers & Support Resources

| Resource | URL |
|----------|-----|
| Help Center (Fulfillment/Seller) | https://support.portal.flexport.com/hc/en-us |
| Help Center (Forwarding) | https://www.flexport.com/help/ |
| Developer Portal | https://developers.flexport.com/ |
| API Reference | https://apidocs.flexport.com/ |
| Developer FAQ | https://developers.flexport.com/faq/general/ |
| Webhook FAQ | https://developers.flexport.com/faq/webhooks/ |
| Submit Support Request | https://support.portal.flexport.com/hc/en-us/requests/new |
| Pricing/Billing Help | https://www.flexport.com/help/category/quoting-pricing-and-billing/ |

**Live support:** Chat with live agent via Seller Portal, Monday-Friday 7AM-5PM CST.

**Community forums:** No dedicated community forum found. Flexport does not appear to
maintain a public developer community or forum.

## 8. Pricing Model

### Freight Forwarding

- **Model:** Custom/quote-based per shipment
- **Structure:** Not publicly listed; depends on mode, lane, volume, service level
- **Access:** Contact sales for quotes; quotes available through the platform
- **Volume tiers:** Larger shippers (20+ containers/month) get dedicated account managers

### Fulfillment (D2C/B2B)

- **Model:** Usage-based with minimum monthly spend
- **Unit-based pricing:** Includes inbound receiving, inventory placement, picking, packing, packaging material, shipping
- **Zone-based pricing:** Includes inbound receiving, picking, packing, packaging material, shipping (storage billed separately)

**Minimum monthly fees (significant recent change):**

| Period | Minimum Monthly Spend |
|--------|----------------------|
| Jul 1 - Dec 31, 2025 | $500/month |
| Jan 1, 2026+ | $5,000/month |

If eligible spend falls below the minimum, Flexport charges the difference as a fee.
This change has driven some smaller sellers away from the platform.

**Annual carrier rate increases:** 6-10% above 1lb; 15-30% below 1lb (2025 rates).

### Software/Platform

- No separate SaaS subscription fee documented; platform access appears bundled with freight forwarding or fulfillment services
- No self-serve pricing page; custom pricing via sales engagement

## 9. Pros & Cons (Aggregated from G2, Capterra, Trustpilot, Speed Commerce)

### Pros

- **Excellent visibility platform** — Real-time tracking down to SKU level; intuitive dashboard with shipment location display
- **Modern, intuitive UI** — "Cutting edge and very easy to use" (Capterra); clean navigation and milestone notifications
- **Strong technology stack** — AI-powered compliance, routing optimization, freight consolidation suggestions
- **Comprehensive document management** — 35+ document types, automated customs workflows
- **Good API/integration ecosystem** — Well-documented REST APIs, EDI support, 80+ ERP integrations
- **Collaborative portal** — Reduces phone calls and improves response times vs. traditional forwarders
- **Multi-modal coverage** — Ocean, air, truck, rail in a single platform
- **Competitive rates** — Firm quotes help with landed cost calculations
- **Sandbox environment** — Available for Logistics API testing

### Cons

- **Slow quote/booking response times** — Multiple users report delays of days to weeks; traditional forwarders respond in hours
- **Expensive for small shippers** — Higher pricing than traditional forwarders; limited support below 20 containers/month
- **Minimum spend requirements** — $5,000/month minimum (2026+) pushes out smaller sellers
- **Support disparity by volume** — Dedicated account managers only for high-volume clients; smaller accounts get less attention
- **Software-first, logistics-second criticism** — "A software company, not a freight forwarder"; lacks the advisory depth of traditional forwarders
- **Less flexible for ad-hoc needs** — Works best with well-planned logistics; less adaptive to urgent/unplanned shipments
- **No public SDKs** — REST-only; no official client libraries
- **EDIFACT not supported** — X12 only; may be a gap for European trading partners
- **No community/forum** — No public developer community for peer support
- **Financial instability concerns** — Missed 2024 profitability targets; CEO turnover history; high burn rate
- **Fulfillment inventory retrieval issues** — Some users report difficulty getting inventory back when leaving the platform

## 10. Competitive Position for First-Mile

### Strengths as First-Mile Platform

- True multi-modal coverage (ocean, air, truck, rail) in a single API
- PO-to-delivery visibility is core to first-mile use case
- Booking API enables programmatic shipment creation
- EDI 850/856 support covers PO and ASN workflows
- Customs brokerage built-in reduces integration complexity
- Carbon calculation API is a differentiator

### Weaknesses for First-Mile Integration

- Tightly coupled to Flexport-as-forwarder — API is for Flexport customers, not a neutral platform
- No rate-shopping across carriers (Flexport IS the carrier/forwarder)
- Cannot use APIs without being a Flexport freight customer
- Limited to Flexport's carrier network and lane coverage
- No TMS-style carrier management or bid/tender workflows
- Token request rate limit (10/day) is very restrictive for high-throughput integrations

### Key Differentiators vs. Pure TMS/Visibility Platforms

| Feature | Flexport | Pure TMS (e.g., project44, FourKites) |
|---------|----------|--------------------------------------|
| Moves freight | Yes (forwarder) | No (visibility only) |
| Carrier-neutral | No | Yes |
| API for non-customers | No | Yes (often) |
| Customs brokerage | Built-in | Separate integration |
| Fulfillment/warehousing | Yes | No |
| Rate shopping | No (Flexport rates only) | Yes (multi-carrier) |

## 11. Integration Patterns

### Recommended Integration Approach

1. **Authentication:** OAuth 2.0 client credentials flow; cache JWT for 24h
2. **Data sync:** REST API polling + webhook push for real-time events
3. **Idempotency:** Use `idempotency-key` header on all POST/PATCH operations
4. **Error handling:** Expect RFC 7807 error responses (Logistics API); standard HTTP codes (Forwarding API)
5. **Environments:** Sandbox available for Logistics API; no documented sandbox for Forwarding API
6. **EDI:** X12 4010 for high-volume PO/ASN/status exchange

### Rate Limits

- Token acquisition: 10 requests/day (Forwarding API)
- API calls: Not publicly documented; 429 responses with `Retry-After` header
- Webhook retries: At least 24 hours of retry attempts

## Sources

- [Flexport Developer Portal](https://developers.flexport.com/)
- [Flexport API Reference (v2)](https://apidocs.flexport.com/)
- [Logistics API Docs (2023-10)](https://docs.logistics-api.flexport.com/2023-10/)
- [EDI Documentation](https://developers.flexport.com/edi/)
- [API Credentials Tutorial](https://developers.flexport.com/tutorials/using-api-credentials/)
- [Webhook FAQ](https://developers.flexport.com/faq/webhooks/)
- [Flexport Services](https://www.flexport.com/logistics/logistics-services/)
- [Flexport Platform](https://www.flexport.com/products/flexport-platform/)
- [Flexport Integrations](https://www.flexport.com/products/integrations/)
- [Flexport Trucking](https://www.flexport.com/products/trucking/)
- [Flexport Air Freight](https://www.flexport.com/products/air-freight/)
- [Help Center](https://support.portal.flexport.com/hc/en-us)
- [Forwarding Help Center](https://www.flexport.com/help/)
- [2025 Fulfillment Pricing FAQs](https://support.portal.flexport.com/hc/en-us/articles/20420070120087-2025-Flexport-Fulfillment-Pricing-FAQs)
- [Fulfillment Pricing Overview](https://support.portal.flexport.com/hc/en-us/articles/360011693573-Flexport-Omni-Channel-Fulfillment-Pricing-Overview)
- [G2 Reviews](https://www.g2.com/products/flexport/reviews)
- [Capterra Reviews](https://www.capterra.com/p/159808/Flexport/reviews/)
- [Trustpilot Reviews](https://www.trustpilot.com/review/flexport.com)
- [Speed Commerce Review](https://www.speedcommerce.com/vs/flexport-reviews/)
- [Speed Commerce Pricing](https://www.speedcommerce.com/vs/flexport-pricing/)
- [Contrary Research - Flexport](https://research.contrary.com/company/flexport)
- [Stedi EDI Network - Flexport](https://www.stedi.com/edi/network/flexport)
- [SPS Commerce Integration](https://www.flexport.com/products/integrations/sps-commerce/)
