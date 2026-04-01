# Manhattan Active Omni: Order Promising & Sourcing Research

Research date: 2026-03-31

## Executive Summary

Manhattan Active Omni is Manhattan Associates' cloud-native, microservices-based unified commerce platform that combines order management, inventory visibility, fulfillment optimization, customer engagement, and point-of-sale in a single application. It is widely regarded as an industry leader in distributed order management (DOM), receiving the highest possible score (5.0) in 20 of 27 criteria in the Forrester Wave OMS Q1 2025 evaluation. Manhattan is also a 17-time Gartner Magic Quadrant Leader for WMS.

The platform is **heavily gated** — full API documentation, technical specs, and integration guides require a customer license or partner NDA. However, Manhattan has a public developer portal at `developer.manh.com` with partial documentation, and the platform's capabilities are well-documented through press releases, partner materials, and analyst reports.

**Key takeaway for Omnifill integration:** Manhattan is the most capable but also the most difficult-to-access system in the landscape. Integration requires a formal partnership or customer relationship. The REST API is comprehensive (250+ microservices, thousands of endpoints) but fully gated behind OAuth 2.0 authentication tied to a licensed environment.

---

## 1. What It Does

### 1.1 Order Promising

Manhattan's order promising engine delivers **precise, personalized delivery dates** (not static windows like "5-7 days") across all sales channels. It combines three technical pillars:

**Real-Time Inventory Intelligence**
- Maintains a global, real-time perpetual inventory view across every fulfillment location
- Includes on-hand, in-transit, on-order, and third-party inventory
- Advanced constraint engine dynamically adjusts availability based on channel, delivery method, seasonality, store capacity, safety stock levels, and more

**In-Memory Caching Architecture**
- High-capacity in-memory caching technology delivers instantaneous order promises at scale
- Handles massive request volumes from digital commerce channels without degradation
- Critical for peak-season load handling

**Machine Learning-Driven Adaptation**
- Algorithms continuously learn and adapt, automatically adjusting order promises using current and historical data
- Evaluates DC workloads, carrier performance history, and operational constraints
- For specialized fulfillment (e.g., monogramming), dynamically determines optimal locations based on workload and shipping cutoff times

**Promising capabilities include:**
- Available-to-Promise (ATP) — real-time inventory availability checks across all nodes
- Capable-to-Promise (CTP) — factors in production/processing capacity
- Profitable-to-Promise (PTP) — compares realizable profit vs. opportunity cost of fulfilling from a given node
- Store pickup optimization with configurable cutoff times by location and day of week
- Google Merchant Center integration to display fulfillment promises in search results
- "Green" delivery option highlighting for environmentally conscious customers

Source: https://www.manh.com/solutions/omnichannel-software-solutions/order-management-system/precise-order-promising

### 1.2 Sourcing Logic (Optimized Fulfillment Sourcing)

The sourcing engine uses **machine learning with adaptive algorithms** powered by Manhattan's Computational Intelligence technology. It evaluates fulfillment decisions in real-time across these parameters:

| Factor | Description |
|--------|-------------|
| Customer proximity | Distance from fulfillment node to delivery address |
| Shipping & handling costs | Carrier rates, zones, fuel surcharges, labor, packaging |
| Facility capacity | Current workload, historical rejection rates, accuracy metrics |
| Inventory levels | Days of supply, surplus detection, safety stock |
| Delivery method & promised date | SLA compliance for each order |
| Selling price & seasonality | Margin-aware routing, clearance item handling |
| Inventory disposition | Quality status, returns eligibility |
| Tax/tariff considerations | Cross-border cost optimization |

**Key sourcing strategies:**

- **Cost optimization:** Automatically switches sourcing between DCs and stores to avoid markdowns, comparing forecasted markdowns against shipping expenses
- **Merge-in-transit:** Dynamically combines multiple orders for same customer into single shipments
- **Promise fulfillment:** Prioritizes high-volume facilities during peak seasons based on historical rejection rates and accuracy
- **Surplus liquidation:** Routes orders from facilities with excess inventory to reduce markdown risk
- **Service level routing:** Different strategies for free-shipping vs. premium-shipping customers, clearance items, customer classifications

