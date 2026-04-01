# Major Carrier APIs (FedEx, UPS, USPS, DHL)

Research date: 2026-03-31

## FedEx APIs

- **Category:** Full-service parcel, express, and freight carrier
- **API Types:** REST (JSON). Legacy SOAP/XML sunset: March 31, 2026 (providers), June 1, 2026 (customers).
- **Auth:** OAuth 2.0 Client Credentials (API Key + Secret Key + Account Number). Tokens valid 3,600s (1 hour).
- **Developer Portal:** https://developer.fedex.com
- **Docs:**
  - Ship API: https://developer.fedex.com/api/en-us/catalog/ship/docs.html [Source: developer.fedex.com]
  - Rate API: https://developer.fedex.com/api/en-us/catalog/rate.html [Source: developer.fedex.com]
  - Track API: https://developer.fedex.com/api/en-us/catalog/track.html [Source: developer.fedex.com]
  - Address Validation: https://developer.fedex.com/api/en-us/catalog/address-validation.html [Source: developer.fedex.com]
- **SDKs:** Sample code in multiple languages; no official SDK packages
- **Sandbox:** Available without FedEx account
- **Webhooks:** Track API supports webhook push notifications (HTTPS POST, JSON, signature verification, retry)
- **APIs Available:**
  - Ship API — labels (PDF, PNG, ZPL, EPL, DPL), multi-piece, returns
  - Rate API — account-specific or list rates, surcharge breakdowns, transit estimates
  - Track API — real-time status, scanning events, proof of delivery, webhooks
  - Address Validation API — validates/corrects, residential vs. business classification
  - Pickup API — schedule/cancel pickups
  - Service Availability API — available services for origin/destination
  - Ground End of Day API — batch close-out
  - Document API — customs documentation
  - Location API — nearby FedEx facilities
  - Freight LTL API — less-than-truckload freight
- **Rate Limits:**
  - Rate/Ship/Track/Address: 10 req/sec, 10,000/day
  - OAuth Token: 5 req/sec, 1,000/day
  - Overall per project: 1,400 transactions/10 seconds
  - Higher volumes: 1-2 week approval
- **Pricing:** API access free. Standard FedEx shipping rates apply. No per-label API surcharge.
- **Coverage:**
  - Domestic: Ground (1-7 days), Home Delivery, Express Saver, 2Day, Standard Overnight (3 PM), Priority Overnight (10:30 AM), First Overnight (8-9:30 AM)
  - International: 220+ countries. International Priority/Economy/First/Ground (US-Canada)
  - Freight: LTL freight services
- **User Sentiment:**
  - Pros: Modern REST API, comprehensive webhook tracking, sandbox without account, wide service portfolio, no API fees [Source: developer.fedex.com, Reddit r/ecommerce]
  - Cons: Ship API requires certification before production, sandbox doesn't simulate real validation failures, multi-piece requires careful masterTrackingId management, SOAP→REST migration was painful [Source: Reddit r/ecommerce, atoship.com]
- **Gotchas:**
  - Token management critical (401 → immediate refresh)
  - Sandbox vs. production behavior differs for address validation
  - Won't report errors like wrong origin ZIP if no insurance set

---

## UPS APIs

- **Category:** Full-service parcel, express, and freight carrier
- **API Types:** REST (JSON) with OAuth 2.0. Legacy XML APIs sunset summer 2025.
- **Auth:** OAuth 2.0 Client Credentials. Tokens valid ~4 hours (14,399s). **Critical: only ~250 token requests/day — caching mandatory.**
- **Developer Portal:** https://developer.ups.com
- **Docs:**
  - API Reference: https://developer.ups.com/api/reference [Source: developer.ups.com]
  - Postman Collections: https://www.postman.com/ups-api/ups-apis/ [Source: postman.com]
