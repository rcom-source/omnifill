# Kuebix (now Trimble Transportation)

Research date: 2026-03-31

## Overview

Kuebix was a cloud-based Transportation Management System (TMS) founded in 2008, acquired by Trimble in 2020 for ~$200M. Post-acquisition, Kuebix was folded into Trimble Transportation and its standalone product was largely sunset/merged into Trimble's broader transportation suite.

## Capabilities

- Freight rate comparison and quoting (multi-carrier)
- Shipment execution and booking
- Freight tracking and visibility
- Analytics and reporting
- Carrier management
- Freight audit and payment
- Order management

**Modes:** Primarily LTL and FTL (truckload). Limited parcel. No native ocean/air/rail.

**Key differentiator:** Kuebix offered a free "Community" tier TMS — a freemium TMS that let small/mid shippers quote and book LTL shipments at no cost. This tier has been discontinued post-acquisition.

## Technical Documentation & APIs

- **REST API:** Available to Enterprise tier customers, covering rate quotes, shipment creation, tracking, and document retrieval. Never had a public developer portal.
- **EDI (X12):** 204 (Load Tender), 210 (Freight Invoice), 214 (Shipment Status), 990 (Response to Load Tender)
- **Flat file/CSV:** Supported for bulk imports (orders, addresses, item master)
- **ERP connectors:** Pre-built integrations for SAP, Oracle, NetSuite, Microsoft Dynamics
- **No public developer portal** exists (neither original nor Trimble's replacement)
- Post-acquisition, APIs migrated into Trimble Transportation's platform, gated behind partnership/customer agreements

## Authentication

- API Key + Secret (pre-Trimble)
- OAuth 2.0 introduced post-Trimble acquisition
- EDI connections used standard AS2/SFTP transport

## Help Centers & Community

- Original help center (help.kuebix.com) taken offline
- Trimble Transportation support: https://transportation.trimble.com/support
- No public community forums
- Kuebix-specific content is sparse in Trimble's broader knowledge base

## User Reviews

| Pros | Cons |
|------|------|
| Free Community tier was game-changing for small shippers | Post-acquisition, free tier deprecated/restricted |
| Easy to use, intuitive UI for LTL quoting | Limited to North American trucking (no international) |
| Good carrier network out of the box | API access restricted to expensive enterprise tier |
| Fast implementation (weeks, not months) | Reporting was basic compared to competitors |
| Solid rate shopping across multiple carriers | Customer support degraded post-Trimble acquisition |
| | Trimble integration roadmap unclear to existing customers |

## Pricing

- **Community (Free):** Basic LTL rate shopping and booking — now largely discontinued
- **Business:** ~$1,000-3,000/month (estimated, never publicly listed)
- **Enterprise:** Custom pricing, typically $5,000+/month, required for API access
- Post-Trimble: Fully custom/quote-based under Trimble Transportation umbrella

## Data Exposed

- Rate quotes (carrier, service, transit time, cost breakdown)
- Shipment status/tracking events
- BOL and POD documents
- Invoice data (freight audit)
- Carrier performance metrics
- No real-time GPS tracking (relied on carrier-provided status updates via EDI 214)

## Current Status (2026)

Kuebix as a standalone brand is effectively dead. Trimble Transportation absorbed the technology. Customers were migrated to Trimble's platform. The free TMS tier no longer exists.

## Integration Recommendation

Not worth building a standalone adapter. The brand is dead, and Trimble's transportation API is a different, larger integration target. If Trimble Transportation becomes a priority, it should be scoped as its own system.

## Sources

- https://transportation.trimble.com/support [Source: Trimble Transportation support portal]
- https://www.g2.com/products/kuebix-tms/reviews [Source: G2 - Kuebix TMS reviews]
- https://www.capterra.com/p/163159/Kuebix-TMS/ [Source: Capterra - Kuebix TMS]
- https://www.trimble.com/en/our-company/newsroom/press-releases/2020/trimble-acquires-kuebix [Source: Trimble acquisition announcement]
- Reddit r/logistics, r/supplychain [Source: Reddit - searches for "Kuebix", "Trimble TMS"]
