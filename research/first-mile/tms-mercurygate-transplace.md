# First-Mile TMS Research: MercuryGate & Transplace (Uber Freight)

Research date: 2026-03-31

---

## 1. MercuryGate TMS (now Infios TMS)

### 1.1 What It Does

MercuryGate is a cloud-based, multimodal Transportation Management System (TMS) serving shippers, 3PLs, and freight forwarders. It was acquired by Korber Supply Chain Software (joint venture between Korber AG and KKR) in August 2024, and the combined entity rebranded as **Infios** in March 2025.

**Modes Supported (all natively on one platform):**
- Truckload (FTL)
- Less-than-Truckload (LTL)
- Parcel
- Rail
- Intermodal
- Ocean
- Air

**Core Modules & Capabilities:**
- **Planning & Optimization** -- Route optimization, load consolidation/deconsolidation, multimodal optimization
- **Rating** -- Multimodal rating engine, contracted rates, spot quotes, rate negotiation
- **Execution** -- Carrier tendering (automated load tendering), booking, scheduling
- **Carrier Management** -- Onboarding, scorecarding, performance tracking, rate negotiation
- **Shipment Visibility** -- Real-time tracking across all modes, shipment rerouting
- **Freight Audit & Payment** -- Billing automation, audit
- **Business Intelligence** -- Analytics, dashboards, reporting
- **Fleet Management** -- For asset-based operations
- **Fulfillment Tracking** -- Cross-channel, cross-mode tracking

**Key Differentiator:** True omni-modal support on a single platform (most competitors require separate modules per mode).

### 1.2 Technical Documentation & APIs

**Developer Portal:**
- API docs: https://qa-api-docs.mercurygate.net/documentation/
- Home: https://qa-api-docs.mercurygate.net/
- Security overview: https://qa-api-docs.mercurygate.net/documentation/security-overview.html
- Standard data/codes: https://qa-api-docs.mercurygate.net/documentation/standard-data.html

**REST APIs (Swagger/OpenAPI documented):**

| API | Direction | Description |
|-----|-----------|-------------|
| **Rating API** | MercuryGate -> Partner | TMS sends rate requests to partner endpoint (`{host}/svc/rates/v1/rate-request`). Partner returns available rates. |
| **Booking API** | MercuryGate -> Partner | TMS sends booking requests to partner endpoint (`{host}/svc/booking/v1/booking-request`). Partner returns booking confirmation. |
| **Status Update API** | Partner -> MercuryGate | Partners call MercuryGate endpoint to push status updates into the TMS. |

**EDI Support (X12 004010 release):**

| Transaction Set | Direction | Description |
|-----------------|-----------|-------------|
| X12 204 | Outbound (sends) | Motor Carrier Load Tender |
| X12 210 | Inbound (receives) | Motor Carrier Freight Details and Invoice |
| X12 214 | Inbound (receives) | Transportation Carrier Shipment Status Message |
| X12 315 | Inbound (receives) | Status Details (Ocean) |
| X12 990 | Inbound (receives) | Response to a Load Tender |

**Integration Pattern:** Bidirectional -- MercuryGate calls partner-hosted endpoints (rating, booking) and partners call MercuryGate endpoints (status updates). Partners implement REST endpoints that conform to MercuryGate's Swagger specs.

**SDKs:** None documented. Partners implement endpoints against Swagger/OpenAPI specs.

**Third-party EDI integration providers:** Cleo, Stedi, Zenbridge, Orderful

### 1.3 Authentication

MercuryGate uses **OAuth 2.0 Authorization Code Grant with PKCE** for all API communication (both inbound and outbound).

**Key details:**
- All calls must use HTTPS with TLS 1.2+ (TLS 1.3 preferred)
- Partner onboarding: Client registration generates mutual Client ID and Client Secret on both partner system and MercuryGate Authorization Server
- Customer authorization: A Super-User authorizes the integration once, triggering an auth code exchange for access + refresh tokens
- **Access tokens:** Time-limited JWT bearer tokens, included in API requests
- **Refresh tokens:** Long-lived, used to generate new access tokens
- Tenant/partner identity is embedded in token claims (not in request body)
- Self-service authorization (minimal staff intervention) is in development/rollout

