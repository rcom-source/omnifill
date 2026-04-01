# First-Mile Transportation SaaS/TMS Research: Shipwell & Mastery Transportation

**Date:** 2026-03-31
**Purpose:** Evaluate Shipwell and Mastery Logistics Systems (MasterMind) as first-mile transportation platforms for potential Omnifill integration.

---

## 1. Shipwell

**Website:** https://www.shipwell.com/
**Developer Portal:** https://docs.shipwell.com/
**Founded:** 2016, Austin TX
**Architecture:** Cloud-native, multi-tenant SaaS, microservices on REST API

### 1.1 What It Does

Shipwell is an API-first, all-in-one multimodal TMS built on a single codebase. It targets mid-market shippers, 3PLs, and brokers.

**Capabilities/Modules:**
- Shipment planning, rating, booking, and execution
- Carrier procurement and management
- Real-time visibility and tracking (24/7, map-based)
- Freight audit and pay (EDI 210 processing)
- Dock scheduling
- Routing guide automation
- Spot market negotiations and load boards
- Purchase order management
- Contract and rate management
- AI-powered pricing intelligence
- Analytics and reporting

**Transportation Modes Supported:**
| Mode | Status |
|------|--------|
| Truckload (TL/FTL) | Full support |
| Less-Than-Truckload (LTL) | Full support |
| Volume Truckload (VTL) | Full support |
| Partial Truckload (PTL) | Full support |
| Bulk | Full support |
| Parcel | Full support (multi-carrier rate comparison, label gen) |
| Intermodal | Full support |
| Rail | Full support (GPS tracking, SPLC data) |
| Ocean | Container tracking, drayage |
| Air | On roadmap (schedules and booking) |
| Drayage | Full support (automated container tracking) |

### 1.2 Technical Documentation & APIs

**API Architecture:** RESTful, JSON-encoded responses, resource-oriented URLs, standard HTTP verbs.

**API Version:** v2 Core API (current: v2.7.646), OpenAPI/OAS compliant.

**Base endpoint structure:** `/v2/...` (all endpoints require trailing slashes)

**Core API Endpoint Groups (26+ categories):**
1. Locations — address book management
2. Alert Events — notifications
3. Users — user administration
4. Relationships — shipper/carrier relationships
5. Carrier Management — carriers, tags, bids
6. Contracts & Rates — contract and rate config
7. Companies & Customers — company data
8. Documents — document handling
9. Imports — data import
10. Invoicing — billing and invoice management
11. Multi-Mode — multi-modal transportation
12. Permissions — access control
13. Products — product catalog
14. Purchase Orders — PO management
15. Shipments — core shipment CRUD and actions
16. Tenders — tender management
17. Loadboard — load board operations
18. Private Market — private marketplace
19. Quoting — rate quoting
20. Spot Negotiations — spot market
21. Reference Data — standard codes
22. Registration — registration services
23. Policies — policy management
24. Service Agreements — SLA management
25. Service Providers — provider management
26. Suppliers — supplier management

**Additional API Products:**
- Events and Webhooks API
- Freight Pay/Audit API
- Dock Scheduling API
- Shipment Assembly API
- Orders API
- Groups/Auth Microservice API
- Genesis/Carrier Connections API
- Integration Marketplace/Loadboards API

**Integration Methods:**
- REST API (primary)
- Webhooks (event-driven push)
- EDI (204, 210, 214, etc.)
- SOAP (supported but REST preferred)
- Postman collections available for testing

**SDKs:** No official SDKs found. API is REST-first with Postman collections.

### 1.3 Authentication

**Primary: Token-based auth**
- Header: `Authorization: Token <user-token>` (32-char hex string)
- Obtain via `POST /v2/auth/token/` with `{"email": "...", "password": "..."}`
- Verify via `GET /v2/auth/me/` (returns user details or 401)

**Alternate: API Key auth**
- Header: `Authorization: APIkey <api-key>`
- Less common; returned alongside token from auth endpoint

**Security requirements:**
- HTTPS only (HTTP fails)
- Dedicated machine user accounts recommended for integrations
- Environment-specific tokens (sandbox vs production)
- SOC 2 compliant

### 1.4 Webhooks & Event Data

**Event-driven architecture:**
- Subscribe to events via webhook URL configuration
- Events delivered as JSON POST requests
- Example events: `shipment.created`, `shipment.updated`, `purchase_order.line_item.updated`
- Config fields: `enabled_events`, `status`, `url`, `custom_data`, `event_version`

