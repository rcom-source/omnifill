# Warehouse Robotics Platforms Research

Comprehensive research on five warehouse robotics platforms covering capabilities,
APIs, integrations, authentication, user feedback, and pricing.

---

## 1. 6 River Systems (Ocado Intelligent Automation)

### What It Does

6 River Systems builds **Chuck**, a collaborative AMR (Autonomous Mobile Robot) for
warehouse picking operations. Chuck is a **person-to-goods** robot -- it does not
pick items itself but guides human associates through optimized pick paths, carrying
picked items on its shelves.

**Robot types and capabilities:**
- **Chuck AMR**: LiDAR + 3D camera array with SLAM navigation
- Collaborative picking (human follows robot, robot carries goods)
- Zone-based and multi-order batch picking
- Putaway, replenishment, and sorting workflows
- Digital Twin simulation for layout optimization before deployment

**Automation model:** AMR, collaborative (not autonomous picking). Associates scan
items and place on Chuck; Chuck navigates to next location or to pack stations.

**Ownership history:** Founded by ex-Kiva Systems engineers. Acquired by Shopify
(2019), sold to Ocado Group (2024) after Shopify took a significant loss. Now
branded as **Ocado Intelligent Automation / OMRS (Ocado Mobile Robot System)**.

### Technical Documentation & APIs

**Integration architecture:**
- **RESTful API** (JSON over HTTPS) -- API-first design
- WMS-agnostic: maintains WMS as system of record
- 6RS cloud WES sits between WMS and robot fleet
- Bidirectional data flow: orders from WMS -> cloud WES -> Chuck fleet -> confirmations back

**WES (Warehouse Execution System):**
- Cloud-hosted orchestration layer
- Real-time task dispatch and path optimization
- Over-the-air (OTA) firmware updates with signed verification
- Analytics dashboard for throughput monitoring

**Developer documentation:**
- API documentation provided during implementation engagement
- No publicly accessible developer portal or SDK identified
- Implementation guided by 6RS professional services team
- VDA 5050 standard support mentioned for future multi-vendor fleet interoperability

### Authentication & Security

- **TLS 1.2+** encryption for all data in transit
- **WPA2/WPA3-Enterprise** WiFi authentication required
- **VLAN segmentation** isolating robot traffic from corporate networks
- **SOC 2 Type II** compliance for cloud operations
- Signed OTA software updates

### Help Centers & Community

- Official support via implementation and customer success teams
- FAQ available at https://6river.com/faq/
- No public developer community or forums identified
- Knowledge base appears to be customer-only access
- Limited Reddit/community discussion; most feedback is in industry publications

### Pros and Cons (User & Industry Feedback)

**Pros:**
- 2-3x productivity increase in picking operations
- Fast deployment: 8-12 weeks (vs. 12+ months for fixed automation)
- RaaS model eliminates large CapEx
- ISO 3691-4:2020 safety compliance
- Digital Twin pre-deployment simulation reduces risk
- Deployed in 100+ warehouses with 70+ customers
- Minimal training required for associates

**Cons:**
- **Critically dependent on enterprise-grade WiFi** -- network inadequacy is the primary failure cause
- Requires redundant internet connectivity to cloud WES
- Person-to-goods model: not suitable for fully autonomous operations
- Cloud dependency creates single point of failure risk
- Limited public documentation; integration requires vendor engagement
- Ownership transitions (Shopify -> Ocado) create uncertainty

### Pricing Model

**Robots-as-a-Service (RaaS)** subscription:
- Converts CapEx to OpEx
- Pricing based on fleet size and software tier
- No published pricing; requires sales engagement
- Includes hardware, software, maintenance, and support

### WMS Integration Capabilities

- **WMS-agnostic** design -- works with any WMS via REST API
- JSON/HTTPS transport with adapter layer for other message formats
- Compatible with COTS and cloud WMS platforms
- Integration with enterprise ERP, WMS, and MES systems
- WES layer handles execution while WMS remains system of record

