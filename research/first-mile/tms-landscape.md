# TMS & Multi-Modal Orchestration Platform Landscape

Research date: 2026-03-31

This document covers eight transportation management systems (TMS) and multi-modal
platforms relevant to first-mile fulfillment orchestration. For each platform we
document capabilities, API surface, authentication, data exposed, pricing model,
and user-reported strengths and weaknesses.

---

## 1. Oracle Transportation Management (OTM)

**Vendor:** Oracle (part of Oracle Supply Chain Management Cloud)
**Type:** Enterprise TMS
**URL:** https://www.oracle.com/scm/transportation-management/

### Capabilities

Oracle OTM is a full-lifecycle TMS covering planning, execution, freight payment,
and business intelligence across all major transportation modes.

**Modes supported:** Truckload (TL), Less-than-Truckload (LTL), Parcel, Air, Rail,
Ocean, Intermodal, Barge.

**Key features:**
- Multi-modal shipment planning with automated carrier/mode/service selection
- Multi-leg and multi-carrier intermodal routing (single-carrier and multi-carrier models)
- Real-time track and trace with embedded ML-based ETA prediction (air, ocean, rail, intermodal, barge)
- Freight audit and payment
- Dock scheduling and appointment management
- Fleet management for private/dedicated fleets
- Global trade management (GTM) bundled in the same platform
- Continuous move and pool-point optimization
- Routing guide management and core carrier programs

### APIs and Developer Documentation

**API style:** REST (JSON)

**Base URI patterns:**
- Cloud: `/GC3/int-api/...` (integration API, not SSO-protected)
- Cloud: `/logisticsRestApi/resources/...` (SSO-protected, browser-origin)
- On-premise 6.4.x: similar structure

**Documentation:**
- REST API reference (25c): https://docs.oracle.com/en/cloud/saas/supply-chain-and-manufacturing/25c/faips/otm-rest-apis.html
- REST API Getting Started (6.4.3 on-prem, PDF): https://docs.oracle.com/cd/E65625_01/doc.121/api/E92131_01.pdf
- Cloud REST overview: https://docs.oracle.com/en/cloud/saas/transportation/24b/otmol/configuration/about_rest_apis.htm
- On-premise doc library: https://docs.oracle.com/cd/E65625_01/nav/otm.htm

**Metadata discovery:** `GET /GC3/api/metadata/{entityName}` returns fields, data types,
and child record structure for any entity.

**Entity-level design:** All REST interactions occur at the top-level entity. Updating
child records is done through the parent entity endpoint.

**Access control:** Individual REST APIs are protected by ACLs (View and Edit).
Users must be granted ACL access before calling any endpoint.

### Authentication

- **Primary:** HTTP Basic Authentication over HTTPS (Base64 encoded username:password
  of a staged integration user in OTM)
- **OAuth 2.0:** Not natively supported in OTM REST API as of 2026 (per Oracle Support Doc 2696318.1)
- **SSO:** The `/logisticsRestApi/resources` path is SSO-protected for browser-based access

### Data Exposed

- Shipments (orders, order releases, shipment groups)
- Shipment legs and stops
- Carriers and carrier services
- Rate offerings and contracts
- Freight bills and invoices
- Tracking events and milestones
- Location/site master data
- Equipment types
- Business rules and routing guides

### Pricing

- Cloud: Starts at ~$450/month (subscription, scales with shipment volume and modules)
- On-premise: Perpetual license + maintenance (typically enterprise-negotiated)
- Implementation costs are substantial (6-18 months typical)
- Total cost often reaches six to seven figures for enterprise deployments

### Pros

- Perfect 100 score for delivery ETA accuracy in analyst evaluations
- Best-in-class multi-modal optimization (all modes including barge)
- Deeply configurable with extensive business rules engine
- Strong ROI reported by large shippers
- Embedded ML for predictive analytics
- Combined TMS + GTM in one platform

### Cons

- Long implementation timelines (months to over a year)
- Steep learning curve, especially for non-Oracle integrations
- Requires significant internal resources for configuration changes
- Complex setup for multi-system integration
- UI modernization lags behind newer cloud-native competitors

---

## 2. SAP Transportation Management (SAP TM)

**Vendor:** SAP (embedded in S/4HANA or standalone)
**Type:** Enterprise TMS
**URL:** https://help.sap.com/docs/SAP_TRANSPORTATION_MANAGEMENT

