# Last Mile Delivery SaaS Research Index

Research date: 2026-03-31

Comprehensive research on 26 systems across the last-mile delivery landscape, organized into 5 categories. Each file contains per-system details on capabilities, APIs, authentication, pricing, user sentiment, and integration recommendations.

## Files

| File | Systems Covered | Count |
|------|----------------|-------|
| [major-carriers.md](major-carriers.md) | FedEx, UPS, USPS, DHL | 4 |
| [delivery-platforms.md](delivery-platforms.md) | Bringg, Onfleet, DispatchTrack, Routific, OptimoRoute, Tookan, GetSwift | 7 |
| [enterprise-platforms.md](enterprise-platforms.md) | Shipsy, FarEye, Locus, Circuit/Spoke | 4 |
| [crowdsourced-delivery.md](crowdsourced-delivery.md) | Roadie, GoShare, Veho, Pandion (defunct), Dolly | 5 |
| [carrier-aggregators.md](carrier-aggregators.md) | EasyPost, Shippo, ShipEngine, ShipStation, Pirate Ship | 5 |

**Total: 25 systems** (26 researched, Pandion shut down January 2025)

## Category Overview

### 1. Major Carrier APIs (4 systems)
Direct APIs from the Big 4 carriers. All converging on REST + OAuth 2.0. Free API access, pay standard shipping rates.

| Carrier | Webhooks | US Domestic | International | Best For |
|---------|----------|-------------|---------------|----------|
| FedEx | Yes | Strong | 220+ countries | US domestic + intl express |
| UPS | Yes (Quantum View) | Strong | 220+ countries | US domestic + enterprise |
| USPS | No (polling only) | Best price/coverage | 190+ countries | US domestic budget |
| DHL | Yes (Unified Push) | Not available | 220+ (strongest) | International eCommerce |

**Key integration note:** DHL Express uses Basic Auth (not OAuth), USPS lacks webhooks, UPS has 250 token requests/day limit (cache aggressively).

### 2. Delivery Management Platforms (7 systems)
Route optimization, dispatch, driver management, and delivery tracking.

| Platform | API Quality | Price Range | Risk | Best For |
|----------|------------|-------------|------|----------|
| Bringg | Excellent | $10K-$1M+/yr | Low | Enterprise multi-carrier orchestration |
| Onfleet | Very Good | $599-$2,999/mo | Low | Mid-market delivery management |
| DispatchTrack | Good | ~$75+/vehicle/mo | Low | Scheduled heavy-goods delivery |
| Routific | Good | $0.03-$0.15/order | Low | Pure route optimization |
| OptimoRoute | Good | $35-$49/driver/mo | Low | SMB route planning |
| Tookan | Fair | ~$39/mo+ | **HIGH** | Budget hyperlocal (risky) |
| GetSwift | Fair | $0.29-$0.49/delivery | **MEDIUM** | Simple per-delivery tracking |

### 3. Enterprise Delivery Platforms (4 systems)
India-founded platforms with strong APAC presence, targeting Fortune 500.

| Platform | API Access | Dev Experience | Clients |
|----------|-----------|----------------|---------|
| Shipsy | Gated (playground exists) | Poor | Coca Cola, UPS, Kuehne Nagel |
| FarEye | Fully gated | Poor | DHL, Walmart, Hilti, Amway |
| Locus | Gated (SwaggerUI docs) | Moderate | Unilever, Nestle, BlueDart |
| Circuit/Spoke | Public (v0.2b beta) | Best | SMB-focused |

### 4. Crowdsourced & Specialty Delivery (5 systems)
Gig-economy and alternative delivery models.

| Platform | Status | Niche | Coverage | API Access |
|----------|--------|-------|----------|------------|
| Roadie (UPS) | Active | Same-day, any size | 97% US | Sales-gated |
| GoShare | Active | Large/bulky, moving | Nationwide US | Sales-gated |
| Veho | Active | E-commerce parcels | 60 metros | Public (Stoplight) |
| Pandion | **SHUT DOWN** | Was e-commerce parcels | N/A | N/A |
| Dolly (Taskrabbit) | Active | Furniture/appliance | 48 cities | Public (OAuth 2.0) |

**Warning:** Pandion's failure (Jan 2025, after raising $125M) highlights risks of VC-funded alternative carriers.

### 5. Carrier Aggregators (5 systems)
Multi-carrier shipping APIs for rate shopping, label generation, and tracking.

| Platform | Mode | Free Tier | Carriers | Best For |
|----------|------|-----------|----------|----------|
| EasyPost | API-only | 3,000 labels/mo | 100+ (BYOCA) | Mid-volume developers |
| Shippo | API + Dashboard | 30 labels/mo | 40+ built-in | SMB + developers |
| ShipEngine | API-only | Sandbox only | 100+ (BYOCA) | SaaS platforms |
| ShipStation | Dashboard + API | Very limited | Major + BYOCA | Multi-channel sellers |
| Pirate Ship | Dashboard only | Unlimited | USPS + UPS only | Small sellers (free) |

## Cross-Category Integration Architecture

For building a unified delivery orchestration layer, the recommended approach:

### Tier 1: Must-Integrate (highest value, best APIs)
- **EasyPost or Shippo** — carrier aggregation layer (covers FedEx/UPS/USPS/DHL + 40-100 more)
- **Onfleet** — delivery management with strong API/webhooks
- **Routific** — pure route optimization engine

### Tier 2: Enterprise Value-Add
- **Bringg** — enterprise delivery orchestration (250+ carriers)
- **Locus** — best-documented enterprise platform (OpenAPI 2.0)
- **FarEye** — carrier orchestration at Fortune 500 scale

### Tier 3: Specialty/Niche
- **Roadie** — crowdsourced same-day/bulky items
- **Dolly** — furniture/appliance white-glove delivery
- **Veho** — alternative parcel delivery (monitor reliability)
- **Circuit/Spoke** — SMB route planning

### Tier 4: Direct Carrier APIs (when aggregator doesn't suffice)
- **FedEx** — best sandbox, modern REST
- **UPS** — enterprise reliability (cache tokens!)
- **USPS** — cheapest rates, universal US coverage
- **DHL** — international leader (best push tracking)

## Key Findings

1. **Carrier aggregators (EasyPost, Shippo, ShipEngine) provide the fastest path** to multi-carrier support. They abstract away individual carrier API differences (auth methods, webhook patterns, label formats).

2. **The enterprise delivery platforms (Shipsy, FarEye, Locus) all gate their APIs** behind sales engagement. Only Circuit/Spoke offers self-service API access.

3. **India-founded platforms dominate the enterprise delivery space** (Shipsy, FarEye, Locus, Shipsy). Strong APAC coverage but all expanding globally.

4. **Crowdsourced delivery is risky** — Pandion shut down after $125M raised, Veho has 1.3-star Trustpilot rating. Roadie (UPS-backed) and Dolly (Taskrabbit/IKEA-backed) are more stable.

5. **All major carriers are converging on REST + OAuth 2.0** but integration differences remain (DHL Basic Auth, USPS no webhooks, UPS token limits).

6. **Tookan is high-risk** despite low pricing — widely reported support/reliability issues.

7. **Route optimization is a commodity** — Routific, OptimoRoute, and Circuit/Spoke all offer good APIs at different price points. Locus adds ML-powered optimization at enterprise scale.
