# Delivery Management & Route Optimization Platforms

Research date: 2026-03-31

## Bringg

- **Category:** Enterprise delivery orchestration platform
- **API Types:** REST
- **Auth:** OAuth 2.0, API Key, Bearer Token, custom identity token (`x-bringg-identity-token` header)
- **Developer Portal:** https://developers.bringg.com/
- **Docs:**
  - API Reference: https://developers.bringg.com/reference/welcome-to-bringgs-api-reference [Source: developers.bringg.com]
  - Own Fleet v1.0: https://developers.bringg.com/docs/overview [Source: developers.bringg.com]
  - Delivery Hub v2.0: https://developers.bringg.com/v2.0/docs/overview [Source: developers.bringg.com]
- **SDKs:**
  - JavaScript SDK (customer-facing)
  - Android SDK (customer + driver)
  - iOS SDK (customer + driver)
  - Dispatcher SDK (dashboard)
- **Webhooks:** Supported with custom authentication for validation
- **Help Center:** https://help.bringg.com/
- **Capabilities:**
  - Route optimization with centralized planning and dispatch
  - Automated dispatch and delivery scheduling
  - Own-fleet and 3rd-party carrier orchestration
  - Real-time tracking with location sharing along delivery routes
  - Proof of delivery, returns handling
  - 250+ integrated carriers across 70+ countries
- **Pricing:**
  - Custom enterprise pricing only (no published tiers)
  - Range: ~$10,000 to $1,065,000/year (Vendr transaction data)
  - Average ~$20,000/year
- **Clients:** Walmart, Albertsons, H&M, Burger King, Coca-Cola, McDonald's LATAM (800+ enterprise customers)
- **User Sentiment:**
  - Pros: Optimizes routes reducing fuel costs, real-time tracking, flexible/customizable, Salesforce/ERP integrations, manageable learning curve [Source: G2, Capterra, TrustRadius]
  - Cons: Overwhelming for new users, confusing automation setup needs consultants, occasional tracking glitches, enterprise pricing opaque and high [Source: G2, Capterra]
- **Best For:** Enterprise multi-carrier orchestration at scale

---

## Onfleet

- **Category:** Last-mile delivery management
- **API Types:** REST
- **Base URL:** `https://onfleet.com/api/v2/`
- **Auth:** HTTP Basic Auth (API key as username, password blank)
- **Developer Hub:** https://docs.onfleet.com/
- **Docs:**
  - API Reference: https://docs.onfleet.com/reference/introduction [Source: docs.onfleet.com]
  - Setup Tutorial: https://docs.onfleet.com/reference/setup-tutorial [Source: docs.onfleet.com]
- **SDKs (Official):**
  - Node.js: https://github.com/onfleet/node-onfleet
  - Python (pyonfleet): https://github.com/onfleet/pyonfleet
  - PHP, Ruby, Java wrappers (community)
- **Webhooks:** 10+ event triggers (task creation, completion, failure, ETA changes, driver arrival). Configured in Settings > "API & Webhooks".
- **Rate Limits:** 20 requests/second across all organization API keys
- **Help Center:** https://support.onfleet.com/
- **Capabilities:**
  - Automated route optimization with real-time adjustments
  - Auto-dispatch and delivery scheduling
  - Driver management with dedicated mobile app
  - Real-time tracking, SMS/email customer notifications
  - Proof of delivery (photo, signature, barcode, notes)
  - Analytics and reporting dashboard
- **Pricing:**
  - Launch: ~$599/month (up to 2,500 tasks, core features)
  - Scale: ~$1,299/month (advanced route optimization, auto-dispatch, extended reporting)
  - Enterprise: ~$2,999/month (multi-region, enterprise security)
  - 14-day free trial on all plans
  - Additional SMS/telephony costs
- **Clients:** Imperfect Foods, MedMen, various restaurant chains
- **User Sentiment:**
  - Pros: Simple intuitive interface, strong route optimization, excellent driver app, 14-day free trial, good API/webhook ecosystem [Source: G2 4.6/5, Capterra]
  - Cons: UI "dark" and "clunky" with occasional glitches, driver location not always real-time, scalability limitations, SMS sold as add-on, pricing grows with volume [Source: G2, Spoke]
- **Best For:** Mid-market full delivery management with good API

---

## DispatchTrack