- **SDKs:** "UPS Developer Kit" referenced; no official SDK packages. Raw HTTP examples provided.
- **Sandbox:** Separate base URL (`https://wwwcie.ups.com`)
- **Webhooks:** Quantum View platform — push notifications for Manifest, Origin Scan, In Transit, Out for Delivery, Delivered, Exception. Requires UPS account representative to enable. Endpoints must respond 200 within 10 seconds.
- **APIs Available:**
  - Shipping API (`/api/shipments/v2409/ship`) — create shipments, labels, returns
  - Rating API (`/api/rating/v2403/rate`) — rates and transit times
  - Tracking API (`/api/track/v1/details`) — package tracking
  - Address Validation (`/api/addressvalidation/v2/validate`)
  - Time in Transit API — estimated delivery dates
  - Locator API — UPS facilities and Access Points
  - Pickup API — schedule pickups
  - Void API (`/api/shipments/v2409/void/cancel`) — cancel/void labels
  - Paperless Document API — electronic customs docs
  - Dangerous Goods API — hazmat compliance
  - Quantum View — shipment event visibility/notification
- **Rate Limits:**
  - OAuth: ~250/day (caching mandatory)
  - Rating: 1,000/minute
  - Shipping: 500/minute
  - Tracking: 500/minute
  - Address Validation: 1,000/minute
- **Pricing:** Tracking API free to license. API access generally free. Standard UPS shipping rates. No per-label surcharge.
- **Coverage:**
  - Domestic: Next Day Air (1 day), Next Day Air Saver, Next Day Air Early AM, 2nd Day Air, 3 Day Select, Ground (1-5 days)
  - International: 220+ countries. Worldwide Express/Saver/Expedited, Standard to Canada/Mexico
  - Access Points: extensive drop-off/pickup network
- **User Sentiment:**
  - Pros: Comprehensive API suite, OpenAPI/Swagger + Postman collections, enterprise reliability, good rate limits (500-1,000/min) [Source: developer.ups.com, postman.com]
  - Cons: Documentation quality widely criticized ("worst documented API from a corporate" — DevRant), 250 token/day limit catches developers, Quantum View webhooks not self-service, SOAP→REST migration painful [Source: devrant.com/rants/2195628, Reddit]
- **Gotchas:**
  - 250 token requests/day will break apps that don't cache tokens
  - Webhook endpoints must respond within 10 seconds or events drop
  - Must handle duplicate webhook events idempotently

---

## USPS APIs

- **Category:** Government postal service, lowest-cost domestic carrier
- **API Types:** REST (JSON), v3 APIs current. Legacy Web Tools (XML v1/v2) **retired January 25, 2026**.
- **Auth:** OAuth 2.0 (Consumer Key + Consumer Secret → Bearer Token). **API Access Control initiative launching April 2026.**
- **Developer Portal:** https://developers.usps.com
- **Docs:**
  - API Catalog: https://developers.usps.com/apis [Source: developers.usps.com]
  - OAuth: https://developers.usps.com/Oauth [Source: developers.usps.com]
  - GitHub Examples: https://github.com/USPS/api-examples [Source: github.com/USPS]
- **SDKs:** No official SDKs. Postman collections and curl examples provided.
- **Sandbox:** TEM (Testing Environment for Mailers) at `apis-tem.usps.com` — uses production credentials, different base URL
- **Webhooks:** Not available. Tracking is polling-only.
- **APIs Available:**
  - Domestic Labels 3.0 — shipping labels with postage
  - International Labels 3.0 — international labels with customs
  - Domestic Prices 3.0 / International Prices 3.0 — pricing
  - Addresses 3.0 — validate/correct, city/state lookup, ZIP validation
  - Tracking 3.0 — package tracking and delivery status
  - Carrier Pickup 3.0 — schedule free carrier pickups
  - Service Standards 3.0 — expected delivery timeframes
  - Adjustments 3.0 — shipping charge adjustments
  - Disputes 3.0 — submit pricing disputes
  - Containers 3.0 — Intelligent Mail Container barcodes
  - Locations 3.0 — find USPS facilities
  - Informed Delivery Campaigns — interactive mail/package campaigns
- **Rate Limits:** Not publicly documented
- **Pricing:** **Completely free** — all APIs free for registered developers. No per-call charges, no per-label API fees. Standard USPS postage rates (typically lowest among major carriers).
- **Coverage:**
  - Domestic: Priority Mail Express (overnight/2-day guaranteed), Priority Mail (1-3 days), USPS Ground Advantage (2-5 days), First-Class Package (2-5 days, <13 oz), Media Mail, Library Mail
  - International: 190+ countries. Global Express Guaranteed, Priority Mail Express International, Priority Mail International, First-Class Package International
  - Every U.S. address is a delivery point (universal coverage)
