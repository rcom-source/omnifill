# ToolsGroup — Supply Chain Planning Research

Research date: 2026-03-31

## Overview

ToolsGroup is a private vendor (founded 1993, backed by Accel-KKR since 2018) whose core product is SO99+ (Service Optimizer 99+). Recognized in the 2026 Gartner Magic Quadrant for Supply Chain Planning (Discrete Industries). Key acquisitions: Mi9 Retail's JustEnough (2021), Onera (2022), Evo Pricing (2023). Core differentiator: probabilistic, service-driven multi-echelon inventory optimization (MEIO). [Source: https://www.toolsgroup.com/]

**Industries:** Manufacturing, Distribution, Retail, Consumer Goods, Automotive, Industrial

## Core Capabilities

### Demand Sensing & Forecasting
- Probabilistic demand forecasting — identifies range of outcomes with probability of each
- Demand sensing extracts signals from noisy demand for short-term accuracy
- ML engines mapped to every attribute (seasonality, promotions, causals, external factors)
[Source: https://www.toolsgroup.com/solutions/demand-forecasting-planning/]

### Inventory Optimization (Core Differentiator)
- Service-driven MEIO replacing traditional ABC classification
- "Service class" approach
- Network-level inventory decisions avoiding duplicated stock buffers
- Risk-pooling across network echelons
[Source: https://www.toolsgroup.com/product/so99/]

### Replenishment Planning
- Automated, time-phased replenishment aligned with real-world constraints
- Lead times, order cycles, capacity limits, lot sizes
- Execution-ready recommendations

### What-If Simulation
- AI evaluates multiple scenarios and policy options in parallel
- Side-by-side comparisons for pricing, promotions, inventory, supply changes
- Decision-centric planning model

### Additional Modules
- **Decision Hub** (2024): real-time decision layer
- **Data/Inventory Hub:** real-time inventory unification
- **Fulfill.io:** omnichannel order fulfillment
- **PriceAI:** retail pricing optimization (from Evo Pricing acquisition)
- Promotions planning, S&OP

## ML/AI Capabilities

### Model Types
- **Probabilistic forecasting (core):** Full demand distributions (probability ranges), not point forecasts
- **LightGBM:** Recently implemented for faster processing and improved accuracy at scale
- **Deep learning:** For identifying future demand trends from existing data
- **Per-attribute ML engines:** Individual models for seasonality, promotions, causals, external factors per SKU-location

### Data Requirements
- Historical demand data (primary)
- Real-time transactional data (via Kafka/API)
- Promotional calendars and causal factors
- External demand-relevant signals
- Inventory position data across network
- End-to-end modeling at SKU-location level

### Accuracy Claims
- 5-10 percentage point improvement in forecast accuracy
- 3-5 percentage point increase in service levels
- 20-30% inventory reduction simultaneously
- Up to 90% reduction in planning workload
- 10-30% waste reduction
- **Caveat:** Claims customer-reported; Lokad notes lack of independent validation [Source: https://www.lokad.com/review-of-toolsgroup-com/]

## Technical Integration

### APIs (Key Differentiator vs. Peers)
- **OpenAPI 3.0 web API** exposed by SO99+ [Source: https://www.toolsgroup.com/product/so99/]
- OAuth or API-Key authentication
- This is the most significant technical differentiator vs. Logility and many competitors

### Engineering Stack
- React, Java, Python, C#, GraphQL, PostgreSQL, Redis, Kafka, Kubernetes, Docker

### ERP Integration
- Certified integration with SAP ERP 6.0 on SAP HANA (SO99+ Connector) [Source: https://www.prnewswire.com/news-releases/toolsgroup-so99-supply-chain-planning-software-achieves-certified-integration-with-sap-erp-running-on-sap-hana-300192104.html]
- Full integration with Microsoft Dynamics 365 (Power Platform, Dataverse) [Source: https://www.toolsgroup.com/news/toolsgroup-introduces-so99-for-microsoft-dynamics-365/]
- Oracle ERP supported

### Authentication
- **OAuth 2.0** or **API-Key** for OpenAPI 3.0
- SSO support, audit logging, change management (Azure-based)

### Cloud Deployment
- Azure-hosted multi-tenant SaaS
- Available on Microsoft AppSource [Source: https://appsource.microsoft.com/en-us/product/web-apps/toolsgroup.toolsgroup-so99]

## Help Centers & Community

- **knowledge.toolsgroup.com** — product documentation and demo videos (mostly gated)
- No public community forum
- ToolsGroup blog (toolsgroup.com/blog) — extensive SC planning content
- Resources: white papers, webinars, case studies (Aston Martin, Nespresso, McDonald's, Mitsubishi Electric)
- Infosys alliance partnership for implementation

## User Reviews — Pros & Cons

### Ratings
- Gartner Peer Insights: 4.4/5 (53 reviews)
- FeaturedCustomers: Top "Market Leader" Spring 2025 Demand Forecasting
[Source: https://www.gartner.com/reviews/product/so99]

### Pros
- MEIO is genuinely powerful — core differentiator
- Probabilistic forecasting handles uncertainty better than deterministic approaches
- Centralizes order planning and forecast management
- Significant forecast accuracy improvement and reduced workload
- User-friendly interface (post-UI refresh)
- Realistic implementation: 4-6 months (5-month go-live at Mitsubishi Electric Europe)
- OpenAPI 3.0 enables programmatic integration
- "Pay as you grow" pricing for smaller companies
- Up to 90% reduction in planning workload
[Source: https://www.g2.com/products/service-optimizer-99/reviews]

### Cons
- **Algorithm opacity:** AI claims lack reproducible benchmarks (Lokad)
- **Not historically cloud-native** — on-premise origin; cloud migration recent
- **No mobile app** — desktop/browser only
- **Terminology confusion:** overlapping product names without clear SLA definitions
- **Unverified outcome claims** — customer-reported improvements lack independent validation
- **Smaller review base** than competitors
[Source: https://www.trustradius.com/products/toolsgroup/reviews]

## Pricing

- **Quote-based, not publicly disclosed**
- Small business (1-10 users): ~$50-$100/user/month
- Enterprise (100-1,000 users): ~$30-$50/user/month
- Global enterprise (1,000+): custom negotiated
- "Pay as you grow" model for early-stage online retailers [Source: https://www.prnewswire.com/news-releases/toolsgroup-offers-pay-as-you-grow-pricing-model-to-early-stage-online-retailers-300286752.html]
- Implementation: SMB $10K-$50K (3-6 months), Enterprise $100K+ (6-12 months)
[Source: https://www.itqlick.com/toolsgroup/pricing]

## Integration Assessment for Omnifill

**Best integration path:** The OpenAPI 3.0 API with OAuth/API-Key auth is the most accessible integration surface among mid-market planning tools. Modern tech stack (Kafka, GraphQL, Kubernetes) suggests well-architected integration capabilities. Certified SAP and Dynamics connectors. The probabilistic MEIO output would be valuable for inventory optimization decisions in an abstraction layer.

## Sources

- https://www.toolsgroup.com/
- https://www.toolsgroup.com/solutions/
- https://www.toolsgroup.com/product/so99/
- https://www.toolsgroup.com/solutions/demand-forecasting-planning/
- https://www.prnewswire.com/news-releases/toolsgroup-so99-supply-chain-planning-software-achieves-certified-integration-with-sap-erp-running-on-sap-hana-300192104.html
- https://www.toolsgroup.com/news/toolsgroup-introduces-so99-for-microsoft-dynamics-365/
- https://appsource.microsoft.com/en-us/product/web-apps/toolsgroup.toolsgroup-so99
- https://www.gartner.com/reviews/product/so99
- https://www.g2.com/products/service-optimizer-99/reviews
- https://www.trustradius.com/products/toolsgroup/reviews
- https://www.itqlick.com/toolsgroup/pricing
- https://www.prnewswire.com/news-releases/toolsgroup-offers-pay-as-you-grow-pricing-model-to-early-stage-online-retailers-300286752.html
- https://www.lokad.com/review-of-toolsgroup-com/
- https://knowledge.toolsgroup.com/en-us/service-optimizer-99-overview-video
