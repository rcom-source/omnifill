# Oracle Warehouse Management Cloud (WMS Cloud)

## Overview & History

Oracle Warehouse Management Cloud (formerly LogFire Cloud WMS) is a cloud-native SaaS warehouse management system. Oracle acquired LogFire in September 2016 and rebranded it as Oracle WMS Cloud, integrating it into the Oracle Supply Chain Management (SCM) Cloud suite. The platform is designed for complex, high-volume warehouse operations across manufacturing, retail, 3PL, and distribution verticals.

- **Headquarters**: Austin, TX (Oracle SCM Cloud)
- **Parent**: Oracle Corporation
- **Origin**: LogFire (acquired 2016)
- **Market Position**: Named a Leader in the Gartner Magic Quadrant for Warehouse Management Systems for 10 consecutive years (through 2025)
- **Gartner Peer Insights**: 148 verified reviews; strong marks for execution capability and completeness of vision
- **Certifications**: SOC 2 Type II, ISO 27001, GxP (life sciences), FDA 21 CFR Part 11

## What It Does

### Pick Methods

**Wave Picking**
- Advanced wave management using complex algorithms to optimize picking efficiency
- Wave templates define replenishment rules (order-based replenishment)
- Dispatches tasks line by line regardless of source subinventories
- Wave-based allocation ensures orders are fulfilled from optimal locations

**Discrete Picking**
- Dispatches grouped tasks by pick slip grouping rules
- All eligible tasks with the same pick slip ID dispatched to the same operator sequentially
- Uses preassigned pick methodology defined by grouping rules

**Zone Picking**
- Locations must be assigned Pick Zones via the `pick_zone` field
- Zone-based task dispatching for parallel picking across warehouse zones
- Reduces picker travel time within large facilities

**Batch Picking**
- Supports batch pick consolidation across multiple orders
- Combined with put-to-store and cross-docking workflows

**Task Interleaving**
- Assigns nearby work immediately after task completion
- Eliminates "empty travel" time; reported ~10% productivity boost
- AI-optimized task assignment to minimize non-productive movement

### Pack Optimization

- **Cartonization engine**: Minimizes containers used at each packaging hierarchy level subject to volume, weight, and minimum fill percentage settings
- **Multi-level packing**: Inner cartons packed inside outer cartons placed on pallets, with labels generated at each level in a single operation
- **Category segregation**: Separates items by packaging requirements (e.g., refrigerated goods in insulated coolers vs. standard corrugated)
- **Minimum fill percentage**: System suggests smaller container when below threshold
- **Pause/resume packing**: Can halt packing midway and continue later
- **Destination-based consolidation**: Controls packing of multiple orders into the same OBLPN when destination facility matches
- **Shipping tolerance**: Supports pick quantities above allocation when max shipping tolerance > 0%

### Shipping & Carrier Selection

**Native Parcel Integration**
- Built-in integration with UPS and FedEx via their SOAP web services
- Integration with DHL GlobalMail via ConnectShip Web Services
- Parcel manifest functionality sends carton info (weight, volume, address) and receives tracking numbers
- FedEx PC Ship Manager for tracking number retrieval and shipping label generation
- Tracking numbers automatically updated in WMS

**Load Management**
- Store-friendly outbound shipment creation
- Multi-stop route support with custom allocations
- Yard-to-dock movement coordination
- OBLPN (Outbound License Plate Number) assignment to loads via API

**Third-Party Carrier Solutions**
- Oracle Transportation Management (OTM) integration for rate shopping and carrier selection
- Third-party multi-carrier platforms (ShipERP, ShipConsole, ProcessWeaver) overlay Oracle WMS for dynamic rate shopping, consolidation, and compliance
- Rate shopping is NOT native to WMS Cloud; requires TMS or third-party overlay

### Labor Management

- Performance standard creation and tracking for picking/packing tasks
- Individual and team productivity monitoring against established goals
- AI-powered slotting analyzes demand patterns, product dimensions, and picking frequency
- Dynamic slotting can reduce picker travel time by 10-15%
- Role-based access to performance metrics (managers see team data)
- Task interleaving for multi-task worker optimization

### Robotics & Automation Integration

**Warehouse Execution System (WES)**
- Integrated WES orchestrates Autonomous Mobile Robots (AMRs)
- Receives orders from WMS and translates into specific robot tasks
- Manages traffic flow and task assignment to prevent bottlenecks
- Reported 2-4x increase in order throughput per customer case studies