### Capabilities

SAP TM is deeply integrated with the SAP ERP ecosystem, providing end-to-end
transportation planning and execution.

**Modes supported:** Truck (FTL/LTL), Rail, Ocean, Air, Intermodal.

**Key features:**
- Transportation planning and optimization with constraint-based solver
- Freight order and freight booking management
- Carrier selection and tendering
- Freight cost calculation and settlement
- Dock scheduling and yard management
- Subcontracting management
- Charge management with complex tariff structures
- Integration with SAP EWM, SAP MM, SAP SD
- Event management and track/trace
- Embedded analytics via SAP BW/HANA

### APIs and Developer Documentation

**API styles:** OData/REST (via SAP Gateway), BAPI/RFC (legacy), IDocs (EDI), SOAP

**Integration patterns:**
- **OData services:** Exposed via SAP Gateway (`/sap/opu/odata/...` path prefix).
  Built using SEGW transaction creating DPC_EXT classes with CRUDQ methods.
- **BAPIs:** Business Application Programming Interfaces callable via RFC protocol.
  Many are being migrated to OData exposure in S/4HANA.
- **IDocs:** Standard EDI document exchange (X12, EDIFACT mappings)
- **CPI/Integration Suite:** SAP Cloud Platform Integration for middleware-based flows

**Documentation:**
- SAP TM help: https://help.sap.com/docs/SAP_TRANSPORTATION_MANAGEMENT
- SAP Business Accelerator Hub (API catalog): https://api.sap.com/
- SAP Developers portal: https://developers.sap.com/
- S/4HANA Cloud TM: https://help.sap.com/docs/SAP_S4HANA_CLOUD (transportation section)

### Authentication

- **Basic Auth:** Standard for OData service consumption
- **OAuth 2.0:** Supported via SAP Cloud Platform Identity Authentication Service
- **X.509 certificates:** For system-to-system RFC/IDoc connections
- **SAP Logon Tickets / SAML:** For SSO scenarios

### Data Exposed

- Freight orders and freight bookings
- Freight units and packaging
- Transportation planning points
- Carrier and forwarding agent master data
- Rate tables and tariff structures
- Freight cost documents and settlement
- Tracking events
- Vehicle and resource data
- Scheduling and dock appointments

### Pricing

- S/4HANA embedded: Part of S/4HANA license (starts at ~$800K for enterprise)
- Standalone: Annual license blocks (~$2.5M per block in some contract structures)
- Implementation: Typically $500K-$5M+ depending on scope (12-24 month timelines common)
- Requires ongoing SAP TM specialist/consultant resources

### Pros

- Seamless integration with SAP ERP modules (MM, SD, EWM, FI)
- Strong analytics and reporting (88/100 in analyst scoring)
- Robust dock scheduling and yard management
- Process automation reduces manual work
- Multi-modal planning on a single platform
- HANA-powered real-time analytics

### Cons

- Extremely complex implementation (months to years)
- Steep learning curve requiring experienced SAP TM consultants
- High total cost of ownership (licensing + implementation + specialists)
- Excessive clicks/data entry for routine tasks (poor UX)
- Tightly coupled to SAP ecosystem (difficult for non-SAP shops)
- Configuration of tariffs and pricing is particularly challenging

---

## 3. Blue Yonder TMS (formerly JDA)

**Vendor:** Blue Yonder (acquired by Panasonic, formerly JDA Software)
**Type:** Enterprise TMS
**URL:** https://blueyonder.com/solutions/transportation-management

### Capabilities

Blue Yonder TMS provides transportation planning, execution, and optimization
with strong ties to Blue Yonder's WMS and supply chain planning suite.

**Modes supported:** Truck (TL/LTL), Air, Ocean, Rail, Intermodal, Parcel.

**Key features:**
- Transportation planning and optimization (route, mode, carrier selection)
- Transportation execution and tendering
- Real-time tracking and tracing
- Freight audit and payment
- Carrier management and compliance
- Load consolidation and optimization
- Fleet management
- Analytics and reporting dashboards
- Integration with Blue Yonder WMS and demand planning

### APIs and Developer Documentation

**API styles:** REST, SOAP, EDI (X12, EDIFACT), OData

**Integration platform:** Blue Yonder Connect - API & Expansion Pack
- Massive library of pre-built connectors
- Enhanced API management tools
- Supports legacy SOAP, REST, EDI, OData protocols
- API key management and traffic throttling
- Higher throughput capacity