**Sources:**
- https://6river.com/
- https://6river.com/meet-chuck/
- https://bestopschainai.com/warehouse-inventory/6-river-systems-ocado-robotics-review
- https://www.logiwa.com/blog/6-river-robotics
- https://www.softwareadvice.com/scm/6-river-systems-chuck-profile/

---

## 2. Locus Robotics

### What It Does

Locus Robotics builds **autonomous mobile robots (AMRs)** for warehouse picking,
operating through its **LocusONE** software platform. The robots are collaborative
(person-to-goods), navigating autonomously to pick locations where human associates
pick items and place them on the robot.

**Robot types and capabilities:**
- **LocusBot** family of AMRs for each-picking and case-picking
- Collaborative goods-to-person picking
- Multi-bot coordination for batch and zone picking
- Sortation and putaway workflows
- Interleaving of pick, replenishment, and count tasks

**Automation model:** AMR fleet managed by LocusONE WES. Robots travel to pick
faces, associates pick items, robots transport to pack/sort stations. AI optimizes
mission routing and task assignment.

### Technical Documentation & APIs

**LocusONE Platform:**
- Cloud-based Warehouse Execution System (WES)
- Sits between WMS (system of record) and physical floor
- Real-time execution decisions: multi-bot coordination, dynamic task reallocation
- Analytics dashboard with throughput KPIs

**LocusConnect Middleware:**
- REST API-first architecture
- Universal translator between WMS and LocusONE
- Bidirectional data flow: orders in, confirmations out
- Supports embedded calls to custom endpoints within workflows
- Pre-built connectors for major WMS platforms
- Custom API set for homegrown/highly-customized WMS

**Integration timeline:** Standard 6-8 week deployment including workflow design,
WMS integration, physical deployment, and training.

**Developer documentation:**
- No public developer portal identified
- Documentation described as a gap by users: "discovering new features by accident"
- Self-service resources for managers reported as insufficient
- Recommended: bi-weekly calls with account managers for feature discovery

### Authentication & Security

- **OAuth 2.0** for API endpoint authentication
- **SSO (Single Sign-On)** support for enterprise environments
- **2FA (Two-Factor Authentication)** for manager portal (mandatory recommended)
- **RBAC (Role-Based Access Control)** for data visibility by operational scope
- **TLS 1.2+** for data in transit
- **AES-256** encryption at rest
- **SOC 2 Type II** certified
- **WPA2/WPA3-Enterprise** WiFi security
- **VLAN segmentation** recommended for robot fleet
- **ISO 3691-4** compliance for autonomous vehicle safety
- Shared responsibility model: vendor secures platform, customer secures network

### Help Centers & Community

