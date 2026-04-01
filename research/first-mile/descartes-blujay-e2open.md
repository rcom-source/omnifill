# Descartes Systems Group, BluJay Solutions, and E2open — First-Mile TMS Research

Research date: 2026-03-31

---

## 1. Descartes Systems Group

**Headquarters:** Waterloo, Ontario, Canada
**Founded:** 1981
**Public:** NASDAQ: DSGX
**Website:** https://www.descartes.com

### 1.1 What It Does

Descartes is a global leader in cloud-based logistics technology. Recognized by ARC Advisory Group in 2025 as the #1 provider of cloud-based TMS solutions. The company has grown through 20+ acquisitions since 2012 (Aljex, MacroPoint, Datamyne, 3GTMS in March 2025, and others).

**Core Capabilities:**
- Multimodal TMS (truckload, LTL, parcel, ocean, air, rail, intermodal)
- Real-time freight visibility (via MacroPoint — connected to carrier telematics)
- Route planning, optimization, and dispatch
- Dock scheduling and yard management
- Fleet mobile applications
- Carrier connectivity and rate management
- Freight audit and payment
- Customs compliance and global trade intelligence (CustomsInfo, Datamyne)
- Denied party screening
- B2B connectivity and EDI messaging

**Modes Supported:**
- **Truck:** FTL, LTL, private fleet, parcel, last-mile
- **Ocean:** 70+ carriers, 500+ ports/terminals, ACE compliance, container tracking
- **Air:** Air cargo tracking, airline industry software
- **Rail:** Rail visibility via IES Web Tracking (key milestones)
- **Intermodal:** Cross-mode planning and execution

**Product Portfolio (selected):**
- Descartes Shipper TMS — multimodal shipper execution
- Descartes Aljex — freight broker TMS
- Descartes 3GTMS — acquired March 2025, extends TMS footprint
- Descartes Forwarder TMS — freight forwarder enterprise suite
- Descartes MacroPoint — real-time visibility and carrier sourcing
- Descartes CustomsInfo — HS code classification, duty rates, trade content
- Descartes Datamyne — global trade data analytics (import/export data from 50+ nations)

### 1.2 Technical Documentation & APIs

**API Portal:** https://api.descartes.com
**API List:** https://api.descartes.com/apis
**API Connectivity Page:** https://www.descartes.com/solutions/b2b-connectivity-and-messaging/api-connectivity

**Descartes MacroPoint APIs (most documented):**

- **Visibility API docs:** https://docs.macropoint.com/
  - REST API for creating, managing, and monitoring shipment tracking sessions
  - Webhook callbacks push visibility updates back to customer systems
  - Location data can be pushed via API or CSV flat file
  - Integration from any TMS via standard API
- **Carrier Integration docs:** https://carrierdocs.macropoint.com/
  - Carrier-side API: lat/long coordinates, complete address, load event updates (arrival/departure), tracking method assignment
- **Capacity Integration docs:** https://capacitydocs.macropoint.com/
  - API and flat file integration for carrier capacity data
- **Postman Workspace (public):** https://www.postman.com/macropoint-telematics
  - Descartes MacroPoint Visibility Customer Integrations collection
  - Descartes MacroPoint Capacity Integration collection

**Descartes CustomsInfo APIs:**
- REST-based, supports JSON and XML
- Endpoints for: HS codes, tariff rates, preferential tariff details, duty calculations, import/export restrictions, licensing requirements, safety certifications, ECCN, Schedule B, FTA/ROO data, denied party screening
- Integrates with WMS, ERP, TMS platforms

**Global Logistics Network (GLN):**
- 26,000+ customers, 200,000+ connected parties, 160+ countries
- 24 billion+ messages annually, 1 billion+ shipping routes managed
- Supported messaging formats: EDIFACT, ANSI X12, XML, partner-specific formats
- Communication protocols: HTTP(S), AS2/AS4, API, sFTP, FTPs, WebServices, OFTP, X400