**Delivery characteristics:**
- At-least-once delivery (not exactly-once)
- 5 retry attempts with 10-second response timeout
- Order NOT guaranteed (events may arrive out of sequence)
- HTTP 2xx = successful delivery

**Event categories:** Shipment events, purchase order events, carrier events, tracking events.

### 1.5 Data Exposed

- **Tracking:** Real-time GPS-based location, shipment status, ETA, milestones
- **Rates:** Instant multi-carrier rate comparison, contract rates, spot rates
- **Documents:** BOL, POD, invoices, labels (PDF/2PL/EPL2), customs documents
- **ETAs:** Dynamic ETA with configurable updates
- **Events:** Status changes, exceptions, delays, customs holds, demurrage alerts
- **Reference data:** SPLC codes, carrier SCAC, terminal data
- **Financial:** Invoices, freight audit data, carrier payouts

### 1.6 Help Centers & Support

- **Knowledge Base:** Intercom-hosted at https://intercom.help/shipwell/en/ (~118 articles)
- **Developer Portal:** https://docs.shipwell.com/ (API docs, guides, OpenAPI spec)
- **Support Portal:** Dedicated TMS support portal (contact CSM or CustomerSuccess@shipwell.com)
- **Resources Hub:** https://www.shipwell.com/resources (guides, webinars, case studies)
- **FAQ:** https://www.shipwell.com/faq
- **Blog/Knowledge Center:** https://shipwell.com/category/knowledge-base/
- **No public community forum found**

### 1.7 Pricing

- **Model:** SaaS subscription
- **Starting price:** ~$1,000/month (per SelectHub/GetApp)
- **Custom pricing** based on volume, features, company size
- **No per-shipment pricing publicly listed**
- **Contact sales for quotes**

### 1.8 User Reviews (Pros & Cons)

**Ratings:**
- Capterra: 4.4/5 (17 reviews)
- G2: Listed with positive reviews
- Gartner Magic Quadrant: Named 2021, 2022, 2023

**Pros:**
- Extremely intuitive UI, usable with zero logistics background
- Real-time tracking is a standout feature
- Strong customer service and CSM support
- API-first architecture makes integration straightforward
- Cost savings from consolidating tools
- Good multi-modal support in a single platform
- Modern tech stack (vs legacy TMS platforms)

**Cons:**
- Location/tracking updates sometimes lag or show incorrect info
- Freight class occasionally misclassified, leading to surcharges
- Some shipping options show available but don't return quotes
- Repetitive manual tasks lack dropdown/quick-select options
- Limited automation in certain workflow areas
- Smaller carrier network compared to established players
- Relatively new platform (less battle-tested at massive scale)

**No dedicated Reddit threads found on r/logistics or r/supplychain specifically about Shipwell.**

---

## 2. Mastery Logistics Systems (MasterMind)

**Website:** https://www.mastery.net/
**Developer Portal:** No public developer portal found
**Founded:** 2019, Chicago IL (by Coyote Logistics founders)
**Architecture:** Cloud-native on Microsoft Azure, analytics on Snowflake

### 2.1 What It Does

MasterMind is an enterprise-grade, cloud-native TMS designed for large carriers, 3PLs, brokers, and shippers. It emphasizes automation, unified operations, and scale. Tagline: "The World's First Lovable TMS."

**Capabilities/Modules:**
- Freight procurement and automated capacity creation
- Contract management with automated tender acceptance
- Dynamic routing guides with rule-based carrier assignment
- Back office automation (invoice verification, billing)
- Fleet management (private fleets, dedicated fleets, for-hire)
- Driver management (HOS, preferences, availability, pay/settlements)
- Real-time visibility and Dynamic Load ETA
- Load planning and optimization
- Multi-mode route comparison
- Integrated CRM
- Compliance monitoring
- Analytics and reporting (Snowflake-powered)
- Minion self-service admin portal (configuration, integrations, rules engine)

**Transportation Modes Supported:**
| Mode | Status |
|------|--------|
| Truckload (TL/FTL) | Full support |
| Less-Than-Truckload (LTL) | Full support |
| Drayage | Full support |
| Bulk | Full support |
| Intermodal | Full support |
| Dedicated fleets | Full support |
| Private fleets | Full support |
| Freight brokerage | Full support |
| Power-only / Relay | Full support |
| Rail | Not explicitly documented |
| Ocean | Not explicitly documented |
| Air | Not explicitly documented |
| Parcel | Not explicitly documented |