**Fulfillment Optimization Simulation Engine:**
- Model and compare alternative fulfillment strategies
- Balance cost, speed, service level, and margin trade-offs
- "What-if" scenario planning with side-by-side comparison
- Self-serve interface for adjusting rules and rerunning simulations

Source: https://www.manh.com/solutions/omnichannel-software-solutions/order-management-system/optimized-fulfillment-sourcing

### 1.3 Inventory Visibility (Available to Commerce)

Manhattan's **Available to Commerce (ATC)** is a patented (U.S. Pat. No. 10,115,071) promising engine that filters real-time inventory views according to business objectives and operational constraints.

**How it works:**
1. Maintains a real-time global inventory view ("Manhattan Interactive Inventory") across all nodes
2. Creates configurable **inventory "Views"** that control which inventory is exposed to which channels
3. Each View is defined by a combination of factors:
   - Selling channel (online, mobile, in-store, wholesale, marketplace)
   - Retail brand
   - Delivery method
   - Seasonality rules
   - Store capacity and fulfillment capability
   - Inventory accessibility and disposition
   - Presentation stock rules (protect walk-in customer inventory)
   - Safety stock levels

**Virtual Inventory Segmentation:**
- Segment inventory visibility virtually without physical separation
- Expose both on-hand and future inventory (in-transit, on-order)
- Protect inventory for different selling channels (e.g., exclude store inventory from online fulfillment if location lacks capability)
- Automatically manage availability through operational constraints (fulfillment outages, store workload)

**Technical interface:**
- REST-based APIs for global and location-specific inventory pulling/pushing
- Real-time inventory lookup availability delivered to any channel
- Conditional and automatic item substitutions based on business rules
- Reserve and publish ship dates for orders across channels

Source: https://www.manh.com/products/available-to-commerce

### 1.4 Distributed Order Management (Global Order Orchestration)

**End-to-end order lifecycle management** from capture through settlement:
- Manages orders across multiple brands, countries, channels through single system
- Supports: ship-to-customer, in-store pickup, ship-to-store, ship-from-store, same-day delivery, curbside pickup
- Configuration inheritance: rules and workflows inherited from existing country/brand with modifications
- Business-user-controlled rules via graphical interfaces (no technical resources required for basic configuration)
- Autonomous order monitoring with dynamic notifications and actions when delays/exceptions occur
- Customer self-service order modification capabilities based on order state
- Post-purchase monitoring detects abandonment risk and can automatically notify agents or customers

**Fulfillment methods orchestrated:**
- Distribution center fulfillment
- Store fulfillment (ship-from-store)
- Vendor/supplier drop-ship
- Third-party logistics (3PL)
- Merge-in-transit consolidation

Source: https://www.manh.com/solutions/omnichannel-software-solutions/order-management-system/global-order-orchestration

### 1.5 Enterprise Promise & Fulfill (B2B)

A separate product offering for B2B merchants that augments existing ERP systems:
- Layers advanced routing optimization atop current ERP infrastructure (no rip-and-replace)
- AI-driven routing across warehouses, 3PLs, drop-ship suppliers, retail locations
- Accounts for future inventory through POs and ASNs
- SLA compliance: customer-specific carrier preferences, consolidation requirements, delivery schedules
- Multi-ERP support

Source: https://www.manh.com/solutions/b2b-commerce/order-routing-optimization-with-enterprise-promise-fulfill

### 1.6 Adaptive Network Fulfillment

ML-driven dynamic optimization across the fulfillment network:
- Real-time routing decisions analyzing DC capabilities, store capacity, transportation costs, customer SLAs
- Learn from historical rejection rates, accuracy metrics, and workload patterns
- Balance workload across facilities dynamically
- Create incentives/deterrents using real-time data (surplus inventory, capacity limits)
- Full cost breakdown visibility for every fulfillment decision
- Real-time global network performance metrics

Source: https://www.manh.com/solutions/omnichannel-software-solutions/order-management-system/adaptive-network-fulfillment

---

## 2. Technical Documentation & API

### 2.1 Developer Portal

**URL:** https://developer.manh.com/

The developer portal provides:
- REST API documentation and reference
- Authentication guides
- Code integration guides
- Postman collection setup
- Tutorials, how-to guides, coding samples
- Application reference for Manhattan Active Omni (MAO): https://developer.manh.com/docs/reference/app/mao/

