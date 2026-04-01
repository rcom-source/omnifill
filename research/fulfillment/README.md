# Fulfillment SaaS Systems — Research Index

> Comprehensive research on warehouse management, fulfillment, and robotics platforms.
> Research date: 2026-03-31
> Bead: fl-sz4

---

## Systems Researched

### Enterprise WMS (Tier 1 — Large-scale, gated documentation)

| System | File | API Access | Integration Difficulty | Key Differentiator |
|--------|------|-----------|----------------------|-------------------|
| [Manhattan Associates](manhattan-associates.md) | manhattan-associates.md | Gated (NDA) | HIGH | Best-in-class WMS + LMS, cloud-native Active platform |
| [Blue Yonder](blue-yonder-wms-research.md) | blue-yonder-wms-research.md | Gated (MOCA) | HIGH | MOCA architecture, Luminate AI platform |
| [SAP EWM](sap-ewm-research.md) | sap-ewm-research.md | Partial (OData) | HIGH | Deep S/4HANA integration, MFS for automation |
| [Oracle WMS Cloud](oracle-wms-cloud.md) | oracle-wms-cloud.md | Public (REST) | MODERATE | Full REST API with lgfapi, public docs |
| [Körber/Infios](korber-infios.md) | korber-infios.md | None public | VERY HIGH | WCS/WES for automation, legacy HighJump base |

### Mid-Market WMS & Fulfillment Platforms (Tier 2 — Accessible APIs)

| System | File | API Access | Integration Difficulty | Key Differentiator |
|--------|------|-----------|----------------------|-------------------|
| [ShipBob](shipbob-research.md) | shipbob-research.md | Public (REST) | LOW | Full developer portal, sandbox, 60+ carriers |
| [ShipHero](shiphero-research.md) | shiphero-research.md | Public (GraphQL) | LOW | GraphQL API, credit-based rate limiting |
| [Extensiv/3PL Central](extensiv-3pl-central.md) | extensiv-3pl-central.md | Public (REST x8) | MODERATE | 8 APIs, purpose-built for 3PLs |
| [Logiwa](logiwa-research.md) | logiwa-research.md | Public (REST/Swagger) | LOW | OpenAPI/Swagger, good for D2C fulfillment |
| [Deposco](deposco.md) | deposco.md | Partial (REST) | MODERATE | Cloud-native WMS+OMS, Basic Auth |
| [Softeon](softeon.md) | softeon.md | Gated | MODERATE-HIGH | Best-in-class WES for automation orchestration |

### 3PL Fulfillment Services (Tier 3 — Service + tech)

