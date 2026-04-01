# Promise & Sourcing SaaS Systems Research

Research date: 2026-03-31
Researcher: Polecat furiosa (ps-p8o)

## Overview

Comprehensive research on all major SaaS systems in the order promising and sourcing space — covering inventory availability (ATP/CTP), distributed order management, order orchestration, and sourcing optimization. This research supports the Omnifill project's goal of building a unified promising/sourcing abstraction layer.

## Research Files

### Primary Systems (Individual Deep-Dive Files)

| File | System | Category |
|------|--------|----------|
| [manhattan-active-omni.md](manhattan-active-omni.md) | Manhattan Active Omni | Enterprise DOM/OMS |
| [salesforce-order-management.md](salesforce-order-management.md) | Salesforce Order Management | Platform OMS |
| [fluent-commerce.md](fluent-commerce.md) | Fluent Commerce | Cloud-native DOM |
| [ibm-sterling-oms.md](ibm-sterling-oms.md) | IBM Sterling OMS | Enterprise DOM/OMS |
| [oracle-dom-order-promising.md](oracle-dom-order-promising.md) | Oracle DOM / Order Management Cloud | Enterprise DOM |
| [oms-systems-research.md](oms-systems-research.md) | Kibo Commerce, Fabric OMS, Deposco OMS, Deck Commerce | Mid-market OMS |
| [orderful.md](orderful.md) | Orderful | EDI Platform (Transport) |
| [radial.md](radial.md) | Radial | OMS + Fulfillment Services |
| [additional-systems.md](additional-systems.md) | 11 additional systems | Various |

### Additional Systems Covered

The [additional-systems.md](additional-systems.md) file covers: Tecsys, Softeon, Commercetools, Brightpearl (Sage), Linnworks, Cin7, OneStock, Aptos (Epicor), Enspire Commerce, Pulse Commerce, Blue Yonder (Luminate Commerce).

---

## System Classification

### Tier 1: Enterprise DOM/Promising Engines
Full-featured distributed order management with advanced promising (ATP/CTP) and AI-driven sourcing.

| System | Promising | Sourcing AI | API Access | Integration Difficulty |
|--------|-----------|-------------|------------|----------------------|
| **Manhattan Active Omni** | ATP/CTP/PTP | ML-driven | Gated (NDA) | Very High |
| **IBM Sterling OMS** | ATP/CTP/PTP | AI Optimizer | Gated (customer) | High |
| **Blue Yonder Luminate** | ATP/CTP/ML | ML/AI | Gated (partner) | Very High |
| **Oracle DOM** | ATP/GOP | Rule-based | Public docs | High |
| **Salesforce OMS** | ATP (routing rules) | Rule-based | Public (Salesforce API) | Medium |

### Tier 2: Cloud-Native DOM Specialists
Modern, API-first platforms purpose-built for distributed order management.

| System | Promising | Sourcing AI | API Access | Integration Difficulty |
|--------|-----------|-------------|------------|----------------------|
| **Fluent Commerce** | ATP/CTP | A/B testing + AI (2026) | Public (GraphQL) | Medium |
| **Kibo Commerce** | ATP/CTP | Rule-based | Public (REST+GraphQL) | Medium |
| **OneStock** | ATP/CTP | AI-enhanced | Closed | Medium-High |

### Tier 3: Combined OMS/WMS Platforms
Systems that combine order management with warehouse management for tight integration.

| System | Promising | WMS Integrated | API Access | Integration Difficulty |
|--------|-----------|----------------|------------|----------------------|
| **Deposco** | AI DOM | Yes (Bright Suite) | Partial (login required) | Medium |
| **Softeon** | ATP | Yes | Closed | Medium-High |
| **Fabric OMS** | OFL rules engine | No (separate) | Public (REST) | Low-Medium |

### Tier 4: Mid-Market / SMB OMS
Simpler order management with basic routing, targeting smaller businesses.

| System | Best For | API Access | Price Range |
|--------|----------|------------|-------------|
| **Deck Commerce** | D2C brands | Closed | Custom |
| **Brightpearl** | Retail mid-market | Public API | From $700/mo |
| **Linnworks** | Marketplace sellers | Public API | From $449/mo |
| **Cin7** | Product brands | Public API | From $349/mo |

### Tier 5: Specialized / Adjacent
Systems that are adjacent to promising/sourcing rather than core DOM.

| System | Function | Relevance to Omnifill |
|--------|----------|----------------------|
| **Orderful** | EDI-as-a-Service | Transport layer for EDI partners |
| **Radial** | OMS + Fulfillment services | Fulfillment node to orchestrate |
| **Commercetools** | Headless commerce | Downstream platform to integrate |

---

## Key Findings for Omnifill

### 1. Market Gaps (Opportunities for Omnifill)
- **No universal promising API**: Every vendor has proprietary promising logic. No standard exists for ATP/CTP queries across systems.
- **Closed ecosystems dominate enterprise**: Manhattan, Blue Yonder, and IBM Sterling have the best promising but require full platform adoption.
- **Mid-market under-served**: The gap between "basic order routing" (Tier 4) and "enterprise AI-driven DOM" (Tier 1) is huge. Kibo and Fluent are the only cloud-native options bridging this gap.
- **No open-source DOM**: Unlike WMS (where OpenBoxes exists), there is no viable open-source distributed order management system.