- **Category:** AI-powered last-mile delivery (furniture, appliances, heavy goods)
- **API Types:** REST
- **Auth:** API Key (Admin tab of dashboard)
- **Docs:**
  - Last Mile API: https://apidocs-lastmile.dispatchtrack.com/ [Source: apidocs-lastmile.dispatchtrack.com]
  - Planner API: https://apidocs-planner.dispatchtrack.com/ [Source: apidocs-planner.dispatchtrack.com]
  - Webhooks: https://webhooks-lastmile.dispatchtrack.com/ [Source: webhooks-lastmile.dispatchtrack.com]
  - Beetrack API (legacy): https://apidoc.beetrack.com/ [Source: apidoc.beetrack.com]
- **SDKs:** Java API wrapper (Wildstar Technologies, community)
- **Help:** https://www.dispatchtrack.com/company/support | 24/7 support: 1-866-437-3573 ext 2
- **Capabilities:**
  - AI route optimization with claimed 98% ETA accuracy
  - Customer appointment windows and scheduling
  - Driver mobile app (98% driver uptake rate)
  - Real-time tracking with ETA notifications
  - Proof of delivery (photo/signature)
  - Two-way messaging, AI chat agent ("DT Agent")
  - Driver AI for turn-by-turn optimization
  - ERP/SAP, POS, telematics, WMS integrations
- **Pricing:**
  - Starts at ~$75/vehicle license/month
  - Contract-based pricing (not published)
  - Implementation, ERP integrations, custom workflows additional
- **Coverage:** Global, 50+ countries. Strong in North America, Latin America, Europe, India.
- **User Sentiment:**
  - Pros: 98% ETA accuracy, strong customer communication, high driver app adoption, good support, AI features differentiating [Source: G2, Capterra, TrustRadius]
  - Cons: Hard to navigate, lacks route customization, inaccurate maps with missing roads, outdated mobile app UI, slow data loading, heavy reliance on support [Source: G2, Capterra]
- **Best For:** Scheduled heavy-goods delivery (furniture, appliances)

---

## Routific

- **Category:** Route optimization engine (not full delivery management)
- **API Types:** REST
- **Base URL:** `https://api.routific.com`
- **API Version:** 1.11
- **Auth:** API Key (obtained via developer portal)
- **Docs:**
  - Developer Portal: https://dev.routific.com/ [Source: dev.routific.com]
  - API Documentation: https://docs.routific.com/ [Source: docs.routific.com]
  - API Reference: https://docs.routific.com/reference/api-reference [Source: docs.routific.com]
- **Key Endpoints:**
  - `/vrp` — Vehicle Routing Problem (basic optimization)
  - `/pdp` — Pickup & Delivery Problem (same-day P&D)
  - `/vrp-long` — Long-running VRP (60+ visits)
  - `/pdp-long` — Long-running PDP (60+ visits)
- **Features:**
  - Time-window and vehicle capacity constraints
  - Open-ended routes (no depot return)
  - Idle time minimization
  - Route recalculation and ETA computation
  - New order insertion into existing routes
  - Planning horizon up to 96 hours
  - Up to 10,000 stops per request
- **Capabilities:**
  - Route optimization (core strength — routes 15% shorter than open-source engines)
  - Basic delivery scheduling with time windows
  - Basic driver assignment
  - Customer notifications with ETAs
  - Proof of delivery (photo)
  - **No real-time GPS tracking** (only relays last delivery point)
  - **No automated dispatch**
  - **No returns handling**
- **Pricing:**
  - Free: 100 orders/month forever
  - 101-1,000 orders: $150/month flat
  - 1,001-2,000: $0.15/order
  - 2,001-5,000: $0.10/order
  - 5,001-10,000: $0.07/order
  - 10,001-20,000: $0.05/order
  - 20,000+: $0.03/order
  - 7-day free trial with 5,000 orders
- **User Sentiment:**
  - Pros: Extremely easy to use, routes 15% shorter than alternatives, very fast optimization (10K stops), excellent customer support, good value, free tier [Source: Capterra 98% satisfaction, G2]
  - Cons: No real-time vehicle tracking, cannot adjust ETAs live, missing delivery management features beyond routing, limited API for custom workflows [Source: Capterra, G2]
- **Best For:** Pure route optimization as a complement to other tools

---

## OptimoRoute

