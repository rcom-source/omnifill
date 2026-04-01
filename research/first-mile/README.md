# First Mile Transportation SaaS Research

Research date: 2026-03-31

Comprehensive research on first mile transportation SaaS systems (supplier-to-destination freight), covering TMS platforms, freight forwarders with APIs, multi-modal orchestration platforms, carrier connectivity platforms, and visibility providers.

## Research Files

| File | Systems Covered | Category |
|------|----------------|----------|
| [flexport.md](flexport.md) | Flexport | Freight forwarder with APIs |
| [visibility-platforms.md](visibility-platforms.md) | project44, FourKites | Real-time visibility platforms |
| [tms-mercurygate-transplace.md](tms-mercurygate-transplace.md) | MercuryGate (Infios), Transplace/Uber Freight TMS | Transportation management systems |
| [descartes-blujay-e2open.md](descartes-blujay-e2open.md) | Descartes, BluJay, E2open (INTTRA) | Supply chain networks & TMS |
| [tms-landscape.md](tms-landscape.md) | Oracle OTM, SAP TM, Blue Yonder TMS, Manhattan Active TMS, Trimble TruckMate, Descartes Aljex, 3Gtms, Blume Global | Enterprise & mid-market TMS |
| [carrier-connectivity-platforms.md](carrier-connectivity-platforms.md) | Convoy/DAT, Uber Freight, Loadsmart, DAT, Trucker Tools, MacroPoint, Motive, Samsara | Carrier matching, visibility & fleet IoT |
| [shipwell-mastery-research.md](shipwell-mastery-research.md) | Shipwell, Mastery Transportation | Cloud TMS platforms |
| [kuebix-trimble.md](kuebix-trimble.md) | Kuebix (Trimble) | Cloud TMS (defunct brand) |
| [turvo.md](turvo.md) | Turvo | Collaborative TMS |
| [haven.md](haven.md) | Haven | Freight procurement (defunct) |

## Systems Covered (30+)

### TMS Platforms
| System | API Access | Modes | Auth | Status |
|--------|-----------|-------|------|--------|
| Flexport | REST (customer-only) | Ocean, Air, Truck, Rail | OAuth 2.0 | Active |
| MercuryGate/Infios | REST + EDI (partial docs) | All modes | OAuth 2.0 PKCE | Active |
| Transplace/Uber Freight TMS | REST (gated) | All modes | SAML SSO | Active |
| Shipwell | REST (public OpenAPI) | 8+ modes | Token + API Key | Active |
| Turvo | REST + Webhooks (gated) | FTL, LTL, Intermodal, Drayage | OAuth 2.0 | Active |
| Oracle OTM | REST (public docs) | All modes + Barge | Basic Auth | Active |
| SAP TM | OData/REST + BAPI/RFC | All modes | OAuth 2.0 / X.509 | Active |
| Blue Yonder TMS | REST/SOAP (gated) | All modes | API Keys | Active |
| Manhattan Active TMS | REST microservices (public) | All modes | OAuth 2.0 | Active |
| Trimble TruckMate | REST (public) | Truck only | OAuth 2.0 | Active |
| Descartes Aljex | REST + EDI (gated) | Truck | Not public | Active |
| 3Gtms | REST via Integration Hub (gated) | TL/LTL/Parcel/Intermodal | Not public | Active |
| Mastery Transportation | Gated (no public API) | Truck | Not public | Active |
| Kuebix | Absorbed into Trimble | LTL, FTL | API Key / OAuth | Defunct brand |
| Haven | Offline | FTL, LTL | API Key | Defunct |

### Visibility Platforms
| System | API Access | Modes | Auth | Status |
|--------|-----------|-------|------|--------|
| project44 | REST (OpenAPI v4) | All modes | OAuth 2.0 | Active |
| FourKites | REST + Postman collections | All modes | API Key / Basic / Digest | Active |
| Blume Global | REST (6 API categories) | All modes | API Key | Active |
| Descartes MacroPoint | REST (XML) | All modes | Basic Auth | Active |

### Carrier Connectivity & Freight Matching
| System | API Access | Function | Auth | Status |
|--------|-----------|----------|------|--------|
| DAT | REST (developer portal) | Load board + analytics | Service accounts | Active |
| Uber Freight | REST (partner-gated) | Digital freight matching | OAuth 2.0 | Active |
| Loadsmart | REST (gated) | AI freight brokerage + TMS | OAuth | Active |
| Trucker Tools | Custom integration only | Carrier visibility | Encrypted key | Active |
| Convoy | Merging into DAT | Digital freight matching | N/A | Acquired by DAT |

