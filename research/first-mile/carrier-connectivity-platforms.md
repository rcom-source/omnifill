# Carrier Connectivity & Freight Broker Platform Research

Research into carrier connectivity, digital freight brokerage, load boards, and fleet
management/telematics platforms relevant to first-mile transportation integration.

---

## 1. Convoy (now DAT / formerly Flexport)

### What It Does

Convoy was a digital freight brokerage platform that used automated freight matching to
connect shippers with carriers. Originally an independent company, Convoy's tech stack was
acquired by Flexport in November 2023 for ~$16M after Convoy shut down. Flexport rebuilt it
as a neutral digital freight execution layer. In July 2025, Flexport sold the Convoy
Platform to DAT Freight & Analytics (reportedly near $250M).

**Current Status:** The Convoy Platform is being integrated into DAT One. It is no longer an
independent product.

**Capabilities:**
- Automated freight matching using ML/AI models
- Carrier vetting and fraud prevention (ML-based verification)
- Digital load booking and execution
- QuickPay for carriers (available on every load)
- Paperwork management (BOL, POD)
- ~30,000 carriers on the platform (primarily owner-operators and small fleets)

**Modes:** FTL (Full Truckload) primary focus

### APIs and Developer Documentation

- **Flexport Developer Portal:** https://developers.flexport.com/
  - Bookings, Commercial Invoices, Customs Entries, Documents (35+ types), Freight Invoices,
    Products, Purchase Orders, Shipments APIs
  - Logistics API docs: https://docs.logistics-api.flexport.com/2023-10/
- **Convoy Platform API:** No standalone public API documentation. Being merged into DAT One.
- **DAT Developer Portal:** https://developer.dat.com/ (where Convoy capabilities will land)

### Authentication

- Flexport APIs: API credentials (key-based), details via tutorials on developer portal
- DAT: Service accounts with RESTful API access; portal registration required

### User Reviews / Pros & Cons

**Pros:**
- High carrier satisfaction and usability
- Strong automated matching reduced broker overhead
- Instant pricing and booking
- QuickPay on every load attracted carriers

**Cons:**
- Platform no longer independent -- future depends on DAT integration
- Convoy originally failed as a standalone business (shut down Oct 2023)
- Transition uncertainty: carriers and shippers face migration to DAT One

### Pricing Model

- No standalone pricing (being absorbed into DAT)
- Historically operated on a brokerage margin model (percentage of freight cost)

### Data Exposed

- Load/shipment details, carrier assignments, pricing, tracking status
- As part of DAT: will expose rate data, capacity analytics, carrier verification

**Key URLs:**
- https://convoy.com/ (platform landing page)
- https://developers.flexport.com/
- https://www.dat.com/company/news-events/news-releases/dat-to-acquire-convoy-platform-from-flexport

---

## 2. Uber Freight

### What It Does

Uber Freight is a digital freight matching platform that connects shippers with carriers
through a mobile app and web platform. It applies Uber's marketplace model to trucking,
offering instant pricing, real-time visibility, and streamlined booking.

**Capabilities:**
- Instant freight quoting with dynamic pricing (supply/demand algorithms)
- Digital load booking and management
- Real-time shipment tracking and visibility
- Signature confirmation / proof of delivery
- Electronic payment processing
- Scheduling API (dock appointment scheduling, pilot launched 2024)
- TMS integration (NetSuite, SAP, etc.)
- Managed transportation services

**Modes:** FTL, LTL

### APIs and Developer Documentation

- **Developer Portal:** https://developer.uberfreight.com/get-started
- **Uber Developers (general):** https://developer.uber.com/
- **Microsoft Power Automate Connector:** https://learn.microsoft.com/en-us/connectors/uberfreight/

**Known API Capabilities:**
- Instant Pricing API: receive rates for load requests
- Tender cancellation
- Price quote generation
- Scheduling API (dock appointments, standards-based)
- Shipment tracking

**Note:** Developer portal is partner-gated. Full API docs require completing a partnership
application form. Not a fully open/self-serve developer experience.

### Authentication

