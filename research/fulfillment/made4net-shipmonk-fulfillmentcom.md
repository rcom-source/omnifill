# Fulfillment SaaS Research: Made4net, ShipMonk, Fulfillment.com

Research date: 2026-03-31

---

## 1. Made4net (SCExpert / WarehouseExpert)

### What It Does

Made4net is a global provider of cloud-based supply chain execution (SCE) and warehouse management solutions. Their flagship platform, **SCExpert**, is a unified suite encompassing:

- **WarehouseExpert (WMS)** -- Tier-one WMS handling operations from pop-up microfulfillment sites to complex automated warehouses. System-directed workflows, mobile data capture, configurable rules engine. Claims 20%+ productivity and capacity improvements.
- **LaborExpert** -- Warehouse labor standards solution for assessing and optimizing processes. Engineered labor standards, performance tracking, and incentive management.
- **TransportExpert** -- Transportation management with automatic invoice generation, carrier rate management, driver fees/bonuses calculations.
- **YardExpert** -- Yard management for dock scheduling and trailer tracking.
- **RoutingExpert** -- Last-mile delivery route optimization with proof of delivery (POD).
- **3PLExpert** -- Multi-client 3PL warehouse management with client-level billing.

**Pick Methods:** Supports wave picking, batch picking, zone picking, voice-directed picking, and pick-to-light. Voice-directed putaway, replenishment, and cycle counts also supported.

**Pack Optimization:** Configurable packing rules, cartonization logic, and compliance labeling.

**Shipping/Carrier Selection:** Integrated via TransportExpert with carrier rate shopping. Documented carrier partnerships include USPS, FedEx, DHL, UPS.

**Robotics Integration:** Native WCS (Warehouse Control System) managing ASRS, shuttles, and AGVs directly. Demonstrated integrations with Locus Robotics and Robust.ai AMRs at MODEX 2024. Pre-built connectors for AMR solutions.

**Labor Management:** Dedicated LaborExpert module with engineered standards, real-time performance dashboards, and incentive programs.

### Technical Documentation & APIs

**Architecture:**
- Built on Microsoft technology stack (.NET)
- Service-Oriented Architecture (SOA)
- Messaging-based distributed execution
- Cloud or on-premise deployment

**API / Integration Layer:**
- "Open Integration Layer" with service-based, configurable transaction framework
- Pre-built ERP connectors: SAP, Microsoft Dynamics, NetSuite, Sage
- E-commerce cart integration (WooCommerce documented)
- API is available but **no public developer portal or self-service API documentation exists**
- Integration typically handled through Made4net professional services or partners
- Third-party middleware (e.g., Makini) offers API connectivity to SCExpert

**Developer Tools:**
- Drag-and-drop screen customization (no-code editor)
- Dynamic dashboard builder ("Dashboard Wizards")
- Extensible data model supporting multiple inventory/document configurations
- Extensible business logic at organization, warehouse, and client levels
- New React-based mobile application with dynamic screen generator (2026 release)

### Authentication & Integration Patterns

- LDAP/SAML authentication for user access
- Role-based access control (RBAC)
- Integration is primarily service-oriented (SOA-based messaging) rather than open REST API
- No documented OAuth or API key patterns for external developers
- Integration patterns are typically point-to-point via the Open Integration Layer or through ERP connectors

### Help Centers & Community

- **Knowledge Center:** https://made4net.com/knowledge-center/ -- FAQs, case studies, guides
- **Ask the Experts:** https://made4net.com/knowledge-center/ask-the-experts-faqs/
- **No public developer community or forum** -- support is direct through Made4net
- Gartner Peer Insights reviews available
- PeerSpot profile exists but limited reviews
- G2 profile under "SCExpert Suite"

### Pros and Cons (from Gartner, SelectHub, industry analysts)

**Pros:**
- Very stable platform; does what it advertises
- Strong 3PL understanding -- built for multi-client operations
- Excellent implementation and customization support (onsite and remote)
- Unified platform (WMS + TMS + YMS + Labor + WCS) reduces integration complexity
- Flexible rules engine enables deep customization without code
- Native WCS eliminates need for separate warehouse control system
- Recognized in 2025 Gartner Magic Quadrant and Midmarket Context for WMS
- "Excellent" User Favorite rating on SelectHub
- Average go-live in ~20 weeks