**Full API reference (requires authentication):** https://api.developer.manh.com

**Key documentation pages:**
- API overview: https://developer.manh.com/docs/how-to/rest-api/
- Authentication: https://developer.manh.com/docs/how-to/rest-api/authentication/
- Code integration: https://developer.manh.com/docs/how-to/rest-api/yourcode/
- Postman setup: https://developer.manh.com/docs/how-to/rest-api/postman/
- API reference: https://developer.manh.com/docs/how-to/rest-api/reference/
- Technology overview: https://developer.manh.com/docs/overview/technology-overview-manhattan-active-cloud/
- All apps reference: https://developer.manh.com/docs/reference/app/

### 2.2 API Architecture

- **Style:** REST (primary), with mentions of GraphQL playground availability
- **Data format:** JSON request/response
- **HTTP verbs:** Standard (GET, POST, PUT, DELETE)
- **Response codes:** Standard HTTP status codes
- **URL pattern:** Predictable, resource-oriented URLs
- **Scale:** 250+ microservices, thousands of API endpoints
- **Performance:** Processes over 1 billion API calls per day with average response times under 150ms

### 2.3 Authentication

**Primary method: OAuth 2.0**

Supports two grant types:
1. **Authorization Code Grant** — web server flow (recommended for production integrations)
2. **Resource Owner Password Credentials Grant** — password flow (for development/testing)

**Configuration required:**

| Setting | Format |
|---------|--------|
| API URL | `https://<unique_id>.omni.manh.com` |
| Token URL | `https://<unique_id>-auth.omni.manh.com/oauth/token` |
| Authorization URL | `https://<unique_id>-auth.omni.manh.com` |
| Client ID | Custom value from admin console |
| Client Secret | Custom value from admin console |
| Username | Resource owner email |
| Password | Resource owner credential |

**Additional auth modes:** OpenID Connect (OIDC), SAML — supported for SSO scenarios.

### 2.4 Integration Patterns

**Pre-built Integration Apps:**
Manhattan Active Omni ships with integration adapters for common third-party services:
- **Payments:** Adyen, Aurus, Chase, CyberSource, First Data, Fiserv, Mercado Pago
- **Alternate payments:** Afterpay, Amazon Pay, Klarna, PayPal
- **Tax:** Avalara, OneSource, Taxware
- **Fraud:** Adyen, ClearSale, CyberSource, Signifyd
- **Address verification:** Avalara, Canada Post, Experian QAS, Loqate, UPS
- **Parcel carriers:** 15+ providers including DHL, FedEx, UPS, USPS
- **Gift cards:** Clutch, Givex, SVS, ValueLink, Voucher Express
- **Promotions:** Oracle Relate, Salesforce, XCCommerce
- **Customer master:** Salesforce Commerce Cloud
- **Loyalty:** 500friends
- **E-commerce:** Shopify (deep native integration)

**Shopify Integration (reference implementation):**
- Uses Shopify GraphQL API mutations (`inventorySetQuantities`, `orderCapture`, `refundCreate`)
- Shopify webhooks for real-time order synchronization (order creation, cancellation, modification)
- Threshold-based inventory updates: define low/medium/high thresholds that trigger automatic inventory sync to Shopify
- Available to Commerce (ATC) views control which inventory segments are shared with Shopify
- Pre-configured data mapping, connectors, and business logic
- Source: https://www.shopify.com/enterprise/blog/order-management-manhattan-shopify

**Webhooks / Event-Driven:**
- Platform supports webhook management APIs
- Event-driven integration architecture documented but specifics gated
- Shopify integration confirms webhook pattern support for order lifecycle events
- SCIM 2.0 support: unconfirmed/not publicly documented

### 2.5 Developer Tools

**Manhattan Proactive (Low-Code Platform):**
- Visual application platform for building extensions
- Configure, call, or extend any function via API endpoints
- Track, provision, and monitor extension lifecycles
- Migrate extensions between environments

**Development philosophy:** "No code, low code, your code" — three tiers of customization:
1. Configuration via UI (no-code)
2. Visual extensions via Proactive (low-code)
3. Full API integration (your-code)

**Data management:**
- Configuration Director for comparing, moving, importing/exporting environment configs
- Pre-defined KPI-driven reports with customization capabilities