- OAuth 2.0 authorization
- Client ID, Client Secret, and Server Token provided via Auth tab
- Secure HTTPS endpoints

### User Reviews / Pros & Cons

**Pros:**
- Easy, intuitive UI for booking and managing shipments
- Real-time visibility into capacity and shipment status
- Instant quoting reduces negotiation time
- Large carrier network leveraging Uber's brand
- Good load-building features for shippers

**Cons:**
- Quotes expire in 15 minutes; pricing can be unpredictable
- Limited customer support; frustrating for time-sensitive issues
- Carriers report low rates ("cheap")
- 2.5% QuickPay fee for carriers (previously free)
- Poor claims process; disputes often sided with carrier
- Detention pay process burdensome for carriers
- Appointment confirmation unreliable at low rate points

**Overall satisfaction:** ~81% based on 55 reviews across review sites.

### Pricing Model

- No subscription fee for shippers or carriers
- Transaction-based: Uber Freight takes a margin on each load
- Dynamic pricing based on real-time market conditions
- Carriers: 2.5% fee for quick payment

### Data Exposed

- Real-time shipment location and ETA
- Rate quotes and pricing
- Load details (origin, destination, equipment, weight)
- Appointment scheduling data
- Invoice and payment status

**Key URLs:**
- https://www.uberfreight.com/en-US/partners/integrations
- https://developer.uberfreight.com/get-started

---

## 3. Loadsmart

### What It Does

Loadsmart is an AI-powered digital freight platform offering brokerage services, a TMS
(ShipperGuide), dock scheduling (Opendock), and carrier management (CarrierGuide). It
emphasizes instant pricing, 100% tender acceptance, and AI-driven optimization.

**Capabilities:**
- AI-powered instant freight pricing and booking
- ShipperGuide TMS: multimodal freight management (procure, plan, execute)
- Opendock: dock scheduling and yard management
- CarrierGuide: carrier-facing tools
- Reliable Contracts: dynamic pricing with 100% primary tender acceptance (PTA)
- Freight CoPilot: generative AI assistant embedded in ShipperGuide
- Managed transportation services

**Modes:** FTL, LTL, PTL (Partial Truckload), Drayage, Intermodal

### APIs and Developer Documentation

- **Developer Portal:** https://developer.loadsmart.com/docs/
- **Getting Started:** https://developer.loadsmart.com/docs/shipperguide/overview/getting-started
- **API Reference:** https://developer.loadsmart.com/docs/shipperguide/api-reference
- **Integration Network Docs:** https://integration-network-docs.loadsmart.com/

**API Capabilities:**
- Shipment creation from existing data
- Carrier EDI integration (transactional data exchange)
- Quote and tender via API
- Pricing considers equipment type, location, and market variables
- Webhooks
- Rate limiting

### Authentication

- OAuth-based: Client ID + Client Secret
- Requires active Shipper account (sign up at app.shipper.guide)
- API credentials requested through Account Manager (not self-serve)

### User Reviews / Pros & Cons

**Pros:**
- Strong AI-driven pricing; instant bookable rates
- Multimodal support (FTL, LTL, PTL, Drayage, Intermodal)
- 100% tender acceptance on Reliable Contracts
- Good TMS integration via API
- Generative AI CoPilot for real-time insights

**Cons:**
- API access not self-serve; must go through account manager
- Pricing not publicly disclosed
- Smaller carrier network compared to DAT or Uber Freight
- Documentation site has had loading issues (Docusaurus config problems noted)

### Pricing Model

- Brokerage margin model (no published rates)
- Dynamic pricing via API with market-rate safeguards
- Custom enterprise pricing for ShipperGuide TMS
- Opendock pricing separate

### Data Exposed

- Shipment details and status
- Rate quotes (instant pricing)
- Carrier assignments
- Dock scheduling data (via Opendock)
- Freight analytics and AI insights

**Key URLs:**
- https://loadsmart.com/
- https://developer.loadsmart.com/docs/

---

## 4. DAT / Truckstop.com

### What It Does

DAT Freight & Analytics operates the largest freight matching network in North America.
It provides load boards, rate data/analytics, carrier vetting, and freight matching for
brokers, carriers, and shippers. Often referred to as "trucking's super-database."

