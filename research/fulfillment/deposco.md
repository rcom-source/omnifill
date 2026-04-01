# Deposco — Comprehensive Research

> Cloud-native supply chain platform. Bright Suite: WMS + OMS + procurement.
> Research date: 2026-03-31

---

## 1. Overview & History

Deposco is a cloud-native supply chain execution platform founded in 2006, headquartered in Atlanta, GA. Their "Bright Suite" includes WMS, OMS, procurement, and analytics modules. Targets mid-market to enterprise fulfillment operations, particularly eCommerce, retail, and 3PL providers.

**Key differentiators:**
- Cloud-native from inception (not a legacy migration)
- Unified data model across WMS + OMS
- Strong in multi-tenant 3PL operations
- Growing market presence (mid-tier between Extensiv and Manhattan)
[Source: https://www.deposco.com/about/]

---

## 2. What It Does: Core Fulfillment Capabilities

### Pick Methods
- **Wave picking** — Traditional wave-based with configurable wave rules
- **Waveless/continuous picking** — Demand-driven release
- **Batch picking** — Multi-order batch consolidation
- **Zone picking** — Zone-based with downstream sort
- **Cluster picking** — Cart-based multi-order
- **Discrete picking** — Single-order for priority/VIP
- **Directed picking** — System-optimized pick paths with mobile scanning
[Source: https://www.deposco.com/solutions/warehouse-management/]

### Pack Optimization
- Cartonization (automated box selection)
- Pack verification via scanning
- Multi-item consolidation
- Custom packing rules per client/channel
- Kitting and assembly
- Gift wrap and insert management
[Source: https://www.deposco.com/solutions/warehouse-management/]

### Shipping & Carrier Selection
- Multi-carrier shipping integration
- Rate shopping
- Label generation
- Manifest management
- Integration with carrier APIs (UPS, FedEx, USPS, DHL)
- Small parcel + LTL support
[Source: https://www.deposco.com/solutions/]

### Labor Management
- Task-based labor tracking
- Productivity reporting per employee
- Performance dashboards
- Not as deep as dedicated LMS (Manhattan, Blue Yonder)
[Source: https://www.deposco.com/solutions/warehouse-management/]

### Robotics Integration
- AMR integration capabilities (partners with robotics providers)
- ASRS integration
- Conveyor/sortation system integration
- API-based WES layer for automation coordination
[Source: https://www.deposco.com/integrations/]

---

## 3. Technical Documentation

### API Architecture
- **REST API** — Primary integration method
- **Base URL:** Varies per tenant (provided by account manager)
- **Format:** JSON request/response
- **Developer portal:** https://developer.deposco.com/ (partially public)
- **Full documentation:** https://doc.deposco.com/ (requires login)

### Key API Endpoints
- **Inventory:** Query inventory by facility, location, SKU; adjust quantities
- **Customer Orders:** Create/import orders, update status, cancel
- **Purchase Orders:** Create/manage inbound POs
- **Organizations:** Manage tenant/client data
- **Shipments:** Track outbound shipments
- **Receipts:** Manage inbound receiving

### Community Client
- GitHub: https://github.com/launched-la/deposco-api — Community-maintained API client (unofficial)
[Source: https://github.com/launched-la/deposco-api]

### Webhooks
- Event-based notifications available
- Configurable per event type (order status, shipment, inventory)
- HTTP POST to configured endpoints
[Source: https://developer.deposco.com/]

### SDK / Tools
- No official SDKs published
- Community Python client on GitHub
- Postman collections available from implementation teams

---

## 4. Authentication & Integration Patterns

### Basic Authentication
- **Tenant Code** — Identifies the Deposco tenant/environment
- **API Username** — Dedicated API user account
- **API Password** — Associated password
- Credentials provided by Deposco account manager during onboarding
- Base64-encoded `username:password` in `Authorization: Basic` header

### Integration Patterns
1. **Direct REST API** — Real-time order push, inventory query
2. **File-based (SFTP)** — Batch CSV/XML file imports for orders, inventory
3. **EDI** — Standard EDI transaction sets via VAN
4. **Middleware** — MuleSoft, Boomi, Celigo connectors available
5. **Pre-built connectors** — Shopify, Amazon, Magento, NetSuite, SAP

### Rate Limits
- Not publicly documented
- Enterprise accounts get higher throughput
- Contact support for high-volume API usage requirements
[Source: https://developer.deposco.com/]

---

## 5. Help Centers, Knowledge Bases & Community

- **Help portal:** https://doc.deposco.com/ (login required) [Source: https://doc.deposco.com/]
- **Developer portal:** https://developer.deposco.com/ (partially public) [Source: https://developer.deposco.com/]
- **Support:** Email and phone support, dedicated CSMs for enterprise
- **Training:** Deposco Academy (customer training programs)
- **No public community forum**
- **Limited public knowledge base** — Most documentation is behind auth
- **Blog:** https://www.deposco.com/blog/
- **YouTube:** Product demos and customer stories
[Source: https://www.deposco.com/resources/]

---

## 6. Carrier Integration Capabilities

- Multi-carrier parcel: UPS, FedEx, USPS, DHL
- LTL carrier integration
- Rate shopping across carriers and service levels
- Automated carrier selection rules
- Label generation (ZPL thermal, PDF)
- Tracking number propagation
- Manifest generation
- Returns label generation
- International shipping documentation
[Source: https://www.deposco.com/solutions/]

---

## 7. Pricing Model

- **Not publicly available.** Custom quotes only.
- SaaS subscription model
- Pricing factors:
  - Number of facilities/warehouses
  - Transaction volume (orders/month)
  - Modules licensed (WMS, OMS, procurement)
  - Number of users
  - Integration count
- Estimated range: $2,000–$10,000+/month depending on scale (industry estimates)
- Implementation fees separate
[Source: https://www.g2.com/products/deposco/reviews — pricing discussions]

---

## 8. Pros & Cons from Real Users

### Pros
- **True cloud-native** — Modern architecture, quick to deploy vs. legacy WMS [Source: https://www.g2.com/products/deposco/reviews]
- **Unified WMS + OMS** — Single platform for warehouse and order management
- **Good for multi-client 3PLs** — Multi-tenant architecture
- **Flexible configuration** — Highly configurable without custom code
- **Strong eCommerce integration** — Pre-built connectors for major platforms
- **Rapid implementation** — Weeks to months vs. 6-18 months for enterprise WMS
- **Responsive development team** — Users report good feature request responsiveness

### Cons
- **API documentation is thin** — Developer portal partially gated, docs incomplete [Source: https://www.g2.com/products/deposco/reviews]
- **Basic Auth only** — No OAuth 2.0 for API access (less secure than modern standards)
- **Reporting limitations** — Built-in reporting needs improvement, often need external BI
- **Mobile UX** — Scanner/mobile interface could be more polished
- **Limited public API surface** — Not all WMS functions exposed via API
- **Smaller ecosystem** — Fewer SI partners and integrations vs. Manhattan/Extensiv
- **Growing pains** — As company scales, some users report slower support response

[Source: https://www.g2.com/products/deposco/reviews]
[Source: https://www.capterra.com/p/163025/Deposco/reviews/]
[Source: Reddit r/supplychain — Deposco discussion threads]

---

## 9. Implications for Omnifill Integration

### Integration Feasibility: MODERATE
- REST API exists but documentation is partially gated
- Basic Auth (not OAuth) simplifies initial integration but limits security
- Need account manager engagement for full API access and docs
- Community API client on GitHub provides some reference

### Recommended Approach
1. Request full API documentation from Deposco (via https://developer.deposco.com/ access request)
2. Reference community client at https://github.com/launched-la/deposco-api for endpoint patterns
3. Start with order import + inventory query endpoints
4. File-based (SFTP) as fallback integration pattern

### Key Challenges
- Partial documentation — will need to discover some endpoints empirically
- Basic Auth credentials management
- No public sandbox environment
- Rate limits unknown — need to negotiate with vendor

---

## Sources

- https://www.deposco.com/about/
- https://www.deposco.com/solutions/warehouse-management/
- https://www.deposco.com/solutions/
- https://www.deposco.com/integrations/
- https://www.deposco.com/resources/
- https://developer.deposco.com/
- https://doc.deposco.com/
- https://github.com/launched-la/deposco-api
- https://www.g2.com/products/deposco/reviews
- https://www.capterra.com/p/163025/Deposco/reviews/
- Reddit r/supplychain — Deposco discussion threads
