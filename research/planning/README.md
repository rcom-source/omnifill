# Supply Chain Planning & Prediction SaaS — Research Index

Research date: 2026-03-31

Comprehensive research covering every major SaaS system in the supply chain planning and prediction space (demand forecasting, inventory optimization, supply planning, network design, predictive analytics, ML-driven planning).

## Systems Researched (18 primary + 11 additional)

### Tier 1: Enterprise Leaders (Gartner MQ Leaders)

| System | File | API Access | ML/AI Depth | Pricing |
|--------|------|-----------|-------------|---------|
| [Kinaxis Maestro](kinaxis-rapidresponse.md) | kinaxis-rapidresponse.md | Gated REST + Developer Studio | Moderate (heuristic-first) | $500K-$2M+/yr |
| [o9 Solutions](o9-solutions.md) | o9-solutions.md | No public API (NDA) | Deep (AutoML, causal AI, NLP, GNN) | $250K-$5M+/yr |
| [Blue Yonder Luminate](blue-yonder-luminate.md) | blue-yonder-luminate.md | Gated (200+ MuleSoft connectors) | Deep (Cyclic Boosting OSS) | $100K-$2M+/yr |
| [SAP IBP](sap-ibp.md) | sap-ibp.md | **Public OData V2 APIs** | Deep (xGBoost, LSTM, Transformers) | ~$29K+/yr |
| [Oracle SCM Planning](oracle-scm-planning.md) | oracle-scm-planning.md | **Public REST APIs (JSON)** | Deep (18 Bayesian ensemble methods) | $300/user/mo |

### Tier 2: Strong Challengers

| System | File | API Access | ML/AI Depth | Pricing |
|--------|------|-----------|-------------|---------|
| [RELEX Solutions](relex-solutions.md) | relex-solutions.md | No public API | Strong (GBDT, neural nets, fresh optimization) | $200K-$5M+/yr |
| [Anaplan](anaplan.md) | anaplan.md | **Public REST API** + CloudWorks | Moderate (PlanIQ AutoML) | $200K-$3M+/yr |
| [Coupa/LLamasoft](coupa-llamasoft.md) | coupa-llamasoft.md | **Public REST API** (BSM); limited for SC design | Optimization-focused (MILP) | $150K-$1M+/yr |
| [Logility](logility.md) | logility.md | No public API | Ensemble + GenAI (DemandAI+) | $100-$500/user/mo |
| [ToolsGroup](toolsgroup.md) | toolsgroup.md | **OpenAPI 3.0** (OAuth/API-Key) | Strong (probabilistic, LightGBM, MEIO) | $30-$100/user/mo |

### Tier 3: Specialized / Niche

| System | File | API Access | ML/AI Depth | Pricing |
|--------|------|-----------|-------------|---------|
| [Antuit.ai / Zebra](antuit-zebra.md) | antuit-zebra.md | Gated (API key via sales) | Deep (DL, ensemble, MLOps) | Enterprise quote |
| [Solvoyo](solvoyo.md) | solvoyo.md | REST/SOAP/SFTP (no public docs) | Claims AI (unvalidated) | Enterprise quote |
| [John Galt / Atlas](john-galt-solutions.md) | john-galt-solutions.md | Limited (REST POST, JSON export) | Moderate (Procast, stat methods) | Price competitive |
| [ForecastRx](forecastrx.md) | forecastrx.md | Platform integrations only | Basic (100+ stat models) | $100-$400/mo |
| [Inventory Planner/Sage](inventory-planner-sage.md) | inventory-planner-sage.md | OAuth 2.0 (Sage platform) | Basic (statistical) | $245+/mo |
| [StockIQ](stockiq.md) | stockiq.md | REST (not documented) | Basic (algorithm tournament) | Quote-based |
| [Lokad](lokad.md) | lokad.md | SFTP/FTPS (file-based) | Deep (probabilistic, differentiable programming) | $150+/mo |
| [Additional Systems](additional-systems.md) | additional-systems.md | Varies | Varies | Varies |

## Key Findings for Omnifill Integration

### Best API Access (self-service integration possible)
1. **SAP IBP** — Public OData V2 APIs with sandbox testing on api.sap.com
2. **Oracle SCM Planning** — Public REST APIs (JSON), well-documented
3. **Anaplan** — Public REST API (Transactional + Bulk) with CloudWorks connectors
4. **Coupa BSM** — Public REST API with Swagger specs (procurement side; SC design limited)
5. **ToolsGroup** — OpenAPI 3.0 with OAuth/API-Key (most accessible mid-market)

### Gated but Integrable (requires partnership/NDA)
- Kinaxis (Developer Studio + REST, gated docs)
- Blue Yonder (200+ MuleSoft connectors, gated portal)
- RELEX, o9, Logility (all require enterprise engagement)

### Open Source Assets
- **Blue Yonder Cyclic Boosting** — github.com/Blue-Yonder-OSS/cyclic-boosting (scikit-learn compatible, fully explainable demand forecasting)
- **Lokad Envision** — Proprietary DSL but publicly documented at docs.lokad.com

### ML/AI Model Landscape

| Approach | Systems Using It |
|----------|-----------------|
| Gradient Boosted Trees (XGBoost/LightGBM) | SAP IBP, o9, RELEX, ToolsGroup, Blue Yonder |
| LSTM / Deep Learning | SAP IBP, o9, RELEX |
| Transformer Networks | SAP IBP, o9 (newer releases) |
| Bayesian Ensemble | Oracle SCM, SAP IBP |
| Probabilistic Forecasting | ToolsGroup, Lokad, Blue Yonder |
| AutoML | o9, Anaplan (PlanIQ), Logility |
| MILP Optimization | Coupa/LLamasoft, Oracle |
| Causal Inference | o9, SAP IBP, RELEX |
| Knowledge Graph | o9 (core architecture) |
| Cyclic Boosting | Blue Yonder (open source) |

### Authentication Patterns

| Method | Systems |
|--------|---------|
| OAuth 2.0 | SAP IBP, Oracle, Anaplan, Kinaxis, ToolsGroup, Coupa |
| API Key | Blue Yonder, ToolsGroup, Coupa, Antuit/Zebra |
| SAML 2.0 SSO | All enterprise systems |
| Certificate-based | SAP IBP, Anaplan |
| Basic Auth (deprecated) | SAP IBP, Oracle (being phased out) |

### Pricing Tiers

| Tier | Annual Cost Range | Systems |
|------|------------------|---------|
| Enterprise | $500K-$5M+ | Kinaxis, o9, SAP IBP (full), Blue Yonder, Oracle (full) |
| Mid-Market | $100K-$500K | RELEX, Logility, Coupa, Anaplan, ToolsGroup |
| SMB | $1K-$50K | ForecastRx, Lokad, StockIQ, Inventory Planner |
| eCommerce | $100-$500/mo | ForecastRx, Inventory Planner, Prediko, Flieber |

### Key Takeaway for Architect/ML Crew

For building planning adapters or better predictive engines:
1. **Start with SAP IBP and Oracle SCM** — best-documented public APIs, largest installed base
2. **ToolsGroup OpenAPI 3.0** — best mid-market API surface for MEIO/probabilistic planning
3. **Evaluate Blue Yonder Cyclic Boosting** — open-source, explainable, production-proven at scale
4. **Study o9 Knowledge Graph architecture** — most differentiated approach but requires NDA for API access
5. **Lokad's Envision DSL** — most rigorous mathematical approach to probabilistic optimization, good for ML engineer study