**Supported Automation**
- Autonomous Mobile Robots (AMRs): Locus Robotics, 6 River Systems, Fetch Robotics
- Automated Guided Vehicles (AGVs)
- Conveyor systems and sortation (carton sorter, tilt tray sorter)
- Pick-to-light systems
- Carousels
- Scales
- WCS (Warehouse Control System) connectivity for all MHE types

### Returns Management

- Automated Returns Merchandise Authorization (RMA) creation
- AI-guided disposition recommendations based on item condition, sales velocity, and inventory levels
- Routes items to restocking, value-added services, or liquidation areas
- Return authorization and vendor return process automation

## Technical Documentation

### REST API (lgfapi)

Oracle WMS Cloud exposes its REST API through the **lgfapi** module. This is the primary programmatic interface for data integration and WMS operations.

**URL Format**:
```
[Protocol]://[Domain]/[Environment]/[App]/lgfapi/[Version]/[Module]/[Resource Path]
```

**Example**:
```
GET https://example.oracle.com/wms/lgfapi/v10/entity/order_hdr/123
GET https://example.oracle.com/wms/lgfapi/v9/entity/?format=json
GET https://example.oracle.com/wms/lgfapi/v9/print/label/?format=json
```

**Versioning**:
- Format: `v#` (starts at `v9`)
- New versions created only for major releases (e.g., WMS 9.0.0 = lgfapi v9)
- Minor releases (e.g., 9.0.1) update APIs but do not create new version numbers
- Older versions supported ~1 year after newer version release
- Best practice: use latest version in production

**Available Modules**:
- `entity` - Examine and interact with OCWMS business resources (CRUD operations on orders, inventory, locations, etc.)
- `print/label` - Label printing functionality

**API Root Discovery**:
```
GET .../lgfapi/v10/entity/?format=json
```
Returns a structured list of all available endpoints for the module.

**Request/Response Format**:
- Supports `format=json` query parameter for JSON responses
- Default response format is XML
- Trailing slashes are optional

**Available API Operations** (Integration API):

| API | Description | Version |
|-----|-------------|---------|
| Init Stage Interface | Main API for input data integration | 6.4.0 |
| Run Stage Interface | Trigger validation & processing of staged data | 6.1 |
| Update OBLPN Tracking Number | Update tracking number and parcel stats | 6.1 |
| Run MHE Stage Interface | Invoke MHE interface for stage table processing | 6.2 |
| Assign OBLPN to Load | Assign outbound LPN to load | 7.0.0 |
| Create LPN | Create single-SKU IBLPN with inventory | 7.0.1 |
| Induct LPN | Induct LPN into MHE | 8.0.0 |
| Load LPN | Load an LPN | 8.0.2 |
| Entity Update API | Update entity attributes | 8.0.2 |
| Update Output Interface | Set status/error on transmitted output interface | 8.0.0 |

**HTTP Status Codes**:

| Status | Message | Methods | Description |
|--------|---------|---------|-------------|
| 200 | Ok | GET, POST, HEAD | Successful request |
| 201 | Created | POST | Resource created |
| 204 | No Content | POST | Success, no body |
| 304 | Not Modified | HEAD | Unchanged since target date |
| 400 | Bad Request | GET, POST, HEAD | Invalid data (from Release 21D+) |
| 401 | Unauthorized | all | Invalid credentials |
| 403 | Forbidden | all | Insufficient permissions |
| 404 | Not Found | all | Resource doesn't exist |
| 405 | Method Not Allowed | - | HTTP method unsupported |
| 409 | Conflict | all | Concurrent modification |
| 500 | Server Error | all | Unhandled error |

**Successful Response Example (XML)**:
```xml
<?xml version="1.0" encoding="utf-8"?>
<root>
  <success>True</success>
  <response>
    <message>Process stage item submitted for file group 41415472</message>
    <errors/>
    <data/>
  </response>
</root>
```

**Error Response Example**:
```xml
<?xml version="1.0" encoding="utf-8"?>
<root>
  <success>False</success>
  <response>
    <message>Record not found</message>
  </response>
</root>
```

**Note**: Prior to Release 21D, APIs returned HTTP 200 for all responses (even errors). From 21D onward, proper HTTP status codes (e.g., 400 for validation errors) are returned.

**lgfapi Archive Logging** (per-user, configured via Users UI):