### 1.4 Help Centers & Knowledge Bases

| Resource | URL |
|----------|-----|
| Knowledge Center (blogs, webinars, articles) | https://mercurygate.com/knowledge-center/ |
| User Community (advisory council, expert discussion) | https://mercurygate.com/tms-solutions/community/ |
| Product Education Hub | Available through MercuryGate portal |
| API Documentation | https://qa-api-docs.mercurygate.net/documentation/ |
| Infios (post-rebrand) portal | https://www.infios.com/en/supply-chain-solutions/transportation-management |

**Support channels:** Phone and email during business hours. Dedicated account managers and onsite training for enterprise customers. Training courses and tutorials available online.

### 1.5 User Reviews (Pros & Cons)

**G2 Rating:** 4.2/5

**Pros (from G2, Capterra, SelectHub, ITQlick):**
- True multimodal support on a single platform -- rare among competitors
- Highly configurable and customizable workflows
- Strong routing, scheduling, and optimization capabilities
- Intuitive interface for basic freight management tasks
- Comprehensive carrier management and freight audit/payment
- Good for both shippers and 3PLs

**Cons (from G2, Capterra, SelectHub, ITQlick):**
- **Support is widely criticized** -- tickets can go unanswered for 30+ days; support team described as "basically non-existent" by some users
- **Custom development is expensive** and custom features become available for purchase by competitors (no exclusivity)
- Complex initial implementation; legacy system integration can be challenging
- UI can be cumbersome and feel outdated in some areas
- System processing speed is slow; queries sometimes fail without explanation
- Sensitive to updates (upgrades can break things)
- Rebrand/acquisition uncertainty (MercuryGate -> Korber -> Infios) may affect roadmap

**No significant Reddit discussion found** in r/logistics, r/supplychain, or r/freight specifically about MercuryGate.

### 1.6 Pricing

Subscription-based, per-user pricing:

| Users | Approx. Monthly Cost |
|-------|---------------------|
| 1 | ~$500 |
| 10 | ~$4,500 |
| 100 | ~$40,000 |
| 1,000 | ~$350,000 |

**Implementation costs:** $5,000 (small business) to $50,000+ (enterprise)

Pricing is not publicly listed -- requires sales engagement. Custom quotes based on modules, volume, and integration complexity.

### 1.7 Data Exposed

| Data Type | Available | Method |
|-----------|-----------|--------|
| **Rates/Quotes** | Yes | Rating API (REST), contracted rates |
| **Booking confirmation** | Yes | Booking API (REST) |
| **Shipment status/tracking** | Yes | Status Update API (REST), EDI 214, EDI 315 (ocean) |
| **Load tenders** | Yes | EDI 204 |
| **Tender responses** | Yes | EDI 990 |
| **Freight invoices** | Yes | EDI 210 |
| **ETAs** | Yes | Via tracking/status data |
| **Events** | Yes | Status updates include time, date, location, route, conveyance |
| **Documents** | Unclear | Not explicitly documented in public API docs |
| **Analytics/BI** | Yes | Via TMS dashboards (not API-exposed) |

---

## 2. Transplace / Uber Freight TMS

### 2.1 What It Does

Transplace was founded in 2005 as a managed transportation and TMS provider. Uber Freight acquired Transplace in 2021 for $2.25 billion. The TMS is now branded as **Uber Freight TMS** but the legacy `tms.transplace.com` domain is still active for customer/tracking portals.

The platform underwent a major rebuild announced in 2024-2025, described as the most comprehensive update since the acquisition.

**Modes Supported:**
- Truckload (FTL)
- Less-than-Truckload (LTL)
- Rail
- Ocean
- Air
- Intermodal

**Core Modules & Capabilities:**