**EDI support:** X12 and EDIFACT for inbound/outbound Motor Carrier, Air, and Ocean freight.
Standard messages include load tenders, replies, shipment status, invoicing,
reservation/booking requests, confirmations, scheduling, itineraries.

**Documentation:** Gated behind Blue Yonder Success Portal (customer/partner login required)
- URL: https://success.blueyonder.com (login required)
- No public developer portal or API reference

### Authentication

- **API keys:** Managed through Blue Yonder Connect
- **Security features:** Data access monitoring, API key management, traffic throttling
- **Specific auth protocols:** Not publicly documented

### Data Exposed

- Shipment orders and load plans
- Carrier rates and contracts
- Tracking events and status updates
- Freight invoices and audit data
- Route and lane data
- Carrier performance metrics
- Inventory visibility (via WMS integration)

### Pricing

- Subscription-based, starting at ~$100,000/year
- Scales with usage, user count, and modules
- Cloud and on-premise deployment options
- Implementation costs: hundreds of thousands to millions
- Positioned for large enterprises with significant resources

### Pros

- Centralized hub for all transportation activities
- Real-time tracking and tracing
- Strong analytics and cost optimization tools
- Deep integration with Blue Yonder WMS
- 85% user satisfaction rating across 211 reviews

### Cons

- Extremely outdated user interface
- Basic functions are unnecessarily complicated
- Complex and time-consuming implementation
- Requires experienced users for advanced features
- Only viable for large enterprises with significant budgets
- No public API documentation (fully gated)

---

## 4. Manhattan Associates TMS

**Vendor:** Manhattan Associates
**Type:** Enterprise TMS (Manhattan Active Transportation Management)
**URL:** https://www.manh.com/solutions/supply-chain-management-software/transportation-management

### Capabilities

Manhattan Active TMS is a cloud-native, microservices-based platform providing
transportation planning, execution, and optimization.

**Modes supported:** Truck (TL/LTL), Parcel, Rail, Ocean, Air, Intermodal.

**Key features:**
- Multi-modal transportation planning and optimization
- Dynamic load building and consolidation
- Carrier selection, tendering, and compliance
- Real-time visibility and tracking
- Freight audit and payment
- Appointment scheduling
- Route optimization
- Unified with Manhattan Active WM and Manhattan Active Omni
- "Lego approach" microservices architecture enabling rapid customization

### APIs and Developer Documentation

**API style:** REST (JSON), fully microservices-based

**Architecture:** Every Manhattan Active solution is composed entirely from microservice
APIs. All APIs are publicly accessible to licensed customers for calling, sharing,
and extending.

**Documentation:**
- Developer Hub: https://developer.manh.com/
- API Reference: https://developer.manh.com/docs/how-to/rest-api/reference/
- Calling APIs: https://developer.manh.com/docs/how-to/rest-api/
- Authentication Guide: https://developer.manh.com/docs/how-to/rest-api/authentication/
- Postman Guide: https://developer.manh.com/docs/how-to/rest-api/postman/
- Enterprise Integration (async vs sync): https://developer.manh.com/docs/concept-guides/enterprise-integration/

**Integration patterns:**
- Synchronous: HTTPS REST endpoints
- Asynchronous: Messaging (event-driven)
- All APIs use JSON payloads with consistent calling conventions

### Authentication

- **OAuth 2.0:** Primary authentication method with OAuth authorization grants/flows
- **HTTPS:** All API endpoints require HTTPS
- **JWT tokens:** Used for authenticated session management

### Data Exposed

- Orders (purchase orders, sales orders, transfer orders)
- Shipments and loads
- Carrier rates and contracts
- Stops and appointments
- Tracking events and milestones
- Freight costs and invoices
- Location and site data
- Equipment and vehicle data
- Driver and carrier profiles
- Thousands of endpoints across the full platform

### Pricing

- Subscription-based (monthly or yearly per user)
- Small business (10 users): $500-$1,000/user/month
- Enterprise (1,000 users): $100-$300/user/month
- Implementation: $10K-$50K (small) to $100K-$500K (enterprise)
- Among the most expensive options (ITQlick score 10/10 on cost)

### Pros

- Modern cloud-native microservices architecture
- Intuitive interface praised for ease of use
- Thousands of open API endpoints
- Comprehensive developer documentation (public Developer Hub)
- Strong integration with Manhattan Active WM
- Great value for money despite high price (per user reviews)
- Easiest integrated TMS per some reviews