MasterMind's strength is land-side transportation (truck, intermodal, drayage) and fleet management. Ocean/air/parcel support is not prominently featured.

### 2.2 Technical Documentation & APIs

**Critical finding: No public developer portal or API documentation exists.**

Mastery does NOT publish an open API reference, developer portal, or SDK. Integration is handled through:

**Integration Methods:**
- **API connections** — described as available but documentation is private/customer-only
- **EDI** — Full EDI support through flexible data gateway
  - EDI 204 (Load Tenders)
  - EDI 990 (Load Tender Responses)
  - EDI 214 (Shipment Status Messages)
  - EDI integration via Orderful partnership
- **Ingress APIs** — for routing EDI data directly
- **JSON-defined workflows** — Minion portal allows custom task definitions in JSON
- **ELD integrations** — direct sync with electronic logging devices
- **MileMaker API** — native routing integration (Guide 20 endpoint)
- **Platform Science integration** — driver tablet connectivity

**Integration Architecture:**
- Minion "Connection Station" — toggle-based activation of third-party integrations
- No-code/low-code configuration for EDI and workflow rules
- Customer-specific rule sets configured during implementation
- Changes activate immediately without IT tickets or code deployment

**Authentication:** Not publicly documented. Likely handled through implementation partnership.

### 2.3 Authentication & Integration Patterns

- **No public auth documentation** — authentication is managed through direct customer integration projects
- **Enterprise integration model** — Mastery works alongside customer IT teams during onboarding
- **Closed ecosystem** — unlike Shipwell's open API-first approach, MasterMind operates as a managed integration platform
- **Partnership-based access** — technical details shared during sales/implementation process

### 2.4 Data Exposed

Based on product documentation and case studies:
- **Tracking:** Real-time shipment visibility, Dynamic Load ETA, GPS-based location
- **Rates:** Contracted rates, automated rate validation, dynamic pricing
- **Documents:** BOL, invoices, settlement documents, compliance records
- **ETAs:** Dynamic Load ETA with real-time updates
- **Events:** Status updates (EDI 214), load tender responses (EDI 990), milestone events
- **Fleet data:** Driver HOS, equipment status, trailer tracking, driver availability
- **Financial:** Automated invoicing, driver pay/settlements, accessorial charges
- **Analytics:** Snowflake-powered reporting and utilization analytics

### 2.5 Help Centers & Support

- **No public help center or knowledge base found** for MasterMind TMS
- **In-app training tools** with utilization reporting
- **Customized training packages** per customer
- **Training materials released with every product update**
- **Minion admin portal** serves as self-service configuration interface
- **Direct customer support** through implementation and CSM teams
- **No public community forum**
- **LinkedIn presence:** https://www.linkedin.com/company/mastery-logistics-systems

### 2.6 Pricing

- **Model:** Enterprise SaaS (custom pricing)
- **No public pricing available**
- **Company revenue estimated at $250M-$500M** (LeadIQ data)
- **Targets large enterprise customers** (Werner, Prime, Schneider, Averitt, Keurig Dr Pepper)
- **Contact sales required** for pricing information

### 2.7 User Reviews (Pros & Cons)

**No G2 or Capterra product reviews found for MasterMind TMS.** Available feedback comes from enterprise case studies and Glassdoor employee reviews.

**Pros (from customer case studies and product marketing):**
- Trusted by major carriers: Werner Enterprises, Prime Inc., Schneider, Averitt
- Co-designed with enterprise customers (not built in isolation)
- True cloud-native architecture (vs cloud-hosted legacy systems)
- Unified platform for brokerage, fleet, and 3PL operations
- Strong automation capabilities reduce manual work
- Minion self-service portal reduces vendor dependency
- Azure/Snowflake infrastructure provides scale and analytics
- Handles complex multi-mode, multi-division operations

**Cons (from Glassdoor employee reviews and analysis):**
- Closed ecosystem — no public API docs, hard to evaluate technically
- Enterprise-only positioning — not accessible to mid-market
- Founded 2019, still maturing (though backed by Coyote founders)
- Glassdoor employee reviews mention poor internal communication and demanding work culture
- No independent user reviews on standard review platforms
- Limited public documentation makes integration assessment difficult
- EDI-heavy approach may lag behind pure API-first competitors
- No visible parcel, ocean, or air capabilities

**No Reddit discussions found on r/logistics or r/supplychain about MasterMind TMS.**

---