| Level | Behavior |
|-------|----------|
| NONE | No archiving |
| ALL | Archive all request/response |
| ERROR | Archive only on errors |
| EDIT_AND_ERROR | Archive for non-GET/HEAD methods or errors |

### Developer Portal & SDKs

- **No dedicated developer portal** or SDK distribution. All API documentation is in the Oracle Help Center docs.
- **No official SDKs** in any language; integrators use raw HTTP/REST calls
- **Testing**: Postman recommended for API testing (referenced in Oracle docs)
- **Sandbox**: Available through Oracle Cloud trial/demo environments; no self-service sandbox sign-up
- **API docs**: Two primary guides:
  - **WMS REST API Guide** (lgfapi entity/print modules)
  - **Integration API Guide** (stage interface, MHE, LPN operations)

### Webhooks & Event Notifications

Oracle WMS Cloud does **not natively support webhooks**. Outbound event-driven integration is achieved through:

- **Oracle Integration Cloud (OIC)**: Subscribe to WMS business events (e.g., "Outbound Shipment Request") and route them to external systems
- **Output Interface**: Polling-based mechanism where external systems query for completed/changed records
- **Stage Interface**: Inbound data integration pattern (push data into WMS staging tables, trigger processing)

### WCS/WES Interfaces

- Native WCS connectivity for pick-to-light, carton sorters, tilt tray sorters, carousels, conveyors, and scales
- MHE Stage Interface API for programmatic MHE integration
- Induct LPN API for automating LPN flow into MHE systems
- Integrated WES for AMR fleet orchestration

## Authentication Methods

### BasicAuth

The legacy and simplest authentication method:

- HTTP Basic Authentication with WMS username and password
- Required permission: `lgfapi_update_access` (formerly `can_run_ws_stage_interface`)
- User must have access to relevant facility/company combinations
- CRUD application-level permissions required for specific HTTP methods

**Example**:
```bash
curl -u "username:password" \
  "https://<domain>/<env>/wms/lgfapi/v10/entity/order_hdr/?format=json"
```

### OAuth 2.0

Available since WMS 9.0.0. Two grant types supported:

**1. Resource Owner Password Credentials**
```bash
curl -v -X POST \
  -u "<ClientId>:<ClientSecret>" \
  -d "grant_type=password&username=<wms_user>&password=<wms_pwd>" \
  "https://<wms-domain>/<env-name>/api/oauth2/token/"
```

**2. Authorization Code**
- Authorization URI: `https://<wms-domain>/<env-name>/api/oauth2/authorize/`
- Token URI: `https://<wms-domain>/<env-name>/api/oauth2/token/`
- Requires redirect URI (e.g., for OIC: `https://<oic-host>:<oic-port>/icsapis/agent/oauth/callback`)

**Client Registration**:
1. Create a screen using module `api/oauth2/applications` (Screen Type UI-HTML-PP)
2. Navigate to screen and register a new application
3. System generates Client ID and Client Secret per application
4. Requires permission: `OAuth2 / Manage OAuth2 Applications`

### Integration Patterns

**Inbound (data into WMS)**:
1. Push data to stage tables via Init Stage Interface API
2. Trigger processing via Run Stage Interface API
3. WMS validates and processes staged records

**Outbound (data from WMS)**:
1. Query entity module for current state (polling)
2. Subscribe to business events via Oracle Integration Cloud (OIC)
3. Poll Output Interface for transmitted records

**Oracle-to-Oracle Integration**:
- Seamless native integration with Oracle Fusion Cloud ERP and NetSuite
- Pre-built real-time data synchronization
- Single source of truth for orders and inventory

**Non-Oracle ERP Integration**:
- Requires Oracle Integration Cloud (OIC) middleware
- OIC handles mapping, transformation, and routing
- Additional cost and complexity layer
- Requires specialized dual-system expertise

## Help Centers, Knowledge Bases & Community

| Resource | URL | Description |
|----------|-----|-------------|
| Oracle Help Center | docs.oracle.com/en/cloud/saas/warehouse-management/ | Official documentation: user guides, API guides, implementation guides, security guides |
| My Oracle Support (MOS) | support.oracle.com | 1M+ knowledge articles, patch notes, bug reports, service requests |
| Oracle Cloud Customer Connect | community.oracle.com/customerconnect | Community forums, expert Q&A, events, peer discussions |
| Oracle University | education.oracle.com | Training courses, certification (1Z0-1045 exam) |
| WMS Info Center (MOS) | Via My Oracle Support | Aggregated release notes, known issues, best practices |
| Release-specific docs | support.oracle.com (e.g., Doc ID 2959863_1) | Per-release documentation indexes (23C, 24B, 24C, 24D, 25A, 26A) |