### Cons

- Premium pricing limits accessibility
- No mobile access (desktop only as of 2026)
- Some users find customization options limited
- Requires Manhattan Active ecosystem for full value
- Rated 63/100 overall among supply chain systems despite 4/5 stars

---

## 5. TMW Systems / Trimble TMS

**Vendor:** Trimble Transportation (acquired TMW Systems in 2012 for $335M)
**Type:** Trucking/Fleet TMS
**Products:** TMW.Suite, TruckMate
**URL:** https://transportation.trimble.com/

### Capabilities

Trimble's TMS products (TMW.Suite and TruckMate) are purpose-built for the
trucking and freight brokerage industry, with deep fleet management capabilities.

**Modes supported:** Truck (TL/LTL), primarily surface transportation. Not designed
for ocean, air, or rail (trucking-centric).

**Key features:**
- Dispatch and fleet management
- Order management and load planning
- Driver management and compliance (HOS, ELD integration)
- Brokerage operations
- Fuel tax reporting (IFTA)
- Equipment and maintenance tracking
- Integrated accounting (Microsoft Dynamics GP integration)
- Load board connectivity (multiple marketplace integrations)
- Rate quoting and contract management
- Billing and settlements

### APIs and Developer Documentation

**API style:** RESTful (JSON)

**Available APIs (TruckMate):**
1. **TruckMate API** - Business-critical data: orders, reports, trips, and more
2. **Master Data API** - Configuration data: client/vendor/driver profiles, sites, zones, commodity codes
3. **Finance API** - Invoices, payments, GL entries (available since v2024.3)

**Key endpoints (Master Data examples):**
- `GET /clients` - Client profiles
- `GET /serviceLevels` - Service level codes
- `GET /commodities` - Commodity codes
- `GET /aChargeCodes` - Accessorial charge codes
- `POST /tm/orders?type=q` - Rate quotes

**Documentation:**
- Developer portal: https://developer.trimble.com/docs/truckmate/
- Authentication: https://developer.trimble.com/docs/truckmate/authentication/
- Getting started: https://developer.trimble.com/docs/truckmate/guides/access/
- TruckMate API reference: https://developer.trimble.com/docs/truckmate/reference/openapi/truckmate/
- General Trimble developer docs: https://www.trimble.com/en/developer/docs

**API licensing:** Hundreds of endpoints available when APIs are licensed. Requires
separate API license in addition to base TruckMate license.

### Authentication

- **OAuth 2.0 Bearer Token:** Primary method. Bearer token must be set in the
  Authorization header of every request.
- Token obtained through OAuth 2.0 flow against on-premise API server

### Data Exposed

- Orders and order details
- Trips and trip legs
- Drivers and driver profiles
- Equipment (trucks, trailers)
- Client and vendor profiles
- Sites and zones
- Commodity codes
- Service levels
- Accessorial charges
- Invoices, payments, GL entries (Finance API)
- Reports

### Pricing

- Quote-based, not publicly listed
- Three tiered plans based on modules, users, and data integration requirements
- Estimated range: $100-$500+ per user/month
- Cloud-based and on-premise deployment options
- API access requires separate licensing

### Pros

- Deep specialization for trucking/fleet operations
- Comprehensive accounting integration (Dynamics GP)
- Cloud-based with auto-save
- Multiple load board integrations
- Well-documented REST API with OpenAPI spec
- Strong dispatch and driver management
- Good for LTL operations

### Cons

- Very antiquated technology (origins in 1980s)
- TMW.Suite requires multiple standalone modules open simultaneously
- Frequent crashes and stability issues reported
- Complex driver/tariff setup is error-prone
- Learning curve is significant
- Not suitable for multi-modal (ocean/air/rail)
- Separate API licensing adds cost

---

## 6. Descartes Aljex (formerly Aljex Software)

**Vendor:** Descartes Systems Group (acquired Aljex)
**Type:** Freight Broker TMS
**URL:** https://www.aljex.com/

### Capabilities

Descartes Aljex is a cloud-based TMS designed specifically for freight brokers
and 3PLs, emphasizing speed, compliance, and connectivity.

**Modes supported:** Truck (TL/LTL), with connectivity to multi-modal through
Descartes Global Logistics Network.

