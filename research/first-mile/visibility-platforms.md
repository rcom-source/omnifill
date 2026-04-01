# First-Mile Transportation Visibility Platforms: project44 & FourKites

Research date: 2026-03-31

---

## 1. project44

**Website:** https://www.project44.com/
**Developer Portal:** https://developers.project44.com/
**Support Portal:** https://support.p-44.com/
**Knowledge Base:** https://www.project44.com/company/customer-knowledge-base/

### 1.1 What It Does

project44 is a supply chain visibility and decision intelligence platform connecting shippers, carriers, 3PLs, and LSPs for real-time tracking and predictive analytics across the global supply chain. Branded as the "Movement" platform, it provides end-to-end shipment visibility from origin to destination.

**Modules:**
- **Visibility** -- real-time tracking across all modes
- **Predictive ETAs** -- ML models using telematics, ELDs, traffic, weather (claims 5-10% improvement over legacy systems)
- **Exception Management** -- automated alerts for delays, disruptions
- **Execution** -- LTL rate quoting, transit times, shipment scheduling
- **Network Management Center (NMC)** -- carrier onboarding and management
- **Yard Management System (YMS)** -- dock scheduling, yard operations
- **Inventory Tracking** -- multimodal inventory visibility
- **Supply Chain AI** -- AI-driven analytics and decision support
- **Order Visibility** -- PO/SO/STO/SKU-level tracking

**Transportation Modes:**
- Full Truckload (FTL)
- Less-Than-Truckload (LTL)
- Parcel
- Rail (wagon-level visibility globally)
- Ocean (container-level, including RoRo for non-containerized freight)
- Air
- Intermodal (ocean-to-rail stitching in single view)
- Last mile

### 1.2 Technical Documentation & APIs

**API Architecture:** RESTful, OpenAPI/Swagger spec available (v4.0.0)
- Spec download: https://developers.project44.com/_spec/api-reference/@v4/api-docs.yaml

**Key API Endpoint Groups:**
- **Shipment: Tracking** -- unified shipment tracking across modes
- **Ocean: Tracking** -- container/vessel-level ocean tracking
- **Multi-Modal: Document** -- search and retrieve shipment documents
- **OAuth 2.0: Client Applications** -- token management
- **Webhook** -- event-driven push notifications
- **Inventory, Order, and Load** -- webhook push data
- **LTL Rate Quoting** -- rate quotes and transit times
- **LTL Shipment Scheduling** -- dispatch/scheduling

**Developer Resources:**
- Developer Portal: https://developers.project44.com/
- API Reference: https://developers.project44.com/api-reference/api-docs
- Webhook Guide: https://developers.project44.com/api-reference/webhook-guide
- Authentication Guide: https://developers.project44.com/api-reference/authentication
- Shipper/LSP guides and Carrier/Capacity Provider guides
- Release notes

**SDKs:** No public SDKs found. Integration is REST API-based.

### 1.3 Authentication Methods & Integration Patterns

**Authentication:**
- **OAuth 2.0 (Client Credentials Grant)** -- primary method. Client ID + secret issued upon registration, used to generate bearer tokens over HTTPS.
- **Basic Authentication** -- deprecated for all APIs except token generation.

**Webhook Authentication Options (for push notifications):**
- API_KEY -- key name + value in Authorization header with Basic identifier
- BASIC -- username/password
- OAUTH2 -- access token URI, client secret, client ID, client_credentials grant
- MTLS -- mutual TLS
- AD_OAUTH2_CERT -- Azure AD OAuth2 with certificate

**Integration Patterns:**
1. **REST API** (preferred) -- HTTP/JSON/XML
2. **Webhooks** -- granular delta updates, filtered by event type or mode; smaller payloads than polling
3. **Batch/Flat File** -- CSV or XML file exchange
4. **EDI** -- supported but explicitly discouraged by project44 as "slow to implement, error prone and expensive"
   - EDI 204 (Load Tender), EDI 214 (Shipment Status), EDI 990 (Tender Response)