- **Control Tower** -- Command center for supply chain leaders; real-time data, end-to-end visibility across all modes, shipment creation through final delivery
- **Procurement** -- Freight procurement, RFP management, real-time market pricing with guaranteed spot rates
- **Execution** -- Load planning, automated tendering, scheduling, carrier management
- **Visibility & Tracking** -- Global end-to-end shipment visibility across modes (air, ocean, rail, road); LTL tracking; service prediction
- **Financial Management** -- AR/AP workflows, freight spend visibility/forecasting, freight audit & payment (OCR-driven), accessorial management via carrier self-service
- **Optimization** -- Route optimization, shipment consolidation
- **AI Agents** -- 30 embedded AI agents automating tendering, scheduling, carbon tracking, anomaly detection, and optimization recommendations
- **Mobile App** -- Available on iOS and Android (app: `com.transplace.tms`)

**Key Differentiator:** Deep integration with Uber Freight's marketplace/capacity network; AI-first approach with 30 embedded agents; modular architecture allowing same-day integration.

### 2.2 Technical Documentation & APIs

**Developer Portal:**
- https://developer.uberfreight.com/get-started
- https://developer.uberfreight.com/accounts/login (SAML SSO login required)
- Legacy: https://developer.uberfreight.com/portals/api/sites/transplace-apiportal/liveportal/sso/login

**Note:** The developer portal requires authentication to access -- API documentation is not publicly browsable. This is a gated portal.

**Known APIs:**

| API | Description |
|-----|-------------|
| **Pricing/Rating API** | Instant real-time pricing and tendering; guaranteed spot rates by day for up to 14 days; pricing with as little as 4 hours before pickup |
| **Scheduling API** | SSC (Scheduling Standards Consortium) compliant; appointment scheduling between shippers and carriers; pilot launched 2024, GA to all TMS users |
| **Tracking API** | Real-time shipment tracking, signature confirmation |
| **Load Management** | Load booking and management |

**EDI Support (X12):**

| Transaction Set | Description |
|-----------------|-------------|
| X12 204 | Motor Carrier Load Tender |
| X12 210 | Motor Carrier Freight Invoice |
| X12 214 | Transportation Carrier Shipment Status Message |
| X12 810 | Invoice |
| X12 850 | Purchase Order |
| X12 855 | Purchase Order Acknowledgement |
| X12 856 | Ship Notice/Manifest (ASN) |
| X12 990 | Response to a Load Tender |

**ERP/TMS Integrations:**
- Pre-built integrations with BluJay, Oracle, SAP, NetSuite
- Modular architecture for rapid integration (advertised as "same-day")
- Third-party EDI compliance providers: TrueCommerce, Orderful, Cleo, Zenbridge

**SDKs:** None publicly documented.

### 2.3 Authentication

- Developer portal uses **SAML SSO** for login
- API authentication details are behind the gated developer portal -- not publicly documented
- EDI connections follow standard AS2/SFTP patterns (via third-party providers)

### 2.4 Help Centers & Knowledge Bases

| Resource | URL |
|----------|-----|
| Uber Freight Help Center | https://help.uber.com/freight |
| Carrier Support | https://help.uber.com/en/freight/carrier |
| Customer Portal (Transplace) | https://tms.transplace.com/ct/ |
| Tracking Portal | https://tms.transplace.com/web/tracking-portal-ui/ |
| Developer Portal | https://developer.uberfreight.com/get-started |
| Blog / Release Notes | https://www.uberfreight.com/blog/uber-freight-technology-release-notes-q224/ |

**Support channels:** In-app support (Account -> Contact Support), phone, email, chat at uberfreight.com. Uber Freight representatives assigned to accounts.

**No public community forum found.** Support is primarily through direct account management.

### 2.5 User Reviews (Pros & Cons)

**Gartner Peer Insights, Capterra, TrustRadius reviews:**

