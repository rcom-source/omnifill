# Softeon — Comprehensive Research

> WMS + WES platform. Strong in fulfillment optimization and automation orchestration.
> Research date: 2026-03-31

---

## 1. Overview & History

Softeon is a supply chain software company founded in 1999, headquartered in Reston, VA. Provides WMS, WES, and supply chain execution solutions. Positioned as a mid-to-enterprise WMS with particular strength in fulfillment optimization and warehouse execution.

**Products:**
- **Softeon WMS** — Core warehouse management system
- **Softeon WES** — Warehouse execution system (orchestration of automation)
- **Softeon Distributed Order Management (DOM)** — Order routing and orchestration
- **Softeon Supply Chain Execution** — Broader supply chain platform

**Market position:** Mid-market to enterprise. Strong in retail, eCommerce, 3PL. Recognized in Gartner Magic Quadrant for WMS (Visionary/Challenger). Differentiated by strong WES capabilities. [Source: https://www.softeon.com/about/]

---

## 2. What It Does: Core Fulfillment Capabilities

### Pick Methods
- **Wave picking** — Configurable wave rules, dynamic wave building
- **Waveless/streaming** — Continuous demand-driven release
- **Batch picking** — Multi-order batch with sort
- **Zone picking** — Zone-based with consolidation
- **Cluster picking** — Cart-based multi-order
- **Discrete picking** — Single-order for priority
- **Voice picking** — Vocollect integration
- **Pick-to-light** — Light-directed picking integration
- **Goods-to-person** — ASRS/AMR-driven picks via WES
[Source: https://www.softeon.com/solutions/warehouse-management-system/]

### Pack Optimization
- **Advanced cartonization** — Pre-pack box selection optimization
- Pack verification via scanning
- Directed packing workflows
- Multi-line consolidation
- Custom packaging rules
- VAS (kitting, gift wrap, inserts)
- Dimensional weight optimization
[Source: https://www.softeon.com/solutions/warehouse-management-system/]

### Shipping & Carrier Selection
- Multi-carrier parcel management
- Rate shopping
- Carrier selection rules engine
- Label generation
- Manifest management
- Small parcel + LTL
- Integration with shipping platforms
[Source: https://www.softeon.com/solutions/]

### Labor Management
- Task management and assignment
- Productivity tracking per employee
- Performance dashboards
- Engineered labor standards (basic)
- Not as deep as Manhattan's dedicated LMS
[Source: https://www.softeon.com/solutions/warehouse-management-system/]

### Robotics Integration — KEY DIFFERENTIATOR
- **Softeon WES** is the standout here — native automation orchestration
- AMR integration (Locus Robotics, 6 River Systems, Fetch/Zebra, inVia)
- ASRS integration (AutoStore, Dematic, Swisslog, OPEX)
- Conveyor and sortation control
- Put-wall integration
- Robotic arm integration
- **WES orchestrates work between human workers and automation systems**
- Single pane of glass for manual + automated workflows
[Source: https://www.softeon.com/solutions/warehouse-execution-system/]

---

## 3. Technical Documentation

### API Architecture
- **REST APIs** — Available for integration
- **SOAP/XML** — Also supported for enterprise integrations
- **No public developer portal** — API documentation provided during implementation
- **Middleware support** — Pre-built connectors for MuleSoft, Dell Boomi
- **EDI** — Standard transaction sets supported

### WCS/WES Interfaces — NOTABLE
- Softeon WES provides standardized interfaces to automation:
  - **AMR vendors:** REST API integration with fleet management systems
  - **ASRS:** Proprietary protocols per vendor (AutoStore Port API, Dematic WCS)
  - **Conveyors:** PLC communication, OPC-UA
  - **Sortation:** Real-time sort induction control
  - **Put-walls:** Light-directed put integration
  - **Robotic arms:** Task dispatch via vendor APIs
[Source: https://www.softeon.com/solutions/warehouse-execution-system/]

### Developer Resources
- No public API documentation
- No public SDK or client libraries
- Integration specs shared under NDA during implementation
- Professional services team handles custom integrations

---

## 4. Authentication & Integration Patterns

### Authentication
- Not publicly documented
- Token-based auth for REST APIs (proprietary)
- WS-Security for SOAP
- Credentials managed per deployment

### Common Integration Patterns
1. **ERP integration** — SAP, Oracle, Microsoft Dynamics, NetSuite
2. **eCommerce** — Shopify, Magento, Salesforce Commerce Cloud
3. **Marketplace** — Amazon, Walmart, Target
4. **Shipping** — Multi-carrier platforms
5. **File-based (SFTP)** — Batch CSV/XML exchange
6. **EDI** — Via VAN partners
7. **Middleware** — iPaaS connectors
[Source: https://www.softeon.com/solutions/ — integrations section]

---

## 5. Help Centers, Knowledge Bases & Community

- **Softeon Customer Portal** — Support and documentation (login required) [Source: https://www.softeon.com/support/]
- **No public community forum**
- **No public knowledge base**
- **Support:** Phone, email, dedicated CSMs
- **Training:** Softeon training programs for customers
- **Blog:** https://www.softeon.com/blog/ (industry content)
- **YouTube:** Product demos and customer success stories
- **Annual user conference** and regular webinars
[Source: https://www.softeon.com/resources/]

---

## 6. Carrier Integration Capabilities

- Multi-carrier parcel: UPS, FedEx, USPS, DHL, regional carriers
- Rate shopping engine
- Carrier selection rules (cost, speed, destination, weight)
- Label generation (thermal, PDF)
- Manifest creation
- Tracking integration
- Returns label generation
- LTL carrier support
- International shipping documentation
[Source: https://www.softeon.com/solutions/warehouse-management-system/ — shipping section]

---

## 7. Pricing Model

- **Not publicly available.** Enterprise sales engagement required.
- SaaS subscription model (cloud deployment)
- Perpetual license available for on-prem
- Pricing factors:
  - Number of warehouses
  - Modules (WMS, WES, DOM)
  - Transaction volume
  - User count
  - Automation integrations
- Estimated: $3,000–$15,000+/month depending on scale (industry estimates)
- Implementation: $100K–$500K+ via Softeon PS or SI partners
[Source: Industry estimates, Gartner analysis]

---

## 8. Pros & Cons from Real Users

### Pros
- **Best-in-class WES** — Automation orchestration is a genuine differentiator [Source: https://www.g2.com/products/softeon-wms/reviews]
- **Flexible and configurable** — Highly adaptable to complex fulfillment workflows
- **Strong fulfillment optimization** — Good for high-volume eCommerce operations
- **DOM capability** — Distributed order management adds order routing intelligence
- **Responsive vendor** — Users report good collaboration with Softeon team
- **Cloud and on-prem options** — Deployment flexibility
- **Growing innovation** — Active R&D investment in AI/ML for warehouse optimization

### Cons
- **No public API** — Documentation gated, can't evaluate without vendor engagement [Source: https://www.g2.com/products/softeon-wms/reviews]
- **Smaller market presence** — Less name recognition than Manhattan, Blue Yonder
- **Partner ecosystem smaller** — Fewer SI partners and pre-built integrations
- **UI/UX could be better** — Not the most modern interface
- **Reporting** — Users want more built-in analytics capabilities
- **Mobile experience** — Scanner app UX improvement needed

[Source: https://www.g2.com/products/softeon-wms/reviews]
[Source: https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/softeon]
[Source: Reddit r/supplychain — Softeon discussion threads]

---

## 9. Implications for Omnifill Integration

### Integration Feasibility: LOW-MODERATE
- REST APIs exist but are not publicly documented
- No developer portal or sandbox
- Vendor engagement required for integration specs
- WES integration patterns are well-defined (good reference for Omnifill's own orchestration layer)

### Recommended Approach
1. **Study Softeon WES architecture** — Their automation orchestration patterns are a model for Omnifill
2. **SFTP/file-based** as initial integration (portable, doesn't require vendor engagement)
3. **EDI** for standardized operations
4. **Vendor engagement** for REST API access if Softeon becomes priority target

### Key Value for Omnifill
- Softeon's WES pattern (unified orchestration of manual + automated work) is directly relevant to Omnifill's unified abstraction goal
- Their approach to multi-vendor robotics integration is a reference architecture

---

## Sources

- https://www.softeon.com/about/
- https://www.softeon.com/solutions/warehouse-management-system/
- https://www.softeon.com/solutions/warehouse-execution-system/
- https://www.softeon.com/solutions/
- https://www.softeon.com/support/
- https://www.softeon.com/resources/
- https://www.softeon.com/blog/
- https://www.g2.com/products/softeon-wms/reviews
- https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/softeon
- Reddit r/supplychain — Softeon discussion threads