- Implementation support team during deployment
- 24/7 remote support included in RaaS subscription
- Remote diagnostics capability (can diagnose issues and ship replacements)
- Gartner Peer Insights reviews available
- G2 reviews available (https://www.g2.com/products/locus-locus/reviews)
- No public developer community or forums identified

### Pros and Cons (User & Industry Feedback)

**Pros:**
- 2-3x productivity increase (60-90 UPH baseline -> 250+ UPH)
- 99.9%+ order accuracy (94% reduction in mis-picks)
- Training time under 15 minutes for new associates
- Gamified associate interface drives engagement
- Flexible seasonal scaling (add/remove bots as needed)
- Fast deployment (6-8 weeks)
- Integrates with 50+ WMS systems
- SOC 2 Type II compliance

**Cons:**
- **Steep learning curve for managers** using LocusONE platform
- Manager UX described as "a black box sometimes"
- Documentation and self-service resources insufficient
- Support resolution can have long lead times
- **High long-term TCO risk**: per-pick RaaS fees become "astronomical" during peak periods
- VP of Finance (3PL): "Great for Year 1... in Year 3 RaaS payments are a massive line item"
- Not cost-effective for small-to-midsize businesses
- Customization options limited, hindering adaptability
- Update sprints not frequent enough

### Pricing Model

**Robots-as-a-Service (RaaS)** subscription:
- No public pricing; custom quotes required
- Monthly recurring fee based on: robot count, facility size, integration complexity
- Includes hardware, software, maintenance, 24/7 support
- No large upfront CapEx
- ROI typically within 12-24 months
- **Warning:** Long-term TCO can exceed expectations, especially during peak volume periods

### WMS Integration Capabilities

**Pre-built connectors for:**
- Manhattan Associates
- Blue Yonder (JDA)
- SAP EWM
- Oracle NetSuite
- Korber
- Barcodes
- Logiwa
- Thomax
- Peak
- Made4net
- Tecsys

**Also compatible with:**
- Any modern WMS via LocusConnect REST API
- Homegrown/custom WMS via full custom API set
- ERP systems (SAP, Oracle)
- Sortation, packaging, and other automation systems

**Sources:**
- https://locusrobotics.com/locusone/automated-warehouse-software/integrations
- https://locusrobotics.com/locusone/automated-warehouse-software
- https://bestopschainai.com/warehouse-inventory/locus-robotics-review-ai-warehouse
- https://www.g2.com/products/locus-locus/reviews
- https://www.gartner.com/reviews/market/multiagent-orchestration-platforms/vendor/locus-robotics/product/locusone

---

## 3. AutoStore

### What It Does

AutoStore is a **robotic cube storage** automated storage and retrieval system (AS/RS).
It uses a dense grid of stacked bins with robots operating on top of the grid to
retrieve and deliver bins to human operators at workstation ports. This is a true
**goods-to-person** system.

**System components:**
- **Grid**: Aluminum framework holding stacked inventory bins
- **Robots (R5, R5+, B1)**: Travel on top of grid, dig through bin stacks to retrieve target bins
- **Ports (ConveyorPort, CarouselPort, SwingPort, RelayPort, PickUpPort)**: Workstations where bins are presented to operators
- **Controller**: Software managing robot fleet, routing, and task orchestration
- **Router**: Algorithm engine optimizing robot movement in real-time

**Automation model:** Fixed grid infrastructure, not AMR. Robots are confined to the
grid. Goods-to-person: bins are brought to operators at ports for picking/putaway.
Up to 4x storage density increase vs. manual warehouses.

### Technical Documentation & APIs

**Two integration interfaces:**

1. **XML API via HTTP POST:**
   - Primary control interface between WCS and AutoStore Router
   - Task Interface: WCS sends task groups (sets of bins to pick together),
     sequenced by priority, handling requirements, shipment properties
   - Bin Interface: manages Preparation Queue (bins needing accessibility)
     and Port Queue (bins due for delivery to specific workstations)
   - Handles conflict resolution when multiple workstations request same bin

2. **Log Publisher (TCP/IP Streaming):**
   - TCP/IP server delivering event stream to connected clients
   - CSV format, comma-separated values
   - Human-readable (viewable via telnet)
   - Event tags with optional parameters, terminated by CRLF
   - Provides real-time system state snapshots on client connection
   - Used for monitoring, analytics, and event-driven integrations

**CubeVerse Platform (launched 2025-2026):**
- Unified software platform for design, operations, and analytics
- Standardized APIs providing single integration layer
- Cloud-based data and orchestration
- Common data architecture (unified source of truth)
- Connects 10+ data sources and 20+ proprietary AI models
- CubeVerse is NOT a WCS or WES -- works alongside any WES/WMS/ERP
- Reduces integration complexity with reusable integration tools

**Controller/Router Software:**
- Manages robot fleet movement and task optimization
- Advanced path-planning algorithms
- Real-time conflict resolution for robot routing

### Authentication & Security

- **TLS 1.2+** for data-in-transit encryption
- **AES-256** for data-at-rest encryption
- **Role-Based Access Control (RBAC)** and multi-factor authentication (CubeVerse)
- **Secure boot processes** for hardware/firmware
- **Shared security responsibility:** AutoStore secures hardware/firmware;
  WMS integration partner handles SOC 2 Type II and ISO 27001 certifications
- End-to-end encryption in CubeVerse (built with Databricks)
- AI trained only on aggregated operational/simulation data, never customer inventory

### Help Centers & Community

- Documentation provided through certified integration partners
- AutoStore partner network: https://www.autostoresystem.com/partners
- No public developer portal or API reference identified
- Integration partner quality is critical (Swisslog, Dematic, Korber, Element Logic, Kardex)
- AutoStore Insights knowledge base: https://www.autostoresystem.com/insights/

### Pros and Cons (User & Industry Feedback)

**Pros:**
- **4x storage density** vs. manual warehouses
- **99.7% system uptime** globally (MTBF 3,000+ hours)
- 99.8%+ order accuracy with goods-to-person model
- 35-50% labor reduction in picking operations
- 100% access to stock, 24/7 operability
- Modular and scalable (add robots/bins/ports incrementally)
- Proven at scale: PUMA targeting 200K daily orders
- ROI typically 2.6-3.7 years (Forrester: 79% ROI over 3 years)

**Cons:**
- **High capital investment** (entry-level systems start in the low millions)
- Partner-dependent success: quality of integrator is critical variable
- Complex floor requirements: 1,500-3,000 kg/m2 structural load capacity
- Fire safety compliance required (sprinkler or hypoxic air systems)
- Grid system requires dedicated footprint (less layout flexibility than AMRs)
- Maintenance access challenging (robots on top, bins stacked vertically)
- Annual maintenance: 2-5% of initial system cost
- No standard list pricing; highly variable by configuration

### Pricing Model

**Two models:**

1. **Traditional CapEx purchase:**
   - Entry-level systems: low millions USD
   - Cost depends on grid size, robot count, port quantity/type, integration partner fees
   - Annual maintenance: 2-5% of initial system cost

2. **Pio Pay-Per-Pick (for SMBs, launched 2024-2025):**
   - Fee per individual item picked
   - AutoStore (via Pio) owns and maintains robots, ports, and software
   - Customer purchases only product bins and grid frames
   - Lowers barrier to entry for smaller operations

### WMS Integration Capabilities

**Integration partners providing WCS:**
- Swisslog
- Dematic
- Korber
- Element Logic
- Kardex (FulfillX software)
- StrongPoint (Order Fulfillment Platform)
- 4SiGHT

**Compatible WMS platforms (via partners):**
- Manhattan Associates
- SAP
- Oracle
- NetSuite
- HighJump (now Korber)
- Any WMS via XML API + WCS middleware

**Integration pattern:**
ERP -> WMS -> WCS (partner) -> AutoStore Router (XML API / HTTP POST)
AutoStore -> Log Publisher (TCP/IP CSV) -> WCS -> WMS (confirmations/events)

**Sources:**
- https://www.autostoresystem.com/system/cubeverse-platform
- https://www.autostoresystem.com/insights/warehouse-control-systems-wcs-ultimate-guide
- https://bestopschainai.com/warehouse-inventory/autostore-review-definitive
- https://www.autostoresystem.com/partners
- https://www.kardex.com/en/technology/autostore/kardex-fulfillx

---

## 4. Berkshire Grey

### What It Does

Berkshire Grey builds **AI-powered robotic picking, sorting, and packing systems**
for warehouse fulfillment. Unlike AMR-based systems, Berkshire Grey focuses on
**robotic manipulation** -- physically picking and sorting items with robotic arms
using computer vision and AI.

**Product lines:**
- **Robotic Product Sortation (RPS/RPSi):** AI-powered robotic arms sorting up to
  2,400 items/hour with dynamic gripper selection
- **Robotic Shuttle Put Wall (RSPW):** Fleet of fast shuttle robots automating
  order consolidation at 3x manual speed
- **Robotic Pick & Pack:** AI-powered piece-picking with intelligent end-of-arm
  tooling (suction, compliant finger, hybrid grippers)
- **End-of-Arm Tooling (EOAT):** Proprietary intelligent grippers selected by AI
  based on item properties (polybags, apparel, electronics, etc.)

**Automation model:** Fixed automation with robotic manipulation. Not AMR-based.
AI computer vision identifies items without pre-training. Handles diverse SKU
profiles including difficult items (polybags, deformable goods).

**Ownership:** Acquired by SoftBank Group Corp. (July 2023). Also has formal
partnership with Kardex for AutoStore integration (September 2024).

### Technical Documentation & APIs

**Integration architecture:**
- **RESTful API using JSON** for WMS/ERP integration
- Functions as a **Warehouse Execution System (WES)**
- WMS remains "strategic manager of inventory"
- WES is the "real-time fulfillment orchestration engine"
- Takes order batches from WMS, optimizes execution on floor
- Manages robotic queues and orchestrates physical movement

**WES capabilities:**
- Real-time order batch optimization
- Dynamic task interleaving for maximum throughput
- Robotic queue management with intelligent failover
- Automatic rerouting on hardware failure
- Peak throughput prioritization during multi-robot operations
- Real-time analytics dashboard with actionable KPIs

**Developer documentation:**
- "Well-documented RESTful API using JSON" per industry reviews
- No public developer portal, SDK, or API reference identified
- Implementation supported by detailed planning workshops
- Integration teams described as "strategic partners" with deep supply chain knowledge
- Not plug-and-play: 4-8 weeks minimum integration planning

### Authentication & Security

- **OAuth 2.0** token-based authentication for API access
- **TLS 1.3** encryption for all data in transit
- **Role-Based Access Controls (RBAC)** with granular permissions
- **API keys** with limited, specific permissions (not universal access)
- **SOC 2 Type II** certified (security, availability, confidentiality)
- **99.5%+ uptime** with redundant high-availability architecture
- OSHA guidelines compliance for automated systems
- ANSI/RIA R15.06 robotic safety standard
- Light curtains, emergency stops, controlled-speed zones for cobot areas

### Help Centers & Community

- Implementation teams with deep supply chain expertise
- Planning workshops during integration
- Support praised as "strategic partners" not just technical support
- No public community forums or developer community identified
- Limited user reviews on public platforms (niche enterprise product)

### Pros and Cons (User & Industry Feedback)

**Pros:**
- **SKU versatility:** AI vision handles diverse products (polybags, apparel,
  electronics) without pre-training per item -- key differentiator
- 2-3x throughput increase
- Up to 50% reduction in manual labor
- 99.8%+ order accuracy
- Fleet learning: shared intelligence across global robot fleet
- SOC 2 Type II certified security
- Flexible deployment with RaaS option
- Partnership with Kardex enables AutoStore + robotic picking ("one-touch" fulfillment)

**Cons:**
- **Significant capital requirements** (millions for large deployments)
- **Complex integration** -- not plug-and-play, requires deep WMS/ERP integration
- Requires capable IT and operations team
- Demands fundamental changes to operational workflows
- 4-8 weeks minimum for integration planning (plus implementation)
- Organizational change management challenges
- Limited public documentation
- Niche market: fewer reference customers than AMR vendors

### Pricing Model

**Two models:**

1. **Capital Expenditure (CapEx):** Traditional upfront purchase with full ownership.
   Large deployments typically involve millions of dollars.

2. **Robotics-as-a-Service (RaaS):** Subscription converting costs to OpEx.
   Recommended for piloting specific warehouse areas to de-risk investment.

- No published standard pricing
- Typical ROI payback: 14-18 months for verified implementations
- Labor cost reduction: 30-50% for automated processes

### WMS Integration Capabilities

**Compatible WMS platforms:**
- SAP (including SAP EWM)
- Oracle
- NetSuite
- Manhattan Associates
- Blue Yonder

**Integration pattern:**
WMS (order batches) -> Berkshire Grey WES (REST API/JSON) -> Robotic systems
Robotic systems -> WES (confirmations, analytics) -> WMS

**Additional integration:**
- Conveyor and sortation system interfaces
- Plant PLC connectivity
- Kardex AutoStore integration (since September 2024)

**Sources:**
- https://www.berkshiregrey.com/
- https://www.berkshiregrey.com/technologies/ai-software/
- https://bestopschainai.com/warehouse-inventory/berkshire-grey-review-ai-robotics
- https://bestopschainai.com/warehouse-inventory/berkshire-grey-overview-features
- https://logisticsviewpoints.com/2021/12/01/a-first-hand-look-at-berkshire-greys-warehouse-robotic-solutions/

---

## 5. Fetch Robotics (Zebra Technologies)

> **CRITICAL NOTE (2025-2026):** Zebra Technologies is winding down its Fetch
> Robotics AMR division. Most robotics staff will be let go by end of 2025, with
> ~25% retained until March 2026 to manage existing deployments. Zebra is seeking
> a buyer for the division. The future of FetchCore and existing customer
> deployments is uncertain.

### What It Does

Fetch Robotics builds **autonomous mobile robots (AMRs)** for warehouse material
movement, picking assistance, and data capture. The robots are managed by
**FetchCore**, a cloud-based robotics platform.

**Robot types:**
- **CartConnect100/500:** Cart-based transport AMRs
- **HMIShelf:** Interactive shelf robot with display
- **FlexShelf:** Flexible shelving AMR for picking workflows
- **RollerTop:** Conveyor-top AMR for automated handoffs
- **PalletTransport1500:** Heavy-duty pallet-moving AMR
- **Freight500/1500:** General material transport AMRs
- **TagSurveyor:** RFID inventory tracking robot (autonomous cycle counts)

**Automation model:** AMR fleet for collaborative picking, material transport,
putaway, replenishment, cross-docking, and waste removal. Person-to-goods for
picking; autonomous for transport. 3D cameras and laser scanners for obstacle
avoidance.

### Technical Documentation & APIs

**FetchCore Cloud Platform:**
- Cloud-based fleet management and orchestration
- Warehouse annotation (maps pick locations without QR codes)
- Wave management for order batching
- Pick heatmap analytics
- Forklift detection for safety
- Advanced fulfillment analytics

**FetchCore APIs:**
- REST APIs for connecting AMRs with external applications (WMS, WCS, ERP, MES)
- Presented at Zebra DevCon 2023: "FetchCore APIs, Workflows and IoT Integration"
- Workflow Builder: drag-and-drop visual workflow editor within FetchCore
- Supports custom automation workflow creation and modification
- IoT integration capabilities

**Fetch Research Edition (ROS-based, open-source):**
- ROS (Robot Operating System) API for research robots
- Open-source components: https://github.com/ZebraDevs/fetch_ros
- Not the same as commercial FetchCore API

**Developer documentation:**
- DevCon presentations (2023) provide API overview
- No publicly accessible commercial API reference documentation found
- FetchCore documentation appears to be customer/partner-only
- Zebra developer portal integration mentioned but not publicly detailed
- Research edition docs at: https://docs.fetchrobotics.com/api_overview.html

### Authentication & Security

- Cloud-based platform (FetchCore hosted by Zebra)
- Enterprise cloud security (specific auth methods not publicly documented)
- No-go zone configuration for operational safety
- Dynamic obstacle avoidance and overhang detection
- Integration with Zebra's broader enterprise security ecosystem

### Help Centers & Community

- Zebra support infrastructure (while operational)
- FetchCore cloud dashboard for remote monitoring
- GitHub for open-source ROS components: https://github.com/ZebraDevs/fetch_ros
- Limited community given wind-down announcement
- Existing deployments supported through March 2026

### Pros and Cons (User & Industry Feedback)

**Pros:**
- Up to 3x productivity increase in fulfillment operations
- 50% faster than some competing fulfillment AMRs
- Broad robot portfolio (8 models covering diverse workflows)
- Cloud-based management enables remote operations
- Drag-and-drop workflow builder (low-code)
- No QR codes needed (warehouse annotation feature)
- RaaS subscription option
- RFID TagSurveyor for automated inventory tracking (unique capability)
- Integration with broader Zebra ecosystem (wearables, scanners, printers)

**Cons:**
- **CRITICAL: Zebra is winding down the division** (2025-2026)
- Future support and software updates highly uncertain
- Customer deployments at risk if no buyer found
- FetchCore cloud dependency: if Zebra shuts down servers, robots lose orchestration
- $290M acquisition (2021) resulted in strategic failure
- Limited public API documentation
- Developer ecosystem never fully matured

### Pricing Model

**Robots-as-a-Service (RaaS):**
- Subscription model for on-demand automation
- No published pricing
- Includes hardware, FetchCore software, and support

**Given the wind-down, new RaaS commitments carry significant risk.**

### WMS Integration Capabilities

**FetchCore integrates with:**
- Leading WMS and WES platforms (specific list not publicly documented)
- ERP systems
- Zebra peripherals (wearable computers, scanners, printers)
- Industrial control systems via REST API

**Integration features:**
- Warehouse annotation eliminates need for physical markers
- Automatic adjustment to reslotting within warehouse
- Wave management and batch optimization
- Fulfillment workflow orchestration across labor and robots

**Zebra Symmetry Fulfillment (launched early 2025):**
- Combined AMRs + wearable tech + software + analytics
- Robot-assisted picking solution
- May represent the last major product update before wind-down

**Sources:**
- https://fetchrobotics.com/
- https://cssi.com/fetch-robotics/
- https://github.com/ZebraDevs/fetch_ros
- https://www.therobotreport.com/zebra-technologies-winding-down-fetch-based-mobile-robot-group/
- https://www.thenewwarehouse.com/2025/02/10/561-maximizing-profits-with-fewer-robots-the-breakthrough-from-zebra-robotics-in-amr-utilization/

---

## Cross-Platform Comparison Summary

| Feature | 6 River Systems | Locus Robotics | AutoStore | Berkshire Grey | Fetch Robotics |
|---------|----------------|----------------|-----------|----------------|----------------|
| **Type** | AMR (collaborative) | AMR (collaborative) | Cube AS/RS (goods-to-person) | Robotic arms (pick/sort) | AMR (transport + picking) |
| **API** | REST/JSON | REST (LocusConnect) | XML/HTTP POST + TCP/IP CSV | REST/JSON | REST (FetchCore) |
| **Auth** | TLS 1.2+, WPA2/3 | OAuth 2.0, SSO, 2FA | TLS 1.2+, AES-256, RBAC | OAuth 2.0, TLS 1.3, RBAC | Cloud-based (undocumented) |
| **WMS Agnostic** | Yes | Yes (50+ WMS) | Yes (via WCS partner) | Yes | Yes |
| **Pricing** | RaaS | RaaS | CapEx or Pay-Per-Pick | CapEx or RaaS | RaaS |
| **Deploy Time** | 8-12 weeks | 6-8 weeks | Months (infrastructure) | 4-8 weeks planning + impl | Weeks (cloud-based) |
| **Productivity** | 2-3x | 2-3x (250+ UPH) | 35-50% labor reduction | 2-3x, 50% labor reduction | Up to 3x |
| **Key Risk** | Ocado ownership transition | High long-term TCO | High CapEx, partner dependency | High CapEx, complex integration | **Division being shut down** |
| **SOC 2** | Yes (Type II) | Yes (Type II) | Via partner | Yes (Type II) | Unknown |
| **Public API Docs** | No | No | No (partner-mediated) | No | No (research edition only) |

### Key Observations for Omnifill Integration

1. **No public APIs:** None of these platforms offer publicly accessible API
   documentation or developer portals. Integration requires vendor/partner
   engagement and likely NDA-protected documentation.

2. **WES pattern dominant:** Most platforms (6RS, Locus, Berkshire Grey) position
   themselves as WES layers between WMS and physical execution. This aligns well
   with Omnifill's abstraction layer approach.

3. **AutoStore is different:** Uses XML/HTTP POST rather than REST/JSON, and
   requires a WCS middleware partner. Integration would go through the WCS partner,
   not AutoStore directly.

4. **Fetch Robotics risk:** Given Zebra's wind-down, investing in Fetch integration
   is high-risk. Monitor for acquisition news.

5. **Authentication convergence:** OAuth 2.0 + TLS is the standard pattern for
   the REST-based systems (Locus, Berkshire Grey). AutoStore defers security to
   integration partners.

6. **RaaS model implications:** Most platforms use subscription pricing, meaning
   the robotics vendor maintains ongoing system access. This may provide
   integration leverage (vendor motivation to support API connectivity).