**Pros:**
- User-friendly, intuitive interface (both web and mobile)
- Strong end-to-end visibility across all modes including ocean, air, rail
- Control Tower module is highly praised for actionable real-time data
- Dedicated and helpful account teams; customer service is a strength
- Rapid technology evolution -- frequent feature releases, AI integration
- Direct API integrations are faster and more stable than traditional EDI
- Uber's marketplace provides deep capacity access
- Modular architecture -- adopt what you need

**Cons:**
- **Support response times can be slow** despite good account relationships
- Occasional platform bugs and reliability issues
- Load cancellations without notice (marketplace side, not TMS)
- Navigation quirks -- difficulty going "back" in certain UI sections
- Developer portal is gated/opaque -- hard to evaluate API capabilities without account
- Legacy Transplace systems still visible (dual portals, legacy URLs) -- transition not fully clean
- Pricing not transparent

**No significant Reddit discussion found** specifically about the TMS product (r/freight discussions tend to focus on the marketplace/brokerage side).

### 2.6 Pricing

- Not publicly listed
- Estimated starting range: $500-$1,000/month (varies significantly by tier)
- Enterprise pricing requires sales engagement
- Some sources mention per-load or per-shipment pricing components
- The TMS is sometimes bundled with managed transportation services

### 2.7 Data Exposed

| Data Type | Available | Method |
|-----------|-----------|--------|
| **Rates/Quotes** | Yes | Pricing API (real-time, guaranteed spot rates) |
| **Shipment tracking** | Yes | Tracking API, EDI 214, tracking portal |
| **Shipment status events** | Yes | EDI 214, API |
| **Load tenders** | Yes | EDI 204 |
| **Tender responses** | Yes | EDI 990 |
| **Invoices** | Yes | EDI 210, EDI 810 |
| **Purchase orders** | Yes | EDI 850, 855 |
| **Ship notices (ASN)** | Yes | EDI 856 |
| **Scheduling/appointments** | Yes | Scheduling API (SSC compliant) |
| **ETAs/Service prediction** | Yes | Control Tower, tracking |
| **Signature confirmation** | Yes | Tracking API |
| **Carbon tracking** | Yes | AI-driven, within TMS |
| **Financial data** | Yes | AR/AP via TMS (API exposure unclear) |
| **Documents (BOL, POD)** | Likely | Not explicitly confirmed in public docs |

---

## 3. Comparison Summary

| Dimension | MercuryGate (Infios) | Uber Freight TMS (Transplace) |
|-----------|---------------------|-------------------------------|
| **Founded** | 2000 | 2005 (Transplace), acquired 2021 |
| **Current Owner** | Korber/KKR (Infios) | Uber Technologies |
| **Modes** | All (truck, LTL, parcel, rail, ocean, air, intermodal) | All (truck, LTL, rail, ocean, air, intermodal) |
| **API Style** | REST (Swagger/OpenAPI), partner-hosted endpoints | REST (gated portal), pre-built ERP integrations |
| **Auth** | OAuth 2.0 + PKCE | SAML SSO (portal); API auth behind gate |
| **EDI** | X12 204, 210, 214, 315, 990 | X12 204, 210, 214, 810, 850, 855, 856, 990 |
| **API Docs Public** | Partially (qa-api-docs.mercurygate.net) | No (gated developer portal) |
| **SDKs** | None | None |
| **G2 Rating** | 4.2/5 | N/A (reviews on Gartner, not G2) |
| **Pricing** | ~$500-$40K+/mo (user-based) | ~$500-$1K+ starting (opaque) |
| **AI/ML** | Basic optimization | 30 embedded AI agents |
| **Marketplace/Capacity** | No native marketplace | Yes (Uber Freight network) |
| **Support Quality** | Widely criticized | Mixed (good account teams, slow tickets) |
| **Acquisition Risk** | High (MercuryGate -> Korber -> Infios rebrand) | Moderate (Uber strategic asset) |

## 4. Integration Feasibility for Omnifill