### 1.3 Authentication Methods & Integration Patterns

- **API Key authentication** (confirmed via developer portal)
- **EDI/B2B:** Traditional EDI via GLN with protocol-level security (AS2/AS4, sFTP)
- **Integration patterns:**
  - Direct REST API integration
  - EDI messaging via GLN
  - Flat file (CSV) upload via SFTP/FTPS
  - Webhook callbacks (MacroPoint visibility)
  - Pre-built connectors to SAP, Oracle, Infor ERPs

### 1.4 Help Centers & Knowledge Bases

- **Service Desk:** servicedesk@descartes.com | 877-786-9339 (NA) | +800-7866-3390 (intl)
- **Support Portal:** ITIL-based, 24/365, issue tracking + knowledge base for self-help
- **Product-specific support:**
  - Aljex Support Center: https://www.aljex.com/support/
  - MacroPoint Support: https://macropoint.com/support/
  - QuestaWeb Support: https://questaweb.com/contact-us/support/
- **No public community forum identified** — support is primarily through service desk and expertise centers

### 1.5 User Reviews — Pros and Cons

**G2 Rating:** 4.6/5 stars (Shipper TMS) — #1 Grid Leader in 12 categories (2024-2025)

**Pros (from G2, Capterra, TrustRadius, Gartner):**
- Centralized view of all lanes, rates, and carriers in one platform
- Excellent route optimization and load consolidation (load optimizer)
- Comprehensive multimodal visibility and real-time tracking
- User-friendly interface, easy setup
- Excellent customer support
- Strong carrier connectivity and multiple tendering options
- Cost control, scheduling, detention management
- Advanced routing and modeling capabilities

**Cons:**
- Upgrades occasionally introduce bugs that are not caught in testing; some persist for extended periods
- Initial setup and configuration can be complex
- Higher cost compared to alternatives
- Ticket-based support can be frustrating — users prefer direct consultant contact
- Acquired-product integration can feel fragmented (many acquisitions = many sub-products)

**Reddit:** No significant Reddit discussions found on r/logistics or r/supplychain specifically about Descartes TMS.

### 1.6 Pricing Model

- **SaaS subscription + per-transaction hybrid model**
- Subscription based on: number of users, transactions, vehicles, or other metrics
- Per-transaction charges for shipment processing, customs filings
- Sample: starts ~$1,000/month for basic transportation visibility, scales up
- Customs solutions: priced by modules needed, monthly declaration volume, concurrent users
- Sellercloud (e-commerce): per-order pricing with 12-month license
- **No public price list** — custom quotes based on requirements

### 1.7 Data Exposed

- **Tracking:** Real-time GPS/telematics positions, arrival/departure events, milestone updates (via MacroPoint)
- **Rates:** Carrier rates, contract rates, spot market rates
- **Documents:** BOL, customs filings, shipping instructions, trade compliance docs
- **ETAs:** Predicted arrival times based on real-time tracking
- **Events:** Load tender, tender acceptance/rejection, pickup, in-transit, delivery, exceptions
- **Trade data:** HS codes, duty rates, tariff schedules, import/export activity, denied party lists
- **Capacity:** Carrier capacity availability and sourcing data

---

## 2. BluJay Solutions (now part of E2open)

**Acquired by E2open:** 2021
**Original HQ:** Chelmsford, UK (European roots)
**Legacy Website:** https://www.blujaysolutions.com (redirects to E2open)

### 2.1 What It Does

BluJay was a leading cloud-based logistics execution platform before acquisition by E2open. It brought a robust suite of logistics applications and a trade network of 50,000+ participants serving 5,700+ global customers.

**Core Capabilities (now under E2open brand):**
- Transportation Management for Shippers (North America and Europe/Australia/Africa variants)
- Freight forwarding and customs management
- Warehouse management
- Parcel shipping
- Supply chain visibility
- Carrier management and rate shopping
- Freight audit and payment
- Trade compliance