**Capabilities:**
- Load board (284M+ loads and trucks posted annually)
- Rate data and analytics (RateView)
- Carrier verification and compliance tools (FMCSA)
- BookNow instant booking
- DAT Tracking (shipment visibility)
- Freight posting automation
- Credit/payment tools
- Convoy Platform integration (coming -- automated freight matching)
- Access to 1.7M+ trucks

**Modes:** FTL, LTL

**Note:** Truckstop.com is a separate competitor, not the same company as DAT. Both are
major load boards. DAT is the larger network.

### APIs and Developer Documentation

- **Developer Portal:** https://developer.dat.com/ (login required)
- **API Support:** developersupport@dat.com
- **Help Center:** https://one.support.dat.com/

**Available APIs:**
- Load Board API (post, search, match loads)
- BookNow API
- DAT Tracking API
- Freight Posting API
- RateView API (requires premium subscription)
- Carrier verification/analytics

**Access Requirements:**
- RESTful API integration available at any Load Board subscription level
- RateView API requires RateView Combo Pro or Premium
- Developer portal registration required
- $500-$1,000 setup fee for production API use

### Authentication

- Service account credentials via developer portal
- RESTful API with standard auth (details in portal)

### User Reviews / Pros & Cons

**Pros:**
- Largest freight network in North America
- Comprehensive rate data and market analytics
- Integrated brokers see 25% faster load matching
- Reduces empty miles by up to 30%
- Strong carrier verification tools
- Convoy Platform acquisition adds automated matching

**Cons:**
- Pricing volatility: users report 45% price hikes on renewal
- Per-user licensing multiplies costs for growing companies
- API setup fee ($500-$1,000)
- Learning curve for full platform
- Rate data accuracy varies by lane

### Pricing Model

**Carrier Plans:**
- DAT One Standard: $49/month
- DAT One Enhanced: $99/month
- DAT One Pro: $149/month

**Broker Plans:**
- Starting at $159/month
- Combo plans (carrier + broker): $299-$449/month

**API:**
- Basic access: free (limited)
- Production use: $500-$1,000 setup fee
- RateView API: requires Pro/Premium subscription

### Data Exposed

- Load postings (origin, destination, equipment, rate)
- Historical and real-time rate data (by lane, equipment type)
- Carrier profiles, authority, insurance, safety scores
- Capacity/supply metrics
- Tracking/visibility data
- Market analytics and trends

**Key URLs:**
- https://www.dat.com/
- https://www.dat.com/api-integration
- https://developer.dat.com/

---

## 5. Trucker Tools

### What It Does

Trucker Tools is a freight operations platform focused on real-time load tracking, carrier
visibility, and capacity matching for freight brokers and 3PLs. It provides a free carrier
app and broker-facing SaaS tools.

**Capabilities:**
- Real-time load tracking (GPS from driver app, every 5-15 minutes)
- Smart Capacity: predictive carrier matching
- Smart Load Board: automated spot market load management
- Private Load Board: branded load board for trusted carriers
- Carrier Sourcing: access to 350,000+ unique carriers
- Book-It-Now functionality
- Automated rate negotiation
- ELD integration for tracking
- Check-call reduction (up to 40%)

**Modes:** FTL (Truckload) primary

### APIs and Developer Documentation

- **No public developer portal.** Integration is partner-managed.
- **TMS Integration page:** https://info.truckertools.com/tms-integration
- **Contact:** integrations@truckertools.com, support@truckertools.com

**Integration Methods:**
- API connection (custom, arranged through Trucker Tools team)
- SFTP/FTP: CSV file upload for location data
- ELD integration: requires API key/credentials + MC number
- TMS integrations: pre-built for several TMS platforms (TAI, FTM, Banyan, etc.)

**Authentication:**
- Encrypted key provided by Trucker Tools (placed under Account Number)
- ELD: API key/credentials + MC number

### User Reviews / Pros & Cons

**Pros:**
- Free driver app for carriers (17+ tools)
- Reliable load tracking reduces check-calls significantly
- Easy for both broker and driver to use
- Large carrier network (350,000+)
- Good TMS integrations