### 2. Common Promising Patterns
Every system with ATP/CTP follows a similar conceptual model:
1. **Inventory query**: Check availability across nodes (on-hand - reserved - safety stock = available)
2. **Sourcing rules**: Apply criteria to select fulfillment location(s) (proximity, cost, capacity, inventory depth)
3. **Promise calculation**: Determine delivery date based on selected source + shipping method
4. **Allocation**: Reserve inventory at selected location

Omnifill can abstract this pattern across all systems.

### 3. Integration Feasibility Matrix

| System | API Quality | Auth Complexity | Adapter Feasibility |
|--------|-------------|-----------------|---------------------|
| Fluent Commerce | Excellent (GraphQL) | Medium (OAuth 2.0) | **High** |
| Kibo Commerce | Excellent (REST+GQL) | Medium (OAuth 2.0) | **High** |
| Salesforce OMS | Good (REST) | Medium (OAuth 2.0) | **High** |
| Fabric OMS | Good (REST) | Low (Bearer token) | **High** |
| Commercetools | Excellent (REST+GQL) | Medium (OAuth 2.0) | **High** |
| Oracle DOM | Good (REST) | Medium (OAuth 2.0) | **Medium** |
| IBM Sterling | Moderate (REST/XAPI) | High (JWT/OAuth) | **Medium** |
| Deposco | Basic (REST) | Low (Basic Auth) | **Medium** |
| Brightpearl | Good (REST) | Medium (OAuth 2.0) | **Medium** |
| Manhattan Active Omni | Unknown (gated) | High (OAuth 2.0) | **Low** (NDA required) |
| Blue Yonder | Unknown (gated) | High | **Low** (partner required) |
| Radial | Unknown (gated) | Unknown | **Low** (customer only) |

### 4. Recommended Adapter Priority for Omnifill

Based on API accessibility, market coverage, and promising depth:

1. **Fluent Commerce** — Best public API (GraphQL), strong promising, growing enterprise adoption
2. **Kibo Commerce** — Full public API, mature ATP/CTP, good mid-market coverage
3. **Salesforce OMS** — Massive install base, public APIs via Salesforce platform
4. **Fabric OMS** — Modern REST APIs, easy auth, good for smaller deployments
5. **IBM Sterling** — Largest enterprise install base, but API access requires licensing
6. **Oracle DOM** — Public docs, enterprise market, good REST APIs
7. **Commercetools** — Not a DOM itself, but extremely common downstream system
8. **Manhattan Active Omni** — Industry leader but gated docs make adapter dev dependent on partnerships

### 5. Key Technical Patterns to Support

| Pattern | Systems Using It | Omnifill Implication |
|---------|-----------------|---------------------|
| GraphQL APIs | Fluent, Kibo, Commercetools | Must support GraphQL client |
| REST APIs | All others | Standard REST adapter pattern |
| OAuth 2.0 | Most systems | Standard auth flow |
| Webhooks/Events | Fluent, Kibo, Fabric, Salesforce | Event-driven inventory updates |
| EDI/X12 | Orderful, Radial, legacy systems | EDI gateway integration |
| Batch/SFTP | Deposco, Radial, legacy | Batch inventory sync adapter |

---

## Coverage Summary

| # | System | File | Promising | Sourcing | API Documented |
|---|--------|------|-----------|----------|----------------|
| 1 | Manhattan Active Omni | manhattan-active-omni.md | ATP/CTP/PTP | ML | Gated |
| 2 | Salesforce OMS | salesforce-order-management.md | ATP (routing) | Rules | Public |
| 3 | Fluent Commerce | fluent-commerce.md | ATP/CTP | AI (2026) | Public |
| 4 | IBM Sterling OMS | ibm-sterling-oms.md | ATP/CTP/PTP | AI | Gated |
| 5 | Oracle DOM | oracle-dom-order-promising.md | ATP/GOP | Rules | Public |
| 6 | Kibo Commerce | oms-systems-research.md | ATP/CTP | Rules | Public |
| 7 | Fabric OMS | oms-systems-research.md | OFL rules | Rules | Public |
| 8 | Deposco OMS | oms-systems-research.md | AI DOM | Rules | Partial |
| 9 | Deck Commerce | oms-systems-research.md | AI estimates | Rules | Closed |
| 10 | Orderful | orderful.md | N/A (EDI) | N/A | Limited |
| 11 | Radial | radial.md | ATP | Rules | Closed |
| 12 | Tecsys | additional-systems.md | ATP | Rules | Closed |
| 13 | Softeon | additional-systems.md | ATP | ML | Closed |
| 14 | Commercetools | additional-systems.md | None (DIY) | None | Public |
| 15 | Brightpearl | additional-systems.md | Basic ATP | Rules | Public |
| 16 | Linnworks | additional-systems.md | None | Basic | Public |
| 17 | Cin7 | additional-systems.md | None | Basic | Public |
| 18 | OneStock | additional-systems.md | ATP/CTP | AI | Closed |
| 19 | Aptos/Epicor | additional-systems.md | ATP | Rules | Limited |
| 20 | Enspire Commerce | additional-systems.md | Basic | Rules | Closed |
| 21 | Pulse Commerce | additional-systems.md | Basic | Basic | Closed |
| 22 | Blue Yonder | additional-systems.md | ATP/CTP/ML | ML/AI | Gated |

**Total systems researched: 22**
