# Carrier Aggregator / Multi-Carrier Shipping Platforms

Research date: 2026-03-31

## EasyPost

- **Category:** Developer-first shipping API aggregator
- **API Types:** REST
- **Auth:** API key (HTTP header), separate test/production keys
- **Docs:**
  - API Docs: https://docs.easypost.com/
  - Getting Started: https://www.easypost.com/getting-started
  - Tracking API: https://www.easypost.com/tracking-api/
  - GitHub: https://github.com/EasyPost
- **SDKs:** Ruby, Python, PHP, Java, Node.js, C#, Go (7 languages, monthly updates)
- **Webhooks:** Supported for tracking updates and shipment events
- **Capabilities:**
  - Multi-carrier rate shopping, label generation/purchasing
  - Package tracking with webhooks
  - Address verification
  - Shipping insurance (1% of shipment value, $0.65 minimum)
  - Returns management, customs forms
  - SmartRate API: ML-powered delivery date predictions using historical carrier data
  - Carbon offset API
  - EasyPost Forge: white-label shipping solutions ($390/month)
- **Carrier Support:**
  - Wallet Carriers (built-in): USPS, UPS, FedEx, DHL eCommerce, DHL Express, Canada Post, Asendia
  - BYOCA (Bring Your Own Carrier Account): 100+ carriers
- **Pricing:**
  - Free tier: 3,000 labels/month, then $0.08/label
  - Developer Plan: 120,000 free labels/year
  - BYOCA: $20/month + $0.08/label
  - Tracking API: $0.01-$0.02/shipment
  - Enterprise: custom pricing
- **User Sentiment:**
  - Pros: Excellent API docs, fast integration, generous free tier, strong SDK support, SmartRate predictions
  - Cons: Customer support widely criticized (Trustpilot 1.7/5), billing disputes, "one-call buy" returns dummy 1-cent rate (confusing), managing multiple accounts for same carrier is awkward
- **Best For:** Mid-volume developers needing API-first shipping

---

## Shippo

- **Category:** Multi-carrier shipping API + web dashboard
- **API Types:** REST
- **Auth:** API token via `ShippoToken` HTTP header, separate live/test tokens
- **Docs:**
  - API Docs: https://docs.goshippo.com/
  - Quickstart: https://docs.goshippo.com/docs/guides_general/api_quickstart
  - Auth: https://docs.goshippo.com/docs/guides_general/authentication
  - Webhooks: https://docs.goshippo.com/docs/tracking/webhooks
  - Webhook Security (HMAC): https://docs.goshippo.com/docs/tracking/webhooksecurity/
  - Carrier Capabilities: https://docs.goshippo.com/docs/carriers/carriercapabilities/
  - Postman Collection: https://www.postman.com/shippo/shippo-docs/documentation/8hcj187/shippo-api
- **SDKs:** Ruby, Python, PHP, Java, Node.js, C# (+ community Perl and Go)
- **Webhooks:** Supported with HMAC security or query parameter token
- **Capabilities:**
  - Rate comparison across 40+ carriers
  - Label generation, package tracking
  - Address validation, returns label creation
  - Customs/international docs, batch shipping
  - Pickup scheduling, branded tracking pages
- **Carrier Support:** 40+ carriers built-in: USPS, FedEx, UPS, DHL Express/eCommerce, Canada Post, Australia Post, Royal Mail, Deutsche Post, Purolator, OnTrac, LSO, Better Trucks, Veho, Sendle, Aramex, DPD, GLS, and more
- **Pricing:**
  - Starter (Free): Up to 30 labels/month
  - Pro: Starting at $19/month (scales with volume)
  - Per-label surcharge: $0.05/label for BYOCA (waived for Shippo default carriers)
  - 30-day free trial of Pro
- **User Sentiment:**
  - Pros: Very user-friendly, excellent for SMBs, good Shopify/Etsy/eBay integrations, competitive default rates, strong international carrier support, fast integration (4-6 hours)
  - Cons: $0.05/label BYOCA surcharge, free tier very limited (30 labels), no LTL/freight, some carrier-specific features hidden by abstraction
- **Best For:** SMBs needing both dashboard and API, international shipping

---

## ShipEngine (ShipStation API)

