# Order Promising, Sourcing & Distributed Order Management Systems

Research date: 2026-03-31

---

## Table of Contents

1. [Orderful](#1-orderful)
2. [Radial (formerly GSI Commerce / eBay Enterprise)](#2-radial)
3. [Fluent Commerce](#3-fluent-commerce)
4. [Kibo Commerce](#4-kibo-commerce)
5. [IBM Sterling Order Management](#5-ibm-sterling-order-management)
6. [Manhattan Associates](#6-manhattan-associates)
7. [commercetools](#7-commercetools)
8. [OneStock](#8-onestock)
9. [Deck Commerce](#9-deck-commerce)
10. [Pipe17](#10-pipe17)
11. [Softeon](#11-softeon)
12. [Tecsys (Elite / Itopia / OrderDynamics)](#12-tecsys)
13. [Aptos (formerly Epicor Retail)](#13-aptos)
14. [Korber / Enspire Commerce](#14-korber--enspire-commerce)
15. [Pulse Commerce](#15-pulse-commerce)
16. [Brightpearl (by Sage)](#16-brightpearl-by-sage)
17. [Linnworks](#17-linnworks)
18. [Cin7](#18-cin7)
19. [Celigo](#19-celigo)
20. [Vinculum](#20-vinculum)
21. [Deposco](#21-deposco)

---

## 1. Orderful

**Category:** EDI Platform / Supply Chain Integration
**Website:** https://www.orderful.com

### What It Does

Orderful is a **cloud-native, API-first EDI platform** that modernizes electronic data interchange for supply chain operations. It is not a traditional OMS or order promising system -- rather, it provides the **EDI connectivity layer** that order management systems rely on to exchange transactions (purchase orders, invoices, ASNs, shipment notices) with trading partners.

Key capabilities:
- **API-native EDI workflows** -- single standardized API replaces per-partner mapping
- **AI-powered mapping (Mosaic)** -- uses AI to interpret and transform data, eliminating manual EDI map creation; learns from 10,000+ trading partner network
- **Real-time validation and monitoring** of EDI transactions
- **Trading partner onboarding** in 9 days or less (vs. weeks/months traditional)
- Reduces engineering hours by 90-95% compared to traditional EDI

### Technical Documentation

- **Developer Hub:** https://docs.orderful.com/
- **API Reference:** https://docs.orderful.com/reference/overview
- **API Type:** RESTful API with JSON payloads
- **Base URL:** Documented in developer portal
- **Key Endpoints:**
  - Create a Transaction: https://docs.orderful.com/docs/create-a-transaction
  - Authentication reference: https://docs.orderful.com/reference/authentication
  - Best Practices: https://docs.orderful.com/reference/best-practices

### Authentication

- **Method:** API Key in request header
- **Header Key:** `orderful-api-key`
- **Token Generation:** Automatically generated upon account creation
- **Access:** Settings > Organization Settings > API Credentials in Orderful UI
- No OAuth flow -- straightforward API key authentication on every request

### Integration Patterns

- Single integration per transaction type (not per partner)
- Supports standard EDI document types (850 PO, 855 PO Ack, 856 ASN, 810 Invoice, 214 Status, etc.)
- Microsoft Dynamics 365 Intelligent Order Management integration available
- Cloud Elements connector available
- NetSuite integration available

### User Reviews

**G2:** https://www.g2.com/products/orderful-edi/reviews
**Capterra:** https://www.capterra.com/p/191612/Orderful/reviews/

**Strengths:**
- Modern, intuitive, API-first platform
- Dramatically faster partner onboarding (90% reduction in time)
- Excellent customer support -- quick, knowledgeable
- JSON-based interface abstracts EDI complexity

**Weaknesses:**
- Web EDI interface criticized as underdeveloped ("laughable" per Reddit r/edi)
- Reporting capabilities are limited/basic
- Pricing can be prohibitive for small businesses

**Reddit:** r/edi has threads discussing Orderful experience -- generally positive on API side, negative on Web EDI interface.

### Pricing

- **Web EDI:** Starting at $189/month per trading partner
- **Integrated (API):** Starting at $1,999/month
- **Enterprise:** Custom pricing
- No setup fees, no per-transaction charges, no hidden costs
- Example: 3 retail partners = $567/month ($6,804/year) vs. $30K-$100K with legacy providers
- Pricing page: https://www.orderful.com/pricing

### Multi-Node Inventory Handling

Orderful does **not** handle inventory directly. It is an EDI communication layer. Multi-node inventory visibility would come from the OMS/WMS systems that Orderful connects via EDI transactions.

---

## 2. Radial (formerly GSI Commerce / eBay Enterprise)

**Category:** Omnichannel OMS + Fulfillment Services
**Website:** https://www.radial.com

### What It Does

Radial is a **full-service omnichannel order management and fulfillment provider** with 30+ years of expertise (founded 1995 as GSI Commerce, became eBay Enterprise, rebranded Radial 2016). It combines software (OMS) with physical fulfillment services (30+ fulfillment centers in North America and Europe).

Key capabilities:
- **Order brokering and routing** across fulfillment networks (own DCs, 3PL, stores)
- **Unified enterprise inventory visibility** across all nodes
- **Distributed order management** with configurable sourcing rules
- **Store fulfillment** (BOPIS, ship-from-store)
- **Dropship management** and marketplace integration
- **Payment/fraud solutions** (Risk Assessment API)
- **Customer care tools**
- **Business intelligence modules**

### Technical Documentation

- **Developer Portal:** https://developer-apina.gsipartners.com/technology/retail-order-management
- **Documentation Hub:** https://docs.radial.com/
- **Order Management APIs:** https://docs.radial.com/Content/order-management/order-management-apis.htm
- **API Reference:** https://docs.radial.com/Content/Topics/api-reference.htm
- **Order Management Setup Guide:** https://docs.radial.com/Content/order-management/order-management-setup-guide.htm
- **JDA-Based OMS docs:** https://docs.radial.com/jda/

### Authentication & Integration Patterns

- **API Architecture:** REST-compliant with **XML payloads** (not JSON)
- **Transport:** HTTPS (XML messages sent to defined URIs)
- **Schema:** Each service defined via .xsd files with accompanying URI structure
- **Security Layer:** Public API behind an API Security Layer
- **Integration types:**
  - REST APIs for real-time operations (order create, inventory check, risk assessment)
  - Batch feed APIs for bulk operations (order shipment feed, orders-to-fulfill feed, item master feed)
- **Key APIs:**
  - Order Create: https://docs.radial.com/Content/api-tutorial/howto-build-order-create-requests.htm
  - Order Shipment Feed: https://docs.radial.com/rom/Content/Topics/feeds/order-shipment-feed.htm
  - Orders to Fulfill Feed: https://docs.radial.com/Content/feeds/order/orders-to-fulfill-feed.htm
  - Risk Assessment API: https://docs.radial.com/ptf/Content/Topics/risk/risk-assessment-api.htm
  - Item Service (catalog/product): https://docs.radial.com/Content/rom-general-topics/build-an-item-catalog.htm

### User Reviews

**G2:** https://www.g2.com/products/radial/reviews (limited reviews, mostly from 2018)
**Capterra:** https://www.capterra.ca/software/210671/radial

**Strengths:**
- Great analytics with ability to measure ROI
- 30+ years of expertise in ecommerce fulfillment
- Comprehensive end-to-end solution (software + physical fulfillment)
- Strong sourcing engine for complex fulfillment scenarios

**Weaknesses:**
- UI described as complicated and difficult to navigate
- Limited recent public reviews (enterprise nature = fewer public testimonials)
- XML-based API is legacy compared to modern JSON/GraphQL approaches

### Pricing

- Enterprise/custom pricing -- not publicly listed
- Flexible pricing models covering: warehousing, labor, setup fees, receiving costs, monthly minimums, carrier rates, transportation, pick/pack
- Designed for mid-to-large enterprise retailers
- Fulfill.com profile: https://www.fulfill.com/3pl/profile/radial

### Multi-Node Inventory Handling

**Strong.** Radial's core value proposition is unified inventory visibility across:
- Company-owned distribution centers
- 3PL warehouses
- Retail stores (for ship-from-store / BOPIS)
- Dropship vendors
- Marketplace channels

The sourcing engine considers inventory availability, location proximity, cost optimization, and capacity constraints when routing orders.

---

## 3. Fluent Commerce

**Category:** Cloud-Native Distributed Order Management
**Website:** https://fluentcommerce.com

### What It Does

Fluent Commerce is a **cloud-native, rules-based distributed order management platform** purpose-built for complex order orchestration. It is recognized as a Leader/Strong Performer in Gartner and Forrester evaluations for DOM.

Key capabilities:
- **Distributed order orchestration** across multiple fulfillment locations, channels, inventory sources
- **Rules-based engine** for order routing and sourcing logic
- **Real-time inventory visibility** across all nodes
- **Omnichannel fulfillment** (BOPIS, ship-from-store, endless aisle, dropship)
- **Configurable workflows** without code changes
- **Pre-built components and SDKs** for extension

### Technical Documentation

- **Documentation Portal:** https://docs.fluentcommerce.com/
- **APIs Overview:** https://docs.fluentcommerce.com/essential-knowledge/apis-overview
- **GraphQL API:** https://docs.fluentcommerce.com/essential-knowledge/graphql-api (primary, actively supported)
- **REST API:** https://docs.fluentcommerce.com/essential-knowledge/rest-api (platform-level only: auth, integration, workflow)
- **Authentication:** https://docs.fluentcommerce.com/essential-knowledge/authentication-api

### Authentication

- **Method:** OAuth 2.0 (password grant type)
- **Requires:** Client ID, Client Secret (from Fluent), plus username/password
- **Token:** Common authentication token used across both GraphQL and REST APIs

### API Architecture

- **Primary API:** GraphQL (for Product Availability, Orders, Fulfillments, Products)
- **Platform REST APIs (v4.1):** Event API, Workflow API, Job API, Plugin API, User Action API
- **Deprecated:** Domain-based REST endpoints (maintenance mode only -- DO NOT use for new implementations)
- **Additional:** Webhooks for event notifications, retry/exponential backoff patterns

### User Reviews

**Gartner Peer Insights:** https://www.gartner.com/reviews/market/distributed-order-management-systems (listed)
**Salesforce AppExchange:** https://appexchange.salesforce.com/appxListingDetail?listingId=a0N3A00000GBlIsUAL

**Strengths:**
- True cloud-native microservices architecture
- Highly flexible rules engine for order routing
- Strong commercetools integration
- Modern GraphQL API

**Weaknesses:**
- Requires technical expertise to configure
- Enterprise pricing (not for SMBs)

### Pricing

Not publicly listed. Enterprise custom pricing. Contact Fluent Commerce directly.

### Multi-Node Inventory Handling

**Excellent.** Core competency. Real-time inventory aggregation across warehouses, stores, DCs, 3PLs, suppliers with configurable allocation/reservation rules and intelligent routing.

---

## 4. Kibo Commerce

**Category:** Unified Commerce & Order Management
**Website:** https://kibocommerce.com

### What It Does

Kibo Commerce provides a **composable, unified commerce platform** combining order management, ecommerce, and subscription capabilities. Named a Challenger in 2025 Gartner Magic Quadrant for Digital Commerce.

Key capabilities:
- **Order orchestration and intelligent routing** across fulfillment network
- **Real-time inventory visibility** across all channels
- **Composable OMS** -- deploy modules independently
- **BOPIS, ship-from-store, curbside pickup** support
- **Subscription management**
- **B2B and B2C** order management

### Technical Documentation

- **Documentation Portal:** https://docs.kibocommerce.com/
- **Commerce/OMS API:** https://docs.kibocommerce.com/developer-guides/commerce
- **Orders API Overview:** https://docs.kibocommerce.com/help/orders-api-overview
- **API Overviews:** https://docs.kibocommerce.com/help/api-overviews
- **API Guides:** https://docs.kibocommerce.com/help/api-guides
- **Making API Calls:** https://docs.kibocommerce.com/help/making-api-calls

### Authentication

- **Method:** OAuth 2.0 JWT
- **Token Endpoint:** `/api/platform/applications/authtickets/oauth`
- **Requires:** Client ID, Shared Secret (managed via Kibo SDK Configuration object)
- **Note:** Inventory, Fulfillment, and Order Routing services **only** accept JWT bearer tokens

### Key API Endpoints

- `GET/POST /commerce/orders` -- Create, Get, Update orders
- `DELETE /commerce/orders/{id}/draft` -- Delete order draft
- Order import: `POST /commerce/orders` with `isImport=true`
- Historical import: `isHistoricalImport=true`
- Order drafts: ApplyToDraft, ApplyToOriginal, ApplyAndCommit modes
- Supports Authorize.net, PayPal Express 2 payment integrations

### User Reviews

**Gartner:** https://www.gartner.com/reviews/market/distributed-order-management-systems (Challenger)
**Forrester TEI Study:** 167% ROI, $8M NPV, payback in under 6 months

**Strengths:**
- Composable architecture (pick modules needed)
- Strong order orchestration/routing
- Unified commerce approach (ecom + OMS together)
- Proven ROI

**Weaknesses:**
- Documentation could be more comprehensive
- Smaller ecosystem than IBM/Manhattan

### Pricing

Enterprise custom pricing. Not publicly listed. Forrester study indicates strong economic returns.

### Multi-Node Inventory Handling

**Strong.** Real-time inventory visibility across all nodes; intelligent order routing considers inventory levels, proximity, cost, and capacity.

---

## 5. IBM Sterling Order Management

**Category:** Enterprise Order Management & Fulfillment
**Website:** https://www.ibm.com/products/order-management

### What It Does

IBM Sterling is a **market-leading enterprise order management system** with the most mature order orchestration capabilities in the industry. Part of the broader IBM Sterling suite (B2B integration, supply chain).

Key capabilities:
- **Order orchestration** (widely considered market-leading)
- **Omnichannel fulfillment** (BOPIS, ship-from-store, curbside, dropship)
- **Inventory visibility** across all channels and nodes
- **Available-to-promise (ATP)** calculations
- **B2B order management** with EDI support
- **AI-powered insights** for fulfillment optimization
- **Store engagement** tools

### Technical Documentation

- **Documentation Portal:** https://www.ibm.com/docs/en/order-management
- **APIs & Services:** https://www.ibm.com/docs/en/order-management?topic=database-sterling-order-management-system-apis-services
- **REST XAPI Tester:** https://www.ibm.com/docs/en/order-management?topic=application-http-rest-xapi-tester
- **GitHub examples:** https://github.com/IBM/oms-convey-integration
- **Community:** https://www.ibm.com/community/101/sterling/oms/

### Authentication & Integration

- **API Types:** REST (XAPI framework), SOAP/XML, custom APIs
- **REST Framework:** HTTP REST XAPI Tester for testing RESTful APIs
- Both standard supplied APIs and custom/extended APIs supported
- Integration with ERP, WMS, ecommerce platforms

### User Reviews

**G2:** https://www.g2.com/products/ibm-sterling-order-management/reviews
**ITQlick:** https://www.itqlick.com/sterling-commerce-order-management

**Strengths:**
- Market-leading order orchestration
- Extremely mature and battle-tested at scale
- Comprehensive B2B and B2C capabilities
- Strong ATP/promising capabilities

**Weaknesses:**
- Complex to implement (often requires SI partners)
- Expensive licensing
- Legacy architecture in some components
- Steep learning curve

### Pricing

Enterprise licensing -- not publicly listed. Typically $500K+ for initial implementation with ongoing licensing. One of the most expensive OMS solutions.

### Multi-Node Inventory Handling

**Best-in-class.** IBM Sterling has been the gold standard for enterprise inventory visibility and order promising across complex multi-node networks including DCs, stores, dropship, 3PLs, and suppliers.

---

## 6. Manhattan Associates

**Category:** Enterprise Order Management & Supply Chain
**Website:** https://www.manh.com

### What It Does

Manhattan Associates provides **Manhattan Active Omni**, a cloud-native unified commerce platform that received the **highest possible score (5.0) in 20 of 27 criteria** in Forrester's evaluation. In June 2025, they launched **Enterprise Promise & Fulfill** for B2B ERP environments.

Key capabilities:
- **Order orchestration** with sophisticated routing rules
- **Inventory segmentation and allocation** (5.0 Forrester score)
- **Store inventory management** (5.0 Forrester score)
- **Global order orchestration** across complex networks
- **Pre- and post-purchase customer experience** management
- **Enterprise Promise & Fulfill** -- new B2B cloud app for ERP order management

### Technical Documentation

- **Fully gated** -- no public developer portal
- Requires customer license or Partner Program membership (https://www.manh.com/partners)
- API types: REST + GraphQL (Active platform), SOAP/XML (legacy WMOS/SCALE)
- Auth: OAuth 2.0 / OIDC + JWT

### User Reviews

**Gartner Peer Insights:** https://www.gartner.com/reviews/market/distributed-order-management-systems/vendor/manhattan-associates/product/manhattan-active-order-management
**2025 Forrester Wave Leader:** https://www.manh.com/our-insights/resources/research-reports/forrester-wave-order-management-systems

**Strengths:**
- Highest-rated OMS in Forrester Wave 2025
- True cloud-native architecture (Active platform)
- Unified commerce across all channels
- Strong inventory segmentation and allocation

**Weaknesses:**
- Gated documentation -- requires partnership/license
- Premium enterprise pricing
- Complex implementation

### Pricing

Enterprise custom pricing. Premium tier. Not publicly listed.

### Multi-Node Inventory Handling

**Best-in-class.** Scored 5.0/5.0 for inventory segmentation, allocation, and store inventory management in Forrester's evaluation. Handles complex multi-node networks with sophisticated sourcing rules.

---

## 7. commercetools

**Category:** Composable Commerce Platform (MACH)
**Website:** https://commercetools.com

### What It Does

commercetools is a **composable, API-first commerce platform** following MACH principles. Order management is one module within a broader commerce suite, not a standalone DOM. Best suited for organizations building custom commerce experiences.

Key capabilities:
- **Order lifecycle management** (create from cart/quote/import)
- **Order search and indexing** with GraphQL
- **Cart and checkout management**
- **Product information management**
- **Composable modules** deployable independently
- **Recurring orders / subscriptions** (new scopes added Dec 2025)

### Technical Documentation

- **API Docs:** https://docs.commercetools.com/api
- **Orders API:** https://docs.commercetools.com/api/projects/orders
- **Order Search:** https://docs.commercetools.com/api/projects/order-search
- **Carts & Orders Overview:** https://docs.commercetools.com/api/carts-orders-overview
- **Order Import:** https://docs.commercetools.com/api/import-export/order
- **API Releases:** https://docs.commercetools.com/api/releases
- **Full Documentation:** https://docs.commercetools.com/docs

### Authentication

- **Method:** OAuth 2.0
- **Scopes:** Granular per resource (e.g., `manage_orders`, `view_orders`, `manage_recurring_orders`)
- New OAuth scopes for Recurrence Policies introduced Dec 2025

### User Reviews

**G2:** https://www.g2.com/products/commercetools/reviews (91% satisfaction, 92 reviews)
**Gartner:** https://www.gartner.com/reviews/market/digital-commerce/vendor/commercetools/product/commercetools
**Capterra:** https://www.capterra.com/p/174960/commercetools/

**Strengths:**
- True MACH architecture, API-first
- Excellent developer experience and documentation
- Highly flexible and composable
- Strong ecosystem (Fluent Commerce, OneStock, Pipe17 integrations)

**Weaknesses:**
- Order management features described as needing improvement (not a dedicated OMS)
- No built-in DOM/order routing -- requires partner solution (Fluent, OneStock)
- Requires significant development expertise
- Expensive for smaller operations

### Pricing

- **Model:** Annual license proportional to revenue + pay-as-you-use for add-ons
- **Example:** ~$100M annual revenue = ~$120K/year license
- **Editions:** Core, Foundry ($150K+/year), Premium
- **Pricing page:** https://commercetools.com/pricing

### Multi-Node Inventory Handling

**Limited natively.** commercetools handles basic inventory/stock tracking but does **not** include native distributed order management, order routing, or sophisticated sourcing logic. Organizations pair it with Fluent Commerce, OneStock, or similar DOM solutions for multi-node fulfillment.

---

## 8. OneStock

**Category:** AI-Driven Distributed Order Management
**Website:** https://www.onestock-retail.com

### What It Does

OneStock is a **MACH-certified, API-first distributed order management system** with AI-driven orchestration. European-headquartered, strong in retail.

Key capabilities:
- **Stock unification** across all nodes
- **AI-driven intelligent order orchestration**
- **Store fulfillment** (BOPIS, ship-from-store, click-and-collect)
- **Returns management**
- **Endless aisle / order-in-store**
- **100% API coverage** with real-time webhooks

### Technical Documentation

- **APIs Portal:** https://www.onestock-retail.com/services/developers/api-portal/
- **Architecture:** Microservices, API-First, Cloud-Native SaaS, Headless (MACH)
- **Integration types:**
  - Synchronous APIs (import, update, delete, query)
  - Asynchronous APIs (bulk data imports)
  - Webhooks (event notifications)
  - Standard files (CSV) for stock feeds
- **Integrations page:** https://www.onestock-retail.com/platform/open-oms/integrations/
- **commercetools marketplace:** https://marketplace.commercetools.com/integration/onestock

### Authentication

Not publicly documented in detail. API portal access required.

### User Reviews

Strong presence in European retail. Listed in Gartner Market Guide for DOM.

### Pricing

Enterprise custom pricing. Not publicly listed.

### Multi-Node Inventory Handling

**Excellent.** Core capability -- stock unification across warehouses, stores, DCs, suppliers with AI-driven orchestration for optimal routing.

---

## 9. Deck Commerce

**Category:** D2C Order Management System
**Website:** https://www.deckcommerce.com

### What It Does

Deck Commerce is a **cloud-native, API-first OMS** focused on direct-to-consumer (D2C) brands. Emphasizes operational reliability and performance.

Key capabilities:
- **Advanced order routing / DOM** across fulfillment network
- **BOPIS, BORIS, ROPIS, ship-from-store**
- **Marketplace and channel management**
- **1M+ orders/day peak processing**
- **Sub-250ms API response times**
- **99.999% uptime SLA**

### Technical Documentation

- **API-first design** with REST APIs
- **Event-driven architecture**
- **75+ prebuilt integrations** (ERP, WMS, POS, ecommerce)
- **Shopify App:** https://apps.shopify.com/deckcommerce
- **Salesforce AppExchange:** https://appexchange.salesforce.com/appxListingDetail?listingId=5ce62035-504b-44d2-9c05-e02c84781a3b

### Pricing

Not publicly listed. Contact for quote.

### Multi-Node Inventory Handling

**Strong.** Unifies inventory and fulfillment across every system and channel with intelligent routing.

---

## 10. Pipe17

**Category:** AI-Native Order Operations Platform
**Website:** https://pipe17.com

### What It Does

Pipe17 is an **AI-native order operations platform** for mid-market and enterprise brands and 3PLs. Focuses on managed connectivity and intelligent order management without requiring API development.

Key capabilities:
- **Unified API** standardizing commerce data across all systems
- **AI routing** (proximity, real-time inventory, weather conditions)
- **300+ managed connectors** (selling channels, fulfillment, ERPs, WMSs)
- **No-code rule configuration** for order routing, SKU mapping, split shipments
- **AI agent "Pippen"** for order operations automation
- **Bundle/kit management, returns, exception handling**

### Technical Documentation

- **Technology page:** https://pipe17.com/technology/
- **Unified API** available (standardizes data across connected systems)
- **Note:** One source states Pipe17 does not have a public API -- the platform emphasizes no-code configuration rather than developer API access
- **commercetools integration:** https://marketplace.commercetools.com/integration/pipe17-inc
- **Radial integration:** https://pipe17.com/integration/radial/

### User Reviews

**G2:** https://www.g2.com/products/pipe17/reviews
**GetApp:** https://www.getapp.com/operations-management-software/a/pipe17/

**Strengths:**
- Easy setup with prebuilt connectors
- No-code rule configuration
- Excellent for Shopify/ecommerce operations
- Strong customer support

**Weaknesses:**
- Pricing increases reported (128% in under 2 years per one review)
- Long contracts
- Bugs reported
- Enterprise Support charged separately

### Pricing

- **Starting:** $99/month
- **Shopify App:** $24,000/year
- **Enterprise:** Custom pricing
- Pricing page: https://pipe17.com/pricing/

### Multi-Node Inventory Handling

**Good.** AI routing considers real-time inventory across connected nodes. Relies on connected systems for source inventory data.

---

## 11. Softeon

**Category:** DOM + WMS (Joint Deployment)
**Website:** https://www.softeon.com

### What It Does

Softeon is a **Tier-1 WMS expert** that also offers a powerful Distributed Order Management (DOM) system. Market leader in joint DOM-WMS deployments.

Key capabilities:
- **Distributed order management** across diverse fulfillment networks
- **Real-time inventory visibility** across company DCs, 3PL, stores, suppliers
- **Order routing** based on customer service requirements and cost optimization
- **Capacity and constraint-aware** fulfillment decisions
- **Order lifecycle management** (entry, pricing, promotions, credit, invoicing)
- **Subscription management, backorders, SKU bundling**

### Technical Documentation

- **DOM page:** https://www.softeon.com/solutions/distributed-order-management-system-dom/
- **OMS page:** https://www.softeon.com/our-solutions/product-solutions/order-management
- **API status:** Conflicting reports -- one source says no API, another says API available
- **Integration:** Enterprise Integration Workbench (EIW) with standard APIs for ERP, WMS integration
- Pre-built connections to retail vendors

### User Reviews

**G2:** https://www.g2.com/products/softeon-distributed-order-management-system/reviews
**GetApp:** https://www.getapp.com/operations-management-software/a/softeon/
**Capterra:** https://www.capterra.com/p/208942/DOMS/
**Gartner:** https://www.gartner.com/reviews/product/softeon-warehouse-management-system

**Strengths:**
- Tier-1 WMS with integrated DOM
- Strong for complex warehouse operations
- Granular inventory visibility

**Weaknesses:**
- API availability unclear / possibly limited
- Enterprise-focused, may be heavy for mid-market
- Pricing not transparent

### Pricing

Not publicly listed. Enterprise custom pricing. Contact required.

### Multi-Node Inventory Handling

**Excellent.** Core capability -- granular, real-time visibility across company-owned facilities, 3PL DCs, stores, suppliers with cost-optimized routing considering capacity constraints.

---

## 12. Tecsys (Elite / Itopia / OrderDynamics)

**Category:** Supply Chain Management / OMS
**Website:** https://www.tecsys.com

### What It Does

Tecsys provides supply chain management solutions including:
- **Elite Distribution ERP** -- built on Itopia low-code platform
- **OrderDynamics** -- cloud-native SaaS OMS for omnichannel retail
- **Elite WMS** -- warehouse management (11 consecutive years on Gartner MQ)

Key capabilities:
- **Distributed order management** (OrderDynamics)
- **Real-time inventory visibility**
- **Advanced order routing and consolidation**
- **Store fulfillment**
- **Returns management**
- **Distribution ERP** with order processing, fulfillment, billing

### Technical Documentation

- **Itopia Platform:** https://www.tecsys.com/elite-solutions/itopia-low-code-application-platform
- **API Integration infographic:** https://infohub.tecsys.com/hubfs/Infographics/API-Integration-infographic.pdf
- **Developer Guide (VA):** https://www.oit.va.gov/Services/TRM/files/TECSYSDeveloperGuideiTopiaFramework.pdf
- **API status:** Conflicting reports -- open APIs and connectors for ERP, material handling, automation
- Itopia's APIs for scaling technology ecosystem

### User Reviews

**G2:** https://www.g2.com/products/tecsys-elite/reviews
**Capterra:** https://www.capterra.com/p/121313/TECSYS-Distribution-Management/reviews/
**Gartner:** https://www.gartner.com/reviews/market/warehouse-management-systems/vendor/tecsys/product/elite-warehouse-management

**Strengths:**
- Very customizable for advanced users
- Strong WMS capabilities (Gartner MQ for 11 years)
- Comprehensive feature set
- Healthcare and distribution specialization

**Weaknesses:**
- Licensing and maintenance fees add up quickly
- Requires significant daily upkeep/maintenance
- Steep learning curve

### Pricing

Not publicly listed. Enterprise licensing. G2 notes pricing not available on their platform. Licensing + maintenance can be significant.

### Multi-Node Inventory Handling

**Good.** OrderDynamics provides real-time inventory visibility and distributed order management across multiple locations. Elite ERP handles multi-warehouse inventory management.

---

## 13. Aptos (formerly Epicor Retail)

**Category:** Unified Retail Commerce / OMS
**Website:** https://www.aptos.com

### What It Does

Aptos (spun off from Epicor in 2015) provides a **unified commerce platform** for retail, with 122,000 stores live on the platform and 100+ websites generating $1B+ in web orders.

Key capabilities:
- **Enterprise Order Management** -- anticipate, adapt, align to customer expectations
- **Store fulfillment** (BOPIS, Click & Collect, ship-from-store, endless aisle)
- **Intelligent order routing** with real-time monitoring
- **Merchandising and inventory management**
- **POS / mobile POS**
- **Digital commerce**

### Technical Documentation

- **OMS page:** https://www.aptos.com/product/order-management
- **Store Fulfillment:** https://www.aptos.com/product/store-fulfillment
- **API:** Confirmed available, but documentation is **not publicly accessible**
- Developer portal access likely requires customer/partner relationship
- Brochure: https://www.aptos.com/assets/aptos-eom-brochure-091218-en_p5J2Rbj.pdf

### User Reviews

Limited public reviews. Enterprise retail focus. Listed in CIO Radar 2022 for Order Management.

### Pricing

Not publicly listed. Enterprise retail pricing.

### Multi-Node Inventory Handling

**Strong.** Built on unified commerce platform -- manages inventory across stores, DCs, and digital channels with intelligent order routing.

---

## 14. Korber / Enspire Commerce

**Category:** Unified Commerce / OMS (Microservices)
**Website:** https://koerber-supplychain.com

### What It Does

Korber acquired enVista's Enspire Commerce platform in September 2022. It is one of the **first OMS providers to offer cloud-based microservices order management**.

Key capabilities:
- **Order orchestration** with microservices architecture
- **Enterprise inventory availability** in real-time
- **Store fulfillment, dropship, marketplace integration**
- **Customer care tools**
- **Subscriptions management**
- **PIM, POS/mPOS, mobile fulfillment**
- **Shipment experience management**
- **Multi-currency, multi-language, multi-tax** support

### Technical Documentation

- **OMS page:** https://koerber-supplychain.com/supply-chain-solutions/supply-chain-software/order-management-system/
- **Unified Commerce:** https://koerber-supplychain.com/supply-chain-solutions/supply-chain-software/unified-commerce-platform/
- **Architecture:** Microservices-based, API-first, headless
- **APIs:** Enhance integration with ERP, CRM, WMS, loyalty, subscriptions, payment, email, tax systems
- No public developer portal identified

### User Reviews

**The Retail Exec:** https://theretailexec.com/tools/koerber-order-management-system/ (detailed review)
**Capterra:** https://www.capterra.com/p/147168/Enspire-Commerce/
**GetApp:** https://www.getapp.com/operations-management-software/a/enspire-commerce/

**Strengths:**
- Early mover in cloud microservices OMS
- Comprehensive unified commerce platform
- Strong international support (multi-currency/language)
- Good for mid-to-large retailers

**Weaknesses:**
- Transition from enVista to Korber may create confusion
- Documentation not publicly available

### Pricing

Not publicly listed. Enterprise pricing.

### Multi-Node Inventory Handling

**Excellent.** Enterprise inventory availability across warehouses, stores, fulfillment centers with real-time updates. Handles transfers, replenishments, and avoids double-selling.

---

## 15. Pulse Commerce

**Category:** Omnichannel Order & Inventory Management
**Website:** https://www.pulse-commerce.com

### What It Does

Pulse Commerce provides a complete order and inventory platform for **growing enterprises**, with particular strength in mid-market retail.

Key capabilities:
- **Distributed order management** with intelligent order routing
- **Enterprise inventory** -- multi-location allocation, tracking, ATP (Available-to-Promise)
- **Pre-sale and back-order management**
- **Fulfillment optimization** (pick-and-pack, carrier integration, order splitting)
- **Customer service and loyalty** (order capture/modify/cancel, returns, credits, reward points)
- **Product Information Manager (PIM)**
- **Fraud and tax management**

### Technical Documentation

- **OMS page:** https://www.pulse-commerce.com/products/order-management-system/
- **API:** Robust APIs for real-time inventory updates from WMS and POS systems
- **Native integrations:** Certified APIs for Shopify, Magento, BigCommerce
- **Shipping integrations:** FedEx, UPS, DHL, USPS, Endicia, Echo Global
- **Open API** for custom system connections
- **Shopify App:** https://apps.shopify.com/pulse-commerce

### User Reviews

Limited public reviews. Mid-market focus.

### Pricing

Not publicly listed. Contact for pricing.

### Multi-Node Inventory Handling

**Good.** Multi-location inventory allocation and tracking with ATP capabilities. Real-time updates from WMS and POS across locations.

---

## 16. Brightpearl (by Sage)

**Category:** Retail Operating System / ERP-lite
**Website:** https://www.brightpearl.com

### What It Does

Brightpearl (acquired by Sage in 2022) is the **#1 Retail Operating System** for ecommerce, multichannel retail brands and wholesalers.

Key capabilities:
- **Order management** across all channels
- **Inventory and warehouse management**
- **Purchasing and supply chain**
- **Accounting and financial management** (integrated with Sage Intacct)
- **CRM and customer management**
- **Analytics and reporting**
- **Returns management**

### Technical Documentation

- **API Docs:** https://api-docs.brightpearl.com/
- **Sage Developer Portal:** https://developer.sage.com/brightpearl
- **Developer Area:** https://help.brightpearl.com/hc/en-us/categories/201519763-API-Developer
- **Getting Started:** https://help.brightpearl.com/hc/en-us/articles/211124866-Getting-Started-with-the-API-Apps

### Authentication

- **Recommended:** OAuth 2.0 (Instance app method)
- **Token endpoint:** OAuth 2.0 specification compliant
- **Private apps:** Headers `brightpearl-app-ref` + `brightpearl-account-token`
- **Legacy auth:** Also supported but not recommended for new apps
- **Token introspection:** https://api-docs.brightpearl.com/utilities/oauth-token-introspect/post.html
- **Developer account:** Required at https://developer.brightpearl.com/

### User Reviews

**Capterra:** https://www.capterra.com/p/124180/Brightpearl/
**Shopify App Store:** https://apps.shopify.com/brightpearl-by-sage

**Strengths:**
- Comprehensive retail operating system (orders + accounting + inventory)
- Deep API access with good documentation
- Large integration library (Plug & Play)
- Strong Sage Intacct integration for financials
- Good for multichannel retailers

**Weaknesses:**
- Not a true DOM/order promising system (simpler routing)
- Limited advanced sourcing optimization
- Better suited for mid-market, not enterprise complexity

### Pricing

Not publicly listed on review sites. Contact Brightpearl/Sage for pricing.

### Multi-Node Inventory Handling

**Moderate.** Manages inventory across multiple locations/warehouses with sync capabilities but lacks sophisticated DOM-level sourcing optimization and order promising.

---

## 17. Linnworks

**Category:** Multichannel Order & Inventory Management
**Website:** https://www.linnworks.com

### What It Does

Linnworks provides **connected commerce operations for multichannel retail growth**, automating order management, inventory sync, and fulfillment across channels.

Key capabilities:
- **Multichannel order management** in single dashboard
- **Automatic order sorting, prioritization, and routing** at scale
- **Inventory sync** across all channels
- **100+ integrations** (Amazon, eBay, Shopify, Magento, carriers)
- **Amazon Multi-Channel Fulfillment (MCF)** integration
- **Multichannel listing management**
- **Analytics and forecasting**

### Technical Documentation

- **Documentation:** https://docs.linnworks.com/
- **API Reference:** https://apidocs.linnworks.net/
- **API Reference (detailed):** https://apidocs.linnworks.net/reference/overview
- **Orders API:** https://help.linnworks.com/support/solutions/folders/7000032995
- **Developer Portal:** https://developer.linnworks.com
- **Complete API list:** http://apps.linnworks.net/Api
- **Support Center API section:** https://help.linnworks.com/support/solutions/7000000878

### Key API Endpoints

- `GetOpenOrders` -- Pull open orders
- `GetOrdersById` -- Detailed order information
- `GetStockLocations` -- Available locations and IDs
- API access enables advanced customization

### User Reviews

**The Retail Exec:** https://theretailexec.com/tools/linnworks-review/ (detailed 2026 review)
**Shopify App Store:** https://apps.shopify.com/linnworks

**Strengths:**
- Excellent multichannel connectivity (100+ integrations)
- Strong automation capabilities
- Good for ecommerce sellers managing multiple marketplaces
- Amazon MCF integration

**Weaknesses:**
- Not an enterprise DOM solution
- Limited advanced order promising/sourcing
- More focused on marketplace sellers than complex retail

### Pricing

Not publicly detailed in search results. Check Linnworks website.

### Multi-Node Inventory Handling

**Moderate.** Syncs inventory across channels and locations. Automated routing rules. But not a sophisticated multi-node sourcing optimizer -- better for marketplace channel management.

---

## 18. Cin7

**Category:** Inventory & Order Management for SMB/Mid-Market
**Website:** https://www.cin7.com

### What It Does

Cin7 is a **cloud-based inventory management platform** that integrates inventory, sales channels, purchasing, and accounting. Offers two products: **Cin7 Core** (formerly DEAR Inventory) and **Cin7 Omni**.

Key capabilities:
- **Multi-location inventory management** across warehouses and stores
- **Order management** and shipping automation
- **700+ integrations** (ecommerce, marketplaces, 3PL, shipping)
- **Real-time inventory tracking**
- **Pick-and-pack fulfillment**
- **Purchasing and receiving**
- **Manufacturing and production**

### Technical Documentation

- **Cin7 Omni API:** https://api.cin7.com/
- **Cin7 Core Developer Portal (Apiary):** https://dearinventory.docs.apiary.io/
- **API Help:** https://help.core.cin7.com/hc/en-us/sections/10207284005007-Cin7-API
- **API V1 Introduction:** https://help.core.cin7.com/hc/en-us/articles/9982508120975-API-V1-introduction
- **Connection Guide:** https://help.core.cin7.com/hc/en-us/articles/9982480315407-Connecting-to-the-Cin7-Core-API

### Authentication

- **Method:** API Key authentication via headers
- **Headers:** `api-auth-accountid` + `api-auth-applicationkey`
- **Key Generation:** https://inventory.dearsystems.com/ExternalAPI
- **Data Format:** JSON
- **API Version:** V2 recommended (migration from V1)

### User Reviews

**Shopify App Store:** https://apps.shopify.com/dear-inventory
**ShipStation partner page:** https://www.shipstation.com/partners/cin7/

**Strengths:**
- Simple and affordable for SMB
- Large integration library (700+)
- Good inventory management features
- Manufacturing support

**Weaknesses:**
- Not a DOM solution
- No advanced order promising or sourcing optimization
- Better for simpler operations

### Pricing

Check website. SMB pricing model.

### Multi-Node Inventory Handling

**Basic-to-Moderate.** Multi-location inventory tracking with per-warehouse sync. Not a sophisticated sourcing/routing optimizer.

---

## 19. Celigo

**Category:** iPaaS / Integration Platform (Not an OMS)
**Website:** https://www.celigo.com

### What It Does

Celigo is an **Integration Platform as a Service (iPaaS)**, not an order management system. It connects applications, automates workflows, and synchronizes data. Relevant to this space as a **middleware/integration layer**.

Key capabilities:
- **1,000+ prebuilt connectors** (ERP, CRM, ecommerce, marketing)
- **Packaged Integration Processes (PIPs)** for order-to-cash, quote-to-cash
- **Full lifecycle API management** (build, secure, publish, monitor)
- **Supports:** HTTP, FTP, JDBC, AS2, GraphQL, Webhooks
- **Automates 70% faster** with IT-governed templates

### Technical Documentation

- **Platform:** https://www.celigo.com/platform/
- **API Management:** https://www.celigo.com/platform/api-management/
- **Connection docs:** https://docs.celigo.com/hc/en-us/articles/360038520652-Set-up-a-connection-to-Celigo-integrator-io
- **integrator.io:** https://integrator.io/

### Relevance to Order Promising/Sourcing

Celigo is a **connector/middleware**, not a source of promising or sourcing capabilities. It can be used to integrate OMS, WMS, ERP, and ecommerce systems. Relevant as infrastructure but not a direct competitor to DOM/OMS vendors.

### Pricing

Tiered pricing. Contact for details. https://www.celigo.com/ has pricing info.

---

## 20. Vinculum

**Category:** Omnichannel OMS + WMS (Asia-Pacific focus)
**Website:** https://www.vinculumgroup.com

### What It Does

Vinculum provides an **AI-driven SaaS suite** for omnichannel commerce, with strong presence in Asia-Pacific and emerging markets.

Key capabilities:
- **Omnichannel OMS** (BOPIS, BORIS, ship-from-store, endless aisle)
- **Unified inventory** across warehouses, stores, 3PLs, marketplaces
- **WMS** for warehouse operations
- **150+ ecommerce/fulfillment partner integrations**
- **Seller panel** for marketplace management

### Technical Documentation

- **Product Guide:** https://docs.vineretail.com/
- **API Documentation:** https://vinculumhelpdesk.freshdesk.com/support/solutions/folders/9000195283
- **eRetail Sales:** https://docs.vineretail.com/eretail-sales-section/
- **Admin docs:** https://docs.vineretail.com/vin-eretail-admin/
- API supports order creation, status updates, inventory reconciliation, order edits
- Real-time fulfillment status push (pick confirmation, shipment, delivery exceptions)

### Pricing

Not publicly listed. Contact for pricing.

### Multi-Node Inventory Handling

**Good.** Unified inventory across warehouses, stores, 3PLs, marketplaces. Supports complex omnichannel fulfillment scenarios.

---

## 21. Deposco

**Category:** Unified OMS + WMS Platform
**Website:** https://deposco.com

### What It Does

Deposco provides **unified order and warehouse management on a single platform**, targeting mid-market and growing enterprises.

Key capabilities:
- **Order management and orchestration**
- **Warehouse management system**
- **Distributed fulfillment**
- **Inventory optimization**
- **Demand planning**

### Technical Documentation

- **Developer Portal:** https://developer.deposco.com/ (login required)
- **GitHub client:** https://github.com/launched-la/deposco-api
- **Authentication:** Tenant Code + Username + Password
- **Key Endpoint:** `PUT /integration/{code}/import/{businessUnit}/customerOrder/{orderNumber}`
- **Parameters:** Tenant Code, Deposco URL, API Username, API Password, Business Unit
- **Integration connectors** via Patchworks, Extensiv, DropStream

### Pricing

Not publicly listed. Contact for pricing.

### Multi-Node Inventory Handling

**Good.** Unified platform handles inventory across fulfillment locations with order orchestration capabilities.

---

## Market Summary & Comparison Matrix

### By Category

| Category | Vendors |
|----------|---------|
| **Enterprise DOM (Tier 1)** | IBM Sterling, Manhattan Associates, Fluent Commerce |
| **Enterprise OMS** | Radial, Kibo Commerce, Softeon, Korber/Enspire |
| **Mid-Market OMS** | Deck Commerce, Pulse Commerce, Tecsys OrderDynamics, OneStock |
| **Composable Commerce** | commercetools (+ DOM partner), Kibo |
| **Multichannel/SMB** | Brightpearl, Linnworks, Cin7, Vinculum |
| **Order Operations** | Pipe17 |
| **EDI/Connectivity** | Orderful |
| **iPaaS/Integration** | Celigo |
| **Unified OMS+WMS** | Deposco, Softeon, Tecsys |

### API Maturity Comparison

| Vendor | API Type | Auth | Public Docs | Developer Portal |
|--------|----------|------|-------------|------------------|
| **Orderful** | REST/JSON | API Key | Yes | docs.orderful.com |
| **Radial** | REST/XML | API Security Layer | Yes | docs.radial.com |
| **Fluent Commerce** | GraphQL (primary) + REST | OAuth 2.0 | Yes | docs.fluentcommerce.com |
| **Kibo Commerce** | REST/JSON | OAuth 2.0 JWT | Yes | docs.kibocommerce.com |
| **IBM Sterling** | REST (XAPI) + SOAP | Varies | Partial | ibm.com/docs |
| **Manhattan** | REST + GraphQL | OAuth 2.0/OIDC | Gated | Requires license |
| **commercetools** | REST + GraphQL | OAuth 2.0 | Yes | docs.commercetools.com |
| **OneStock** | REST + Webhooks | Unknown | Partial | API Portal available |
| **Deck Commerce** | REST | Unknown | No | N/A |
| **Pipe17** | Unified API (internal) | N/A | No | No public API |
| **Softeon** | REST (via EIW) | Unknown | No | N/A |
| **Brightpearl** | REST | OAuth 2.0 | Yes | developer.sage.com/brightpearl |
| **Linnworks** | REST | API Token | Yes | apidocs.linnworks.net |
| **Cin7** | REST/JSON | API Key | Yes | api.cin7.com / Apiary |
| **Vinculum** | REST | API Key | Partial | Freshdesk portal |
| **Deposco** | REST | User/Pass | Login required | developer.deposco.com |

### Order Promising / ATP Capabilities

| Vendor | ATP/CTP | Sourcing Optimization | Multi-Node Routing |
|--------|---------|----------------------|-------------------|
| **IBM Sterling** | Best-in-class | Advanced | Advanced |
| **Manhattan** | Best-in-class | Advanced | Advanced |
| **Fluent Commerce** | Strong | Rules-based | Advanced |
| **Kibo Commerce** | Strong | AI-enhanced | Advanced |
| **Radial** | Strong | Cost-optimized | Advanced |
| **Softeon** | Strong | Constraint-aware | Advanced |
| **OneStock** | Strong | AI-driven | Advanced |
| **Korber/Enspire** | Good | Configurable | Good |
| **Deck Commerce** | Good | Rule-based | Good |
| **Pulse Commerce** | Good (explicit ATP) | Basic | Moderate |
| **Tecsys** | Good | Configurable | Good |
| **Aptos** | Good | Retail-focused | Good |
| **Pipe17** | Moderate | AI routing | Moderate |
| **Brightpearl** | Basic | Basic | Basic |
| **Linnworks** | Basic | Channel-based | Basic |
| **Cin7** | Basic | Basic | Basic |
| **commercetools** | None (needs partner) | None | None |
| **Orderful** | N/A (EDI layer) | N/A | N/A |
| **Celigo** | N/A (iPaaS) | N/A | N/A |

---

## Additional ATP/CTP Software Vendors (ERP-Embedded)

These vendors provide order promising as part of broader ERP/MRP systems:

| Vendor | Product | ATP/CTP | Notes |
|--------|---------|---------|-------|
| **Microsoft** | Dynamics 365 SCM | Both | Full ATP + CTP with production capacity consideration |
| **DELMIAWorks** | Manufacturing ERP | Both | CTP with scheduling, material, and capacity checks |
| **SAP** | S/4HANA / EWM | Both | Enterprise ATP with global available-to-promise (gATP) |
| **Oracle** | SCM Cloud | Both | Advanced ATP with supply/demand planning |
| **E21 ERP** | Enterprise 21 | Both | Mid-market manufacturing ERP with ATP/CTP |
| **TGI** | Enterprise 21 | Both | Web ERP with ATP/CTP for manufacturing |

---

## Sources

- [Orderful Platform](https://www.orderful.com)
- [Orderful Developer Hub](https://docs.orderful.com/)
- [Orderful Pricing](https://www.orderful.com/pricing)
- [Orderful G2 Reviews](https://www.g2.com/products/orderful-edi/reviews)
- [Radial OMS](https://www.radial.com/solutions/omnichannel-solutions/order-management-system)
- [Radial Developer Portal](https://developer-apina.gsipartners.com/technology/retail-order-management)
- [Radial Documentation](https://docs.radial.com/)
- [Radial API Reference](https://docs.radial.com/Content/Topics/api-reference.htm)
- [Fluent Commerce](https://fluentcommerce.com)
- [Fluent Commerce Docs](https://docs.fluentcommerce.com/)
- [Kibo Commerce](https://kibocommerce.com)
- [Kibo Docs](https://docs.kibocommerce.com/)
- [IBM Sterling OMS](https://www.ibm.com/products/order-management)
- [IBM Sterling Docs](https://www.ibm.com/docs/en/order-management)
- [Manhattan Associates OMS](https://www.manh.com/solutions/omnichannel-software-solutions/order-management-system)
- [Manhattan Enterprise Promise & Fulfill](https://www.businesswire.com/news/home/20250603427856/en/)
- [commercetools API](https://docs.commercetools.com/api)
- [commercetools Pricing](https://commercetools.com/pricing)
- [OneStock OMS](https://www.onestock-retail.com)
- [OneStock API Portal](https://www.onestock-retail.com/services/developers/api-portal/)
- [Deck Commerce](https://www.deckcommerce.com)
- [Pipe17](https://pipe17.com)
- [Pipe17 Pricing](https://pipe17.com/pricing/)
- [Softeon DOM](https://www.softeon.com/solutions/distributed-order-management-system-dom/)
- [Tecsys Itopia](https://www.tecsys.com/elite-solutions/itopia-low-code-application-platform)
- [Tecsys OrderDynamics Capterra](https://www.capterra.com/p/191871/OrderDynamics/)
- [Aptos OMS](https://www.aptos.com/product/order-management)
- [Korber OMS](https://koerber-supplychain.com/supply-chain-solutions/supply-chain-software/order-management-system/)
- [Pulse Commerce](https://www.pulse-commerce.com)
- [Brightpearl API Docs](https://api-docs.brightpearl.com/)
- [Brightpearl Developer Portal](https://developer.sage.com/brightpearl)
- [Linnworks API Docs](https://apidocs.linnworks.net/)
- [Linnworks Documentation](https://docs.linnworks.com/)
- [Cin7 Omni API](https://api.cin7.com/)
- [Cin7 Core API (Apiary)](https://dearinventory.docs.apiary.io/)
- [Celigo Platform](https://www.celigo.com/platform/)
- [Vinculum](https://www.vinculumgroup.com)
- [Deposco Developer Portal](https://developer.deposco.com/)
- [Gartner DOM Reviews](https://www.gartner.com/reviews/market/distributed-order-management-systems)
- [Gartner 2025 Market Guide for DOM](https://www.gartner.com/en/documents/5085931)
- [Forrester Wave 2025 OMS](https://www.manh.com/our-insights/resources/research-reports/forrester-wave-order-management-systems)
- [OMS Market $3.64B by 2030](https://www.globenewswire.com/news-release/2025/03/31/3052346/0/en/)
- [The Retail Exec - Best DOM Software](https://theretailexec.com/tools/best-distributed-order-management-software/)
- [Deposco Best OMS 2026](https://deposco.com/blog/best-order-management-systems-oms-2026/)
- [Pipe17 Top 15 OMS 2025](https://pipe17.com/blog/top-15-order-management-systems-for-agentic-commerce-in-2025/)
- [Microsoft Dynamics 365 Order Promising](https://learn.microsoft.com/en-us/dynamics365/supply-chain/sales-marketing/delivery-dates-available-promise-calculations)
- [DELMIAWorks CTP](https://www.solidworks.com/product/delmiaworks/manufacturing-erp/manufacturing/scheduling/ctp/)