**Cons:**
- Limited resources compared to larger WMS vendors (smaller company)
- Cloud strategy lacks maturity relative to cloud-native competitors
- No public API documentation -- integration requires vendor engagement
- Smaller partner ecosystem than SAP/Oracle/Manhattan
- Limited self-service for developers; heavily reliant on professional services
- Pricing not transparent; requires custom quotes
- Fewer pre-built marketplace/e-commerce integrations compared to modern 3PL platforms

### Pricing Model

- **SaaS subscription model** with monthly fees
- Starting range: ~$500-$1,000/month (entry-level)
- Scales based on users, warehouses, and modules deployed
- Implementation costs are additional (professional services)
- Custom quotes required -- no public price list
- ROI calculator available on website

### Carrier Integration

- Integrated carrier rate management via TransportExpert
- Documented partnerships: USPS, FedEx, DHL, UPS, Vuzix
- Small-parcel shipping with compliance labeling
- LTL/TL carrier support through transportation module
- Native WCS for material handling equipment (conveyors, sorters, ASRS)

---

## 2. ShipMonk

### What It Does

ShipMonk is a technology-driven 3PL (third-party logistics) provider offering end-to-end ecommerce fulfillment services. Founded in 2014, headquartered in Fort Lauderdale, FL.

**Core Services:**
- **Order Fulfillment** -- Pick, pack, and ship for DTC and B2B orders
- **Inventory Management** -- Real-time stock tracking across all warehouse locations
- **Warehousing** -- 3M+ sq ft across 12+ owned/operated fulfillment centers
- **Returns Processing** -- Managed returns with inspection and restocking
- **Subscription Box Fulfillment** -- Specialized kitting and assembly
- **Freight Management** -- Inbound freight coordination

**Pick Methods:** Standard pick-and-pack operations managed by ShipMonk staff. Not user-configurable (ShipMonk manages warehouse operations internally).

**Pack Optimization:** Custom packaging options, branded inserts, gift messaging ($1/blank card, $0.80/custom card + pick fee), fragile item wrapping available.

**Shipping/Carrier Selection:** Virtual Carrier Network (VCN) -- carrier-agnostic rate shopping that automatically selects optimal carrier per shipment based on cost, speed, and destination.

**Labor Management:** Not applicable -- ShipMonk manages all warehouse labor internally. Clients do not manage labor.

**Robotics Integration:** ShipMonk operates their own facilities with proprietary technology. No client-facing robotics integration.

### Technical Documentation & APIs