**Carrier Integration Methods:**
- API push (lat/long, milestone events, UTC timestamps)
- DriveView mobile app
- Telematics/ELD account connection
- EDI (least preferred)
- CSV flat file

### 1.4 Help Centers & Community

- **Support Portal:** https://support.p-44.com/ -- ticket submission, search, and tracking
- **Customer Knowledge Base:** https://www.project44.com/company/customer-knowledge-base/ -- step-by-step instructions, troubleshooting, product videos for Movement, YMS, NMC
- **Developer Portal:** https://developers.project44.com/ -- API docs, guides, release notes
- **Help Center:** https://www.project44.com/support -- contact information
- **No public community forum found** -- support is primarily through the portal and direct contact

### 1.5 User Reviews: Pros & Cons

**G2 Rating:** #1 on G2 Spring 2025 Enterprise Grid for Supply Chain Visibility. 691+ reviews. Named to G2's 2025 Top 100 Best Software Products (#80) and #3 for Supply Chain & Logistics.

**Gartner:** Leader in 2025 Gartner Magic Quadrant for RTTVP. Named "Customer's Choice" in Gartner Voice of the Customer report.

**Pros (from G2, Gartner, and industry reviews):**
- Real-time visibility and data accuracy consistently praised
- User-friendly interface
- Strong API integration -- ease of connecting to existing systems
- Responsive customer support
- Shipment exception tracking and inland rail tracking improved significantly (last 24 months)
- Comprehensive multimodal coverage
- Predictive ETAs using ML outperform legacy systems
- Reduced manual tracking effort, increased customer satisfaction

**Cons (from G2, Gartner, Reddit, and industry reviews):**
- Pricing changed without warning for some customers; opaque pricing model
- Tracking for smaller/niche carriers can be inconsistent
- Initial setup and integration can be complex and time-consuming
- Reporting features difficult to navigate; UI lacks visual clarity
- Promised rail tracking capabilities not always fully realized (carrier restrictions)
- Some users want more robust customer support response times

### 1.6 Pricing Model

- **Enterprise custom pricing** -- no public price tiers
- **Per-shipment/per-container model:** Ocean freight approximately $3.03/container (so a 3-container B/L ~$9)
- **Annual SaaS fees** with multi-year contracts; no-cancellation clause reported
- **No monthly options** for public plans
- **Factors:** shipment volume, transport modes, analytics depth, number of carriers
- Contact sales required: https://www.project44.com/

### 1.7 Data Exposed

| Data Type | Available | Notes |
|-----------|-----------|-------|
| Real-time location (lat/long) | Yes | All modes |
| Predictive ETAs | Yes | ML-powered, multi-factor |
| Milestone events | Yes | Pickup, in-transit, delivered, exceptions |
| Shipment status | Yes | Via API and webhooks |
| Documents | Yes | Search/retrieve via Document API |
| Rate quotes | Yes | LTL rate quoting API |
| Transit times | Yes | LTL transit time API |
| Temperature tracking | Yes | For FTL shipments |
| PO/SO/STO/SKU-level detail | Yes | Order-level visibility |
| Exception alerts | Yes | Configurable via webhooks |
| Inventory position | Yes | Multimodal inventory tracking |
| Carrier/vessel info | Yes | Ocean: vessel, container; Rail: wagon-level |

---

## 2. FourKites

**Website:** https://www.fourkites.com/
**Developer Portal:** https://developer.fourkites.com/
**Support Center:** https://fourkites.my.site.com/hc/s/
**Public Knowledge Base:** https://fourkites.my.site.com/publicKB/
**Status Page:** https://status.fourkites.com/

### 2.1 What It Does

FourKites is an AI-powered supply chain orchestration and visibility platform founded in 2014 (Chicago). Tracks 3+ million shipments daily across 200+ countries and territories. Core product is the "Intelligent Control Tower" that unifies real-time data, digital twins, and AI for predictive, actionable insights.