- **Category:** Developer-first headless shipping API (rebranded to ShipStation API Feb 2025)
- **API Types:** REST (OpenAPI 3.0 spec)
- **Auth:** API key via `API-Key` HTTP header, `TEST_` prefix for sandbox keys
- **Docs:**
  - Developer Portal: https://www.shipengine.com/docs/
  - API Reference (OpenAPI 3.0): https://shipengine.github.io/shipengine-openapi/
  - Getting Started: https://www.shipengine.com/docs/getting-started/
  - Rates: https://www.shipengine.com/docs/rates/
  - Rate Limits: https://www.shipengine.com/docs/rate-limits/
  - Auth: https://www.shipengine.com/docs/auth/
  - ShipEngine Connect: https://connect.shipengine.com/
- **SDKs:** JavaScript, PHP, Python, Ruby, C#, Java (all on GitHub)
- **Capabilities:**
  - Label creation, rate shopping, address validation
  - Package tracking, batch labels, return labels
  - Manifests, PUDO (Pick-Up/Drop-Off) location search
  - Tax/duty calculations for international
  - ShipEngine Connect: build custom carrier/marketplace integrations
  - White-label shipping enablement for platforms
  - LTL (Less-Than-Truckload) freight support
- **Carrier Support:** 100+ carriers globally, LTL freight carriers, programmatic account connection
- **Pricing:**
  - Free: Sandbox access, discounted rates via ShipStation carrier accounts only (no BYOCA)
  - Advanced 1K: $75/month (1,000 labels, $0.075/additional)
  - Advanced 5K: $325/month (5,000 labels, $0.065/additional)
  - Advanced 10K: $600/month (10,000 labels, $0.060/additional)
  - Enterprise: Custom (25,000+ shipments/month)
- **User Sentiment:**
  - Pros: Best-in-class developer experience, excellent OpenAPI spec, sandbox environment, white-label enablement, LTL freight support, very scalable
  - Cons: Confusing branding transition, paid plans expensive ($75/month minimum for BYOCA), carrier rate adjustments post-purchase if dimensions inaccurate
- **Best For:** SaaS platforms and marketplaces embedding shipping as a feature

---

## ShipStation

- **Category:** Cloud-based shipping management software (GUI-first with API add-on)
- **API Types:** REST (V1 legacy + V2 newer)
- **Auth:** V1: Basic auth (API Key + Secret); V2: API key
- **Docs:**
  - V2 API Docs: https://docs.shipstation.com/
  - V1 API Docs: https://www.shipstation.com/docs/api/
  - General Docs: https://www.shipstation.com/documentation/
  - Help Center: https://help.shipstation.com/
- **Capabilities:**
  - Order management from 300+ integrations (Shopify, Amazon, eBay, Walmart, Etsy, BigCommerce, WooCommerce)
  - Batch label printing, rate shopping
  - Automated shipping rules (rule-based carrier selection)
  - Branded tracking pages, returns portal
  - Inventory management, multi-user/multi-warehouse
- **Carrier Support:** USPS, UPS, FedEx, DHL, GlobalPost + BYOCA. 300+ platform integrations.
- **Pricing:**
  - Free: Very limited, chatbot support only
  - Starter: $14.99/month
  - Standard: $29.99/month (phone support)
  - Premium: $349.99/month (dedicated account management)
  - API access requires higher-tier plans
  - Postage/insurance costs separate
- **User Sentiment:**
  - Pros: Excellent UI, massive integration ecosystem, automation rules, multi-channel order management, branded tracking/returns
  - Cons: API access gated behind higher plans, V2 API still in early release, recent pricing changes frustrating, not developer-first
  - G2: ~4.3/5, Capterra: ~4.6/5
- **Best For:** Non-technical multi-channel sellers

---

## Pirate Ship

- **Category:** Free shipping label platform (GUI only, NO API)
- **API Types:** None (no public API)
- **Auth:** N/A (email/password login)
- **Docs:** No developer documentation. Unofficial community API wrapper on GitHub (not supported).
- **Capabilities:**
  - Label purchase/printing for USPS and UPS only
  - Rate comparison (USPS vs UPS)
  - Batch label creation, package tracking
  - CSV upload or platform import (Shopify, Etsy, eBay, Amazon, WooCommerce, Squarespace)
  - Access to Priority Mail Cubic pricing (normally requires high-volume USPS agreement)