### 2.6 SDKs

No public SDKs identified. Integration is REST API-first. Manhattan provides:
- Postman collections for API exploration
- Code examples in developer hub documentation
- OAuth playground for auth flow testing
- GraphQL playground (availability mentioned but not detailed publicly)

---

## 3. Platform Architecture

### 3.1 Cloud Infrastructure

- **Cloud provider:** Google Cloud Platform (GCP)
- **Orchestration:** Google Kubernetes Engine (GKE)
- **Database:** Google Cloud SQL
- **Messaging:** Google PubSub
- **Analytics:** Google BigQuery
- **Networking:** Google Interconnect
- **Deployment model:** Multi-tenant SaaS

### 3.2 Microservices Architecture

- **250+ microservices** grouped into solutions (Active Omni, Active Supply Chain, etc.)
- **Language/framework:** Java / Spring Boot
- **Containerization:** Docker images using Debian-based OpenJDK base layers
- **Kubernetes specs used:** Deployment (stateless), StatefulSet (stateful), Service (load balancing), ConfigMap/Secret (configuration), Ingress (gateway)
- **Deployment framework:** "Rubik" — modular shell scripts, YAML templates, bundled CLI tools
- **Customer isolation:** Each customer environment deploys in isolated "Rubik Stack" with dedicated Kubernetes cluster

### 3.3 Key Architecture Properties

- **Versionless:** Continuous delivery model, no disruptive version upgrades
- **Update cadence:** Features delivered every 90 days
- **API-first:** All business interfaces and data operations exposed as REST endpoints
- **Elasticity:** GKE autoscaling, node auto-provisioning, auto-repair
- **Performance:** 1 billion+ API calls/day, <150ms average response time
- **System services:** Indexing, messaging, identity/authorization, service discovery, monitoring, logging

---

## 4. Help Centers, Knowledge Bases, Community

### 4.1 Support Channels

| Channel | Details |
|---------|---------|
| Developer Hub | https://developer.manh.com/ — API docs, guides, code samples |
| Product page | https://www.manh.com/solutions/omnichannel-software-solutions |
| Phone support | 24/7 global product support |
| Email/Help desk | Online contact form + support portal |
| Video tutorials | Available through support portal |
| Partner ecosystem | 4SiGHT, ITOrizon, JBF Consulting, Locus IT Services |

### 4.2 Documentation Access

| Resource | Access Level |
|----------|-------------|
| Developer portal (developer.manh.com) | Partially public — basic guides and architecture visible; full API reference requires auth |
| Full API reference (api.developer.manh.com) | **Gated** — requires customer/partner credentials |
| Integration app documentation | **Gated** — requires licensing |
| Knowledge base / help center | **Gated** — customer support portal login required |
| Community forums | No public community forum identified |

### 4.3 Training & Certification

Manhattan offers training through partner system integrators (4SiGHT, ITOrizon, Locus IT). No public certification program identified. Training is typically part of implementation engagements.

---

## 5. User Reviews: Pros and Cons

### 5.1 Strengths (from G2, Gartner Peer Insights, Capterra, analyst reports)

| Strength | Source |
|----------|--------|
| Industry-leading order orchestration and inventory visibility | Forrester Wave 2025 (5.0 scores in 20/27 criteria) |
| Speed to market for new features | Gartner Peer Insights |
| Excellent implementation support from Manhattan PS team | G2, Capterra |
| High accuracy integrations — seamlessly connects online with physical locations | Capterra |
| Real-time inventory visibility across all channels reduces stockouts | Multiple sources |
| Low downtime — system runs reliably at scale | G2 |
| Unified platform for online, mobile, in-store, and wholesale | Multiple sources |
| Product Managers accessible, competent R&D and Professional Services | Gartner Peer Insights |
| Only OMS with native RFID capabilities in-store | Forrester Wave 2025 |
| Fulfillment Insights dashboard for peer benchmarking | Forrester Wave 2025 |
| Postgame Spotlight for identifying inventory allocation decisions hindering fulfillment | Forrester Wave 2025 |
| Mature cloud engineering — modern stack, versionless updates | Lokad independent review |
| Shopify deep integration available | Manhattan/Shopify partnership |

### 5.2 Weaknesses (from G2, Gartner Peer Insights, Capterra, Lokad)