**MercuryGate/Infios:**
- Public API docs exist (partially) -- easier to evaluate
- OAuth 2.0 + PKCE is a well-understood auth pattern
- Bidirectional API design (MercuryGate calls you, you call MercuryGate) adds complexity
- EDI support is standard but limited set (5 transaction types)
- Rebrand/ownership changes may affect API stability

**Uber Freight TMS:**
- Gated developer portal -- requires account/relationship to evaluate API surface
- Broader EDI support (8 transaction types including purchase orders and ASNs)
- Pre-built integrations with major ERPs (Oracle, SAP, NetSuite) suggest mature connector ecosystem
- SSC-compliant scheduling API is a differentiator
- Uber's engineering culture suggests more modern API design, but lack of public docs is a barrier

**Recommendation for adapter priority:**
Both are relevant for first-mile TMS connectivity. MercuryGate is easier to start with due to partially public API docs. Uber Freight requires a sales/partnership relationship to access developer documentation.

---

## Sources

- [MercuryGate API Documentation](https://qa-api-docs.mercurygate.net/documentation/)
- [MercuryGate API Security Overview](https://qa-api-docs.mercurygate.net/documentation/security-overview.html)
- [MercuryGate Standard Data and Codes](https://qa-api-docs.mercurygate.net/documentation/standard-data.html)
- [MercuryGate Knowledge Center](https://mercurygate.com/knowledge-center/)
- [MercuryGate User Community](https://mercurygate.com/tms-solutions/community/)
- [MercuryGate G2 Reviews](https://www.g2.com/products/mercurygate-tms/reviews)
- [Infios TMS Capterra Reviews](https://www.capterra.com/p/127795/MercuryGate-TMS/)
- [MercuryGate ITQlick Review](https://www.itqlick.com/mercurygate-tms-software)
- [Infios TMS (post-rebrand)](https://www.infios.com/en/supply-chain-solutions/transportation-management)
- [Korber Acquires MercuryGate](https://www.infios.com/en/knowledge-center/news/koerber-supply-chain-software-completes-acquisition-of-mercurygate)
- [Korber Rebrands as Infios](https://www.infios.com/en/knowledge-center/news/koerber-supply-chain-software-rebrands-as-infios)
- [MercuryGate EDI on Stedi](https://www.stedi.com/edi/network/mercurygate)
- [MercuryGate EDI via Cleo](https://www.cleo.com/solutions/application-connectors/mercurygate)
- [Uber Freight Developer Portal](https://developer.uberfreight.com/get-started)
- [Uber Freight API Benefits Blog](https://www.uberfreight.com/en-US/blog/uber-freight-api-benefits)
- [Uber Freight TMS Announcement](https://www.uberfreight.com/blog/introducing-the-upgraded-uber-freight-tms/)
- [Uber Freight Scheduling API](https://www.uberfreight.com/en-US/blog/uber-freight-releases-pilot-for-scheduling-api)
- [Uber Freight Technology Release Notes](https://www.uberfreight.com/blog/uber-freight-technology-release-notes-q224/)
- [Uber Freight Help Center](https://help.uber.com/freight)
- [Uber Freight Capterra Reviews](https://www.capterra.com/p/206000/Uber-Freight/)
- [Uber Freight Gartner Reviews](https://www.gartner.com/reviews/market/transportation-management-systems/vendor/uber-freight/product/uber-freight-transportation-management-system-tms)
- [Uber Freight SelectHub Review](https://www.selecthub.com/p/tms-software/uber-freight-tms/)
- [Transplace Capterra Reviews](https://www.capterra.com/p/162721/Transplace-TMS/reviews/)
- [Transplace EDI on Orderful](https://www.orderful.com/network/transplace)
- [Uber Freight EDI via Cleo](https://www.cleo.com/trading-partner-network/uber-freight)
- [Uber Freight EDI via TrueCommerce](https://www.truecommerce.com/trading-partner/uber-freight/)
- [FreightWaves: Uber Freight Rebuilt TMS](https://www.freightwaves.com/news/uber-freights-new-solutions-rebuilt-tms-procurement-wide-ai-use)