**Cons:**
- Book-It-Now feature underutilized by carriers
- App can lag; posted loads sometimes stale
- No in-app chat/messaging between brokers and carriers
- Lacks advanced AI/automation compared to newer platforms
- No public API documentation; integration requires direct engagement

### Pricing Model

- **Carrier app:** Free
- **Broker plans:** Custom pricing, not publicly disclosed
- Load Tracking: volume-based pricing
- Contracts: typically 1-2 year terms (more flexible terms emerging)

### Data Exposed

- Real-time carrier location (GPS coordinates)
- Load status and tracking events
- Carrier capacity and availability
- ELD data (via integration)
- Load board postings and bid data

**Key URLs:**
- https://www.truckertools.com/
- https://info.truckertools.com/tms-integration
- https://www.truckertools.com/partners/partner-directory/

---

## 6. Descartes MacroPoint

### What It Does

Descartes MacroPoint is a carrier tracking and freight visibility platform. It provides
real-time tracking of shipments by connecting to carriers via multiple tracking methods
(mobile app, ELD, GPS). It is the industry standard for broker-to-carrier visibility.

**Capabilities:**
- Real-time shipment tracking across all modes
- Multi-method tracking: cell/app-based, ELD, GPS/trailer tracking
- Tracking session management (create, update, stop/cancel)
- Webhook callbacks for visibility updates
- Proof of Delivery (POD) automation
- Carrier onboarding and compliance
- Capacity sourcing (MacroPoint Capacity)
- Integration with major TMS platforms

**Modes:** FTL, LTL, Intermodal, Rail, Ocean, Air (multimodal)

### APIs and Developer Documentation

- **Visibility API Docs:** https://docs.macropoint.com/
- **Carrier Integration Docs:** https://carrierdocs.macropoint.com/
- **Capacity Docs:** https://capacitydocs.macropoint.com/
- **Postman Collection:** https://documenter.getpostman.com/view/4593392/RWEcRgiW

**API Details:**
- **Base URL:** `https://macropoint-lite.com/api/1.0/`
- **Format:** XML request/response (`application/xml`)
- **Methods:** REST API or SFTP/FTPS Flat File uploads

**API Capabilities:**
- Create tracking sessions (send shipment + carrier info)
- Update tracking sessions
- Stop/cancel tracking sessions
- Receive visibility updates via webhook callbacks
- Carrier-side API: location updates (lat/long or address), load events (arrival/departure),
  tracking method assignment (cell, ELD vehicle ID, trailer GPS ID)

### Authentication

- **Basic Authentication** (HTTP Basic Auth)
- Credentials provided during onboarding

### User Reviews / Pros & Cons