**Modes Supported:**
- **Truck:** FTL, LTL, dedicated fleet
- **Ocean:** Container shipping, forwarding
- **Air:** Air freight management
- **Rail:** Intermodal/rail support
- **Parcel:** Multi-carrier parcel management

**Key differentiators when independent:**
- Strong European market presence (unlike many US-centric TMS)
- Configurable workflow engine
- Large carrier network
- Integrated trade compliance

### 2.2 Technical Documentation & APIs

BluJay's technical documentation has been absorbed into E2open's ecosystem. See E2open section below for current API access.

**Known integration methods (from BluJay era):**
- EDI connectivity (204, 214, 990 and other standard documents)
- API-based integrations with third-party systems
- Pre-built connectors (e.g., C.H. Robinson integration: https://www.chrobinson.com/en-au/technology/connectivity-integrations/tms-integrations/e2open/)
- Cleo EDI connector for BluJay: https://www.cleo.com/solutions/application-connectors/blujay
- Rating API integration (e.g., Redwood Logistics integrated their Rating API with BluJay TMS)

**No standalone BluJay developer portal exists anymore** — all developer resources are under E2open.

### 2.3 Authentication & Integration

See E2open section — BluJay's systems now use E2open's authentication and integration infrastructure.

### 2.4 Help Centers & Knowledge Bases

- Absorbed into E2open's support infrastructure
- E2open Customer Support Portal: https://e2open.my.site.com/support/s/
- E2open Knowledge Center: https://knowledge.e2open.com/knowledgecenter/

### 2.5 User Reviews — Pros and Cons

**Gartner Peer Insights (BluJay TMS Legacy):**

**Pros:**
- User-friendly, easy to navigate
- Searchable PO numbers and accessorial submission within the system
- Fast and mostly reliable
- Outstanding message visibility functionality — "one of the best I've ever worked with"
- Easily configurable workflows
- Covers most TMS functionalities out of the box
- Strong European logistics capabilities

**Cons:**
- System downtime was a recurring issue (one user called 2020 integration delays "completely crippling")
- Enhancement timelines too long — users wished for faster feature delivery
- Cost of enhancements outside core product is high
- Difficult vendor relationship — "complex to negotiate with poor customer service"
- Contract negotiation described as "a nightmare with their legal counsels"
- Vendor not focused on building long-term relationships
- Post-E2open acquisition uncertainty about product roadmap

**Reddit:** No significant Reddit discussions found specifically about BluJay TMS.

### 2.6 Pricing Model

Pricing was never publicly disclosed by BluJay. Now folded into E2open's pricing model (see below).

### 2.7 Data Exposed

(Now via E2open platform)
- Shipment status and tracking events
- Rate quotes and carrier rates
- EDI documents (204, 214, 990)
- Booking confirmations
- Customs/compliance documents
- Invoice and freight audit data

---

## 3. E2open

**Headquarters:** Austin, Texas, USA
**Website:** https://www.e2open.com
**Public:** NYSE: ETWO

### 3.1 What It Does

E2open is a cloud-native supply chain platform connecting 400,000+ manufacturing, logistics, channel, and distribution partners. Named a Leader in the 2024 Gartner Magic Quadrant for TMS.

**Core Capabilities:**
- Transportation Management for Shippers (multi-modal)
- Transportation Management for LSPs
- Global trade management and compliance
- Supply chain planning (demand, supply, inventory)
- Channel management and partner management
- Supply chain visibility
- Freight audit and payment
- Carrier marketplace and rate management
- Ocean trade platform (via INTTRA acquisition)
- Appointment scheduling

**Modes Supported:**
- **Truck:** FTL, LTL, dedicated
- **Ocean:** Via INTTRA platform — 60+ carriers, 35,000+ shippers, 177 countries, 850,000+ container orders/week
- **Air:** Air freight management
- **Rail:** Intermodal support
- **Parcel:** Multi-carrier parcel

**Key Acquisitions:**
- **BluJay Solutions (2021)** — logistics execution, European TMS
- **INTTRA** — ocean booking, container tracking, shipping instructions (largest multi-carrier ocean e-commerce platform)
- **Cloud Logistics** — TMS for mid-market

### 3.2 Technical Documentation & APIs

**Developer Portal:** https://knowledge.e2open.com/knowledgecenter/developer/
**INTTRA API Docs:** https://apidocs.inttra.com/
**Carrier Marketplace:** https://marketplace.e2open.com/
**E2net Network:** https://e2net.e2open.com/

**Known APIs:**

1. **Partner Register REST API** — register new channel partners into Global Channel Directory
   - URL: https://knowledge.e2open.com/knowledgecenter/developer/partner-register-rest-api/
   - RESTful, requires OAuth 2.0 access token

2. **Partner Search REST API** — search channel partners in Global Channel Directory
   - URL: https://knowledge.e2open.com/knowledgecenter/developer/partner-search-rest-api/
   - RESTful, requires OAuth 2.0 access token

3. **Real-Time Rating API** — carrier rate quotes
   - Used with EDI 204 (Load Tender) messages
   - Includes carrierRateReference for bid tracking

4. **Appointment Scheduling API** — carrier appointment scheduling
   - Real-time communication between carriers and stakeholders
   - Standard API included with TMS

5. **INTTRA Ocean Execution APIs:**
   - Booking API
   - Ocean Schedules API
   - Rates API
   - Visibility/Track & Trace API
   - RESTful over HTTPS, JSON format
   - DCSA (Digital Container Shipping Association) compliant for Track & Trace

**Integration Methods:**
- REST/JSON APIs
- XML standards
- EDI: 204 (Load Tender), 214 (Shipment Status), 990 (Load Tender Response)
- E2net business network for multi-enterprise connectivity
- Pre-built connectors (Oracle, SAP, etc.)

### 3.3 Authentication Methods & Integration Patterns

- **OAuth 2.0** — primary API authentication method
  - Token-based access; implementation guide available (e2open API OAuth 2.0 Implementation Document)
- **EDI:** Traditional EDI authentication via VAN/AS2
- **Network connectivity:** E2net handles B2B partner authentication
- **Integration patterns:**
  - Direct REST API calls with OAuth tokens
  - EDI document exchange
  - E2net network messaging
  - Pre-built ERP connectors
  - Carrier marketplace integrations

### 3.4 Help Centers & Knowledge Bases

- **Resource Center:** https://www.e2open.com/resource-center/ (whitepapers, case studies, webinars)
- **Knowledge Center/Developer Portal:** https://knowledge.e2open.com/knowledgecenter/
- **Customer Support Portal:** https://e2open.my.site.com/support/s/ (login required, Salesforce-based)
- **INTTRA Help:** https://knowledge.e2open.com/knowledgecenter/inttra/
- **INTTRA Status Page:** https://theoceannetwork.inttra.com/status
- **Carrier Marketplace:** https://marketplace.e2open.com/
- **No public community forum identified** — support is through the customer portal

### 3.5 User Reviews — Pros and Cons

**Gartner:** Leader in 2024 Magic Quadrant for TMS
**G2/GetApp:** Mixed reviews, lower ratings than Descartes

**Pros (from Gartner, G2, TrustRadius, Capterra):**
- Stable and reliable after initial setup period
- Fast and easy to use day-to-day
- Outstanding message visibility functionality
- Cloud-based with good partner integration
- Collaborative implementation experience — flexible and customizable
- Automates transportation needs, increases efficiency and scalability
- INTTRA ocean platform is market-leading for container shipping
- Strong multi-enterprise network (400,000+ partners)

**Cons:**
- System downtime and reliability issues (historically significant)
- Enhancement delivery timelines too long
- Cost of enhancements outside core product
- Difficult contract negotiations — "nightmare with legal counsels"
- Poor customer service in vendor relationship
- Complex product suite (result of many acquisitions — BluJay, INTTRA, Cloud Logistics all have different lineages)
- Integration between acquired products can be rough
- Higher implementation costs ($10K-$50K for SMB, much more for enterprise)
- Post-acquisition product roadmap uncertainty

**Reddit:** No significant Reddit discussions found on r/logistics or r/supplychain about E2open or BluJay TMS.

### 3.6 Pricing Model

- **Pay-per-user subscription model** with tiered pricing
- Base license: ~$100/month for 1 user
- 10 users: ~$800/month
- 100 users: ~$7,000-$10,000/month
- 1,000 users (global enterprise): ~$70,000+/month
- TMS-specific pricing starts at $500-$1,000/month range
- Annual plans: 10-20% discount
- Implementation costs: $10,000-$50,000 for SMB (2-6 months)
- **No public price list** — custom quotes required

### 3.7 Data Exposed

- **Tracking:** Real-time container status (INTTRA), shipment tracking events, GPS positions
- **Rates:** Carrier rates via Real-Time Rating API, contract rates, spot rates
- **Documents:** BOL, shipping instructions, customs filings, EDI documents (204/214/990)
- **ETAs:** Estimated arrival times, milestone-based tracking
- **Events:** Booking confirmation, load tender/response, pickup, in-transit, delivery, exceptions, container events (gate-in, loaded, discharged, gate-out)
- **Ocean-specific (INTTRA):** Vessel schedules, port schedules, booking status, container tracking across 60+ carriers
- **Partner data:** Channel partner directory, partner registration/search
- **Appointment data:** Dock scheduling, carrier appointments

---

## Comparative Summary

| Dimension | Descartes | BluJay (E2open) | E2open |
|-----------|-----------|-----------------|--------|
| **Primary strength** | Visibility + GLN network | European TMS execution | End-to-end supply chain platform |
| **Modes** | All (truck, ocean, air, rail) | All | All (strong ocean via INTTRA) |
| **API maturity** | Moderate — MacroPoint well-documented, others gated | Absorbed into E2open | Moderate — OAuth 2.0, REST/JSON, but docs gated |
| **Public API docs** | MacroPoint: Yes; Others: limited | No (legacy) | Developer portal exists but limited public access |
| **EDI support** | Strong (EDIFACT, X12, XML via GLN) | Strong (204, 214, 990) | Strong (EDI + REST + XML) |
| **Auth method** | API Key | N/A (E2open now) | OAuth 2.0 |
| **G2 rating** | 4.6/5 (Leader) | N/A (legacy) | Lower than Descartes |
| **Pricing** | $1K+/mo, custom | Folded into E2open | $100-$70K+/mo by users |
| **Network scale** | 26K customers, 200K parties, 160 countries | 50K+ participants (pre-acq) | 400K+ partners |
| **Postman collections** | Yes (MacroPoint) | No | No |
| **Ocean strength** | Good (70+ carriers) | Moderate | Best (INTTRA: 60+ carriers, 850K orders/week) |
| **Acquisitions** | 20+ (Aljex, MacroPoint, 3GTMS, Datamyne) | Acquired by E2open 2021 | BluJay, INTTRA, Cloud Logistics |

---

## Key Takeaways for Integration

1. **Descartes** has the most accessible API documentation, especially for MacroPoint visibility (public Postman collections, carrier-side API docs, webhook callbacks). The GLN provides robust EDI connectivity. CustomsInfo APIs offer trade compliance data. Authentication is API key-based.

2. **BluJay** no longer exists as an independent entity. All technical resources are under E2open. Legacy BluJay TMS instances still exist at customer sites but new integrations go through E2open.

3. **E2open** uses OAuth 2.0 for API authentication. The INTTRA ocean platform is the standout for container shipping integration (DCSA-compliant track & trace). Developer portal exists at knowledge.e2open.com but much documentation is behind login. REST/JSON is the primary API pattern, with EDI as alternative.

4. **None of these vendors** have fully open, self-service developer portals comparable to modern API-first platforms. All require some level of vendor engagement for full API access and credentials.

---

## Sources

- [Descartes API Portal](https://api.descartes.com/)
- [Descartes API List](https://api.descartes.com/apis)
- [Descartes MacroPoint Visibility Docs](https://docs.macropoint.com/)
- [Descartes MacroPoint Carrier Integration Docs](https://carrierdocs.macropoint.com/)
- [Descartes MacroPoint Capacity Docs](https://capacitydocs.macropoint.com/)
- [Descartes MacroPoint Postman Workspace](https://www.postman.com/macropoint-telematics)
- [Descartes GLN](https://www.descartes.com/solutions/b2b-connectivity-and-messaging/descartes-global-logistics-network)
- [Descartes EDI Solutions](https://www.descartes.com/edi-solutions)
- [Descartes CustomsInfo Trade Content APIs](https://www.customsinfo.com/knowledge-center/trade-content-apis-streamlining-classification-and-enhancing-business-integration/)
- [Descartes Transportation Management](https://www.descartes.com/solutions/transportation-management)
- [Descartes Shipper TMS on G2](https://www.g2.com/products/descartes-shipper-tms/reviews)
- [Descartes Wikipedia](https://en.wikipedia.org/wiki/Descartes_Systems_Group)
- [Descartes Pricing (Vendr)](https://www.vendr.com/buyer-guides/descartes-systems-group)
- [Descartes Support](https://www.descartes.com/customer-success/customer-support-and-training/customer-service-desk)
- [E2open Developer Portal](https://knowledge.e2open.com/knowledgecenter/developer/)
- [E2open Partner Register REST API](https://knowledge.e2open.com/knowledgecenter/developer/partner-register-rest-api/)
- [E2open Partner Search REST API](https://knowledge.e2open.com/knowledgecenter/developer/partner-search-rest-api/)
- [E2open Carrier Marketplace](https://marketplace.e2open.com/product/api-implementation/)
- [E2open Resource Center](https://www.e2open.com/resource-center/)
- [E2open Network Connectivity](https://www.e2open.com/e2open-network-connectivity/)
- [E2open 2024 Gartner MQ for TMS](https://www.e2open.com/news/press-releases/e2open-again-positioned-as-a-leader-in-2024-gartner-magic-quadrant-for-transportation-management-systems/)
- [E2open Pricing (ITQlick)](https://www.itqlick.com/e2open-software/pricing)
- [E2open Pricing (SelectHub)](https://www.selecthub.com/p/tms-software/e2open-tms/)
- [E2open Reviews (TrustRadius)](https://www.trustradius.com/products/e2open/reviews?qs=pros-and-cons)
- [E2open Reviews (Gartner)](https://www.gartner.com/reviews/market/transportation-management-systems/vendor/e2open)
- [BluJay TMS Likes/Dislikes (Gartner)](https://www.gartner.com/reviews/market/transportation-management-systems/vendor/e2open/product/blujay-transportation-management-tms-legacy/likes-dislikes)
- [INTTRA API Docs](https://apidocs.inttra.com/)
- [INTTRA Ocean Trade Platform](https://www.inttra.com/shipper-solutions/ocean_trade_platform/)
- [INTTRA Integration Service](https://www.inttra.com/services/integration/)
- [BluJay Homepage (redirects to E2open)](https://www.blujaysolutions.com/)
- [C.H. Robinson BluJay/E2open Integration](https://www.chrobinson.com/en-au/technology/connectivity-integrations/tms-integrations/e2open/)
- [Cleo BluJay EDI Connector](https://www.cleo.com/solutions/application-connectors/blujay)
- [Descartes on API Tracker](https://apitracker.io/a/descartes)
- [E2open on API Tracker](https://apitracker.io/a/e2open)
- [INTTRA on API Tracker](https://apitracker.io/a/inttra)