- **User Sentiment:**
  - Pros: Completely free API, lowest postage rates, free carrier pickup, universal US coverage, new v3 APIs are modern REST/JSON, GitHub examples [Source: developers.usps.com, lob.com/blog]
  - Cons: Documentation historically poor (PDFs only), no official SDKs, no webhook/push tracking (polling only), rate limits undocumented, technology lags private carriers, no guaranteed delivery for most services, limited international competitiveness [Source: Reddit r/ecommerce, lob.com/blog]
- **Gotchas:**
  - v1/v2 Web Tools APIs dead as of January 2026
  - April 2026 Access Control initiative may require further changes
  - No sandbox with test data; TEM uses production-like data
  - Address validation US-only

---

## DHL APIs

- **Category:** International express, e-commerce, and freight carrier
- **API Types:** REST (JSON) primary. SOAP/XML still available for MyDHL API (legacy).
- **Auth:** Varies by division:
  - DHL Express (MyDHL API): Basic Auth (`Authorization: Basic [Base64(APIKEY:APISECRET)]`)
  - DHL Freight: Dedicated Authentication API
  - Post & Parcel Germany: OAuth-based
  - DHL eCommerce v4: OAuth 2.0
- **Developer Portal:** https://developer.dhl.com
- **Docs:**
  - API Catalog: https://developer.dhl.com/api-catalog [Source: developer.dhl.com]
  - MyDHL API (Express): https://developer.dhl.com/api-reference/mydhl-api-dhl-express [Source: developer.dhl.com]
  - Tracking Unified Push: https://developer.dhl.com/api-reference/shipment-tracking-unified-push [Source: developer.dhl.com]
  - eCommerce Americas: https://docs.api.dhlecs.com/ [Source: docs.api.dhlecs.com]
- **SDKs:** No official SDKs. Active GitHub community (github.com/topics/dhl-api).
- **Sandbox:** 500 invocations/day. Not all APIs provide sandbox.
- **Webhooks:** Shipment Tracking Unified Push API — proactive push notifications across ALL DHL divisions
- **APIs Available:**
  - **DHL Express (MyDHL API):** Shipment creation, labels, rate quoting, transit times, service availability, courier pickup, tracking, customs docs
  - **DHL eCommerce:** eConnect (Europe), eCommerce Americas v4, eCommerce UK — parcel shipping, cross-border, labels, track & trace, returns, duty/tax
  - **Tracking:** Shipment Tracking Unified — status across ALL DHL types (single API); Push variant for webhooks
  - **Location Finder Unified** — search DHL locations globally
  - **Deutsche Post International** — international mail/merchandise labels
  - **DHL Freight APIs** — LTL freight with price quotes
  - **Landed Cost API** — duty and tax calculations (PAID)
- **Rate Limits:** Test: 500/day. Production: varies by API (calls/day and calls/second).
- **Pricing:** Developer portal free. All APIs free except Landed Cost. Standard DHL shipping rates. No per-label surcharge.
- **Coverage:**
  - **International leader:** 220+ countries (every UN-recognized nation)
  - Express: Next-day/2-day for major markets (Worldwide, Express 12:00, Express 9:00)
  - eCommerce Europe: 1-3 day transit within Europe
  - eCommerce Americas: cost-effective international for lightweight packages
  - Freight: full LTL across Europe
  - **No US domestic service** — not viable for US-to-US shipping
- **User Sentiment:**
  - Pros: Best international coverage, unified tracking API across all divisions, push tracking webhooks, free API access, comprehensive duty/tax calculation, well-documented portal (DevPortal Awards nomination 2024) [Source: developer.dhl.com, onextstudio.com]
  - Cons: No US domestic service, inconsistent auth across divisions (Basic Auth vs OAuth), not all APIs have sandbox, eCommerce v4 missing features (no COD, limited insurance), fragmented API landscape across divisions [Source: onextstudio.com, Reddit]
