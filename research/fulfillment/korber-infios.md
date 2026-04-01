# Korber/Infios (formerly HighJump) — Comprehensive Research

> Enterprise WMS with no public API. Integration via SFTP, SQL, ERP connectors.
> Research date: 2026-03-31

---

## 1. Overview & History

Complex acquisition history:
- **HighJump Software** — Founded 1984 as part of 3M. Mid-market WMS leader.
- **Accellos** — Acquired by HighJump in 2014 (added mid-market WMS)
- **Körber AG** — German industrial conglomerate, acquired HighJump in 2017
- **Körber Supply Chain** — Rebranded division housing WMS products
- **Infios** — Rebranded again ~2024 as Körber's supply chain software brand

**Products:**
- **Körber WMS (formerly HighJump)** — Core WMS for mid-to-enterprise warehouses
- **Körber WCS** — Warehouse control system for MHE/automation
- **Körber WES** — Warehouse execution system (orchestration layer)
- **K.Motion** — Cloud platform initiative

**Market position:** Mid-tier enterprise. Strong in manufacturing, distribution, 3PL. Less visible in pure eCommerce. [Source: https://www.koerber-supplychain.com/]

---

## 2. What It Does: Core Fulfillment Capabilities

### Pick Methods
- **Wave picking** — Traditional wave management with flexible wave rules
- **Batch picking** — Multi-order batch consolidation
- **Zone picking** — Zone-based with consolidation
- **Discrete picking** — Single-order
- **Cluster picking** — Cart-based
- **Voice picking** — Vocollect/voice-directed integration
- **RF scanning** — Mobile-directed picking workflows
- **Pick-to-light** — Integration with pick-to-light hardware
[Source: https://www.koerber-supplychain.com/solutions/warehouse-management/]

### Pack Optimization
- Directed packing with verification
- Cartonization
- Pack-to-order workflows
- VAS (value-added services) workstation management
- Custom packaging rules
[Source: https://www.koerber-supplychain.com/solutions/warehouse-management/]

### Shipping & Carrier Selection
- Multi-carrier shipping via integration (not native rate shopping)
- Label generation
- Manifest management
- ERP connector handles shipping in many deployments
- Integration with parcel shipping platforms (ShipStation, ProShip, ConnectShip)
[Source: https://www.koerber-supplychain.com/solutions/]

### Labor Management
- Basic labor tracking in WMS
- Task assignment and monitoring
- Productivity reporting
- Not a dedicated LMS module (less deep than Manhattan)
[Source: https://www.koerber-supplychain.com/solutions/warehouse-management/]

### Robotics Integration
- **Körber WCS** — Native warehouse control system for MHE
- Conveyor integration
- Sortation system integration
- ASRS communication
- AMR integration (partnerships with Locus, Fetch/Zebra)
- Körber has its own material handling division (separate from software)
[Source: https://www.koerber-supplychain.com/solutions/automation/]

---

## 3. Technical Documentation

### API Architecture
- **No public API documentation.** This is the primary integration challenge.
- Integration methods (in order of commonality):
  1. **SFTP/FTP** — File-based batch integration (CSV, XML, flat file)
  2. **SQL Server stored procedures** — Direct database integration (common in HighJump deployments)
  3. **REST endpoints** — Limited REST API exists but is not publicly documented
  4. **EDI** — Standard EDI transaction sets via VAN
  5. **ERP connectors** — Pre-built connectors for major ERPs

### Pre-Built ERP Connectors
- SAP (IDoc, RFC)
- Microsoft Dynamics (365, GP, NAV/BC)
- Oracle E-Business Suite
- Infor (SyteLine, CloudSuite)
- NetSuite
[Source: https://www.koerber-supplychain.com/solutions/warehouse-management/ — integration section]

### Developer Portal
- **None.** No public developer portal, API reference, or SDK.
- All integration documentation is provided during implementation under NDA.
- Requires Körber professional services or SI partner engagement.

### WCS/WES Interfaces
- Körber WCS communicates with MHE via:
  - PLC protocols (TCP/IP-based)
  - OPC-UA
  - Proprietary interfaces per MHE vendor
  - REST/SOAP for higher-level orchestration
[Source: https://www.koerber-supplychain.com/solutions/automation/]

---

## 4. Authentication & Integration Patterns

### Authentication
- **Not publicly documented**
- SQL Server: Database credentials for stored procedure integration
- REST (where available): Token-based auth (proprietary)
- SFTP: SSH key or username/password
- ERP connectors: Per-ERP auth mechanisms

### Common Integration Patterns
1. **SFTP flat file exchange** — Most common. Scheduled file drops for orders-in, inventory-out, shipment confirmations. CSV or XML format.
2. **SQL Server integration** — Direct stored procedure calls for real-time integration (requires SQL Server access, common in on-prem deployments)
3. **ERP connector** — Pre-built bidirectional sync with ERP system
4. **EDI** — 940/945/943/944/947 via VAN (SPS Commerce, TrueCommerce)
5. **Middleware** — MuleSoft, Boomi, or custom middleware layer

### Access Path
- Must be a Körber customer or partner
- Integration scope defined during implementation project
- Professional services required for custom integrations
[Source: Industry knowledge, Körber partner materials]

---

## 5. Help Centers, Knowledge Bases & Community

- **Körber Customer Portal** — Support tickets, documentation (login required) [Source: https://www.koerber-supplychain.com/support/]
- **No public knowledge base**
- **No public community forum**
- **Support:** Phone and email support, dedicated CSMs for enterprise
- **Partner network:** Implementation partners (Accenture, Deloitte, various regional SIs)
- **Elevate Conference** — Annual user conference [Source: https://www.koerber-supplychain.com/events/]
- **Training:** Körber Academy (customer training programs)

---

## 6. Carrier Integration Capabilities

- Not natively a shipping platform — relies on integrations
- Common approach: WMS → Shipping platform (ProShip, ConnectShip, ShipStation) → Carrier
- ERP connector handles shipping for many deployments
- Label generation via shipping platform integration
- Carrier-specific manifest formats supported via configuration
- Returns processing supported in WMS (carrier label gen via shipping partner)
[Source: https://www.koerber-supplychain.com/solutions/ — shipping/fulfillment section]

---

## 7. Pricing Model

- **Not publicly available.** Enterprise sales engagement required.
- Licensing models:
  - Perpetual license + annual maintenance (legacy HighJump model)
  - SaaS subscription (newer K.Motion cloud deployments)
- Pricing factors: warehouse count, user count, modules, transaction volume
- Estimated range: $50K–$500K+ annually depending on scale (industry estimates)
- Implementation: $100K–$1M+ via SI partners
[Source: Industry estimates, Gartner analysis]

---

## 8. Pros & Cons from Real Users

### Pros
- **Highly configurable** — Adaptable to complex warehouse processes without custom code [Source: https://www.g2.com/products/korber-wms/reviews]
- **Strong in manufacturing/distribution** — Well-suited for complex inventory (lot, serial, expiry)
- **Mature product** — 35+ years of development, battle-tested
- **WCS/WES capabilities** — Native automation control (conveyor, sortation, ASRS)
- **ERP connectors** — Solid pre-built integrations for major ERPs
- **Flexible deployment** — On-prem, hosted, or cloud (K.Motion)
- **Multi-site capable** — Handles multi-warehouse operations

### Cons
- **No public API** — Major blocker for modern integration patterns [Source: https://www.g2.com/products/korber-wms/reviews]
- **Legacy technology base** — Windows/.NET/SQL Server architecture, not cloud-native
- **Confusing brand history** — HighJump → Körber → Infios rebrand causes market confusion
- **Slow innovation** — Large enterprise pace of development
- **Expensive implementation** — Requires SI partners, long deployment cycles [Source: Reddit r/supplychain — Körber/HighJump discussions]
- **UI/UX dated** — Desktop-oriented interface, mobile experience lags
- **Documentation scarcity** — Difficult to evaluate without vendor engagement
- **Vendor lock-in** — Deep SQL Server integration makes switching costly

[Source: https://www.g2.com/products/korber-wms/reviews]
[Source: https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/koerber]
[Source: Reddit r/supplychain, r/warehousing — HighJump/Körber experience threads]

---

## 9. Implications for Omnifill Integration

### Integration Feasibility: LOW
- No public API documentation
- No developer portal or sandbox
- Integration requires vendor relationship and likely NDA
- Primary integration paths (SFTP, SQL) are legacy patterns

### Recommended Approach
1. **SFTP file-based** as initial integration (most portable, doesn't require deep vendor access)
2. **EDI** for standardized transaction sets (if customer uses EDI VAN)
3. **Explore SQL Server stored procedures** for existing deployments (requires DB access)
4. **Middleware layer** — Use iPaaS with any existing Körber connectors
5. **Long-term:** Engage Körber partnership team if Omnifill needs first-class WMS integration

### Key Challenges
- Cannot prototype or test without customer deployment access
- Each deployment is highly customized
- Integration patterns vary significantly between deployments
- No standard API contract to code against

---

## Sources

- https://www.koerber-supplychain.com/
- https://www.koerber-supplychain.com/solutions/warehouse-management/
- https://www.koerber-supplychain.com/solutions/automation/
- https://www.koerber-supplychain.com/support/
- https://www.g2.com/products/korber-wms/reviews
- https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/koerber
- https://www.capterra.com/p/73479/HighJump-WMS/reviews/
- Reddit r/supplychain — HighJump/Körber WMS discussion threads
- Reddit r/warehousing — Körber implementation experiences