**Modules:**
- **Real-Time Visibility** -- end-to-end shipment tracking
- **Intelligent Control Tower** -- unified command center with digital twins
- **Dynamic Yard** -- yard management, dock scheduling, trailer moves, appointments
- **Advanced Analytics** -- dashboards, reporting, benchmarking
- **Dynamic ETA** -- ML-powered ETAs using billions of data points (shipper/carrier behavior, seasonality, distance, weather)
- **Exception Management** -- automated alerts, disruption management
- **Appointment Scheduling** -- dock door scheduling
- **FourKites Connect** -- carrier self-onboarding platform
- **Supply Chain AI** -- AI digital workers for automation

**Transportation Modes:**
- Full Truckload (FTL)
- Less-Than-Truckload (LTL)
- Rail (including empty rail car tracking)
- Ocean (terminal intelligence, container tracking)
- Air (global air freight visibility)
- Parcel
- Last Mile
- Multimodal (cross-mode journey stitching)

### 2.2 Technical Documentation & APIs

**API Architecture:** RESTful APIs

**Key API Categories:**
- **Tracking Assignment API** -- assign tracking to shipments (TMS integration)
  - GitHub samples: https://github.com/FourKites/Tracking-Information-Assignment-API
  - Multiple language examples (vanilla code + OOP patterns)
- **TMS Locations API** -- location master data management
  - Docs: https://fourkites.my.site.com/publicKB/s/tms-locations-api-integration
- **Dynamic Yard APIs** -- yard operations CRUD
  - Postman collection: https://documenter.getpostman.com/view/19175603/UVXkmZyw
  - Appointments, trailer moves, dock assignments
  - 2-way integration with event subscriptions
- **Status/Load Update APIs** -- push shipment status updates
- **Document Retrieval APIs** -- PRO numbers, shipping documents (LTL)

**Developer Resources:**
- Developer Portal: https://developer.fourkites.com/ -- self-service API key management, API bundles, environment separation
- Public Knowledge Base: https://fourkites.my.site.com/publicKB/
- TMS Integration Guide: https://fourkites.my.site.com/publicKB/s/tms-tracking-assignment-api
- Postman collections for Dynamic Yard APIs
- GitHub code samples for Tracking Assignment API

**SDKs:** No dedicated SDKs. GitHub repo provides integration samples in multiple languages.

### 2.3 Authentication Methods & Integration Patterns

**Authentication:**
- **API Key** -- issued via developer portal; entered during integration setup
- **Basic Authentication** -- username/password
- **Digest Authentication** -- supported alongside Basic

**Integration Patterns:**
1. **REST API** (primary) -- JSON over HTTPS
2. **Webhooks / Event Subscriptions** -- 2-way integration; subscribe to platform events (especially Dynamic Yard)
3. **EDI** -- EDI 214 status messages ingested from carriers (used as "last resort")
4. **SFTP** -- file-based exchange supported
5. **Flat File** -- XML, CSV, JSON formats supported
6. **ELD/GPS Direct Integration** -- telematics provider connections
7. **Web Scraping** -- for carriers without API/EDI (LTL especially)
8. **TMS Integration** -- pre-built connectors for major TMS platforms

**Carrier Integration (FourKites Connect):**
- Self-service carrier onboarding portal
- No cost to carriers for integration or onboarding
- Dedicated carrier onboarding associate provided
- Carriers can connect via ELD/GPS providers or API

### 2.4 Help Centers & Community

- **Support Center:** https://fourkites.my.site.com/hc/s/ -- case submission and tracking via in-app Help Center (question mark icon)
- **Public Knowledge Base:** https://fourkites.my.site.com/publicKB/ -- carrier resources, integration guides, FAQs
- **FourKites Community** -- online forum for customers to share ideas, encourage innovation; functions as social media for supply chain visibility space
- **Carrier FAQ:** https://www.fourkites.com/carrier-faq/
- **Driver Resource Center** -- driver-specific support
- **Contact Support:** https://fourkites.my.site.com/publicKB/s/contactsupport
- **Platform Portal:** https://portal.fourkites.com/

### 2.5 User Reviews: Pros & Cons