**Pros:**
- Industry standard for freight visibility; extremely wide carrier coverage
- Multi-method tracking (doesn't require carrier to use specific app)
- Strong TMS integrations (pre-built for many platforms)
- Reliable tracking data quality
- Scales well for large brokerages

**Cons:**
- XML-based API feels dated (not JSON)
- Per-load pricing can be expensive at low volumes
- Implementation requires onboarding process (not self-serve)
- Part of Descartes ecosystem; may require broader Descartes relationship
- Limited real-time features compared to newer platforms

### Pricing Model

- **Per-load pricing:** $0.40 - $5.00 per load (volume-based discounts)
- **Per-user annual:** starting at $1,000/user/year
- **Implementation fee:** flat fee (amount varies)
- Prices paid upfront
- Support/troubleshooting: included (no extra charge)

### Data Exposed

- Real-time shipment location (lat/long, address)
- Arrival/departure events at stops
- ETA calculations
- Tracking method used per shipment
- Proof of delivery documents
- Carrier compliance data
- Capacity sourcing data (via MacroPoint Capacity)

**Key URLs:**
- https://macropoint.com/
- https://docs.macropoint.com/
- https://carrierdocs.macropoint.com/
- https://capacitydocs.macropoint.com/

---

## 7. Motive (formerly KeepTruckin)

### What It Does

Motive is an all-in-one fleet management and driver safety platform. Originally known as
KeepTruckin, it provides ELD compliance, GPS tracking, dashcams, safety analytics, and
fleet operations tools. It serves carriers, private fleets, and owner-operators.

**Capabilities:**
- ELD compliance (FMCSA and Transport Canada certified)
- Real-time GPS fleet tracking
- AI-powered dashcams (dual-facing)
- Hours of Service (HOS) logging and management
- Driver safety scoring and coaching
- Vehicle diagnostics and fault codes
- IFTA reporting
- DVIR (Driver Vehicle Inspection Reports)
- Reefer monitoring (temperature, humidity)
- Asset tracking
- Fuel management
- Dispatch and workflow management
- App Marketplace for third-party integrations

**Modes:** All surface modes (truckload, LTL, construction, oil & gas, etc.)

### APIs and Developer Documentation

- **Developer Portal:** https://developer.gomotive.com/
- **API Reference:** https://developer-docs.gomotive.com/reference/introduction
- **API Support:** apisupport@gomotive.com

**Base URLs:**
- Primary: `api.gomotive.com`
- Legacy: `api.keeptruckin.com` (still supported)

**Available API Endpoints:**
| Category | Description |
|----------|-------------|
| Users | User management and profiles |
| Vehicles | Vehicle data, fleet info |
| Vehicle Gateway (ELD) | ELD device integration |
| Groups | Organization management |
| HOS Logs | Hours of Service data |
| Locations | GPS location tracking |
| Messaging | In-platform communication |
| Inspection Reports | DVIR data |
| IFTA Reports | Fuel tax reporting |
| Fault Codes | Vehicle diagnostics |
| Driver Performance | Safety events and analytics |
| Assets | Asset tracking (create, update, locate) |
| Reefer | Temperature/humidity data |
| Cameras | Camera control and events |
| Webhooks | Event-driven integrations |

**Response Format:** JSON (primary), XML supported

### Authentication

- **API Key:** `X-Api-Key` header
- **OAuth 2.0:** Bearer token authentication
- Free developer account available (self-serve)

### User Reviews / Pros & Cons

**Pros:**
- Comprehensive all-in-one platform (ELD + GPS + cameras + safety)
- Reliable ELD compliance
- Strong AI-driven safety tools (dashcam analytics)
- Good API with self-serve developer access
- Hardware only $150
- Well-reviewed by small and mid-size fleets
- Active App Marketplace

**Cons:**
- Pricing no longer transparent (moved from tiered to custom quotes)
- Contract lock-in reported by some users
- Camera features can feel intrusive to drivers
- Customer support quality varies
- Legacy "keeptruckin" branding still in API URLs causes confusion

### Pricing Model

- **Hardware:** ~$150 per device (Vehicle Gateway)
- **Subscription:** Starting at ~$25/vehicle/month
- Custom pricing based on fleet size and features
- Previously had tiered plans ($0/20/35/custom per vehicle/month)
- API access: free developer account

### Data Exposed

- Real-time vehicle GPS location
- HOS logs and duty status
- Driver safety scores and events (speeding, hard braking, etc.)
- Vehicle diagnostics (fault codes, engine hours, odometer)
- DVIR inspection data
- IFTA mileage and fuel data
- Reefer temperature/humidity readings
- Camera events and footage metadata
- Asset locations
- Webhook events for all major data changes

**Key URLs:**
- https://gomotive.com/
- https://developer.gomotive.com/
- https://developer-docs.gomotive.com/reference/introduction

---

## 8. Samsara

### What It Does

Samsara is a fleet IoT and telematics platform providing GPS tracking, dashcams, driver
safety, ELD compliance, environmental sensors, and operational analytics. It is the leading
platform for small-to-mid-size fleets and supports a broad range of asset types.

**Capabilities:**
- Real-time GPS fleet tracking (vehicles, trailers, equipment, reefers)
- AI-powered dashcams and driver safety
- ELD compliance and HOS management
- Route planning, optimization, and live ETA sharing
- DVIR (Digital Vehicle Inspection Reports)
- Environmental sensors (temperature, humidity, door open/close)
- Geofencing and address management
- Document and form management (custom fields)
- Driver management (full CRUD, compliance-aware deactivation)
- Third-party app marketplace
- Kafka streaming for high-volume data
- 30+ webhook event types

**Modes:** All surface modes; also supports construction, oil & gas, food/cold chain

**Hardware:** VG34, VG54 vehicle gateways; AG26 asset gateway; environmental sensors

### APIs and Developer Documentation

- **REST API Overview:** https://developers.samsara.com/docs/rest-api-overview
- **Telematics Guide:** https://developers.samsara.com/docs/telematics
- **API Reference:** https://developers.samsara.com/reference/overview

**Key API Resources:**

| Resource | Description |
|----------|-------------|
| Vehicles | Fleet data, stats, location |
| Drivers | CRUD, login credentials, ELD settings |
| Routes | Create/update route plans, ETA, live sharing |
| Addresses | Location management, geofencing |
| Tags | Organizational grouping and filtering |
| DVIRs | Inspection reports |
| Documents/Forms | Custom field document management |
| Messages | Driver communication |
| Safety | Safety scores and events |
| Sensors | Environmental monitoring |
| Users | User management |

**Telematics Endpoints (Vehicle Stats):**
- `GET /fleet/vehicles/stats/feed` -- streaming feed of vehicle stat data (recommended for sync)
- `GET /fleet/vehicles/stats/history` -- historical report between start/end times
- `GET /fleet/vehicles/stats` -- snapshot of last known state

**Data Types Available:** GPS location, speed, odometer, engine hours, fuel level,
ambient/reefer temperature, humidity, barometric pressure, OBD fault codes

**Webhooks:** 30+ event types including alerts, driver updates, vehicle updates, geofence
enter/exit, route milestones, form submissions

**Kafka Integration:** Streaming for telematics data, asset readings, and events (for
high-volume enterprise integrations)

### Authentication

- **OAuth 2.0** (recommended)
- **3rd Party Integration Tokens**
- **Legacy API Tokens** (Bearer scheme)

### User Reviews / Pros & Cons

**Pros:**
- Best-in-class for small fleets (most requested by businesses with <49 vehicles)
- Excellent API with comprehensive documentation (self-serve)
- Broad hardware support (vehicles, trailers, equipment, reefers, sensors)
- Strong IoT/sensor capabilities (temperature, humidity, door sensors)
- Kafka streaming for enterprise-grade data pipelines
- 30-day free trial with free hardware
- Real-world results: 10-15% fuel savings, 60%+ safety incident reduction

**Cons:**
- 3-year minimum contract
- True costs can reach $40-60/vehicle/month with add-ons
- Route optimization limited compared to dedicated routing software
- Customer service inconsistency reported
- Hardware return process can be cumbersome

### Pricing Model

- **Base:** $27-$33/vehicle/month
- **With add-ons:** $40-$60/vehicle/month
- **Contract:** 3-year minimum
- **Hardware:** Included during trial; purchased or leased ongoing
- **Free trial:** 30 days with free hardware
- **API access:** included with subscription (no separate API fee)

### Data Exposed

- Real-time GPS (lat/long, speed, heading, odometer)
- Engine diagnostics (OBD-II, J1939 fault codes, engine hours)
- Fuel consumption and levels
- HOS/ELD duty status
- Safety events (harsh braking, speeding, distraction)
- Dashcam footage and event clips
- Environmental sensor data (temperature, humidity, pressure, door status)
- DVIR inspection reports
- Route progress and ETA
- Geofence enter/exit events
- Custom document/form data
- Driver profiles and compliance status

**Key URLs:**
- https://www.samsara.com/
- https://developers.samsara.com/docs/rest-api-overview
- https://developers.samsara.com/reference/overview

---

## Comparison Matrix

| Platform | Primary Function | Modes | Public API | Auth | Self-Serve Dev Access | Pricing Model |
|----------|-----------------|-------|------------|------|-----------------------|---------------|
| Convoy/DAT | Digital freight matching | FTL | Merging into DAT | Service accounts | Portal registration | Brokerage margin |
| Uber Freight | Digital freight matching | FTL, LTL | Partner-gated | OAuth 2.0 | No (apply) | Transaction margin |
| Loadsmart | AI freight brokerage + TMS | FTL, LTL, PTL, Drayage, Intermodal | Yes (gated) | OAuth (Client ID/Secret) | No (account mgr) | Brokerage margin |
| DAT | Load board + analytics | FTL, LTL | Yes | Service accounts | Portal registration | Subscription + API fee |
| Trucker Tools | Carrier visibility + matching | FTL | No (custom) | Encrypted key | No (contact sales) | Volume-based |
| MacroPoint | Carrier tracking/visibility | FTL, LTL, Intermodal, Rail, Ocean, Air | Yes (XML) | Basic Auth | No (onboarding) | Per-load ($0.40-$5) |
| Motive | Fleet mgmt + ELD | All surface | Yes (JSON) | API Key / OAuth 2.0 | Yes (free account) | $25+/vehicle/month |
| Samsara | Fleet IoT + telematics | All surface | Yes (JSON) | OAuth 2.0 / Tokens | Yes (with subscription) | $27-60/vehicle/month |

## Integration Priority Assessment for First-Mile

**Tier 1 -- High Value, Good API Access:**
- **Samsara** -- Best API docs, comprehensive data, self-serve, Kafka streaming
- **Motive** -- Strong API, free dev accounts, broad fleet data
- **DAT** -- Largest network, rate data, soon includes Convoy matching

**Tier 2 -- High Value, Gated Access:**
- **Descartes MacroPoint** -- Industry standard visibility, documented API (XML)
- **Loadsmart** -- Good API but requires account manager for credentials
- **Uber Freight** -- Large network but partner-gated API

**Tier 3 -- Limited API Access:**
- **Trucker Tools** -- No public API; custom integration only
- **Convoy** -- Being absorbed into DAT; no standalone API path

## Key Takeaways

1. **Samsara and Motive** have the most developer-friendly APIs with self-serve access,
   comprehensive documentation, and modern JSON/REST patterns. These are the best starting
   points for fleet-level telematics integration.

2. **DAT** is the gravitational center of freight matching. With the Convoy Platform
   acquisition, it will be the single most important load board/matching API to integrate.
   API access requires registration and has setup fees.

3. **MacroPoint** is the de facto standard for carrier tracking/visibility but uses an
   XML-based API. Any serious first-mile integration needs MacroPoint support.

4. **Uber Freight and Loadsmart** are valuable but gate their APIs behind partnership
   applications. Plan for business development alongside engineering.

5. **Trucker Tools** has no public API. Integration requires direct engagement with their
   team. Consider deprioritizing unless specific broker customers require it.

6. The **freight brokerage platforms** (Convoy, Uber Freight, Loadsmart) expose transaction
   data (quotes, bookings, tracking), while **fleet platforms** (Samsara, Motive) expose
   operational data (GPS, ELD, diagnostics, safety). A complete first-mile integration
   needs both layers.

## Sources

- https://www.dat.com/ [Source: DAT company website]
- https://developer.dat.com/ [Source: DAT developer portal]
- https://www.uberfreight.com/ [Source: Uber Freight website]
- https://developer.uberfreight.com/ [Source: Uber Freight developer portal (gated)]
- https://loadsmart.com/ [Source: Loadsmart website]
- https://developer.loadsmart.com/ [Source: Loadsmart developer portal]
- https://www.truckertools.com/ [Source: Trucker Tools website]
- https://macropoint-lite.com/api/1.0/ [Source: Descartes MacroPoint API]
- https://developer.gomotive.com/ [Source: Motive developer portal]
- https://developers.samsara.com/docs/rest-api-overview [Source: Samsara developer docs]
- https://developers.samsara.com/reference/overview [Source: Samsara API reference]
- https://www.g2.com/categories/fleet-management [Source: G2 - Fleet management reviews]
- https://www.g2.com/categories/load-boards [Source: G2 - Load board reviews]
- Reddit r/Truckers, r/FreightBrokers, r/logistics [Source: Reddit - carrier platform discussions]