| System | File | API Access | Integration Difficulty | Key Differentiator |
|--------|------|-----------|----------------------|-------------------|
| [ShipMonk](made4net-shipmonk-fulfillmentcom.md#shipmonk) | made4net-shipmonk-fulfillmentcom.md | Public (REST) | LOW | Developer-friendly API, sandbox, 12+ facilities |
| [Fulfillment.com](made4net-shipmonk-fulfillmentcom.md#fulfillmentcom-fdc) | made4net-shipmonk-fulfillmentcom.md | Partial (REST v2) | MODERATE | Global 3PL, 8 facilities, 65+ ecommerce integrations |
| [Radial](radial-research.md) | radial-research.md | Gated (REST/XML) | HIGH | Omnichannel + payments/fraud, 30+ FCs |
| [Quiet Logistics](quiet-logistics-research.md) | quiet-logistics-research.md | Gated | HIGH | Robotics-powered (Locus), now SPARC Group |

### WMS Software Platforms (Tier 4 — On-prem/hybrid)

| System | File | API Access | Integration Difficulty | Key Differentiator |
|--------|------|-----------|----------------------|-------------------|
| [Made4net](made4net-shipmonk-fulfillmentcom.md#made4net-scexpertwarehouseexpert) | made4net-shipmonk-fulfillmentcom.md | None public | HIGH | .NET/SOA, native WCS, LaborExpert, Gartner recognized |

### Warehouse Robotics Platforms

| System | File | Robot Type | WMS Integration | Key Differentiator |
|--------|------|-----------|----------------|-------------------|
| [6 River Systems](robotics-platforms.md#1-6-river-systems) | robotics-platforms.md | AMR (collaborative picking) | REST API (gated) | Chuck robot, now Flexport-owned |
| [Locus Robotics](robotics-platforms.md#2-locus-robotics) | robotics-platforms.md | AMR (picking) | REST API (gated) | Largest install base, DHL partnership |
| [AutoStore](robotics-platforms.md#3-autostore) | robotics-platforms.md | ASRS (cube storage) | Partner WES layer | 4x storage density, goods-to-person |
| [Berkshire Grey](robotics-platforms.md#4-berkshire-grey) | robotics-platforms.md | Robotic arms + sort | Custom (gated) | AI vision picking, automated sorting |
| [Fetch/Zebra](robotics-platforms.md#5-fetch-robotics-zebra-technologies) | robotics-platforms.md | AMR (multi-type) | REST API (gated) | Zebra ecosystem (scanning, RFID, printing) |

---

## Integration Feasibility Summary

### Recommended Priority for Omnifill Adapter Development

**Phase 1 — Public APIs, low barrier (start here):**
1. **ShipBob** — Full REST API, sandbox, OAuth 2.0, excellent docs
2. **ShipHero** — GraphQL API, public schema, good community
3. **Logiwa** — REST with Swagger/OpenAPI, well-documented
4. **ShipMonk** — REST API, sandbox, API key auth

**Phase 2 — Public APIs, moderate complexity:**
5. **Extensiv/3PL Central** — 8 REST APIs, OAuth 2.0, more surface area
6. **Oracle WMS Cloud** — Full REST API, public docs, enterprise auth
7. **Deposco** — REST API, partial docs, Basic Auth

**Phase 3 — Gated APIs, vendor engagement required:**
8. **SAP EWM** — OData APIs browsable on api.sap.com, need license for usage
9. **Softeon** — REST APIs exist but gated, strong WES reference architecture
10. **Manhattan Associates** — REST/GraphQL on Active, requires partnership
11. **Blue Yonder** — MOCA proprietary, requires customer/partner access
12. **Körber/Infios** — No public API, SFTP/SQL fallback

**Phase 4 — Service integrations (3PL providers):**
13. **Fulfillment.com** — REST v2, sparse docs
14. **Radial** — Gated REST/XML API
15. **Quiet Logistics** — Gated, robotics-focused

---

## Common Integration Patterns Across All Systems

### Authentication Methods

| Method | Systems |
|--------|---------|
| OAuth 2.0 | Manhattan Active, SAP EWM, ShipBob, Extensiv, Oracle WMS |
| API Key / PAT | ShipBob, ShipMonk |
| JWT Bearer | ShipHero, Manhattan Active |
| Basic Auth | Deposco, Oracle WMS |
| Client Credentials | Extensiv, Logiwa |
| Gated/Proprietary | Blue Yonder, Körber, Softeon, Radial, Quiet Logistics |

### API Styles

| Style | Systems |
|-------|---------|
| REST (JSON) | ShipBob, Extensiv, Logiwa, Deposco, Oracle WMS, ShipMonk, Radial |
| GraphQL | ShipHero, Manhattan Active |
| OData | SAP EWM |
| SOAP/XML | Manhattan WMOS, Blue Yonder, Radial (legacy) |
| MOCA (proprietary) | Blue Yonder |
| SFTP/file-based | Körber, legacy systems universally |
| EDI | All enterprise WMS (940/943/944/945/947 transaction sets) |

### Webhook Support

| Has Webhooks | Systems |
|-------------|---------|
| Yes | ShipBob, ShipHero, Extensiv, Logiwa, ShipMonk |
| Limited/Undocumented | Deposco, Oracle WMS |
| No/Unknown | Manhattan, Blue Yonder, SAP EWM, Körber, Softeon |

---

## Key Architectural Insights for Omnifill

1. **WES is the missing layer.** Most WMS systems lack good automation orchestration. Softeon's WES and Manhattan's Active WES are the exceptions. Omnifill could provide this unified orchestration layer.

2. **EDI is the universal fallback.** Every enterprise WMS speaks EDI (940/945 transaction sets). An EDI adapter gives Omnifill access to ANY WMS, including fully gated ones.

3. **GraphQL vs REST split.** ShipHero is the only pure GraphQL system. Most others are REST. Omnifill should support both but REST-first.

4. **Robotics integration is siloed.** Each robotics vendor (Locus, Fetch, AutoStore) has their own fleet management cloud. A unified robotics abstraction is high-value and currently unserved in the market.

5. **3PL billing is unique.** Extensiv and ShipHero have 3PL-specific billing APIs. If Omnifill targets 3PL operators, billing integration is important.

6. **Rate limiting varies wildly.** From 60 req/min (Logiwa standard) to 100K req/min (ShipMonk). Adapter design must handle per-system rate limit strategies.

7. **Sandbox availability is rare.** Only ShipBob and ShipMonk offer public sandboxes. Most systems require vendor engagement for test environments.

---

## File Listing

```
research/fulfillment/
├── README.md                           # This file (index)
├── manhattan-associates.md             # Manhattan Associates WMS
├── blue-yonder-wms-research.md         # Blue Yonder (JDA) WMS
├── sap-ewm-research.md                # SAP Extended Warehouse Management
├── oracle-wms-cloud.md                 # Oracle WMS Cloud
├── korber-infios.md                    # Körber/Infios (HighJump)
├── shipbob-research.md                 # ShipBob
├── shiphero-research.md                # ShipHero
├── extensiv-3pl-central.md             # Extensiv (3PL Central / Skubana)
├── logiwa-research.md                  # Logiwa
├── deposco.md                          # Deposco
├── softeon.md                          # Softeon WMS/WES
├── made4net-shipmonk-fulfillmentcom.md # Made4net + ShipMonk + Fulfillment.com
├── radial-research.md                  # Radial (GSI Commerce)
├── quiet-logistics-research.md         # Quiet Logistics
└── robotics-platforms.md               # 6RS, Locus, AutoStore, Berkshire Grey, Fetch/Zebra
```