**API Architecture:**
- RESTful API
- Base URL: https://apidocs.shipmonk.com/
- Versioning: Sequential (v1.###), switched from semantic versioning
- Date/time format: ISO 8601

**Core Endpoints:**
- **Orders** -- Create, update, retrieve, list, submit for processing
- **Products** -- List, create, search, inventory sync
- **Receivings** -- Create, update, list receiving shipments
- **Returns** -- Manage return shipments, list, retrieve
- **Warehouses** -- Retrieve available warehouse locations
- **Webhooks** -- Manage webhook subscriptions

**Webhooks:**
- Shipment notifications
- Order status changes
- Return status updates
- Receiving status notifications

**Rate Limits:**
- General: 100,000 requests/minute (all endpoints except Orders List)
- Orders List: 1,000 requests/30 minutes
- HTTP 429 response with Retry-After header (RFC 1123 format)

**Sandbox Environment:**
- Full sandbox available for testing
- Sandbox maintenance window: 00:00-06:00 EST (typically <30 min)
- Special sandbox-only endpoints for completing orders/receivings/returns

**SDKs:** No official SDKs documented. REST-only.

**Recent API Updates (2025):**
- New endpoints for high-volume inventory synchronization (Products for Inventory Sync POST)
- Pagination improvements for inventory sync results

### Authentication

- **API Key authentication** via `Api-Key` HTTP header
- Keys generated in Account Settings > Stores > Integration API Keys
- Must email support@shipmonk.com to enable API access initially
- No OAuth, no token refresh -- simple static API key

### Help Centers & Community

- **API Docs:** https://apidocs.shipmonk.com/ (comprehensive, with changelog)
- **API Support:** api@shipmonk.com
- **Help Center:** Available through ShipMonk dashboard
- **Shopify App Store** listing with integration docs
- **Third-party integration docs:** Gorgias, Linnworks, Loop Returns, AfterShip, Pandium
- No public developer community forum
- Active presence on review platforms (G2, Capterra, Trustpilot, Software Advice)

### Pros and Cons (from Capterra, G2, Trustpilot, Software Advice, Reddit)

**Pros:**
- Simple, functional UI for order management (hold orders, move inventory, view data)
- Fast fulfillment processing (1-2 day processing and shipping)
- Multiple carrier options with competitive negotiated rates (VCN)
- Backend software is easy to use and frequently updated
- Strong security features
- Good API documentation with sandbox environment
- Large and growing fulfillment center network (12+ locations, 3M+ sq ft)
- Carrier-agnostic approach optimizes shipping costs per package
- International fulfillment capabilities (US, Canada, Mexico, UK, Europe)

**Cons:**
- **Expensive with hidden fees** -- everything costs extra; minimum $250/month platform fee
- **Customer service degradation** -- chat support not always available; tickets go unanswered for days/weeks then marked "resolved" without resolution
- **Operational accuracy issues** -- reports of wrong orders shipped, sloppy packing, inventory loss without credit
- **No FIFO inventory management** -- does not use first-in-first-out for inventory selection
- **Extremely difficult offboarding** -- retrieving inventory takes 6+ months; charged minimum + storage fees throughout; some users resorted to small claims court
- **Billing disputes** -- charges for services not rendered, difficulty getting credits
- **API access requires manual email request** -- not self-service
- No official SDKs
- Trustpilot ratings notably negative compared to curated review sites

### Pricing Model

**Pick & Pack Fees (tiered by monthly volume):**
- <500 orders/month: $3.00 first item
- 501-1,000: $2.50 first item
- 1,001-2,500: $2.25 first item
- 2,501-5,000: $2.00 first item
- 5,001-10,000: $1.80 first item
- 10,000+: Custom pricing
- Additional items: $0.75 each

**Storage:**
- Pallet: $25/month
- Bin: $1-$4/month (varies by size)

**Returns Processing:**
- $2.00 base + $0.50 per additional item

**Other Fees:**
- Minimum monthly platform fee: $250/month
- One-time setup fee (amount not public)
- Receiving: Flat rate for first 2 hours, hourly after
- Gift messaging: $1 (blank) / $0.80 (custom card) + pick fee
- Shipping: Pass-through carrier rates (discounted via VCN)

**Model:** Pay-per-use with volume discounts. Custom quotes for high volume.

### Carrier Integration

**Major Carriers:** UPS, FedEx, USPS, DHL
**Regional Carriers:** LaserShip, OnTrac, ACI
**International:** Passport (DTC international shipping partner)
**Approach:** Virtual Carrier Network (VCN) -- automated rate shopping across all carrier partners per shipment. ShipMonk negotiates bulk rates and passes savings to clients. Carrier selection is automated and optimized per package.

**Warehouse Locations (12+ facilities):**
- Fort Lauderdale, FL (HQ)
- Los Angeles/California (332K sq ft)
- Las Vegas, NV (800K+ sq ft, 2 facilities)
- Pittston, PA (650K sq ft, 2 facilities -- bonded)
- Kentucky
- Texas
- Toronto, Canada
- Czech Republic (EU)
- UK
- Mexico

---

## 3. Fulfillment.com (FDC)

### What It Does

Fulfillment.com (FDC) is a global 3PL provider founded in 2011, specializing in ecommerce order fulfillment. Tagline: "Worldwide Fulfillment Made Easy."

**Core Services:**
- **Order Fulfillment** -- Storage, pick, pack, ship for ecommerce orders
- **Warehousing** -- 8 global fulfillment centers with climate-controlled options
- **Returns Processing** -- Complex return handling and restocking
- **Subscription Fulfillment** -- Recurring order support
- **FDA-Registered Facilities** -- Health and beauty product fulfillment (cGMP-certified manufacturing partnerships)
- **Kitting & Assembly** -- Custom product bundling

**Pick Methods:** Managed internally by FDC operations staff. Not configurable by clients.

**Pack Optimization:** Custom packaging, branded materials, compliance labeling. Address validation to reduce returns. Order grouping for cost reduction.

**Shipping/Carrier Selection:** Multi-carrier approach with negotiated bulk rates. Scheduled carrier pickups at each facility.

**Labor Management:** Not applicable -- FDC manages all warehouse operations internally.

**Robotics Integration:** Not documented. Traditional warehouse operations.

### Technical Documentation & APIs

**Technology Platform -- BestOMS:**
- Proprietary cloud-based Order Management System (OMS) + WMS hybrid
- 24/7 client dashboard access
- Real-time inventory monitoring
- Fulfillment and postage fee verification
- Address validation system
- Product depletion prediction and reorder forecasting
- Order grouping for cost optimization

**API:**
- **RESTful API** (v2 specification)
- Documentation hosted at: https://fulfillment.github.io/api/
- GitHub repository: https://github.com/fulfillment/api
- Supports integration with 65+ ecommerce platforms
- API enables custom-coded integrations beyond pre-built connectors

**Pre-built Integrations:**
- 65+ ecommerce platforms (described as "the world's 43 most popular shopping carts" with additional platforms)
- Integration described as "fast and free" for supported platforms
- CSV upload and manual order input also supported

**Developer Resources:**
- API v2 specification on GitHub Pages (limited public documentation detail)
- No documented SDKs
- No public webhook documentation found
- No documented rate limits
- Technical support likely requires direct engagement with FDC

### Authentication

- Not publicly documented for the API
- BestOMS dashboard uses standard username/password authentication
- API authentication method not specified in publicly available documentation
- Likely requires contacting FDC for API credentials and integration setup

### Help Centers & Community

- **Reviews page:** https://www.fulfillment.com/reviews
- **Resources:** https://www.fulfillment.com/resources/
- No public developer community or forum
- No public knowledge base or help center beyond marketing content
- Listed on WarehousingAndFulfillment.com for third-party reviews
- Trustpilot presence (fulfilment.com -- UK spelling variant)
- Limited presence on G2/Capterra compared to competitors

### Pros and Cons (from reviews, industry analysis)

**Pros:**
- Strong global fulfillment network (8 locations across US, Canada, UK, EU, Australia)
- US network covers 99.97% of households in 1-2 day ground shipping
- Responsive customer service with dedicated account managers
- Competitive pricing compared to major 3PL competitors
- High order accuracy ("spot-on" per multiple reviewers)
- FDA-registered US facilities for health/beauty products
- 65+ ecommerce platform integrations
- RESTful API available for custom integrations
- Address validation reduces failed deliveries
- Long track record (founded 2011)

**Cons:**
- **High minimum volume** -- ~50 orders/day minimum for standard partnership
- **Limited API documentation** -- v2 spec on GitHub Pages is sparse; no comprehensive developer portal
- **No public webhook documentation** -- event-driven integration unclear
- **Pricing not transparent** -- no public price list; custom quotes required
- **Smaller than major competitors** -- fewer facilities and less automation than ShipBob/ShipMonk
- **Scalability concerns for small merchants** -- minimum volume threshold excludes startups
- **Operational inconsistencies across facilities** reported by some users
- **No self-service onboarding** -- requires sales engagement to get started
- **Limited technology transparency** -- BestOMS capabilities not deeply documented
- **No robotics/automation differentiation** -- traditional warehouse operations

### Pricing Model

- **Custom quotes** -- no public pricing
- Previously positioned as "cheapest guys on the block" but has shifted to value-based pricing
- Minimum volume: ~50 orders/day
- Includes: storage, pick & pack, shipping, returns processing
- Carrier rates negotiated in bulk across global warehouse network
- Integration with supported platforms is free
- Expansion programs reportedly in development for smaller merchants

### Carrier Integration

**Documented Carriers:**
- USPS
- FedEx
- UPS
- DHL
- Canada Post
- Chit Chats (Canadian cross-border)
- Parcelforce (UK)
- Royal Mail (UK)
- Australia Post

**Approach:** Multi-carrier with negotiated bulk rates. Scheduled pickups at each facility. Carrier selection optimized per shipment. International shipping supported across all 8 global locations.

**Warehouse Locations (8 global):**
- Salt Lake City, UT (USA)
- Allentown, PA (USA)
- Kansas City, MO (USA)
- Savannah, GA (USA)
- Mississauga, Ontario (Canada)
- Birmingham (UK)
- Neuwied (Germany)
- Dandenong South / Melbourne (Australia)

---

## Comparison Matrix

| Capability | Made4net | ShipMonk | Fulfillment.com |
|---|---|---|---|
| **Type** | WMS Software Platform | 3PL Service + Tech | 3PL Service |
| **Target** | Enterprises running own warehouses | DTC ecommerce brands | Ecommerce brands (50+ orders/day) |
| **API** | SOA integration layer (not public) | REST API (documented) | REST API v2 (sparse docs) |
| **Auth** | LDAP/SAML | API Key header | Not documented |
| **Webhooks** | Not documented | Yes (4 event types) | Not documented |
| **SDK** | None | None | None |
| **Sandbox** | Unknown | Yes | Unknown |
| **Carrier Partners** | USPS, FedEx, DHL, UPS | UPS, FedEx, USPS, DHL + regionals | USPS, FedEx, UPS, DHL + regional/intl |
| **Warehouse Locations** | Client-operated | 12+ owned (US/CA/MX/UK/EU) | 8 owned (US/CA/UK/DE/AU) |
| **Robotics** | Native WCS + AMR integration | Internal only | None documented |
| **Labor Mgmt** | LaborExpert module | Internal | Internal |
| **Min Volume** | Enterprise scale | No minimum (but $250/mo platform fee) | ~50 orders/day |
| **Pricing** | $500-1000+/mo SaaS | Per-pick tiered ($1.80-$3.00) | Custom quotes |
| **Gartner/Analyst** | 2025 MQ recognized | Not in WMS MQ | Not in WMS MQ |

---

## Integration Feasibility for Omnifill

**Made4net:** Hardest to integrate. No public API docs, SOA-based integration requires vendor engagement. Would need partnership or middleware (Makini). Best suited as an adapter target for enterprise customers already running SCExpert.

**ShipMonk:** Most developer-friendly. Public REST API with docs, sandbox, webhooks, and clear authentication. Good candidate for a first-class Omnifill adapter. Rate limits are generous (100K/min). Main risk is operational service quality.

**Fulfillment.com:** Middle ground. REST API exists but documentation is thin. Would require direct engagement with FDC to get full API specs and credentials. Global carrier network is a strength. Volume minimums may limit applicability.


---

## Sources

### Made4net
- https://made4net.com/platform/
- https://made4net.com/made4net-manifest-scexpert-wms-update/
- https://made4net.com/made4net-gartner-2025-midmarket-context-wms/
- https://www.prnewswire.com/news-releases/made4net-demonstrates-warehouse-management-system-capabilities-and-robotics-and-automation-integrations-at-modex-2024-302083296.html
- https://www.g2.com/products/scexpert-suite/reviews

### ShipMonk
- https://apidocs.shipmonk.com/
- https://www.shipmonk.com/platform/api-developer-tools
- https://www.shipmonk.com/pricing
- https://www.shipmonk.com/resources/fulfillment-locations
- https://www.capterra.com/p/153768/ShipMonk/reviews/
- https://www.trustpilot.com/review/shipmonk.com
- https://www.g2.com/products/shipmonk/reviews

### Fulfillment.com
- https://www.fulfillment.com/
- https://fulfillment.github.io/api/
- https://www.fulfillment.com/reviews
