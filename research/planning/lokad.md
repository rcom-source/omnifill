# Lokad — Supply Chain Planning Research

Research date: 2026-03-31

## Overview

Lokad is a quantitative supply chain optimization platform — not a traditional demand planning UI. Uses probabilistic forecasting (quantile forecasts, not point forecasts) and stochastic optimization. Fully programmable via **Envision** (proprietary DSL). Designed for supply chain scientists, not business users. [Source: https://docs.lokad.com/]

**Industries:** Retail, eCommerce, Manufacturing, Aviation/MRO, Distribution

## Core Capabilities

- **Probabilistic Forecasting:** Quantile forecasts generating full demand distributions
- **Stochastic Optimization:** Decisions optimized against probability distributions of future outcomes
- **Fully Programmable:** Envision DSL for custom forecasting and optimization logic
- **Automated Pipelines:** Scheduled execution with failure recovery
- Purchasing, production, stocking, pricing decision optimization
- Philosophically opposed to point-forecast accuracy metrics — advocates economic loss functions instead

## Technical Integration

- **File system IS the API** — FTPS and SFTP are primary integration methods [Source: https://docs.lokad.com/platform/]
- Built-in connectors: Brightpearl, NetSuite, Dear Systems
- Web UI for file upload/download
- Public endpoints for external Envision compilation/execution
- Git-like distributed file system with versioning and atomic operations
- **NO traditional REST API**

### Authentication
- Federated identity via Microsoft Office 365, Google Apps
- Username/password
- Fine-grained ACLs (read/write, dashboard, script editing)
- Separate credentials for third-party uploaders with limited trust

## Help Centers & Community

- **docs.lokad.com** — extensive technical documentation [Source: https://docs.lokad.com/]
- **try.lokad.com** — interactive Envision code playground
- **Lokad TV (YouTube)** — Joannes Vermorel's supply chain lectures
- No traditional community forum
- Active blog publishing critical reviews of competitors

## User Reviews

### Ratings
- G2: 90% user satisfaction [Source: https://www.g2.com/products/lokad/reviews]

### Pros
- Powerful optimization and robust analytics
- Advanced probabilistic forecasting — genuinely differentiated
- Innovative technology
- Flexible and tailorable via Envision
- Increases productivity

### Cons
- **Envision DSL has steep learning curve** for non-technical teams
- **No drag-and-drop UI** — code-only
- Unexpected extra charges reported
- Windows OS compatibility issues
- Requires "Supply Chain Scientist" role to operate

## Pricing

- Starting at $150/month (entry level) [Source: https://www.g2.com/products/lokad/reviews]
- Enterprise pricing not public
- Reports of unclear extra charges

## ML/AI

- **Differentiable programming** built into Envision runtime
- Probabilistic forecasting: full demand distributions (quantiles)
- Stochastic optimization against probability distributions
- **No pre-built ML models** — users write custom logic in Envision
- Emphasis on rigorous math over black-box AI
- Data: historical transactional data as flat files
- Does NOT claim specific accuracy percentages — philosophically opposes point-forecast metrics

## Sources

- https://docs.lokad.com/
- https://docs.lokad.com/platform/
- https://www.g2.com/products/lokad/reviews
- https://try.lokad.com