**G2 Rating:** 4.5/5 stars from 270+ verified reviews (72% 5-star, 21% 4-star, 5% 3-star). 90% user satisfaction across 532 reviews on 4 review sites.

**Gartner Peer Insights:** Reviewed as a leading RTTVP vendor.

**Pros (from G2, Gartner, Capterra, Lokad, and industry reviews):**
- Easy to use; intuitive interface praised consistently
- Real-time tracking significantly enhances visibility and decision-making
- Simple carrier onboarding process (especially FourKites Connect)
- Seamless TMS integration, reducing manual tracking
- Strong multimodal coverage (especially FTL and LTL)
- Detailed shipment information and shareable tracking links
- Dynamic ETAs using ML are highly valued
- Free carrier integration (no cost to carriers)

**Cons (from G2, Gartner, SoftwareConnect, and industry reviews):**
- **Geofencing false positives** -- if a driver enters and leaves geofence, load marked as delivered even if not actually delivered; requires manual follow-up
- Carrier compliance can affect tracking accuracy
- Occasional technical issues and slow customer support response times
- Steep learning curve for some users
- Setup complexity requiring significant technical knowledge
- Slow performance during order searches
- Pricing accessibility concerns, especially in emerging markets
- Some carriers lack direct integration, falling back to web scraping or EDI

### 2.6 Pricing Model

- **Enterprise custom pricing** -- no public pricing page
- **Tiered pricing model** -- tiers not publicly disclosed
- **Starting range:** reportedly $100-$500/month (likely entry-level or per-seat)
- **Factors:** shipment volume, transport modes, analytics depth, modules selected
- **Free carrier onboarding** -- no cost to carriers
- Contact sales required: https://www.fourkites.com/contact/

### 2.7 Data Exposed

| Data Type | Available | Notes |
|-----------|-----------|-------|
| Real-time location (lat/long) | Yes | All modes |
| Dynamic ETAs | Yes | ML-powered, billions of data points |
| Milestone events | Yes | Pickup, in-transit, delivered, exceptions |
| Shipment status | Yes | Via API and event subscriptions |
| Documents (PRO numbers) | Yes | LTL document retrieval |
| Temperature/IoT data | Yes | Via telematics integration |
| Yard operations | Yes | Appointments, trailer moves, dock assignments (Dynamic Yard API) |
| Dwell time analytics | Yes | At facilities |
| Exception alerts | Yes | Configurable |
| Carrier performance | Yes | Via Advanced Analytics |
| Terminal intelligence | Yes | Ocean mode |
| Order-level detail | Yes | TMS integration |
| Digital twin data | Yes | Via Intelligent Control Tower |

---

## 3. Comparison Summary

| Dimension | project44 | FourKites |
|-----------|-----------|-----------|
| **Founded** | 2014 (Chicago) | 2014 (Chicago) |
| **Modes** | FTL, LTL, Parcel, Rail, Ocean, Air, Intermodal, Last Mile | FTL, LTL, Rail, Ocean, Air, Parcel, Last Mile, Multimodal |
| **API Style** | REST (OpenAPI v4) | REST |
| **Auth** | OAuth 2.0 (Client Credentials) | API Key, Basic, Digest |
| **Webhooks** | Yes (granular, delta, filtered) | Yes (2-way event subscriptions) |
| **EDI Support** | Yes (discouraged) | Yes (last resort) |
| **Flat File/SFTP** | CSV/XML batch | XML/CSV/JSON + SFTP |
| **Developer Portal** | Yes (public, comprehensive) | Yes (self-service key mgmt) |
| **Public API Spec** | OpenAPI YAML downloadable | Postman collections |
| **SDKs** | None | None (GitHub samples) |
| **G2 Rating** | #1 Enterprise Grid 2025 | 4.5/5 (270+ reviews) |
| **Gartner** | Leader + Customer's Choice 2025 | Leader in RTTVP |
| **Pricing** | Custom enterprise; ~$3/container ocean | Custom enterprise; starts ~$100-500 |
| **Carrier Cost** | Not specified | Free for carriers |
| **Unique Strength** | Deepest API/spec maturity; intermodal stitching; LTL rate quoting | Intelligent Control Tower; Dynamic Yard; carrier self-onboarding |
| **Key Weakness** | Opaque pricing; small carrier gaps | Geofencing false positives; setup complexity |