**Key features:**
- Order management and load execution
- Carrier procurement and rate management
- Automatic rate confirmations and e-signatures
- Real-time shipment tracking (via Descartes MacroPoint integration)
- Document management and compliance tracking
- Carrier onboarding automation
- Critical event notifications and alerts
- Customer invoicing and billing
- Manifesting
- Load board posting

### APIs and Developer Documentation

**API style:** REST APIs + EDI (via Descartes Global Logistics Network)

**Integration ecosystem:**
- 40+ pre-built integrations with freight technology and SaaS providers
- Connected to thousands of companies via EDI and API through Descartes Global Logistics Network
- Integrations with carrier tracking systems, WMS, OMS, and other logistics platforms

**Documentation:** Not publicly available. Integration documentation provided to
customers and partners through the Descartes partner program.

**Pricing page (with integration info):** https://www.aljex.com/pricing/
**Partners/integrations:** https://www.aljex.com/partners/

### Authentication

- Not publicly documented
- Likely API key or OAuth-based (standard Descartes patterns)

### Data Exposed

- Load/order data
- Carrier and shipper profiles
- Rate quotes and confirmations
- Tracking events and shipment status
- Documents (BOL, POD, rate confirmations)
- Invoice and billing data
- Carrier compliance and onboarding status

### Pricing

- **Basic plan:** Starts at $290-$350/month for up to 5 users
- Scales to support 2 to several hundred users
- Quote-based for enterprise capabilities
- Pricing designed to support growth and user adoption
- Custom API integrations may add cost

### Pros

- Purpose-built for freight brokers (broker-first design)
- Fast and intuitive interface with good automation
- Deep Descartes MacroPoint integration for real-time tracking
- 15x faster bookings reported by users
- 30-40% less time on load tracking
- 98% on-time delivery performance
- Affordable entry point for small brokers

### Cons

- Interface can feel dated compared to newer competitors
- Occasional performance glitches and slow loading
- Customer support described as slow (callback model)
- Split-screen and some features don't work smoothly
- Limited to brokerage operations (not shipper/enterprise TMS)
- API documentation not publicly accessible

---

## 7. 3Gtms (3G Transportation Management)

**Vendor:** 3G (now part of the go3g.com family with Pacejet Shipping)
**Type:** Cloud TMS (shipper, broker, 3PL)
**URL:** https://www.3gtms.com/ / https://go3g.com/

### Capabilities

3Gtms is a SaaS-first TMS platform targeting omnichannel shippers, freight
brokers, and 3PLs who need to scale across shipment volumes and service offerings.

**Modes supported:** Truckload (TL), Less-than-Truckload (LTL), Parcel, Intermodal.
Ocean and air support is limited or handled through partner integrations.

**Key features:**
- Rating, routing, and optimization (TL, LTL, parcel, intermodal)
- Quote management
- Load execution and tendering
- Track and trace with continuous visibility
- Customer invoicing, billing, and freight audit
- Driver management with activity visibility
- Load planning and optimization
- Complex domestic routing (multi-stop, multi-leg, pool points)
- Integration Hub (proprietary middleware layer)
- Carrier network connectivity
- Native ERP integrations
- Pacejet Shipping for parcel/small package
- Logistics Marketplace for partner tools

### APIs and Developer Documentation

**API style:** REST (via Integration Hub)

**Integration Hub:** Proprietary middleware layer between 3Gtms core and customer
systems, simplifying integration with varied software environments.

**Connectivity:**
- ERP integrations (native-level)
- Carrier network APIs
- Partner marketplace integrations
- Standard EDI support

**Documentation:** Not publicly available. Integration handled through 3Gtms
professional services and the Integration Hub.

- Product page: https://go3g.com/products/3g-transportation-management/
- API blog post: https://go3g.com/blog/using-a-tms-system-and-business-logic-to-complete-the-api-equation/

### Authentication

- Not publicly documented
- Managed through the Integration Hub middleware layer

### Data Exposed

- Orders and shipments
- Rate quotes and carrier rates
- Load plans and optimization results
- Tracking events and visibility data
- Invoices and billing records
- Audit trails
- Driver activity data
- Carrier and customer profiles

### Pricing

- Subscription-based with tiered plans
- Starting at ~$4,000/month
- Varies based on freight under management and transaction volume
- Implementation and onboarding costs additional

### Pros