### Fleet Management & IoT
| System | API Access | Function | Auth | Status |
|--------|-----------|----------|------|--------|
| Samsara | REST + Kafka (public docs) | Fleet IoT/telematics | OAuth 2.0 | Active |
| Motive (KeepTruckin) | REST (public, free dev accounts) | Fleet management + ELD | API Key / OAuth 2.0 | Active |

### Supply Chain Networks
| System | API Access | Function | Auth | Status |
|--------|-----------|----------|------|--------|
| Descartes GLN | Network APIs | Global logistics network | API Key | Active |
| E2open (incl. INTTRA) | REST (gated) | Supply chain + ocean platform | OAuth 2.0 | Active |
| BluJay | Absorbed into E2open | TMS (legacy) | N/A | Defunct brand |

## Integration Priority Tiers

### Tier 1 — Open APIs, Strong Documentation (Start Here)
1. **Shipwell** — Public OpenAPI spec, sandbox, 26+ endpoint groups, token auth
2. **project44** — Public OpenAPI v4 YAML spec, OAuth 2.0, all modes
3. **Manhattan Active TMS** — Public Developer Hub, OAuth 2.0, Postman collections
4. **Samsara** — Excellent developer docs, OAuth 2.0, Kafka streaming
5. **Motive** — Free self-serve dev accounts, comprehensive JSON REST API
6. **DAT** — Developer portal, largest North American freight network

### Tier 2 — Partial Public Docs, Some Gating
7. **FourKites** — REST APIs, Dynamic Yard Postman collections, carrier self-onboarding
8. **Oracle OTM** — Comprehensive Oracle docs, but Basic Auth only
9. **Trimble TruckMate** — Public developer portal, but truck-only
10. **Descartes MacroPoint** — Documented API but XML-based, per-load pricing
11. **MercuryGate/Infios** — Partial Swagger docs, OAuth 2.0 PKCE
12. **Flexport** — Good REST APIs, but customer-only (not carrier-neutral)
13. **Loadsmart** — API exists but credentials require account manager

### Tier 3 — Gated, Requires Partnership
14. **Uber Freight (TMS)** — Developer portal exists but SAML SSO gated
15. **E2open/INTTRA** — Valuable ocean platform, gated behind login
16. **SAP TM** — Enterprise, complex, expensive
17. **Blue Yonder TMS** — Fully gated behind Success Portal
18. **Blume Global** — API categories described but limited technical detail
19. **Turvo** — REST API exists but fully gated
20. **Mastery Transportation** — No public API at all

### Not Viable
- **Kuebix** — Brand dead, absorbed into Trimble
- **Haven** — Company defunct, APIs offline
- **BluJay** — Absorbed into E2open
- **Convoy** — Acquired, merging into DAT
- **Descartes Aljex** — Too small, no public API docs
- **3Gtms** — Integration Hub only, no direct API access

## Key Architectural Patterns

1. **REST dominates** — Nearly all modern platforms offer REST APIs. SOAP/EDI exists for legacy compatibility but is being phased out.
2. **OAuth 2.0 is standard** — Most platforms use OAuth 2.0 (client credentials or authorization code). Some legacy systems still use Basic Auth or API keys.
3. **Webhooks for events** — Real-time event notification via webhooks is widely supported for tracking, status, and document events.
4. **EDI still matters** — X12 (204, 210, 214, 990) remains critical for carrier communication. Many platforms support both REST and EDI.
5. **Two integration layers needed** — Transaction platforms (TMS, brokers) for booking/tracking + operational platforms (fleet IoT) for real-time vehicle data.
6. **Customer-lock-in risk** — Some platforms (Flexport, Uber Freight) only expose APIs to their own customers, limiting vendor-neutral integration.

## Data Model Observations

Common data entities across all platforms:
- **Shipment/Load** — The core entity (origin, destination, mode, equipment, dates)
- **Rate/Quote** — Pricing with carrier, service level, transit time
- **Tracking Event** — Status updates with timestamp, location, milestone type
- **Document** — BOL, POD, invoice, customs docs (image + structured data)
- **Carrier** — Identity, capacity, performance metrics, compliance
- **ETA** — Predicted arrival, often ML-enhanced (project44, FourKites)

These map well to a unified adapter interface with normalized types.