## 3. Comparative Summary

| Dimension | Shipwell | Mastery MasterMind |
|-----------|----------|-------------------|
| **Target Market** | Mid-market shippers, 3PLs, brokers | Large enterprise carriers, 3PLs |
| **API Openness** | Open, public developer portal, OpenAPI spec | Closed, no public API docs |
| **Auth Model** | Token + API Key, self-service | Private, implementation-managed |
| **Primary Modes** | All modes (8+) including ocean, air | Land-focused: TL, LTL, drayage, intermodal, fleet |
| **Integration Style** | API-first (REST + webhooks + EDI) | EDI-first + managed API integrations |
| **Webhooks** | Yes, documented event system | Not publicly documented |
| **Developer Experience** | Strong (portal, Postman, OpenAPI) | Minimal (no public resources) |
| **Self-Service** | Yes (sandbox, docs, API keys) | No (requires partnership/sales) |
| **Help/KB** | Intercom KB (~118 articles) + dev portal | In-app training, no public KB |
| **Public Reviews** | Capterra 4.4/5, G2 listed, Gartner MQ | No public review profiles |
| **Pricing** | From ~$1,000/mo | Enterprise custom (undisclosed) |
| **Key Customers** | Mid-market, various | Werner, Prime, Schneider, Averitt, Keurig Dr Pepper |
| **Founded** | 2016 | 2019 |
| **Cloud Platform** | AWS (implied by microservices arch) | Microsoft Azure + Snowflake |
| **Fleet Management** | Limited | Core strength |

## 4. Integration Feasibility for Omnifill

### Shipwell: HIGH feasibility
- Public REST API with OpenAPI spec enables rapid adapter development
- Self-service sandbox and developer portal
- Token auth is straightforward to implement
- Webhook events enable real-time sync
- 26+ endpoint groups cover shipments, tracking, rates, documents
- Good candidate for first-mile adapter in the Omnifill pattern

### Mastery MasterMind: LOW feasibility (without partnership)
- No public API documentation to build against
- Would require a sales/partnership engagement to access technical specs
- EDI integration is possible but requires direct coordination
- Better suited as a "gated" integration (similar to Manhattan Associates, Blue Yonder in our WMS list)
- If partnership is established, the platform is technically capable (Azure, APIs exist internally)

## 5. Sources

- [Shipwell TMS Platform](https://www.shipwell.com/tms-platform)
- [Shipwell Developer Portal](https://docs.shipwell.com/)
- [Shipwell Authentication Docs](https://docs.shipwell.com/docs/get-connected/authentication/)
- [Shipwell v2 Core API](https://docs.shipwell.com/openapi_pages/backend-core/overview/)
- [Shipwell All Modes TMS](https://www.shipwell.com/solutions/solution-all-modes-tms)
- [Shipwell Webhooks](https://docs.shipwell.com/docs/webhook/what-are-webhooks/)
- [Shipwell Help Center](https://intercom.help/shipwell/en/collections/3317682-knowledge-base)
- [Shipwell FAQ](https://www.shipwell.com/faq)
- [Shipwell Reviews - Capterra](https://www.capterra.com/p/187731/Shipwell/reviews/)
- [Shipwell Reviews - G2](https://www.g2.com/products/shipwell/reviews)
- [Shipwell Pricing - G2](https://www.g2.com/products/shipwell/pricing)
- [Mastery Logistics Systems](https://www.mastery.net/)
- [MasterMind Product Page](https://www.mastery.net/product/)
- [MasterMind EDI Capabilities](https://www.mastery.net/rethinking-edi-how-mastermind-puts-you-in-control/)
- [MasterMind + Platform Science](https://www.platformscience.com/marketplace/mastermind)
- [Mastery + Orderful EDI Integration](https://www.orderful.com/resources/mastery-tms-and-orderful-edi)
- [Werner Deploying MasterMind - FreightWaves](https://www.freightwaves.com/news/werner-deploying-mastermind-tms-investing-in-mastery-logistics-systems)
- [MasterMind Connected Ecosystem](https://www.mastery.net/from-brokerage-to-fleet-how-mastermind-became-the-backbone-of-a-connected-transportation-ecosystem/)
- [Mastery - Microsoft Azure Case Study](https://www.microsoft.com/en/customers/story/1708695620997844688-mastery-logistics-systems-azure-manufacturing-en-united-states)
- [Mastery on Truckstop Marketplace](https://marketplace.truckstop.com/partners/mastery)