- 87% user satisfaction rating (62 reviews)
- Strong load management and driver visibility
- Scalable SaaS architecture
- Good optimization and planning tools
- Integration Hub simplifies connectivity
- Support for complex routing scenarios
- Analytics and reporting portal

### Cons

- Steep learning curve for new users
- BI tools need refinement
- Optimization tool is separate from main system
- Routing maps lack clarity
- No public API documentation
- Ocean and air support limited
- Higher price point than broker-focused TMS options

---

## 8. Blume Global

**Vendor:** Blume Global (acquired by WiseTech Global in 2024)
**Type:** Multi-modal visibility and orchestration platform
**URL:** https://www.blumeglobal.com/

### Capabilities

Blume Global is a cloud-first, API-enabled platform focused on multi-modal
supply chain visibility, asset management, and logistics orchestration. It
connects across the entire logistics ecosystem rather than functioning as a
traditional TMS.

**Modes supported:** Road (truck), Ocean, Rail, Air - full multi-modal coverage
for domestic and international shipments.

**Key features:**
- Real-time multi-modal shipment visibility (single interface for all modes)
- Predictive analytics and ML-based ETA forecasting
- Intelligent control tower functionality
- Proactive exception management
- Asset management and optimization (motor carriers, ocean carriers, IMCs)
- Booking solutions (bills of lading, sailing schedules, voyages)
- Freight audit and pay
- CarrierGo platform for carrier-side operations
- Logistics tendering and settlement
- POD verification
- ELD tracking integration
- Connection to thousands of carriers, terminals, DCs, CFS, IoT sensors

### APIs and Developer Documentation

**API style:** REST (JSON)

**API categories (6 major groups):**

1. **Visibility APIs**
   - Geo Location API (for customers)
   - Get Event API (for customers)
   - Milestone API (for carriers - pull and push variants)
   - ELD Tracking API (for carriers)

2. **Shipment Services APIs**
   - Comprehensive shipment lifecycle management on the platform

3. **Freight Audit & Pay APIs**
   - Separate endpoints for originators and carriers
   - Transparency and granular visibility on freight costs

4. **Asset Management APIs**
   - Optimal logistics move determination for motor carriers, ocean carriers, IMCs

5. **Booking Solutions APIs**
   - Booking management, bills of lading, sailing schedules, voyage data
   - Separate request/response APIs for customers vs. beneficial cargo owners (BCOs)

6. **CarrierGo APIs**
   - Logistics tendering
   - Tracking and event capture
   - POD verification
   - Settlement initiation

**Documentation:**
- Developer docs: https://www.blumeglobal.com/api-documentation-test/
- Booking API (UAT): https://uat-apps.blumesolutions.com/documentation-central/blumeAPIBookingDocuments/index.html
- Platform overview: https://www.blumeglobal.com/platform/

### Authentication

- **API Key:** Primary method. API key sent as authorization token with each request.
  Missing or expired keys return errors.
- Specific OAuth implementation details not publicly documented

### Data Exposed

- Shipment location and tracking data (real-time, multi-modal)
- Event milestones and status updates
- ELD tracking information
- Freight audit and payment details
- Asset availability and optimization data
- Booking and voyage information
- Bills of lading
- Sailing schedules
- Carrier and terminal data
- IoT sensor data (temperature, humidity, shock, etc.)

### Pricing

- Subscription-based (enterprise pricing)
- Structured by shipment volume, enterprise size, and feature access
- Higher price point reflecting enterprise-grade capabilities
- Total cost includes platform fees, implementation services, and ongoing support
- Potentially prohibitive for mid-sized organizations
- Contact sales for quotes

### Pros

- True multi-modal visibility (ocean, air, rail, ground) in single interface
- Broad carrier network with direct integrations (reduces custom API work)
- ML-powered predictive analytics and ETA forecasting
- Six well-structured API categories covering the full logistics lifecycle
- Strong data connectivity across thousands of data sources
- Cloud-first, API-enabled architecture
- WiseTech Global acquisition adds scale and resources

### Cons

- UI described as "raw but usable"
- Less flexible with data ingestion than competitors
- ERP integration and data export can be challenging
- Long implementation timelines for complex supply chains
- High cost for smaller organizations
- API documentation could be more detailed (authentication specifics lacking)

---

## Comparison Matrix