| Weakness | Source |
|----------|--------|
| Limited customization options for specific workflows | G2, Gartner Peer Insights |
| Not suited for FMCG industry — lacks vertical-specific capabilities | Gartner Peer Insights |
| Poor application performance / UI not user-friendly | G2 |
| Expensive — pricing requires significant commitment | G2, ITQlick |
| Pricey modifications on base product when integrating non-Manhattan systems | G2 |
| Onboarding lengthy and resource-intensive | Multiple sources |
| Customer support response times inconsistent | Software review sites |
| Team fragmented across international borders with inflexible waterfall delivery | Gartner Peer Insights |
| Product complexity — difficult to understand what you're getting | Gartner Peer Insights |
| Administrative tools sometimes don't work, require workarounds | G2 |
| AI/ML optimization claims lack algorithmic transparency | Lokad independent review |
| No independent algorithmic validation (no public benchmarks, no peer-reviewed publications) | Lokad independent review |
| Heavily partner-dependent for successful implementation | Lokad independent review |
| Not plug-and-play despite SaaS positioning | Lokad independent review |
| LLM-based AI agents (Maven) lack published safety mechanisms | Lokad independent review |

### 5.3 Reddit / Community Sentiment

No significant Reddit discussions found for Manhattan Active Omni on r/ecommerce or r/supplychain. This is consistent with Manhattan's enterprise positioning — their customer base is large retailers/brands who rarely discuss tooling on public forums. Most user feedback comes through Gartner Peer Insights and G2.

---

## 6. Pricing

Manhattan Active Omni does **not** publish public pricing. Pricing is modular and negotiated per customer.

### Estimated Ranges (from third-party sources)

| Deployment Size | Estimated Monthly Cost | Source |
|----------------|----------------------|--------|
| SMB (1 user, basic POS) | ~$500/month | ITQlick |
| Mid-market (10-50 users) | $5,000-$25,000/month | ITQlick, SelectHub |
| Enterprise (100+ users) | $10,000-$50,000+/month | ITQlick |

**Implementation costs:** Can double or triple first-year expenses. Includes customization, training, data migration, and system integrator fees.

**Target market:** Mid-to-large retailers with annual revenues exceeding $5M and dedicated IT teams. Not appropriate for small businesses or quick, inexpensive setups.

**Pricing model:** Modular — businesses select and pay for specific modules/capabilities. Custom enterprise pricing via sales engagement.

Sources:
- https://www.itqlick.com/manhattan-active-omni/pricing
- https://www.selecthub.com/p/retail-management-software/manhattan-active-omni/

---

## 7. Multi-Node Inventory Aggregation & Real-Time Availability

### Architecture

Manhattan's inventory architecture operates on three layers:

1. **Manhattan Interactive Inventory** — the raw, real-time global inventory view across all nodes (DCs, stores, 3PLs, suppliers, in-transit). This is the "single source of truth" for physical inventory position.

2. **Available to Commerce (ATC)** — the filtering/segmentation layer that creates virtual Views of inventory tailored to specific channels, brands, delivery methods, and business rules. This is where safety stock, presentation stock, store capacity limits, and channel-specific exclusions are applied.

3. **Order Promising Engine** — consumes ATC views and applies ML-driven fulfillment optimization to generate precise delivery promises and sourcing decisions.

### Real-Time Capabilities

- In-memory caching for sub-second promise responses
- REST APIs for both global and location-specific inventory queries
- Threshold-based automatic inventory updates to connected channels (e.g., Shopify)
- Dynamic adjustment of availability views based on operational conditions (outages, workload spikes)
- Conditional item substitutions based on business rules

### Node Types Supported

- Distribution centers (owned)
- Retail stores (ship-from-store, pickup, curbside)
- Third-party logistics providers (3PL)
- Vendor/supplier drop-ship
- In-transit inventory
- On-order / purchase order inventory

### Aggregation Logic

The system aggregates inventory across all node types into a unified view, then applies ATC rules to determine what's available to each channel. Factors in the aggregation:
- Physical on-hand quantities
- Reserved/allocated quantities
- In-transit quantities with expected arrival dates
- Purchase order quantities with expected receipt dates
- Quality/disposition status
- Location-specific fulfillment capability flags
- Safety stock and presentation stock thresholds

