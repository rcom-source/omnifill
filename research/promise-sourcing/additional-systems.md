# Additional Promise & Sourcing Systems Research

Research date: 2026-03-31

This file covers additional systems in the order promising, sourcing, and distributed order management space beyond the primary systems documented in individual files.

---

## 1. Tecsys (Itopia / Elite)

### What It Does
- **Distributed Order Management**: Rule-based order orchestration across warehouses, stores, and 3PLs
- **Order Promising**: ATP checks with inventory allocation and reservation
- **Sourcing**: Configurable sourcing rules (proximity, cost, inventory depth, store capacity)
- **Inventory Visibility**: Unified inventory across nodes with safety stock and channel allocation
- **Specialty**: Strong in healthcare supply chain (hospital inventory, pharmacy, implant tracking)

### Technical Details
- **API Type**: REST APIs, EDI support
- **Developer Docs**: Not publicly available — customer/partner access only
- **Platform**: Cloud-hosted (Tecsys SaaS) or on-premises
- **Auth**: OAuth 2.0 / API key based (per integration documentation)
[Source: tecsys.com product pages]

### User Sentiment
- Praised for healthcare supply chain specialization
- Strong in complex distribution scenarios (multi-echelon)
- Criticized for UI dated compared to newer platforms
- Implementation timelines can be lengthy (6-12 months)
[Source: G2 reviews - https://www.g2.com/products/tecsys/reviews, Capterra]

### Pricing
- Custom enterprise pricing, not publicly available
- Per-user and per-module licensing model
[Source: Vendor discussions]

---

## 2. Softeon

### What It Does
- **Distributed Order Management**: Order orchestration with intelligent routing
- **Order Promising**: Real-time ATP with configurable promising rules
- **Sourcing**: Cost-optimized, proximity-based, and rule-driven fulfillment routing
- **Unique Feature**: Combined WMS + DOM on single platform (similar to Deposco)
- **Fulfillment Optimization**: AI/ML-based order routing optimization
- **Ship-from-Store**: BOPIS, curbside, store fulfillment capabilities

### Technical Details
- **API Type**: REST APIs
- **Developer Docs**: Not publicly available
- **Platform**: Cloud-native (AWS), microservices architecture
- **Integration**: Pre-built connectors for Shopify, Magento, SAP, Oracle, Manhattan WMS
[Source: softeon.com product pages]

### User Sentiment
- "Hidden gem" — less well-known but strong capabilities
- Praised for combined WMS+DOM value
- Good customer support and implementation
- Smaller market presence means smaller ecosystem
[Source: G2 reviews - https://www.g2.com/products/softeon/reviews]

### Pricing
- Custom enterprise pricing
- Reportedly competitive vs. larger vendors (Manhattan, IBM Sterling)
[Source: Vendor comparison sites]

---

## 3. Commercetools

### What It Does
- **Order Management**: API-first, headless commerce platform with order management capabilities
- **Inventory**: Multi-channel inventory tracking with supply channels
- **Order Routing**: Basic order routing via custom logic (no built-in DOM engine)
- **NOT a full DOM**: Commercetools is a commerce platform, not a specialized OMS/DOM — order promising and sourcing must be built or added via extensions

### Technical Details
- **API Type**: REST + GraphQL (primary), fully headless/API-first
- **Developer Portal**: Fully public — https://docs.commercetools.com/
- **Auth**: OAuth 2.0 with client credentials, scopes per API client
- **SDKs**: Official SDKs for Java, TypeScript, Python, PHP, .NET, Go
- **Webhooks**: Subscriptions API for event notifications (AWS SQS, Azure Service Bus, Google Pub/Sub, Confluent Cloud)
- **API Explorer**: https://docs.commercetools.com/api/
[Source: docs.commercetools.com]

### Key APIs for Promising/Sourcing
- **Inventory API**: Track quantities per SKU per supply channel
- **Orders API**: Create/update orders, custom workflows via order state machines
- **Custom Objects API**: Store arbitrary data (could be used for sourcing rules)
- **Extensions API**: Sync HTTP callbacks for custom logic during API calls (could intercept order creation for custom routing)
- **Subscriptions API**: Async event notifications

### User Sentiment
- Praised for developer experience, modern API, and flexibility
- "Best headless commerce platform" for developers
- Criticized for requiring significant custom development for OMS features that are built-in elsewhere
- Not suitable as a standalone DOM — needs complementary systems
[Source: G2 reviews - https://www.g2.com/products/commercetools/reviews, Reddit r/ecommerce]

### Pricing
- Usage-based pricing (API calls + orders)
- Enterprise tier with committed volumes
- Starting around $40K/year for B2C
[Source: commercetools.com/pricing, G2 pricing data]

### Relevance to Omnifill
- **High** as a downstream commerce platform that Omnifill could integrate with
- **Low** as a promising/sourcing engine — would need Omnifill to provide that intelligence
- Excellent API docs make adapter development straightforward

---

## 4. Brightpearl (by Sage)

### What It Does
- **Order Management**: Retail-focused OMS for multichannel commerce
- **Inventory Management**: Multi-warehouse inventory with reorder points
- **Order Routing**: Basic rule-based routing (closest warehouse, inventory availability)
- **Automation Engine**: "Brightpearl Automation" for order workflows
- **Target Market**: Mid-market retailers and wholesalers ($1M-$100M revenue)

### Technical Details
- **API Type**: REST API (comprehensive)
- **Developer Portal**: Public — https://www.brightpearl.com/developer/latest/
- **Auth**: OAuth 2.0 (app authorization flow)
- **Webhooks**: Event notifications for order, inventory, product changes
- **Rate Limiting**: 200 requests per minute per account
[Source: brightpearl.com/developer]

### User Sentiment
- Good for mid-market — purpose-built for retail
- Praised for accounting integration (Sage ecosystem)
- Criticized for limited enterprise features (no sophisticated DOM)
- API well-documented but can be slow for large datasets
[Source: G2 reviews - https://www.g2.com/products/brightpearl/reviews, Capterra]

### Pricing
- Custom quotes starting around $700/month
- Per-user add-ons
[Source: brightpearl.com, G2 pricing data]

---

## 5. Linnworks

### What It Does
- **Multi-channel Order Management**: Centralized order processing across marketplaces (Amazon, eBay, Shopify, etc.)
- **Inventory Sync**: Real-time inventory sync across channels and warehouses
- **Order Routing**: Basic rules (default warehouse, stock availability, location priority)
- **Shipping Management**: Multi-carrier rate shopping and label printing
- **Target Market**: SMB and mid-market e-commerce sellers

### Technical Details
- **API Type**: REST API
- **Developer Portal**: https://developer.linnworks.com/
- **Auth**: Application authorization tokens
- **SDKs**: .NET SDK available
- **Webhooks**: Limited — polling-based integration more common
[Source: developer.linnworks.com]

### User Sentiment
- Good for marketplace sellers needing centralized management
- Praised for marketplace integration breadth
- Criticized for complexity, steep learning curve, unreliable during peak
- API documentation described as "adequate but not great"
[Source: G2 reviews - https://www.g2.com/products/linnworks/reviews, TrustRadius]

### Pricing
- Tiered: starts ~$449/month for base, scales with order volume
- Add-on pricing for warehouses, users, channels
[Source: linnworks.com pricing, G2]

---

## 6. Cin7

### What It Does
- **Inventory & Order Management**: Cloud-native platform combining inventory, orders, POS, and B2B
- **Products**: Cin7 Core (SMB) and Cin7 Omni (mid-market)
- **Order Routing**: Basic rules-based routing
- **Inventory**: Multi-location tracking, stock transfers, reorder points
- **3PL Integration**: Pre-built integrations with major 3PLs
- **Target Market**: Product-based SMBs

### Technical Details
- **API Type**: REST API
- **Developer Portal**: https://developer.cin7.com/ (Core), https://api.cin7.com/ (Omni)
- **Auth**: API key / account key based
- **Webhooks**: Available for key events
[Source: developer.cin7.com]

### User Sentiment
- Good for SMBs needing inventory + order management
- Praised for ease of use and marketplace integrations
- Criticized for limited customization and reporting
- Support quality inconsistent
[Source: G2 reviews - https://www.g2.com/products/cin7/reviews, Capterra]

### Pricing
- Cin7 Core: from $349/month
- Cin7 Omni: from $799/month
- Per-module add-ons
[Source: cin7.com pricing]

---

## 7. OneStock

### What It Does
- **Distributed Order Management**: European-headquartered DOM specialist
- **Order Promising**: Real-time ATP/CTP with delivery promise capabilities
- **Sourcing**: AI-powered order orchestration with multi-criteria routing:
  - Proximity optimization
  - Stock balancing across locations
  - Carbon footprint minimization
  - Store workload capacity
  - Split shipment avoidance
- **Ship-from-Store**: Full BOPIS, reserve-in-store, ship-from-store
- **Unified Inventory**: Real-time aggregation across all fulfillment nodes
- **Target Market**: Mid-to-enterprise retail (LVMH, Intersport, Aldo)

### Technical Details
- **API Type**: REST APIs
- **Developer Portal**: Not publicly available — customer access only
- **Platform**: Cloud-native SaaS
- **Integration**: Pre-built connectors for Salesforce Commerce, SAP, Shopify, Magento
[Source: onestock-retail.com]

### User Sentiment
- Strong in European retail market
- Praised for sustainability-aware routing (carbon optimization)
- Good ship-from-store capabilities
- Smaller global presence vs. Manhattan, IBM Sterling
[Source: G2 reviews, Gartner Peer Insights]

### Pricing
- Custom enterprise pricing, not publicly available
[Source: Vendor discussions]

---

## 8. Aptos (Epicor)

### What It Does
- **Order Management**: Retail-focused OMS (acquired by Epicor in 2024)
- **DOM**: Distributed order management with rule-based routing
- **Inventory**: Enterprise inventory management across stores and DCs
- **Promising**: ATP with store inventory and DC availability
- **Target Market**: Specialty retail, fashion, grocery

### Technical Details
- **API Type**: REST APIs, SOAP (legacy)
- **Developer Docs**: Limited public documentation (post-Epicor acquisition)
- **Platform**: Cloud (Aptos ONE platform) or on-premises
[Source: aptos.com, epicor.com]

### User Sentiment
- Strong in specialty retail
- Acquisition by Epicor introduces uncertainty about product direction
- Legacy technology being modernized
[Source: G2 reviews, Gartner Peer Insights]

---

## 9. Enspire Commerce

### What It Does
- **Order Management**: Cloud OMS for B2C and B2B commerce
- **DOM**: Rules-based order routing
- **Inventory**: Multi-location visibility and allocation
- **Promising**: Basic ATP capabilities
- **Target Market**: Mid-market retailers

### Technical Details
- **API Type**: REST APIs
- **Developer Docs**: Limited public documentation
- Very little public information available — smaller vendor
[Source: enspirecommerce.com]

---

## 10. Pulse Commerce (formerly GoECart)

### What It Does
- **Unified Commerce Platform**: Combined OMS, ecommerce, POS, and CRM
- **Order Routing**: Intelligent order routing with rule-based logic
- **Inventory**: Multi-channel inventory management
- **Target Market**: Mid-market direct-to-consumer brands

### Technical Details
- **API Type**: REST APIs
- **Developer Docs**: Not publicly available
- Small vendor — limited public technical information
[Source: pulsecommerce.com]

---

## 11. Blue Yonder (Luminate Commerce)

### What It Does
- **Luminate Commerce**: Cloud-native commerce and order management
- **Order Promising**: Advanced ATP/CTP with ML-driven demand sensing
- **Sourcing**: AI-powered fulfillment optimization considering:
  - Cost to serve
  - Delivery speed
  - Inventory position
  - Carbon footprint
  - Store capacity
- **Inventory Visibility**: Global real-time inventory aggregation
- **Demand Forecasting**: ML-based demand prediction integrated with promising
- **Target Market**: Large enterprise (tier 1 retailers, CPG companies)

### Technical Details
- **API Type**: REST APIs, MOCA (legacy JDA)
- **Developer Portal**: Gated — Blue Yonder Success Portal (customer/partner login)
- **Platform**: Azure-native (Luminate platform)
- **Auth**: OAuth 2.0 (Azure AD integration)
- **ML Platform**: Integrated ML for demand forecasting and fulfillment optimization
[Source: blueyonder.com product pages, press releases]

### User Sentiment
- Very strong in supply chain planning (heritage from JDA/i2/Manugistics)
- Excellent demand forecasting — considered best-in-class
- Criticized for complexity, cost, and long implementation timelines
- Legacy MOCA-based products being migrated to cloud — transition period creates risk
- Panasonic acquisition (2021) adding IoT/sensor capabilities
[Source: G2 reviews - https://www.g2.com/products/blue-yonder/reviews, Gartner Magic Quadrant for Supply Chain Planning]

### Pricing
- Enterprise pricing, not publicly available
- Reportedly among the most expensive in the category
- Multi-year contracts typical
[Source: Industry discussions, TrustRadius]

---

## Comparison Matrix: Additional Systems

| System | DOM Capability | Promising Depth | API Openness | Target Market | Sourcing AI |
|--------|---------------|-----------------|--------------|---------------|-------------|
| Tecsys | Strong | ATP | Closed | Healthcare/Distribution | Rule-based |
| Softeon | Strong | ATP | Closed | Mid-Enterprise Retail | ML-enhanced |
| Commercetools | Basic (DIY) | None built-in | Fully Open | Developer-led Commerce | None |
| Brightpearl | Basic | Basic ATP | Public API | Mid-market Retail | Rule-based |
| Linnworks | Basic | None | Public API | SMB E-commerce | None |
| Cin7 | Basic | None | Public API | SMB Product Brands | None |
| OneStock | Strong | ATP/CTP | Closed | European Retail | AI-enhanced |
| Aptos/Epicor | Medium | ATP | Limited | Specialty Retail | Rule-based |
| Enspire | Medium | Basic ATP | Closed | Mid-market | Rule-based |
| Pulse Commerce | Basic | Basic | Closed | D2C Brands | None |
| Blue Yonder | Very Strong | ATP/CTP/ML | Gated | Enterprise | ML/AI |

## Sources

- Tecsys: https://www.tecsys.com/, https://www.g2.com/products/tecsys/reviews
- Softeon: https://www.softeon.com/, https://www.g2.com/products/softeon/reviews
- Commercetools: https://docs.commercetools.com/, https://www.g2.com/products/commercetools/reviews
- Brightpearl: https://www.brightpearl.com/developer/latest/, https://www.g2.com/products/brightpearl/reviews
- Linnworks: https://developer.linnworks.com/, https://www.g2.com/products/linnworks/reviews
- Cin7: https://developer.cin7.com/, https://www.g2.com/products/cin7/reviews
- OneStock: https://www.onestock-retail.com/
- Aptos/Epicor: https://www.aptos.com/, https://www.epicor.com/
- Enspire Commerce: https://www.enspirecommerce.com/
- Pulse Commerce: https://www.pulsecommerce.com/
- Blue Yonder: https://www.blueyonder.com/, https://www.g2.com/products/blue-yonder/reviews