**Documentation Guides Available**:
- Getting Started Guide
- User Guide
- Implementation and Configuration Guide
- REST API Guide (lgfapi)
- Integration API Guide (stage interfaces)
- Security Guide
- Technical Requirements Guide
- Online Help (context-sensitive)

## Pros and Cons from Real Users

### Pros

**From TrustRadius (6.0/10 overall)**:
- "Manage a lot of information - we manage 600+ stores of various sizes with millions of products"
- Material requisitions, dispatch, receiving reports, and stock audits synchronized in one dashboard
- Highly parametrizable system for different warehouse configurations
- Process automation reduces manual work and paperwork significantly
- Cycle counting and item tracking from inbound to outbound

**From G2**:
- Integration features work with almost all other systems
- Affordable cost relative to capability
- Efficient tracking for inventories, shipments, and workforce performance
- Supply chain optimization reduces inventory levels

**From Gartner Peer Insights (148 reviews)**:
- Strong control and product traceability for logistics operations
- Measurable reduction in labor hours
- Increased shipping on-time rates and fill-rates
- Robust functionality for warehouse space/equipment management

**From bestopschainai.com (expert analysis)**:
- AI-powered slotting can increase labor efficiency by up to 25% in complex operations
- AMR orchestration can increase order throughput 2-4x
- Enterprise-grade security (SOC 2, ISO 27001)
- Native Oracle ecosystem integration rated 8.5/10

### Cons

**From TrustRadius (Support rated 3/10)**:
- "It takes a long time to implement, took us almost a year"
- "Real-time inventory API is not present, which is an intense need in the e-commerce market"
- "The support is still poor" with slow response times; staff lack product knowledge
- "Difficult for a new user to use it without proper training"
- Manual entry control lacks proper safeguards

**From G2**:
- Requires substantial customization when first implemented
- Struggles with production line replenishment efficiency
- Seeded reports not organization-friendly without customization
- System stability issues during high growth
- Less flexibility in custom development since LogFire acquisition

**From Gartner Peer Insights**:
- Limitations in inventory intelligence and customization
- Integration challenges with ERP; service disruptions during updates
- Custom-made solutions difficult to implement

**From Expert Analysis**:
- Non-Oracle ERP integration rated only 5.5/10
- Voice-directed picking NOT native (requires third-party)
- Mobile/scanner interfaces are complex with steep learning curves
- Implementation: 6-9 months (single site), 12-18 months (multi-site)
- Implementation services cost 1.5-3x first-year subscription fee
- Mandatory OIC middleware for non-Oracle ERP connections adds ~75% of first-year subscription cost

## Pricing Model

Oracle WMS Cloud uses a **subscription-based SaaS pricing model** billed monthly:

| Tier | Estimated Monthly Cost |
|------|----------------------|
| Entry-level | ~$3,000/month |
| Mid-size (typical) | $15,000-$30,000/month |
| Enterprise | Custom pricing (mid-six figures annually) |

**Pricing Factors**:
- Number of warehouse users
- Order/transaction volume
- Modules selected
- Number of warehouses
- Multi-year enterprise contract terms

**Hidden / Additional Costs**:
- Implementation services: 1.5-3x first-year subscription
- Non-Oracle ERP integration (OIC middleware): ~75% of first-year subscription
- Training and change management
- Third-party carrier integration overlays (ShipERP, ShipConsole)
- No large upfront licensing (cloud model eliminates on-premise infrastructure costs)

**Oracle does not publish official pricing publicly.** All pricing requires direct engagement with Oracle sales.

## Carrier Integration Capabilities

### Native Carrier Support

| Carrier | Integration Method | Capabilities |
|---------|-------------------|--------------|
| UPS | SOAP Web Services | Tracking numbers, label generation |
| FedEx | SOAP Web Services + PC Ship Manager | Tracking numbers, shipping labels |
| DHL GlobalMail | ConnectShip Web Services | Tracking numbers |

### What's Included Natively
- Parcel manifest configuration and management
- Carton information exchange (weight, volume, address)
- Tracking number receipt and WMS update
- Shipping label generation (via carrier web services)
- OBLPN tracking number update via REST API

