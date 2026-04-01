# Crowdsourced & Specialty Delivery Platforms

Research date: 2026-03-31

## Roadie (UPS Subsidiary)

- **Category:** Crowdsourced same-day delivery
- **Status:** Active (acquired by UPS in 2021)
- **Model:** Gig-economy, 200,000+ independent drivers with personal vehicles (sedans to cargo vans/trucks)
- **Coverage:** 97% of U.S. households, 30,000+ zip codes, local deliveries up to 100 miles
- **API Types:** REST (v1)
- **Auth:** Bearer token in `Authorization` header (obtained via sales contact)
- **Docs:**
  - API Reference: https://docs.roadie.com/
  - Enterprise: https://www.roadie.com/enterprise/
  - Volume pricing: https://www.roadie.com/enterprise/volume-pricing-request
- **SDKs:** None (no public SDK or developer portal — sales-gated onboarding)
- **Webhooks:** Real-time tracking, photographic chain of custody, signature confirmations
- **Integrations:** Shopify, UPS systems, RoadieXD (cross docking with UPS)
- **Capabilities:**
  - Same-day, next-day, on-demand, scheduled, round-trip, multi-stop deliveries
  - Oversized/bulky items (strength vs. traditional parcel networks)
  - Reverse logistics and inventory movement
  - White-labeled delivery experience
- **Pricing:**
  - Custom/volume-based enterprise pricing (contact sales)
  - Driver payouts: average gig $13; local $25-$50; long-distance up to $650
- **User Sentiment:**
  - Pros: Massive geographic coverage, UPS backing, handles oversized items, fast integration (2-3 weeks), flexible vehicle types
  - Cons: Inconsistent driver quality, text-only support (slow), driver pay dropped post-UPS acquisition, no public pricing transparency
- **Integration Timeline:** Sandbox to go-live in 2-3 weeks

---

## GoShare

- **Category:** On-demand delivery and moving
- **Status:** Active
- **Model:** Gig-economy, 40,000+ delivery professionals with trucks/vans/cars
- **Coverage:** Nationwide U.S., expanding into smaller metros
- **API Types:** REST (JSON)
- **Auth:** Sales-gated (contact business team for API credentials)
- **Docs:**
  - API Landing: https://goshare.co/api/
  - API Docs: https://api.goshare.co/#introduction (gated)
  - Developer Portal: https://goshare.co/developers/
- **SDKs:** None (documentation gated behind sales)
- **Webhooks:** Real-time delivery status updates and driver location
- **Integrations:** TMS, ecommerce, POS, WMS; Zapiet for Shopify
- **Capabilities:**
  - Large/bulky item delivery, LTL freight, moving services
  - Vehicle variety: cars, SUVs, pickup trucks, cargo vans, box trucks
  - Real-time tracking and proof of delivery
- **Pricing:**
  - Per-job based on vehicle type, distance, item size, stairs
  - Approximate rates (driver earnings): Car ~$45/hr, Pickup ~$70/hr, Cargo van ~$105/hr, Box truck ~$168/hr
  - No subscription — pure per-delivery