---

## Sources

- [project44 Developer Portal](https://developers.project44.com/)
- [project44 API Reference](https://developers.project44.com/api-reference/api-docs)
- [project44 Authentication](https://developers.project44.com/api-reference/authentication)
- [project44 Webhook Guide](https://developers.project44.com/api-reference/webhook-guide)
- [project44 Visibility Platform](https://www.project44.com/platform/visibility/)
- [project44 Ocean Visibility](https://developers.project44.com/api-reference/api-docs/ocean:-tracking)
- [project44 Rail Visibility](https://www.project44.com/platform/visibility/rail/)
- [project44 Air Visibility](https://www.project44.com/platform/visibility/air/)
- [project44 Carrier API/EDI](https://www.project44.com/carriers/connect/api/)
- [project44 Support Portal](https://support.p-44.com/)
- [project44 Knowledge Base](https://www.project44.com/company/customer-knowledge-base/)
- [project44 G2 Reviews](https://www.g2.com/products/project44/reviews)
- [project44 Gartner Reviews](https://www.gartner.com/reviews/market/real-time-transportation-visibility-platforms/vendor/project44/product/project44-movement)
- [project44 G2 Spring 2025 #1](https://www.project44.com/blog/project44-ranked-1-in-g2s-spring-2025-enterprise-grid-report-for-supply-chain-visibility/)
- [project44 Pricing Guide (Locus)](https://blog.locus.sh/project44-pricing-guide/)
- [FourKites Developer Portal](https://developer.fourkites.com/)
- [FourKites Real-Time Visibility](https://www.fourkites.com/platform/real-time-visibility/)
- [FourKites Tracking Assignment API (GitHub)](https://github.com/FourKites/Tracking-Information-Assignment-API)
- [FourKites Dynamic Yard APIs (Postman)](https://documenter.getpostman.com/view/19175603/UVXkmZyw)
- [FourKites TMS Tracking Assignment Guide](https://fourkites.my.site.com/publicKB/s/tms-tracking-assignment-api)
- [FourKites TMS Locations API](https://fourkites.my.site.com/publicKB/s/tms-locations-api-integration)
- [FourKites Support Center](https://fourkites.my.site.com/hc/s/)
- [FourKites Carrier FAQ](https://www.fourkites.com/carrier-faq/)
- [FourKites Connect](https://www.fourkites.com/network/fourkites-connect/)
- [FourKites G2 Reviews](https://www.g2.com/products/fourkites/reviews)
- [FourKites Gartner Reviews](https://www.gartner.com/reviews/market/real-time-transportation-visibility-platforms/vendor/fourkites/product/fourkites)
- [FourKites Air Freight Visibility](https://www.fourkites.com/press/fourkites-releases-new-capabilities-for-global-air-freight-visibility/)
- [FourKites Ocean/Rail (Manhattan)](https://www.fourkites.com/press/manhattan-associates-extends-tms-visibility-with-fourkites-to-cover-ocean-and-rail-tracking/)
- [Lokad FourKites Review](https://www.lokad.com/review-of-fourkites-com/)
- [Visibility Platform Cost Comparison (Tradlinx)](https://blogs.tradlinx.com/how-much-does-project44-fourkites-or-vizion-really-cost-what-lsps-need-to-know-before-paying-for-premium-visibility-tools/)
- [FourKites Integration (Cleo)](https://www.cleo.com/solutions/application-connectors/fourkites)
- [FourKites Infrastructure (Kai Waehner)](https://www.kai-waehner.de/blog/2025/07/14/inside-fourkites-logistics-platform-data-streaming-for-ai-and-end-to-end-visibility-in-the-supply-chain/)