### What Requires Third-Party / OTM
- **Rate shopping**: NOT native; requires Oracle TMS or third-party (ShipERP, ProcessWeaver, ShipConsole)
- **Multi-carrier rate comparison**: Requires overlay solution
- **Advanced label customization**: May require third-party
- **EDI-based carrier integration**: Through OIC or middleware
- **LTL/FTL carrier management**: Through Oracle Transportation Management (OTM)

### Integration Architecture for Shipping
```
Oracle WMS Cloud
  |
  +-- Native SOAP --> UPS / FedEx / DHL (basic tracking + labels)
  |
  +-- Oracle TMS (OTM) --> Full rate shopping, carrier selection, route optimization
  |
  +-- Third-party overlay (ShipERP, ShipConsole, ProcessWeaver)
       --> Multi-carrier rate shopping, compliance, consolidation
```

## Competitive Positioning

| Aspect | Oracle WMS Cloud | SAP EWM | Manhattan Active WM |
|--------|-----------------|---------|---------------------|
| Architecture | Cloud-native SaaS | On-premise/private cloud | Cloud-native microservices |
| AI strength | Strong dynamic slotting/labor | Good (improving) | Strong optimization |
| UI/UX | Complex (6.5/10) | Traditional, complex | More intuitive |
| Best for | Oracle ecosystems | SAP ecosystems | Retail/3PL with modern UX |
| API style | REST (lgfapi) + Stage Interface | OData | REST microservices |

## Key Takeaways for Integration

1. **Primary API is lgfapi** (REST) -- entity module for CRUD, stage interface for bulk data integration
2. **Auth**: BasicAuth (simple) or OAuth 2.0 (Resource Owner Password or Authorization Code grant)
3. **No webhooks**: Must use polling or Oracle Integration Cloud for event-driven outbound
4. **No official SDK**: Raw HTTP calls only; Postman recommended for testing
5. **XML is default response format**; add `format=json` query param for JSON
6. **Rate shopping not native**: Requires TMS or third-party overlay
7. **Non-Oracle integration is expensive**: OIC middleware required, adds significant cost
8. **Real-time inventory API gap**: Repeatedly cited by e-commerce users as a critical missing capability

## Sources

- [WMS REST API Guide (Release 26A)](https://docs.oracle.com/en/cloud/saas/warehouse-management/26a/owmre/index.html)
- [Integration API Guide - Response Structure](https://docs.oracle.com/en/cloud/saas/warehouse-management/26a/owmap/response-structure.html)
- [lgfapi URL Format & Versioning](https://docs.oracle.com/en/cloud/saas/warehouse-management/26a/owmre/optional-trailing-slashes.html)
- [OAuth 2.0 Support for Integrations](https://docs.oracle.com/en/cloud/saas/warehouse-management/24a/owmap/oauth-2-0-support-for-integrations.html)
- [Authentication - Security Guide](https://docs.oracle.com/en/cloud/saas/warehouse-management/24b/owsec/authentication.html)
- [Zone Picking (Release 26A)](https://docs.oracle.com/en/cloud/saas/warehouse-management/26a/owmol/executing-pick-zone-tasks-in-the-rf.html)
- [Parcel Carrier Integration](https://docs.oracle.com/en/cloud/saas/warehouse-management/24d/owmap/parcel-carrier-integration.html)
- [Oracle Warehouse Management Cloud (oracle.com)](https://www.oracle.com/scm/logistics/warehouse-management/)
- [TrustRadius Pros & Cons](https://www.trustradius.com/products/oracle-warehouse-management-cloud/reviews?qs=pros-and-cons)
- [G2 Reviews](https://www.g2.com/products/oracle-oracle-warehouse-management-cloud/reviews)
- [Gartner Peer Insights](https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/oracle/product/oracle-warehouse-management-wms-cloud-logfire)
- [Oracle WMS Cloud Review 2025 (bestopschainai.com)](https://bestopschainai.com/warehouse-inventory/oracle-wms-cloud-review)
- [Gartner Magic Quadrant Leader 2024 (Oracle blog)](https://blogs.oracle.com/scm/oracle-leader-2024-gartner-magic-quadrant-warehouse-management-systems)
- [Parcel Manifest Configuration](https://docs.oracle.com/en/cloud/saas/warehouse-management/20d/owmol/user/topics/parcel_manifest_configuration.html)
- [Oracle WMS 9.0.0 Update (OAuth2 introduction)](https://www.oracle.com/webfolder/technetwork/tutorials/tutorial/cloud/scm/900-wms-wn.htm)