---

## 8. Competitive Positioning

### Analyst Recognition

| Analyst | Recognition | Year |
|---------|-------------|------|
| Forrester Wave OMS | **Leader** — highest score possible in 20/27 criteria | Q1 2025 |
| Gartner Magic Quadrant WMS | **Leader** (17th consecutive year) | 2025 |
| Gartner Peer Insights DOM | Listed with positive reviews | 2025-2026 |

### Market Position

- PeerSpot Order Management Hubs mindshare: ~11-24% (fluctuating, 2025 data)
- Founded 1990, NASDAQ-listed (MANH)
- ~$1-1.2B annual revenue, 3,000+ employees
- Thousands of customers globally across retail, logistics, manufacturing

### Key Differentiators vs. Competition

1. **Unified platform** — OMS, WMS, TMS, POS, customer engagement all on same microservices platform
2. **Available to Commerce** — patented virtual inventory segmentation technology
3. **Native RFID** — only OMS with built-in RFID capabilities for store operations
4. **Fulfillment Insights** — peer benchmarking dashboard unique to Manhattan
5. **Postgame Spotlight** — post-fulfillment analysis identifying allocation inefficiencies
6. **AI agents** (as of Jan 2026) — Store Associate Agent, Contact Center Agent, OMS Configuration Agent

---

## 9. Integration Assessment for Omnifill

### Access Path

Manhattan's APIs and documentation are **fully gated**. Integration requires one of:
1. **Customer license** — most direct path, comes with developer hub access
2. **Partner program** — apply at https://www.manh.com/about-us/partners — requires NDA
3. **Sales engagement** — request access through Manhattan sales team

### Integration Feasibility

| Aspect | Assessment |
|--------|-----------|
| API quality | **High** — REST, JSON, well-documented (behind auth wall), 250+ microservices |
| Authentication | **Standard** — OAuth 2.0 (Authorization Code + ROPC grants) |
| Inventory APIs | **Comprehensive** — global and location-specific, real-time, ATC views |
| Order APIs | **Comprehensive** — full lifecycle, multi-channel, orchestration |
| Promising APIs | **Available** — but specific endpoints not publicly documented |
| Webhook support | **Confirmed** — webhook management APIs exist |
| Sandbox/testing | **Available** — developer hub includes sandbox access for licensed users |
| Documentation depth | **Deep** — thousands of endpoints documented, but fully gated |
| Public access | **Minimal** — basic architecture and auth guides visible; everything else requires credentials |

### Recommended Approach

1. Engage Manhattan partner program or sales for API access
2. Use developer portal (developer.manh.com) as primary integration reference
3. Model Omnifill adapter interface based on known capabilities documented above
4. Use Shopify integration as reference implementation pattern for understanding Manhattan's integration model
5. Plan for OAuth 2.0 Authorization Code flow for production, ROPC for development

### Risk Factors

- **Gated access** — cannot prototype without partnership/license
- **Implementation complexity** — not plug-and-play, may require SI involvement
- **Cost** — enterprise pricing, potentially $10K-$50K+/month for access
- **Customization limits** — base product modifications can be expensive
- **Vendor dependency** — deep integration creates switching cost

---

## Sources