- **Category:** Route planning and field service optimization
- **API Types:** REST (WS API v1.33)
- **Base URL:** `https://api.optimoroute.com/v1/`
- **Auth:** API key as query parameter `key=AUTH_KEY` (generated in Administration > Settings > WS API)
- **Rate Limits:** Maximum 5 concurrent requests per account or IP address
- **Docs:**
  - API Documentation: https://optimoroute.com/api/ [Source: optimoroute.com]
  - Help Center: https://help.optimoroute.com/ [Source: help.optimoroute.com]
  - Integration Guide: https://help.optimoroute.com/hc/en-us/articles/27433896960276 [Source: help.optimoroute.com]
- **Key Endpoints:**
  - `/create_order` — single order create/update
  - `/create_or_update_orders` — bulk (up to 500)
  - `/get_orders`, `/delete_order`, `/search_orders` — CRUD
  - `/get_routes` — routes by date
  - `/start_planning`, `/stop_planning`, `/get_planning_status` — optimization control
  - `/update_driver_parameters` — driver settings
  - `/get_events` — mobile app events (up to 500/request)
  - `/get_completion_details`, `/update_order_completion` — completion data
  - `/update_drivers_positions` — bulk position updates
- **Error Codes:** `AUTH_KEY_MISSING`, `AUTH_KEY_UNKNOWN`, `MALFORMED_REQUEST`, `ERR_MISSING_MAND_FIELD`, `ERR_INVALID_PARAM_FORMAT`, `ERR_TOO_MANY_CONNECTIONS`, `ERR_INTERNAL`
- **Community Tools:** TypeScript client (rokala/optimoroute-client on GitHub), Pipedream integration
- **Capabilities:**
  - Route optimization for deliveries and field service
  - Delivery scheduling with time windows and priorities
  - Driver management with mobile app
  - Real-time order tracking, customer notifications
  - Proof of delivery (signature, photo, notes)
  - Multi-day/week planning for recurring routes
  - Workload balancing across drivers
- **Pricing:**
  - Lite: $35.10/driver/month (annual) or $39/month (monthly)
  - Pro: $44.10/driver/month (annual) or $49/month (monthly)
  - 30-day free trial
- **User Sentiment:**
  - Pros: Strong value for money, automatic planning cuts route planning time, responsive support, 30-day trial, flexible subscription [Source: G2 4.8/5, Capterra 4.5/5]
  - Cons: No live traffic data, advanced features missing from base plans, clunky interface, per-driver cost adds up, steep learning curve [Source: G2, Capterra]
- **Best For:** SMB route planning and field service

---

## Tookan (by Jungleworks)

- **Category:** Hyperlocal delivery management
- **API Types:** REST
- **Base URL:** `https://api.tookanapp.com` (v2: `https://api.tookanapp.com/v2`)
- **Auth:** API key from Tookan dashboard (all requests POST with JSON body)
- **Docs:**
  - API Documentation: https://tookanapi.docs.apiary.io/ [Source: tookanapi.docs.apiary.io]
  - Support KB: https://help.jungleworks.com/knowledge-base/tookans-api-documentation/ [Source: help.jungleworks.com]
  - General Docs: https://docs.jungleworks.com/ [Source: docs.jungleworks.com]
- **SDKs:** Tracking SDK for mobile app embedding
- **Webhooks:** Task status changes, agent alerts
- **Integrations:** Shopify, Zapier, Integrately, custom webhooks
- **Capabilities:**
  - Route optimization (basic), delivery scheduling, task assignment
  - Driver/agent management with mobile app
  - Real-time tracking with tracking SDK
  - Proof of delivery (photo, signature)
  - Customer notifications and tracking links
  - Geofencing and territory management
  - Pickup & Delivery workflow management
- **Pricing:**
  - Starts at ~$39/month, 14-day free trial
  - Task-based scaling
  - Part of Jungleworks suite (bundleable)
- **Coverage:** Global, strong in India, Southeast Asia, Middle East
- **User Sentiment:**
  - Pros: Clean UI, highly customizable, good real-time tracking, Shopify integration, affordable entry [Source: G2, Capterra]
  - Cons: **HIGH RISK** — customer support notoriously unresponsive, misleading feature claims (paying for features then told "not possible"), service non-delivery reported, no refunds even when product fails, software bugs and instability [Source: Trustpilot, PeerSpot, G2]
- **Best For:** Budget hyperlocal delivery (with significant risk accepted)

---

## GetSwift