- **Gotchas:**
  - Fragmented API landscape means potentially integrating with multiple APIs
  - Basic Auth on Express API (not OAuth) is less secure
  - 500/day test limit is restrictive
  - February 2026: UTAPI service `post_de` replaced by `svb`

---

## Cross-Carrier Comparison

| Feature | FedEx | UPS | USPS | DHL |
|---------|-------|-----|------|-----|
| **API Type** | REST (OAuth 2.0) | REST (OAuth 2.0) | REST (OAuth 2.0) | REST (Mixed Auth) |
| **API Cost** | Free | Free | Free | Free (except Landed Cost) |
| **Webhooks** | Yes (Track API) | Yes (Quantum View) | No (polling only) | Yes (Unified Push) |
| **Sandbox** | Yes (no account) | Yes (separate URL) | TEM (prod creds) | Partial (500/day) |
| **US Domestic** | Strong | Strong | Best coverage/price | Not available |
| **International** | 220+ countries | 220+ countries | 190+ countries | 220+ countries (strongest) |
| **Documentation** | Good (modern) | Historically poor, improving | Historically poor, improving v3 | Good (award-nominated) |
| **Official SDKs** | Sample code only | Dev Kit (no packages) | Postman/curl only | Community libraries |
| **Best For** | US domestic + intl express | US domestic + enterprise | US domestic budget | International eCommerce |

## Key Recommendation for Omnifill

All four carriers are converging on REST + OAuth 2.0. The major differences for an abstraction layer:
- DHL Express still uses Basic Auth (not OAuth)
- USPS lacks webhook support for tracking (polling only)
- UPS has restrictive token rate limits (250/day — must cache aggressively)
- FedEx sandbox behavior differs from production for address validation

## Sources

- FedEx Developer Portal: https://developer.fedex.com
- FedEx Ship API Docs: https://developer.fedex.com/api/en-us/catalog/ship/docs.html
- FedEx Rate API: https://developer.fedex.com/api/en-us/catalog/rate.html
- FedEx Shipping API Guide (atoship): https://atoship.com/blog/fedex-shipping-api-developer-tools-guide
- UPS Developer Portal: https://developer.ups.com/api/reference
- UPS Shipping API Guide (atoship): https://atoship.com/blog/ups-shipping-api-integration-developer-guide
- UPS APIs on Postman: https://www.postman.com/ups-api/ups-apis/overview
- UPS DevRant Review: https://devrant.com/rants/2195628
- Carrier API Changes 2026 (ShipperHQ): https://blog.shipperhq.com/2025/12/carrier-api-changes-2026/
- USPS Developer Portal: https://developers.usps.com/
- USPS API Catalog: https://developers.usps.com/apis
- USPS OAuth 2.0: https://developers.usps.com/Oauth
- USPS API Retirement Notice: https://developers.usps.com/industry-alert-api-retirement
- USPS GitHub Examples: https://github.com/USPS/api-examples
- USPS API Modernization (Lob): https://www.lob.com/blog/usps-web-tools-developer-experience
- DHL Developer Portal: https://developer.dhl.com/
- DHL API Catalog: https://developer.dhl.com/api-catalog
- MyDHL API (Express): https://developer.dhl.com/api-reference/mydhl-api-dhl-express
- DHL Tracking Unified Push: https://developer.dhl.com/api-reference/shipment-tracking-unified-push
- DHL eCommerce Americas: https://docs.api.dhlecs.com/
- DHL eCommerce v4 Pros/Cons: https://onextstudio.com/insights/dhl-ecommerce-api-v4/
- DHL API Pricing FAQ: https://support-developer.dhl.com/support/solutions/articles/47001175782
- Multi-Carrier Shipping APIs 2025: https://elextensions.com/best-multi-carrier-shipping-api-developers/
- Shipping Rate Comparison (Shippo): https://goshippo.com/blog/ups-vs-fedex-vs-dhl-vs-usps-international-shipping-rates-comparison
- 10 Shipping APIs 2026 (Unified.to): https://unified.to/blog/10_shipping_apis_to_integrate_with_in_2026