### Official Manhattan Associates
- [Order Management System](https://www.manh.com/solutions/omnichannel-software-solutions/order-management-system)
- [Available to Commerce](https://www.manh.com/products/available-to-commerce)
- [Precise Order Promising](https://www.manh.com/solutions/omnichannel-software-solutions/order-management-system/precise-order-promising)
- [Optimized Fulfillment Sourcing](https://www.manh.com/solutions/omnichannel-software-solutions/order-management-system/optimized-fulfillment-sourcing)
- [Global Order Orchestration](https://www.manh.com/solutions/omnichannel-software-solutions/order-management-system/global-order-orchestration)
- [Adaptive Network Fulfillment](https://www.manh.com/solutions/omnichannel-software-solutions/order-management-system/adaptive-network-fulfillment)
- [Enterprise Promise & Fulfill](https://www.manh.com/about-us/newsroom/press-releases/manhattan-associates-transforms-enterprise-selling-with-enterprise-promise-fulfill)
- [B2B Order Routing Optimization](https://www.manh.com/solutions/b2b-commerce/order-routing-optimization-with-enterprise-promise-fulfill)
- [Manhattan Active Platform](https://www.manh.com/solutions/manhattan-active-platform)
- [Developer Tools & APIs](https://www.manh.com/solutions/manhattan-active-platform/developer-tools-api)
- [Developer Hub](https://www.manh.com/solutions/manhattan-active-platform/developer-tools-api/developer-hub)
- [Manhattan + Shopify Partnership](https://www.manh.com/about-us/newsroom/press-releases/manhattan-and-shopify-deliver-seamless-omnichannel-shopping-experiences-with-latest-order-management-collaboration)
- [Jan 2026 Retail Enhancements](https://www.manh.com/about-us/newsroom/press-releases/manhattan-associates-announces-latest-enhancements-for-retailers)
- [Google Cloud Marketplace Launch](https://www.manh.com/about-us/newsroom/press-releases/manhattan-associates-launches-supply-chain-commerce-solutions-on-google-cloud-marketplace)

### Developer Portal
- [Developer Home](https://developer.manh.com/)
- [REST API Guide](https://developer.manh.com/docs/how-to/rest-api/)
- [Authentication](https://developer.manh.com/docs/how-to/rest-api/authentication/)
- [Code Integration](https://developer.manh.com/docs/how-to/rest-api/yourcode/)
- [Postman Setup](https://developer.manh.com/docs/how-to/rest-api/postman/)
- [API Reference](https://developer.manh.com/docs/how-to/rest-api/reference/)
- [Active Omni App Reference](https://developer.manh.com/docs/reference/app/mao/)
- [Technology Overview](https://developer.manh.com/docs/overview/technology-overview-manhattan-active-cloud/)
- [Full API Reference (auth required)](https://api.developer.manh.com)

### Analyst Reports
- [Forrester Wave OMS Q1 2025](https://www.manh.com/our-insights/resources/research-reports/forrester-wave-order-management-systems)
- [Forrester Wave Press Release](https://ir.manh.com/news-releases/news-release-details/manhattan-named-leader-industrys-premier-evaluation-order)
- [Gartner Peer Insights - Active Order Management](https://www.gartner.com/reviews/market/distributed-order-management-systems/vendor/manhattan-associates/product/manhattan-active-order-management)
- [Gartner Peer Insights - Active Allocation](https://www.gartner.com/reviews/market/supply-chain-planning-solutions/vendor/manhattan-associates/product/manhattan-active-allocation)

### User Reviews
- [G2 Reviews](https://www.g2.com/products/manhattan-active-order-management/reviews)
- [Capterra](https://www.capterra.com/p/209714/Manhattan-Active-Omni/)
- [Software Advice](https://www.softwareadvice.com/inventory-management/manhattan-active-omni-profile/)
- [PeerSpot](https://www.peerspot.com/products/manhattan-active-omni-reviews)
- [SelectHub](https://www.selecthub.com/p/retail-management-software/manhattan-active-omni/)
- [GetApp](https://www.getapp.com/all-software/a/manhattan-active-omni/)

### Independent Analysis
- [Lokad Critical Review](https://www.lokad.com/review-of-manh-com/)
- [ITQlick Pricing Analysis](https://www.itqlick.com/manhattan-active-omni/pricing)

### Partner / Third-Party
- [Shopify Integration Guide](https://www.shopify.com/enterprise/blog/order-management-manhattan-shopify)
- [4SiGHT Manhattan Overview](https://4sight.com/about/partners/manhattan-associates/manhattan-active-overview/)
- [4SiGHT Order Management](https://4sight.com/about/partners/manhattan-associates/manhattan-order-management/)
- [ITOrizon Manhattan Active Omni](https://itorizon.com/scm/manhattan/active/omni/)
- [CYBRA - What is Manhattan Active Omni](https://cybra.com/manhattan-active-omni/)
- [Google Cloud Blog - Manhattan Architecture](https://cloud.google.com/blog/topics/partners/how-manhattan-associates-rebuilt-their-platform-on-google-cloud)
- [Google Cloud Blog - Cloud SQL + Manhattan](https://cloud.google.com/blog/products/databases/how-cloud-sql-powers-manhattan-associates-ai-supply-chain-platform)
