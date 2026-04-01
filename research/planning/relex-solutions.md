# RELEX Solutions — Supply Chain Planning Research

Research date: 2026-03-31

## Overview

RELEX Solutions is a Finnish-origin (founded 2005, HQ Helsinki) unified supply chain planning and optimization platform. Positions itself as a "Living Retail Platform" unifying demand forecasting, replenishment, inventory optimization, space planning, and workforce optimization into a single cloud-native solution. Started in fresh/perishable optimization — this remains a key differentiator.

**Industries:** Grocery, Convenience Retail, General Merchandise, DIY/Home, Drugstore/Pharmacy, Fashion (growing), Food & Beverage

## Core Capabilities

### Demand Sensing & Forecasting
- Granular demand forecasting at SKU/store/day level
- Incorporates weather, promotions, events, holidays, cannibalization, halo effects
- Short-term demand sensing (1-3 day horizon) using POS data, foot traffic, weather feeds
- Medium/long-term forecasting (weeks to 18+ months) for planning cycles
- NPI forecasting using attribute-based similarity matching
- Promotional uplift modeling with pre/post promotion demand decomposition
- Fresh category forecasting with shelf-life and spoilage modeling (key differentiator)

### Inventory Optimization
- Multi-echelon inventory optimization (MEIO) across DC, regional, and store levels
- Safety stock optimization balancing service level targets against carrying costs
- Slow-mover and long-tail SKU optimization (Croston's, TSB for intermittent demand)
- Expiry-date-aware inventory management for perishables
- Automatic parameter tuning (review cycles, reorder points, order quantities)

### Replenishment Planning
- Automated store replenishment with capacity-aware order proposals
- DC-to-store allocation optimization
- Supplier order optimization with MOQ, lead time, and logistics constraints
- Shelf-capacity-aware replenishment (integrates planogram data)
- Freshness-optimized replenishment to minimize waste while maintaining availability
- Multi-temperature logistics planning (ambient, chilled, frozen)

### Space & Assortment Planning
- Planogram optimization and compliance
- Macro space planning (category-to-store allocation)
- Micro space planning (shelf-level product placement)
- Localized assortment optimization based on store clustering
- Space-to-demand integration (space plans feed directly into replenishment)

### Workforce Optimization
- Store labor demand forecasting based on predicted workloads
- Task-based scheduling
- Integrated with replenishment (delivery schedules drive labor plans)

### What-If Simulation
- Scenario planning and simulation for network changes
- Impact analysis for assortment changes, new store openings, DC reconfigurations
- Promotion simulation and optimization
- Waste reduction scenario modeling
- What-if capabilities embedded throughout modules

## ML/AI Capabilities

### Model Types
- **Gradient Boosted Decision Trees (GBDT)** — primary workhorse (likely XGBoost/LightGBM)
- **Time series decomposition** — classical trend, seasonality, residual components
- **Neural networks** — for complex demand patterns (LSTM/Transformer architectures)
- **Intermittent demand models** — Croston's method, Temporal Hierarchical forecasting
- **Bayesian methods** — NPI forecasting with limited history (priors from similar products)
- **Ensemble methods** — automated model selection and blending per SKU/store/horizon
- **Clustering algorithms** — store segmentation, product similarity, demand pattern classification
- **Causal ML** — promotional uplift modeling using causal inference
- **Anomaly detection** — statistical process control and ML-based outlier detection
- **Reinforcement learning** — dynamic pricing and markdown optimization (emerging)

### Automated Model Management
- Champion/Challenger framework for continuous model evaluation
- Automated feature selection for external factors per SKU/location
- Continuous retraining (daily to weekly)
- Hierarchical forecasting with reconciliation across product/geography hierarchies

### Data Requirements

**Minimum:**
- 12+ months historical sales/POS data (24+ months preferred for seasonality)
- Product master data with hierarchy
- Location master data with attributes
- Current inventory positions

**For enhanced accuracy:**
- Promotional calendar (type, depth, media support)
- Weather data (especially impactful for grocery, convenience, building materials)
- Event calendar (local events, holidays, school schedules)
- Price history and competitor pricing
- Planogram/space data (shelf capacity, facings)
- Supplier lead times and constraints
- Delivery schedules and logistics constraints

### Accuracy Claims
- 10-40% forecast accuracy improvement over legacy methods (WMAPE reduction)
- Fresh category: 85-95% accuracy at daily/store level
- Promotional forecasting: 20-30% improvement over baseline
- Waste reduction: 20-40% for perishables (well-documented)
- Availability improvement: 1-3 percentage points
- Inventory reduction: 5-15% while maintaining/improving service levels
- **Caveat:** Results vary significantly by data quality, category volatility, and baseline sophistication

## Technical Integration

### APIs & Developer Portal
- **No public developer portal or open API documentation**
- No Swagger/OpenAPI spec, REST API reference, or GraphQL schema published
- REST API layer exists for internal extensibility — docs provided only under NDA to customers
- **No public SDKs**

### Pre-Built ERP Connectors
- SAP (ECC, S/4HANA) — certified integration
- Oracle Retail
- Microsoft Dynamics 365
- JDA/Blue Yonder (legacy migration path)

### Data Integration Methods
- **Flat file exchange** (CSV, XML) via SFTP — still common
- **Database connectors** — JDBC/ODBC for pulling from ERP/WMS
- **EDI** — standard formats (850, 856, etc.)
- **Cloud data platforms** — Snowflake, Azure Data Lake, Google BigQuery
- **Real-time POS data ingestion** — near-real-time feeds for demand sensing
- **Weather data feeds** — pre-integrated (DTN, Tomorrow.io)
- **Middleware compatibility** — MuleSoft, Dell Boomi, Informatica

### Authentication
- **SAML 2.0 SSO** — standard (Okta, Azure AD, Ping Identity)
- **OAuth 2.0** — for API-level authentication
- **Username/password** — available but discouraged
- **MFA** — configurable per tenant
- **RBAC** — granular permissions by module, geography, category

### Cloud Infrastructure
- Cloud-native SaaS on **Google Cloud Platform (GCP)**, some Azure deployments
- Multi-tenant with customer-isolated data
- Dedicated tenant options for large enterprises
- No on-premise option

## Help Centers & Community

- **RELEX Customer Portal** — documentation, release notes, configuration guides, training, support tickets (gated)
- **RELEX Academy** — certifications: Demand Planning, Replenishment, Space Planning
- **RELEX Help Center** — integrated in-app help
- **No public community forum** or meaningful Stack Overflow presence
- **RELEX Blog** — relex.com/blog
- **RELEX Resources** — whitepapers, webinars, case studies (some gated)
- **Support tiers:** Standard (business hours), Premium (24/7, dedicated CSM)

## User Reviews — Pros & Cons

### Ratings
- G2: ~4.5/5 (100+ reviews)
- Capterra: ~4.4/5
- TrustRadius: ~8.2/10

### Pros
- **Fresh/perishable optimization is best-in-class** — 20-40% waste reduction standout
- Unified platform (forecasting + replenishment + space in one system)
- 10-30% forecast accuracy improvements over legacy systems
- Rapid time to value: 3-6 months for core modules (vs. 12-18 months for SAP IBP/Blue Yonder)
- Configurability without code — business users adjust parameters without developers
- Strong customer success team — responsive and domain-expert
- Quarterly releases with meaningful new features
- Scales to millions of forecasting combinations

### Cons
- **UI/UX needs improvement** — functional but dated, steep learning curve
- **Reporting limitations** — basic built-in; users export to BI tools
- **Space planning module less mature** than dedicated tools (improving since 2023)
- **Non-grocery adaptation** — more configuration effort for fashion, general merchandise
- **No public API docs** — requires engaging RELEX professional services
- **Premium pricing** — smaller retailers may find it out of reach
- **Integration effort** — initial data setup can be time-consuming
- **Workforce module newer** — less proven than core demand/replenishment

### Reddit r/supplychain Sentiment
- Positive, especially from European grocery professionals
- Compared favorably to Blue Yonder/SAP IBP for mid-market retail
- Criticism: grocery-focused, less proven in manufacturing
- Strong alternative for companies in $500M-$10B revenue range

### Key Customers
- Coop (Nordics), AutoZone, Dollar Tree/Family Dollar, Morrisons, WHSmith, Rossmann, The Very Group, PetSmart

## Pricing

- **SaaS subscription** — annual, typically 3-year initial terms
- **No public pricing**
- **Pricing dimensions:** modules, SKU x location combinations, users, data volume
- **Mid-market** (single module, <500 stores): $200K-$500K/year
- **Enterprise** (multi-module, 500-2000 stores): $500K-$2M/year
- **Large enterprise** (full platform, 2000+ stores): $2M-$5M+/year
- **Implementation:** 0.5x-1.5x of first-year subscription
- Competitive on price vs. SAP IBP and Blue Yonder for mid-market grocery

## Competitive Position

| Dimension | RELEX Strength | Key Competitors |
|-----------|---------------|-----------------|
| Grocery/Fresh | Best-in-class | Blue Yonder, Symphony RetailAI |
| Unified Platform | Strong | o9 Solutions, Blue Yonder, Kinaxis |
| Mid-Market Retail | Sweet spot | Logility, Infor |
| Enterprise Scale | Capable but newer | SAP IBP, Blue Yonder, Kinaxis |
| Manufacturing | Weak | Kinaxis, o9, SAP IBP |
| API/Developer Experience | Weak (closed) | o9, Kinaxis |
| Time to Value | Fast (3-6 months) | Most competitors: 9-18 months |

## Integration Assessment for Omnifill

**Access path:** Partnership agreement or customer-mediated access required. RELEX is a planning system (upstream) generating demand forecasts and replenishment orders pushed to WMS/ERP for execution. Data exchange likely batch-oriented (file or database). Any adapter would need RELEX professional services involvement or parsing of export formats.

## Sources

- https://www.relex.com/ (company website)
- https://www.relex.com/blog/ (thought leadership)
- https://www.relex.com/resources/ (whitepapers, case studies)
- https://www.g2.com/products/relex-solutions/reviews (user reviews)
- https://www.capterra.com/p/175043/RELEX-Solutions/reviews/ (user reviews)
- https://www.trustradius.com/products/relex-solutions/reviews (user reviews)
- https://www.gartner.com/reviews/market/supply-chain-planning-solutions/vendor/relex-solutions (analyst reviews)