| Platform | Modes | API Style | Auth | Public Docs | Pricing Entry |
|----------|-------|-----------|------|-------------|---------------|
| Oracle OTM | All (TL/LTL/Parcel/Air/Rail/Ocean/Intermodal/Barge) | REST | Basic Auth | Yes (Oracle docs) | ~$450/mo cloud |
| SAP TM | Truck/Rail/Ocean/Air/Intermodal | OData/REST, BAPI/RFC, IDoc | Basic/OAuth2/X.509 | Partial (SAP Help) | ~$800K+ enterprise |
| Blue Yonder TMS | Truck/Air/Ocean/Rail/Intermodal/Parcel | REST/SOAP/EDI/OData | API Keys | No (gated portal) | ~$100K/yr |
| Manhattan Active TMS | Truck/Parcel/Rail/Ocean/Air/Intermodal | REST (microservices) | OAuth 2.0 | Yes (developer.manh.com) | $100-1000/user/mo |
| Trimble (TMW/TruckMate) | Truck (TL/LTL) only | REST | OAuth 2.0 Bearer | Yes (developer.trimble.com) | $100-500/user/mo |
| Descartes Aljex | Truck (TL/LTL) | REST + EDI | Not public | No | $290-350/mo (5 users) |
| 3Gtms | TL/LTL/Parcel/Intermodal | REST (via Integration Hub) | Not public | No | ~$4,000/mo |
| Blume Global | Road/Ocean/Rail/Air (all) | REST | API Key | Partial | Enterprise (contact) |

## Integration Accessibility for Omnifill

**Best API access (public, documented):**
1. **Manhattan Active TMS** - Full Developer Hub with OAuth 2.0, OpenAPI specs, Postman collections
2. **Trimble TruckMate** - Public developer portal with OpenAPI reference, OAuth 2.0
3. **Oracle OTM** - Comprehensive Oracle docs, metadata discovery endpoint, but Basic Auth only

**Moderate access (partial docs, requires licensing):**
4. **SAP TM** - SAP Business Accelerator Hub has some OData specs, but TM-specific endpoints require SAP access
5. **Blume Global** - Developer page exists with API category descriptions but limited technical detail

**Gated/opaque (requires partnership or sales engagement):**
6. **Blue Yonder TMS** - Fully gated behind Success Portal
7. **3Gtms** - Integration Hub managed by professional services
8. **Descartes Aljex** - Integration docs provided only to customers/partners

## Relevance to First-Mile

For first-mile transportation orchestration, the most relevant platforms are:

- **Oracle OTM** and **SAP TM** for enterprise shippers who already run these as their
  TMS of record. Omnifill adapters would need to pull shipment/order data and push
  fulfillment status updates.

- **Manhattan Active TMS** is the most integration-friendly with its microservices
  architecture and public API documentation. Strong candidate for an early adapter.

- **Trimble TruckMate** is critical for trucking-focused first-mile (pickup from
  warehouse to consolidation point). Well-documented REST APIs make it feasible.

- **Blume Global** is the best candidate for multi-modal visibility integration.
  Its visibility APIs can provide real-time tracking data across all modes that
  Omnifill can consume and normalize.

- **Descartes Aljex** and **3Gtms** serve the broker/3PL segment. Integration would
  give Omnifill coverage of the brokerage layer in first-mile logistics.

- **Blue Yonder TMS** remains a gated target requiring partnership engagement,
  similar to the Blue Yonder WMS situation documented in `wms-api-landscape.md`.

## Sources

- https://docs.oracle.com/en/cloud/saas/transportation-management/ [Source: Oracle OTM documentation]
- https://api.sap.com/ [Source: SAP Business Accelerator Hub]
- https://help.sap.com/docs/SAP_TRANSPORTATION_MANAGEMENT [Source: SAP TM help docs]
- https://success.blueyonder.com [Source: Blue Yonder Success Portal (gated)]
- https://developer.manh.com [Source: Manhattan Associates Developer Hub]
- https://developer.trimble.com/docs/truckmate-api [Source: Trimble TruckMate developer portal]
- https://www.aljex.com/ [Source: Descartes Aljex website]
- https://www.3gtms.com/ [Source: 3Gtms website]
- https://www.blumeglobal.com/ [Source: Blume Global website]
- https://www.g2.com/categories/transportation-management [Source: G2 - TMS reviews]
- https://www.capterra.com/transportation-management-software/ [Source: Capterra - TMS reviews]
- Reddit r/logistics, r/supplychain [Source: Reddit - TMS platform discussions]