- **Category:** Delivery logistics automation
- **API Types:** REST (V2)
- **Base URL:** `https://app.getswift.co/api/public/v2/`
- **Auth:** Merchant API key (passed in JSON body, keep server-side only)
- **Docs:**
  - API Documentation: https://app.getswift.co/apidocs/intro [Source: app.getswift.co]
  - Help Center: https://getswift.zendesk.com/ [Source: getswift.zendesk.com]
- **Webhooks:** Supported for delivery status updates
- **Integrations:** POS systems, e-commerce, online ordering platforms
- **Capabilities:**
  - Route optimization, delivery scheduling, dispatch
  - Driver management with assignment and tracking
  - Real-time tracking with tracking URLs for customers
  - Proof of delivery, customer notifications
  - Delivery quoting via API
  - Minimum required: only pickup and dropoff addresses
- **Pricing:**
  - Per-delivery: $0.29-$0.49 (varies)
  - Volume discounts available
  - No upfront subscription required
- **Coverage:** Global (Australian company)
- **User Sentiment:**
  - Pros: Real-time tracking, easy dispatch/routing, route optimization, scales with growth, simple API, accessible per-delivery pricing [Source: Capterra, Software Advice]
  - Cons: Notification problems, hidden delivery fees, missing key functions (barcode, inventory), system becoming unusable with continued billing, service quality declined after ASX listing [Source: TrustRadius, Capterra]
- **Best For:** Simple per-delivery tracking for small operations (with stability risk)

---

## Comparison Matrix

| Platform | Best For | API Quality | Pricing Model | Risk Level |
|---|---|---|---|---|
| **Bringg** | Enterprise multi-carrier | Excellent (REST, OAuth, 4 SDKs) | Custom ($10K-$1M+/yr) | Low |
| **Onfleet** | Mid-market delivery mgmt | Very Good (REST, Basic Auth, SDKs) | Per-task ($599-$2,999/mo) | Low |
| **DispatchTrack** | Scheduled heavy-goods | Good (REST, multiple portals) | Per-vehicle (~$75+/mo) | Low |
| **Routific** | Pure route optimization | Good (REST, clean) | Per-order ($0.03-$0.15) | Low |
| **OptimoRoute** | SMB route planning | Good (REST, documented) | Per-driver ($35-$49/mo) | Low |
| **Tookan** | Budget hyperlocal | Fair (REST, scattered) | Task-based (~$39/mo+) | **HIGH** |
| **GetSwift** | Simple per-delivery | Fair (REST V2) | Per-delivery ($0.29-$0.49) | **MEDIUM** |

## Integration Recommendations

- **Bringg** and **Onfleet** have the most mature, well-documented APIs with official SDKs. Bringg is enterprise-only; Onfleet is more accessible.
- **Routific** and **OptimoRoute** are route optimization focused — not full delivery management. Good APIs but narrower scope.
- **DispatchTrack** has multiple API portals but documentation is gated and less developer-friendly.
- **Tookan** is highest risk despite low pricing — customer support and reliability widely criticized.
- **GetSwift** is simple and affordable but has stability concerns.

## Sources

- Bringg Developer Portal: https://developers.bringg.com/
- Bringg API Reference: https://developers.bringg.com/reference/welcome-to-bringgs-api-reference
- Bringg Help Center: https://help.bringg.com/
- Onfleet Developer Hub: https://docs.onfleet.com/
- Onfleet API Reference: https://docs.onfleet.com/reference/introduction
- Onfleet Support: https://support.onfleet.com/
- Onfleet Node SDK: https://github.com/onfleet/node-onfleet
- Onfleet Python SDK: https://github.com/onfleet/pyonfleet
- DispatchTrack Last Mile API: https://apidocs-lastmile.dispatchtrack.com/
- DispatchTrack Planner API: https://apidocs-planner.dispatchtrack.com/
- DispatchTrack Webhooks: https://webhooks-lastmile.dispatchtrack.com/
- DispatchTrack Support: https://www.dispatchtrack.com/company/support
- Routific Developer Portal: https://dev.routific.com/
- Routific API Docs: https://docs.routific.com/
- OptimoRoute API: https://optimoroute.com/api/
- OptimoRoute Help: https://help.optimoroute.com/
- Tookan API: https://tookanapi.docs.apiary.io/
- Jungleworks Support: https://help.jungleworks.com/
- GetSwift API: https://app.getswift.co/apidocs/intro
- GetSwift Help: https://getswift.zendesk.com/
- G2, Capterra, TrustRadius, Trustpilot reviews for all platforms
- Reddit r/ecommerce, r/supplychain discussions