- **Carrier Support:** USPS and UPS only. No FedEx, DHL, or regional carriers.
- **Pricing:**
  - Platform fee: FREE (zero subscription, zero per-label, zero markup)
  - You pay only actual postage at deeply discounted commercial rates
  - Revenue model: commission from carriers based on volume
  - Savings: up to 89% off USPS retail, up to 81% off UPS retail
- **User Sentiment:**
  - Pros: Completely free, deepest USPS discounts available, Priority Mail Cubic access for everyone, extremely easy to use, strong Reddit community
  - Cons: Only USPS + UPS, no API, no automation, no branded tracking, no returns portal, scalability ceiling ~200-500 shipments/month, limited international support
- **Best For:** Small/hobby sellers wanting cheapest rates with zero fees

---

## Comparison Matrix

| Feature | EasyPost | Shippo | ShipEngine | ShipStation | Pirate Ship |
|---|---|---|---|---|---|
| **Primary Mode** | API-only | API + Dashboard | API-only | Dashboard + API | Dashboard only |
| **Free Tier** | 3,000 labels/mo | 30 labels/mo | Sandbox only | Very limited | Unlimited |
| **Carriers** | 100+ (BYOCA) | 40+ built-in | 100+ (BYOCA) | Major + BYOCA | USPS + UPS |
| **SDKs** | 7 languages | 6 + community | 6 languages | Limited | None |
| **Per-Label Cost** | $0.08 (after free) | $0.05 (BYOCA) | $0.06-$0.075 | Plan-based | $0 |
| **Entry Price** | Free | Free | Free (limited) | $14.99/mo | Free |
| **LTL/Freight** | No | No | Yes | No | No |
| **White-Label** | Yes (Forge) | No | Yes (Connect) | No | No |
| **Best For** | Mid-volume devs | SMB + devs | Platforms/SaaS | Multi-channel sellers | Small sellers |

## Integration Recommendations

- **Building a SaaS/marketplace with embedded shipping:** ShipEngine (ShipStation API)
- **Developer integrating shipping into an app:** EasyPost (best free tier + docs) or Shippo (fastest integration)
- **Non-technical multi-channel seller:** ShipStation
- **Small seller wanting cheapest rates:** Pirate Ship
- **International shipping needs:** Shippo (broadest built-in carrier coverage) or EasyPost (with BYOCA)

## Sources

- EasyPost API Docs: https://docs.easypost.com/
- EasyPost Getting Started: https://www.easypost.com/getting-started
- EasyPost Tracking API: https://www.easypost.com/tracking-api/
- EasyPost GitHub: https://github.com/EasyPost
- EasyPost Trustpilot reviews: https://www.trustpilot.com/review/easypost.com
- Shippo API Docs: https://docs.goshippo.com/
- Shippo Quickstart: https://docs.goshippo.com/docs/guides_general/api_quickstart
- Shippo Auth: https://docs.goshippo.com/docs/guides_general/authentication
- Shippo Webhooks: https://docs.goshippo.com/docs/tracking/webhooks
- Shippo Carrier Capabilities: https://docs.goshippo.com/docs/carriers/carriercapabilities/
- Shippo Postman Collection: https://www.postman.com/shippo/shippo-docs/documentation/8hcj187/shippo-api
- ShipEngine Developer Portal: https://www.shipengine.com/docs/
- ShipEngine OpenAPI: https://shipengine.github.io/shipengine-openapi/
- ShipEngine Connect: https://connect.shipengine.com/
- ShipStation V2 API: https://docs.shipstation.com/
- ShipStation V1 API: https://www.shipstation.com/docs/api/
- ShipStation Help: https://help.shipstation.com/
- Pirate Ship Support: https://support.pirateship.com/
- Pirate Ship community API wrapper: https://github.com/taciturnaxolotl/pirateship-api
- G2, Capterra, TrustRadius, Trustpilot reviews for all platforms
- Reddit r/ecommerce, r/smallbusiness, r/Etsy, r/Flipping discussions
