# Enterprise Delivery & Logistics Platforms

Research date: 2026-03-31

## Shipsy

- **Category:** AI-powered end-to-end logistics platform (first, middle, last mile)
- **Founded:** 2015, Gurugram, India
- **API Types:** REST (HTTPS)
- **Auth:** API Key (shared after enterprise engagement, no self-service)
- **Docs:**
  - API Playground: https://apiplayground.shipsy.in/ [Source: https://apiplayground.shipsy.in/]
  - Help Center (Confluence): https://shipsy.atlassian.net/wiki/spaces/HELP [Source: https://shipsy.atlassian.net/wiki/spaces/HELP/pages]
  - Postman Collection (Exim API): https://www.postman.com/planetary-water-589524/shipsy-exim-api/overview [Source: postman.com]
  - GitHub: https://github.com/shipsy (21 repositories) [Source: github.com/shipsy]
- **SDKs:** None publicly available
- **Webhooks:** Not explicitly documented in public resources
- **Integrations:** API, FTP, EDI. Connects with ERPs (SAP, Oracle), CRM, OMS, WMS, POS, eCommerce, customs systems, 3PLs, shipping lines, cargo carriers [Source: https://shipsy.io/platform/]
- **Capabilities:**
  - AI/ML-powered route optimization, vehicle load optimization, 3PL partner selection ("Intelligence Engine")
  - Automated dispatch with configurable compliance controls
  - Driver companion app (iOS/Android) with performance analytics
  - Real-time tracking across 50+ shipping lines and 40+ 3PLs
  - Proactive ETAs, delay alerts, exception notifications (SMS, WhatsApp, email, chat, web portal)
  - ePOD: photos, signatures, customer IDs, GPS coordinates
  - Full reverse logistics: auto-accept returns, assign drivers, club reverse pickups with planned deliveries
  - Digital Control Tower with dashboard-driven analytics
- **Coverage:** 30+ countries. Offices in India, Dubai, Saudi Arabia, Indonesia, Netherlands, Australia. Customer base: India 44%, US 22%, UAE 12% [Source: https://shipsy.io/about-us/, https://enlyft.com/tech/products/shipsy]
- **Clients:** Coca Cola, Kuehne Nagel, UPS [Source: https://shipsy.io/about-us/]
- **Pricing:** Subscription-based (monthly/yearly/perpetual license). No public pricing — custom quotes only. [Source: https://www.getapp.com/operations-management-software/a/shipsy-1/pricing/]
- **User Sentiment:**
  - Pros: Intuitive field force app, cost-effective, powerful real-time analytics, strong support, high customization [Source: G2, Capterra reviews]
  - Cons: Long onboarding with limited materials, overwhelming interface for beginners, limited customization in some scenarios (distance-only constraints), ERP integration delays (especially SAP), occasional tracking delays, timeline commitments slip [Source: G2, Capterra, elogii.com, gocomet.com]
- **Best For:** Large enterprises needing full supply chain logistics across multiple countries

---

## FarEye

- **Category:** AI-driven last-mile delivery orchestration
- **Founded:** India, now HQ'd in Chicago, IL
- **API Types:** REST (API Key authentication)
- **Auth:** API Key shared by API support team after enterprise engagement (no public OAuth or self-service)
- **Docs:**
  - No public developer portal found — API docs shared privately
  - GitHub: https://github.com/far-eye (limited public repos) [Source: github.com/far-eye]
  - Support Portal: https://support.getfareye.com/ [Source: https://support.getfareye.com/]
  - Enterprise Support Plan: https://fareye.com/security/enterprise-support-plan [Source: fareye.com]
- **SDKs:** None publicly documented
- **Webhooks:** Mentioned in returns process automation context [Source: https://www.clickpost.ai/carrier-integration/fareye]
- **Integrations:** 40+ logistics partner integrations. SAP certified partner. Available on AWS Marketplace and Microsoft AppSource. [Source: https://fareye.com/carrier-integration-software]
- **SAP Store:** https://store.sap.com/dcp/en/product/display-2001012093_live_v1/fareye-platform/ [Source: store.sap.com]
- **Capabilities:**
  - Dynamic routing with real-time traffic, delivery windows, vehicle capacity data
  - Cross-docking, roster management, delivery orchestration
  - GPS routing, electronic POD, hyperlocal order broadcasting
  - End-to-end order-to-door visibility across multiple carriers
  - Omnichannel notifications: WhatsApp, SMS, email with live tracking + ETA
  - Digital POD: signatures, photos, contactless handoff
  - Automated returns: customer-initiated pickup scheduling, reverse logistics
  - Control tower with exception management and real-time delay/disruption alerts
- **Coverage:** 30+ countries, 5 continents. Revenue: Americas/EMEA/APAC roughly even. Customer base: India 41%, US 21%, UAE 16%. [Source: https://fareye.com/news/fareye-delivers-revenue-growth-fy25, https://6sense.com/tech/field-service-management/fareye-market-share]
- **Clients:** DHL, Walmart, Tata Steel, Hilti, Amway, UPS, Gordon Foods, Zalora; 12+ Fortune Global 500 companies [Source: https://fareye.com/news/fareye-delivers-revenue-growth-fy25]
- **Pricing:**
  - Custom enterprise pricing — no published tiers
  - Historical reference (2022): ~$50/month (1 user) to ~$15,000-$20,000/month (1,000 users)
  - Implementation: $5,000 (small) to $50,000+ (large enterprise)
  - [Source: https://www.itqlick.com/fareye/pricing, https://blog.locus.sh/fareye-pricing-guide/]
- **User Sentiment:**
  - Pros: Exceptional driver app, quick support resolution, 40+ pre-built carrier integrations, good value for money (Capterra 4.5/5), quality commitment [Source: G2, Capterra, spoke.com]
  - Cons: Feature complexity overkill for simple use cases, technical glitches (server errors, bulk pickup errors, false GPS blackout alerts), slow software speed, inaccurate live tracking, higher price, steep learning curve [Source: G2, spoke.com]
- **Best For:** Enterprise retail/ecommerce/3PL needing carrier orchestration at scale

---

## Locus (locus.sh)

- **Category:** AI-powered dispatch management and route optimization
- **Founded:** 2015, Bangalore, India
- **API Types:** REST, OpenAPI 2.0 compliant (SwaggerUI)
- **Auth:** Client ID-based (shared by Locus representative after engagement — no self-service)
- **Docs:**
  - Documentation Portal: https://docs.locus.sh/ [Source: https://docs.locus.sh/]
  - API Reference: https://locus.sh/resources/api-references/ [Source: https://locus.sh/resources/api-references/]
  - API Endpoints:
    - Order Management: `https://oms.locus-api.com/v1`
    - Entity Management: `https://locus-api.com/v1`
    - Platform Entities: `https://platform.locus-api.com/v1`
- **SDKs:** None publicly documented
- **Webhooks:** Documented within API docs (order management, carrier tendering) [Source: https://docs.locus.sh/]
- **Integrations:** ERP, OMS, WMS, carrier systems (EDI + API), telematics, CX platforms. Enterprise integration: 3-6 months. [Source: https://locus.sh/]
- **Capabilities:**
  - ML-powered geocoding optimization and dynamic route planning
  - Fast: hundreds of tasks scheduled in under 10 minutes
  - Automated order-to-dispatch with real-time rescheduling
  - Capacity forecasting and resource orchestration
  - ML-based vehicle and driver assignment
  - Driver companion app for order requests and updates
  - Live tracking with route deviation and SLA breach detection
  - ePOD: photo, PIN, e-signature with geotag
  - On-demand returns capture and reverse logistics automation
  - Advanced analytics: delivery costs, SLA compliance, fleet utilization
- **Coverage:** 30+ countries (North America, Europe, Southeast Asia, Middle East, ANZ, India). 200+ clients, 350+ enterprise deployments, 1 billion+ deliveries executed. [Source: https://locus.sh/about/]
- **Clients:** Unilever, Nestle, Bukalapak, Tata Group, BlueDart [Source: https://locus.sh/about/]
- **Impact:** $320M+ in logistics cost savings for customers [Source: https://locus.sh/about/]
- **Pricing:** Subscription starting at ~$15,000/year. Enterprise pricing, not publicly detailed. [Source: https://www.getapp.com/operations-management-software/a/locus-platform/]
- **User Sentiment:**
  - Pros: User-friendly UI, fast route calculations (hundreds of tasks < 10 min), ML-powered geocoding, exceptional support, clean interface, customizable [Source: G2, Capterra]
  - Cons: Strict batch processing (deviations cause errors), non-applicable elements can't be disabled, slow response times, occasional routing errors (wrong routes), limited customization for edge cases, geocoding inaccuracies for similar names [Source: G2, Capterra]
- **Best For:** Enterprise retail/FMCG/3PL dispatch management at scale

---

## Circuit (now Spoke)

- **Category:** Route planning and last-mile delivery management (SMB-focused)
- **Rebranded:** Circuit → **Spoke** (late 2025)
- **API Types:** REST (HTTPS only, v0.2b beta)
- **Base URL:** `https://api.getcircuit.com/public/v0.2b`
- **Auth:** API Key (generated from Settings > Integrations in Spoke Dispatch dashboard)
- **Docs:**
  - Developer Portal: https://developer.dispatch.spoke.com/ [Source: https://developer.dispatch.spoke.com/]
  - API Reference: https://developer.dispatch.spoke.com/api [Source: https://developer.dispatch.spoke.com/api]
  - Data Models: Depot, Driver, Plan, Operation, Route, Stop, Unassigned Stop, Custom Stop Property [Source: https://developer.dispatch.spoke.com/docs/models/route]
  - Webhook API: documented [Source: https://developer.dispatch.spoke.com/]
  - GitHub: https://github.com/getcircuit [Source: github.com/getcircuit]
- **SDKs:** None — users implement HTTP clients against documented endpoints [Source: https://apitracker.io/a/get-spoke]
- **Webhooks:** Documented Webhook API available
- **Integrations:** Shopify, Zapier
- **Help Center:** https://help.spoke.com/en/ [Source: https://help.spoke.com/en/]
- **Capabilities:**
  - Route optimization for delivery stops (algorithmic)
  - Delivery scheduling with time windows, dispatch to drivers
  - Unlimited team members/drivers on all plans
  - Real-time driver location tracking (synced every 15 seconds)
  - Automatic customer notifications: ETA, queue position, live tracking link (customizable per customer)
  - ePOD: barcode scanning, delivery photos, recipient signatures, internal notes (stored indefinitely)
  - Pickup and returns support
  - Analytics: cost per delivery, failed delivery reasons, estimated vs actual route time
- **Pricing (public, transparent):**
  - Route Planner (individual): Free (10 stops) or ~$20/month unlimited
  - Dispatch Starter: $125/month (1,000 stops, unlimited drivers, PoD, tracking, notifications, 30-day history)
  - Dispatch Premium: $200/month (2,000 stops, custom stop properties, 1-year history)
  - Dispatch Expert: $1,000/month (12,000 stops, geo-fencing, personalized onboarding, 5-year history)
  - Overage: 4-7 cents/additional stop depending on plan
  - [Source: https://spoke.com/dispatch/pricing]
- **Coverage:** 190+ countries (uses Google Maps) [Source: https://www.getapp.com/transportation-logistics-software/a/circuit-routing/]
- **User Sentiment:**
  - Pros: Extremely easy to use, highest-rated delivery app (4.7 stars, 20K+ reviews), strong customer notifications, responsive team, well-designed edge case handling [Source: Google Play Store, Capterra, routific.com]
  - Cons: Route optimization can be suboptimal (routes cross, back-and-forth), scalability limitations, expensive per-stop at high volume, free tier limited to 10 stops, no customization for weather/traffic/priority/sequencing/per-stop duration, no recurring route templates [Source: routific.com, kardinal.ai, upperinc.com, Reddit]
- **Best For:** Individual drivers and SMBs needing simple, affordable route planning

---

## Comparison Matrix

| Dimension | Shipsy | FarEye | Locus | Circuit/Spoke |
|-----------|--------|--------|-------|---------------|
| **Focus** | Full supply chain | Last-mile orchestration | Dispatch + routes | Route planning |
| **Target** | Enterprise (Fortune 500) | Enterprise (Fortune 500) | Enterprise (200+ clients) | SMB + individuals |
| **API Access** | Gated (playground exists) | Fully gated | Gated (SwaggerUI docs) | Public (v0.2b beta) |
| **API Style** | REST | REST | REST (OpenAPI 2.0) | REST |
| **Public Pricing** | No | No | ~$15K/yr start | Yes ($125-$1,000/mo) |
| **Coverage** | 30+ countries | 30+ countries | 30+ countries | 190+ countries |
| **Webhooks** | Unknown | Mentioned | Documented | Documented |
| **SDKs** | None | None | None | None |
| **Integration Time** | Weeks-months | Weeks-months | 3-6 months | Self-service (minutes) |
| **Dev Experience** | Poor (gated) | Poor (no public docs) | Moderate (SwaggerUI) | Best (public portal) |

## Integration Recommendations

- **Locus** has the best-documented API among the enterprise platforms (OpenAPI 2.0 with SwaggerUI), making it the most accessible for adapter development
- **Circuit/Spoke** is the only platform with a public, self-service developer portal — ideal for SMB-tier integration
- **Shipsy** has an API Playground which helps, but full docs are gated
- **FarEye** has no public API documentation at all — enterprise sales engagement required
- All four platforms are India-founded with strong APAC presence, useful for non-US market coverage

## Sources

- Shipsy Platform: https://shipsy.io/platform/
- Shipsy About: https://shipsy.io/about-us/
- Shipsy API Playground: https://apiplayground.shipsy.in/
- Shipsy Help Center: https://shipsy.atlassian.net/wiki/spaces/HELP
- Shipsy GitHub: https://github.com/shipsy
- Shipsy Postman: https://www.postman.com/planetary-water-589524/shipsy-exim-api/overview
- Shipsy Reviews: https://www.g2.com/products/shipsy-shipsy/reviews, https://www.capterra.com/p/164099/Shipsy/reviews/
- Shipsy Competitor Analysis: https://elogii.com/blog/shipsy-reviews, https://www.gocomet.com/blog/shipsy-review-competitor-comparison/
- Shipsy Market: https://enlyft.com/tech/products/shipsy
- FarEye Products: https://fareye.com/products/delivery-experience, https://fareye.com/route-optimization-api
- FarEye Tracking: https://fareye.com/products/last-mile-tracking
- FarEye POD: https://fareye.com/proof-of-delivery-app
- FarEye Returns: https://fareye.com/solutions/returns-management
- FarEye Carrier Integration: https://fareye.com/carrier-integration-software
- FarEye Support: https://support.getfareye.com/
- FarEye SAP Store: https://store.sap.com/dcp/en/product/display-2001012093_live_v1/fareye-platform/
- FarEye Reviews: https://www.g2.com/products/fareye/reviews, https://spoke.com/dispatch/blog/fareye-reviews
- FarEye Revenue: https://fareye.com/news/fareye-delivers-revenue-growth-fy25
- FarEye Pricing: https://www.itqlick.com/fareye/pricing, https://blog.locus.sh/fareye-pricing-guide/
- Locus Platform: https://locus.sh/
- Locus About: https://locus.sh/about/
- Locus Docs: https://docs.locus.sh/
- Locus API Reference: https://locus.sh/resources/api-references/
- Locus Dispatch: https://locus.sh/dispatch-management-software/
- Locus DX: https://locus.sh/delivery-experience-management-software/
- Locus Reviews: https://www.g2.com/products/locus-locus/reviews, https://www.capterra.com/p/176446/Locus-Dispatcher/reviews/
- Locus Pricing: https://www.getapp.com/operations-management-software/a/locus-platform/
- Circuit/Spoke Dispatch: https://spoke.com/dispatch
- Spoke Developer Portal: https://developer.dispatch.spoke.com/
- Spoke API: https://developer.dispatch.spoke.com/api
- Spoke Pricing: https://spoke.com/dispatch/pricing
- Spoke Help: https://help.spoke.com/en/
- Spoke GitHub: https://github.com/getcircuit
- Circuit Reviews: https://www.routific.com/blog/circuit-for-teams-route-planner-review-and-alternatives
- Circuit Pricing Analysis: https://www.upperinc.com/blog/circuit-pricing/
- Circuit Route Quality: https://kardinal.ai/circuit-app-for-route-planning-review-and-alternatives/
- Reddit Circuit discussions: https://redditfavorites.com/android_apps/circuit-delivery-route-planner
