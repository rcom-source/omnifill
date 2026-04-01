# Extensiv (3PL Central) — Middle Mile Capabilities

Research date: 2026-03-31

## Company Overview

Extensiv assembles 3PL Central, Skubana, and CartRover into a hub aimed at SMB and lower-mid-market logistics firms.

## Products

| Product | Description |
|---------|-------------|
| 3PL Warehouse Manager | Cloud-based WMS for 3PLs (formerly 3PL Central) |
| Extensiv Hub | Unified omnichannel fulfillment platform |
| Integration Manager (CartRover) | 100+ ecommerce/marketplace connectors |
| Warehouse Manager (TopShelf/Scout) | Mobile/tablet-first inventory for brands/distributors |
| Order Manager (Skubana) | Advanced DOM for omnichannel brands |
| Network Manager | 4PL network management for 3PLs |
| Fulfillment Marketplace | Pre-vetted fulfillment partner matching |

[Source: https://www.extensiv.com/extensiv-3pl-warehouse-manager]

## Middle Mile Capabilities

### Receiving (Inbound)

- SmartScan mobile receiving module
- ASN (Advanced Shipping Notice) receiving — validate against expected shipment
- Rapid Receiving (closed beta) — accelerated workflow
- MU label printing during receiving
- API endpoints: `GET /inventory/receivers`, `POST /inventory/receivers`

[Source: https://help.extensiv.com/en_US/inbound-operations]

### Dock Scheduling (DataDocks)

- **DataDocks** — dedicated dock scheduling product integrated into 3PL Warehouse Manager
- Self-serve carrier portal for appointment booking/changes
- Multi-location appointment scheduling
- Drag-and-drop calendar dashboard
- Workload balancing rules
- Carrier performance reports (on-time by vendor)
- Late delivery fee collection, detention fee avoidance metrics

[Source: https://www.extensiv.com/extensiv-3pl-warehouse-manager/dock-scheduling]
[Source: https://help.extensiv.com/en_US/datadocks/understanding-datadocks]

### Cross-Docking

**Not a native feature.** No dedicated cross-docking module found. Platform focuses on traditional receive-store-ship workflows.

### Yard Management

**No native module.** Extensiv does not advertise yard management as a capability.

## Technical Integration

### REST API

- **Base URL:** `https://secure-wms.com/` (instance-specific)
- **Developer Portal:** https://developer.3plcentral.com/ and https://developer.extensiv.com/
- HTTPS required, HAL+JSON response format with `_embedded` structures
- Pagination via `pgnum`, `pgsiz`; RQL query filtering

**Key Endpoints:**

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/auth/token` | POST | OAuth token generation |
| `/customers` | GET | List customers |
| `/customers/{id}/items` | GET | Customer items/SKUs |
| `/orders` | GET/POST | Orders CRUD |
| `/orders/{id}/packages` | GET | Order packages |
| `/inventory/receivers` | GET/POST | Receivers (inbound) |
| `/inventory/stockdetails` | GET | Stock details |
| `/inventory/pos` | GET | Purchase orders |
| `/properties/carriers` | GET | Carriers |
| `/properties/facilities` | GET | Facilities |

[Source: https://developer.3plcentral.com/]

### Webhooks

- Configured via Customers > Event Notifications
- Requires "Data Connections" permission
- HTTPS destination URL required

**Supported Events:**
- **Order:** Create, Complete, Update, Confirm, Unconfirm, Cancel, FullyAllocated, PickJobDone, PackComplete
- **Receipt:** Create, Complete, Update, Confirm, Unconfirm, Cancel
- **Adjustment:** Create, Confirm, Cancel, Update
- **Assembly:** Create, Cancel, Update, Confirm
- **Order Item:** Pack, Unpack, Pick, Unpick
- **Item:** Create, Update
- **Inventory Summary:** Update

[Source: https://extensiv.helpjuice.com/rest-api/configuring-webhooks]

### Authentication

- **OAuth 2.0 Client Credentials** flow
- **Token endpoint:** `POST https://secure-wms.com/AuthServer/api/Token`
- Required: Client ID, Client Secret, TPL GUID, UserLogin ID
- Authorization header: Basic Auth with Base64(ClientID:ClientSecret)
- Grant type: `client_credentials`
- Token lifetime: 30-60 minutes; refresh every 30 minutes minimum
- Access via: api@extensiv.com or customer success manager

[Source: https://help.extensiv.com/rest-api/providing-rest-api-access]

## User Reviews

### Ratings

| Platform | Rating | Reviews |
|----------|--------|---------|
| G2 | ~4.0/5 | 112 across products |
| Capterra | ~4.1/5 | Multiple |
| ITQlick | 4/5, score 79/100 | Available |

### Pros
- Easy to use, clean UI
- Good marketplace connectors
- Dock scheduling configurable without code
- 40% productivity improvement reported
- Good multi-client management

### Cons
- Additional charges for custom reports ($350+)
- $25/customer surcharge after first 5
- Slow ticket resolution
- Scanning feature quality issues
- System allows inventory overriding leading to errors

[Source: https://www.g2.com/products/extensiv-3pl-warehouse-manager/reviews]
[Source: https://www.capterra.com/p/86175/3PL-Warehouse-Manager/reviews/]

## Pricing

| Plan | Price |
|------|-------|
| Merchant Plan | $39/month |
| EDI Merchant Plan | $99/month |
| 3PL Plan | $99/month |
| Master Account Plan | $199/month |
| 3PL Warehouse Manager | Starting ~$599/month |

- 30-day free trial available
- $25/customer surcharge after initial 5
- Custom report fees reportedly $350+

[Source: https://softwareconnect.com/reviews/extensiv-3pl-warehouse-manager/]

## Integration Assessment

**Classification: OPEN**

| Dimension | Assessment |
|-----------|------------|
| API Surface | Comprehensive REST API with webhooks |
| Public Access | Yes — developer portal, docs publicly accessible |
| Sandbox | None dedicated, but trial available |
| Integration Effort | LOW — well-documented OAuth 2.0, standard REST |
| Middle Mile Strength | WEAK — no YMS, no cross-docking, dock scheduling only |
| Decision Engine | None — basic receiving/fulfillment |

**Note:** Extensiv is primarily a last-mile/warehouse WMS. Middle mile capabilities are limited to dock scheduling (DataDocks) and basic inbound receiving. No transportation routing, allocation engine, or cross-docking.

## Sources

- https://developer.3plcentral.com/
- https://developer.extensiv.com/pages/3pl-wareshouse-manager.html
- https://help.extensiv.com/en_US/inbound-operations
- https://www.extensiv.com/extensiv-3pl-warehouse-manager/dock-scheduling
- https://help.extensiv.com/en_US/datadocks/understanding-datadocks
- https://www.extensiv.com/blog/dock-scheduling
- https://help.extensiv.com/366924-3pl-central/1624716-extensiv-3pl-warehouse-manager-api-permissions
- https://extensiv.helpjuice.com/rest-api/configuring-webhooks
- https://help.extensiv.com/rest-api/providing-rest-api-access
- https://www.extensiv.com/newsroom/extensiv-launches-extensiv-hub
- https://www.extensiv.com/extensiv-network-manager
- https://www.g2.com/products/extensiv-3pl-warehouse-manager/reviews
- https://www.capterra.com/p/86175/3PL-Warehouse-Manager/reviews/
- https://www.trustradius.com/products/extensiv-3pl-warehouse-manager/reviews
- https://softwareconnect.com/reviews/extensiv-3pl-warehouse-manager/
- https://dlthub.com/context/source/three-pl-central
- https://www.stitchdata.com/docs/integrations/saas/3plcentral