- **User Sentiment:**
  - Pros: Vehicle variety covers wide range, good for big/bulky retail (Costco, Lowe's), reasonable pricing for short-distance, no upfront API cost
  - Cons: API docs not publicly accessible, driver pay excludes drive time, slow payment (4+ days), extras add up, inconsistent quality

---

## Veho

- **Category:** Next-day e-commerce parcel delivery
- **Status:** Active
- **Model:** Asset-light with gig drivers, technology-driven
- **Coverage:** 60+ U.S. metro markets (128M Americans), expanding to all major metros by 2026
- **API Types:** REST
- **Auth:** API key in request header (`apiKey: <key>`)
- **Docs:**
  - API Docs (v2, current): https://docs.api.shipveho.com/ (Stoplight-hosted)
  - API Docs (v1, deprecated): https://veho-technologies.github.io/api-basic-docs/ (returns 410 GONE)
- **Key Endpoints:**
  - `POST /packages` — Create package, get barcode/labels
  - `GET /packages/<ID>` — Retrieve package details
- **Label Formats:** ZPL, PDF, PNG
- **Service Classes:** `sameDay`, `nextDay`
- **Integrations:** EasyPost, ShipStation/ShipEngine, TrackingMore
- **Error Codes:** Standard HTTP (400, 401, 403, 404, 422, 429, 500, 503)
- **Capabilities:**
  - Next-day and multi-day e-commerce delivery
  - Photo proof of delivery, real-time SMS updates
  - No peak-season surcharges (key differentiator vs. UPS/FedEx)
- **Pricing:**
  - Service tiers: Ground Plus (1-5 day), Premium Economy (2-5 day, ounce-based for <1lb), FlexSave (broader windows)
  - Per-package pricing, not publicly listed
- **User Sentiment:**
  - Pros: Modern API (OpenAPI spec), photo proof of delivery, no peak surcharges, EasyPost/ShipStation integrations
  - Cons: **1.3-star Trustpilot rating** (180+ reviews), packages delivered to wrong addresses, app crashes ~40% for drivers, driver pay disputes, text-only support, metro areas only
- **Clients:** Sephora, Warby Parker, D2C brands

---

## Pandion — SHUT DOWN (January 10, 2025)

- **Category:** Open delivery network (DEFUNCT)
- **Status:** Ceased all operations January 10, 2025
- **What It Was:**
  - Aggregated regional carriers, USPS, and gig companies behind single API
  - 5 sortation centers (Philadelphia, Dallas, LA, Chicago, Atlanta)
  - ML-powered carrier selection per package
  - Covered 80%+ U.S. homes with 1-5 day ground delivery
  - Pricing started at $5.70/delivery
- **What Happened:**
  - Raised ~$125M over 5 years (including $41.5M Series B in March 2024)
  - Could not achieve scale before VC funding dried up
  - 63 employees, no severance
- **Lesson for Integration Planning:** Pandion's failure highlights the risk of depending on VC-funded delivery startups. Shippers who integrated had to scramble for alternatives. Evaluate financial stability before committing to alternative carriers.

---

## Dolly (by Taskrabbit/IKEA)

- **Category:** Large/heavy item delivery and assembly
- **Status:** Active (acquired by Taskrabbit/IKEA November 2024)
- **Model:** Vetted gig helpers (15,000+, background-checked)
- **Coverage:** 48 major U.S. cities
- **API Types:** REST (JSON)
- **Auth:** Auth0 Machine-to-Machine (M2M) OAuth 2.0 client credentials grant
- **Docs:**
  - Developer Portal: https://developer.dolly.com/docs (now redirects to https://developer.taskrabbit.com/docs)
  - API Reference: https://developer.dolly.com/reference/create-delivery
- **Sandbox:** Available for testing with sample data
- **Postman Collection:** Available
- **Key Operations:**
  - Check service availability by location
  - Get committed quote (with expiration) or rough estimate
  - Create/cancel/edit delivery
  - Status updates via polling or webhooks
- **Webhooks:** Configurable, posts delivery info including status
- **Notifications:** SMS to customers, notifications to retail teams
- **Capabilities:**
  - Same-day delivery of furniture, appliances, mattresses, exercise equipment
  - Small moves, furniture assembly, junk removal, loading/unloading
  - White-glove service with background-checked helpers
- **Pricing:**
  - Per-job: ~$300 for 2 workers / 4 hours (retail delivery)
  - Small apartment move: $400-$450
  - Average hourly rate: ~$70
  - Assembly included in quotes
- **User Sentiment:**
  - Pros: Best-in-class for big/bulky items, 4.7/5 stars (31,000+ reviews), well-documented API with OAuth 2.0 and sandbox, Taskrabbit/IKEA backing, retail partnerships (Costco, Lowe's, Big Lots)
  - Cons: Limited to 48 cities, developer docs redirecting to Taskrabbit (transition uncertainty), dynamic pricing complaints, variable helper quality, higher cost for last-minute
- **Integration Note:** Developer docs now redirect to Taskrabbit — API surface may change during transition

---

## Comparison Matrix

| Dimension | Roadie | GoShare | Veho | Pandion | Dolly |
|---|---|---|---|---|---|
| **Status** | Active (UPS) | Active | Active | SHUT DOWN | Active (Taskrabbit) |
| **Model** | Crowdsourced gig | Crowdsourced gig | Gig drivers | Carrier aggregator | Vetted gig helpers |
| **Niche** | Same-day, any size | Large/bulky, moving | E-commerce parcels | E-commerce parcels | Big/bulky only |
| **Coverage** | 97% of U.S. | Nationwide | 60 metros | Was 80% U.S. | 48 cities |
| **API Docs** | Sales-gated | Sales-gated | Public (Stoplight) | N/A (defunct) | Public (now Taskrabbit) |
| **Auth** | Bearer token | Unknown (gated) | API key header | N/A | OAuth 2.0 (Auth0 M2M) |
| **Sandbox** | Yes (2-3 wk) | Unknown | Unknown | N/A | Yes |
| **Webhooks** | Yes | Yes | Limited | N/A | Yes |
| **Best For** | Same-day + bulky | Truck-scale delivery | D2C parcel volume | N/A | Furniture/appliance |

## Integration Recommendations

- **Best API experience:** Veho (public OpenAPI) and Dolly (OAuth 2.0, sandbox, Postman)
- **Most enterprise-ready:** Roadie (UPS backing, widest coverage, proven scale)
- **Biggest risk:** VC-funded alternative carriers (Pandion's demise is instructive); Veho has poor consumer satisfaction
- **GoShare** occupies unique truck/freight niche but API docs are friction-gated
- **Dolly's Taskrabbit acquisition** creates API transition uncertainty

## Sources

- Roadie API Docs: https://docs.roadie.com/
- Roadie Enterprise: https://www.roadie.com/enterprise/
- GoShare API: https://goshare.co/api/
- GoShare Developers: https://goshare.co/developers/
- Veho API Docs (v2): https://docs.api.shipveho.com/
- Veho Technologies GitHub: https://veho-technologies.github.io/api-basic-docs/
- Dolly Developer Portal: https://developer.dolly.com/docs
- Taskrabbit Developer Docs: https://developer.taskrabbit.com/docs
- Pandion closure reporting (industry news, January 2025)
- Trustpilot reviews for Veho, Roadie
- G2 and Capterra reviews for all platforms
- Reddit r/ecommerce, r/couriers discussions
