# Fluent Commerce: Order Promising & Sourcing Research

> **Last updated:** 2026-03-31
> **Vendor:** Fluent Commerce (fluent commerce.com)
> **Product:** Fluent Order Management (Fluent OMS / OMX)
> **HQ:** Sydney, Australia (offices in UK, US, APAC)
> **Notable customers:** JD Sports, Prada Group, Ted Baker, Aldo, LVMH, Dulux

---

## 1. What It Does

### 1.1 Distributed Order Management (DOM)

Fluent Commerce is a **cloud-native, API-first Distributed Order Management System** built on an event-driven microservices architecture. It orchestrates order flows across multiple sales channels, warehouses, stores, and fulfillment partners.

Core modules:
- **Fluent Order Orchestration** -- end-to-end order lifecycle management including sourcing, allocation, fulfillment, returns, and exceptions
- **Fluent Order Promising** -- real-time delivery and pickup option calculation based on inventory and fulfillment capacity
- **Fluent Big Inventory** -- unified inventory visibility and Available-to-Promise (ATP) across all nodes

### 1.2 Order Promising

Fluent Order Promising calculates and displays delivery and pickup options **before the customer clicks "buy"**, based on:

- Real-time inventory positions across all fulfillment nodes
- Customer location (geo-distance to fulfillment locations)
- Location attributes: capacity, operating hours, carrier pickup times, processing backlogs
- Cart reservation to prevent overselling

**Promise types supported:**
- Available-to-Promise (ATP) -- current on-hand stock minus reservations and safety stock
- Capable-to-Promise (CTP) -- factors in inbound inventory and future stock arrival dates
- Pre-order/backorder promising against inbound inventory with estimated fulfillment times

**ATP configuration levers:**
- Safety/buffer stock per location, channel, product, or category
- Virtual inventory pools controlling which stock appears on which sales channel
- Customer tier/loyalty-based ATP rules (e.g., VIP customers see more stock)
- Basket value-based promising rules

### 1.3 Sourcing Logic

Fluent uses a **Responsive Sourcing Framework** with configurable sourcing profiles, strategies, conditions, and criteria. Released October 2025, this framework enables business users to manage sourcing logic without developer involvement.

**Sourcing strategies include:**
- **Proximity First** -- prioritize closest fulfillment location to customer
- **Cost Optimized** -- minimize total fulfillment cost (shipping + handling)
- **Speed Priority** -- fastest delivery regardless of cost
- **Inventory-based** -- route to location with lowest sell-through, oldest stock, highest discounts, or excess inventory
- **Peak Period** -- special sourcing rules during high-demand periods
- **Bulky Items** -- dedicated routing for oversized goods

**Sourcing decision factors:**
- Distance to customer
- Stock levels at each node
- Delivery times and carrier schedules
- Processing backlogs and location capacity
- Profitability (margin optimization)
- Customer loyalty tier
- Order value
- Product attributes

**Split shipment handling:**
- Cost-aware logic determines optimal split across multiple nodes
- Configurable maximum splits based on order value, customer tier, etc.
- Line-item level inventory reservation at chosen split locations
- Consolidated shipping orchestration for split orders
- Can block splits entirely for low-value orders

**Performance:** The architecture handles up to **500,000 allocation decisions per minute** during peak periods.

### 1.4 AI-Powered Sourcing with A/B Testing (Announced Jan 2026)

A new capability (pilot H1 2026, GA H2 2026) enables retailers to:
- Run parallel sourcing strategies across live orders simultaneously
- Configure test scenarios using AI (e.g., prioritize margin vs. reduce delivery cost)
- Set traffic splits (e.g., 50/50 or 90/10) and test duration
- Measure five KPIs in real-time:
  - Net margin
  - Fulfillment and delivery costs
  - Split shipment rate
  - Order-to-door time
  - Average delivery distance (carbon impact proxy)
- Auto-promote winning sourcing logic at scale

### 1.5 Multi-Node Inventory Aggregation

Fluent Big Inventory acts as the **inventory availability master**:
- Ingests data from ERPs, WMS, POS, and other systems
- Uses **inventory delta updates** (processing only changes, not full snapshots)
- Prioritizes critical inventory updates (fast-moving items processed first)
- Generates a single unified view across all nodes
- Virtual inventory pools segment stock availability per channel
- Supports inbound inventory tracking for future-stock promising

**Scale:** Processed **1.2 billion+ inventory position updates** over Black Friday 2023.

---

## 2. Technical Architecture

### 2.1 Architecture Overview

| Aspect | Detail |
|--------|--------|
| Architecture | Cloud-native, event-driven microservices |
| Deployment | Fully managed SaaS (AWS Marketplace available) |
| API paradigm | API-first; GraphQL (primary) + REST (platform ops) |
| Workflow engine | Rules-based workflow framework with 200+ orchestrated domain rules |
| Extensibility | SDKs for rules, components, and connectors |
| Performance | 675+ orders/second; 500K allocation decisions/minute |

### 2.2 Event-Driven Design

The platform uses an event-based framework where orders, fulfillment, inventory, and returns communicate asynchronously. Middleware subscribes to updates and passes them to other services. This enables:
- Decoupled service scaling
- Real-time inventory position updates
- Webhook-driven external integrations

---

## 3. APIs and Developer Tools

### 3.1 API Surface

**GraphQL API (Primary -- Domain Model):**
- All domain entity operations (orders, inventory, fulfillment, customers, products)
- Single POST endpoint; clients specify exact fields needed
- Multiple queries/mutations per request to reduce latency
- Built-in schema introspection for client-side validation
- Reference docs: `https://api.production.shared-sydney-01.fluentcommerce.com/graphql/docs/`
- Permission-controlled access per operation

**REST APIs (Platform Level):**
| API | Version | Purpose |
|-----|---------|---------|
| Authentication API | -- | OAuth 2.0 token management |
| Event API | v4.1 | Workflow integration and event triggering |
| Workflow API | v4.1 | Business logic orchestration setup |
| Job API | v4.1 | Batch loading operations |
| Plugin API | v4.1 | Plugin bundle management |
| User Action API | v4.1 | Portal and external app interactions |

**Note:** All domain-level REST APIs are **deprecated/maintenance mode**. New integrations must use GraphQL.

### 3.2 Authentication

**OAuth 2.0 flow:**
- Endpoint: `<root_url>/oauth/token` (POST, HTTPS)
- Parameters via `application/x-www-form-urlencoded` (recommended) or query string
- Credentials: username, password, Client ID, Client Secret
- Account ID passed in `fluent.account` header

**Token types:**
| Token | Standard Client | FLUENT_INTEGRATION Client |
|-------|----------------|--------------------------|
| Access token | 24-hour expiry | 30-minute expiry (1800s) |
| Refresh token | -- | 24-hour validity, single-use |

**Additional credentials:**
- API Key: for Store Locator and JavaScript widgets
- API Client ID & Secret: one per retailer for REST API access

**Security best practices (from docs):**
- Store tokens securely; never in client-side code
- Refresh proactively 5-10 minutes before expiry
- Clear tokens on logout or auth errors

### 3.3 Webhooks

- Outbound webhooks from workflow events to external systems
- Connect SDK webhook endpoint: `/api/v1/fluent-connect/webhook`
- **Cryptographic signing:** MD5 checksum of full request body, signed with RSA private key
- Signature in `flex.signature` header
- Verify using Fluent Commerce public key (x509 base64 encoded)
- Method: MD5WithRSA

### 3.4 SDKs

| SDK | Technology | Purpose |
|-----|-----------|---------|
| **Rules SDK** | Java | Custom workflow rules; includes Java API client for REST and GraphQL |
| **Connect SDK** | Java (Spring Boot) | External system integration; Maven archetype for building connector microservices |
| **Component SDK** | React | Custom UI components for Fluent web apps; uses hooks for UX framework features |
| **CLI** | -- | Command-line tooling for development |
| **Builder MCP Server** | -- | Development server tooling |

**Connect SDK architecture:**
- Java Maven Archetype + Java Library Utils
- Builds Spring Boot microservices
- Supports synchronous (real-time) and asynchronous operations
- Cloud-agnostic deployment; independently deployable and scalable
- Standardized credential handling, logging, and configuration
- Integration layer owned and maintained by the solution integrator

**Rules SDK:**
- Java-based toolkit for custom rules in the OMX Workflow Framework
- Includes Java API client for both REST and GraphQL
- Custom rules extend the 200+ built-in domain rules

### 3.5 Sourcing Utilities (Java Library)

The `util-sourcing` library provides four utility classes:
1. **SourcingUtils** -- orchestrates sourcing process, loads sourcing profiles
2. **SourcingContextUtils** -- manages order details, unfulfilled items, supporting data
3. **OrderUtils** -- fulfillment creation and type determination
4. **LocationUtils** -- distance calculations and location caching

**Sourcing execution pipeline:**
1. Load sourcing profile (conditions + strategies)
2. Create sourcing context (customer location, unfulfilled items, available locations)
3. Evaluate strategies (proximity, cost, speed, inventory)
4. Generate sourcing plan (items-to-locations mapping)
5. Create fulfillment objects

### 3.6 Developer Documentation

| Resource | URL |
|----------|-----|
| Main docs portal | https://docs.fluentcommerce.com/ |
| Getting started | https://docs.fluentcommerce.com/landing/get-started |
| GraphQL API | https://docs.fluentcommerce.com/essential-knowledge/graphql-api |
| REST API | https://docs.fluentcommerce.com/essential-knowledge/rest-api |
| Authentication | https://docs.fluentcommerce.com/essential-knowledge/authentication-api |
| APIs overview | https://docs.fluentcommerce.com/essential-knowledge/apis-overview |
| Webhooks FAQ | https://docs.fluentcommerce.com/essential-knowledge/webhooks-frequently-asked-questions |
| Event API | https://docs.fluentcommerce.com/essential-knowledge/using-the-event-api |
| Connect SDK | https://docs.fluentcommerce.com/essential-knowledge/connect-sdk-overview |
| Connect SDK architecture | https://docs.fluentcommerce.com/essential-knowledge/fluent-connect-sdk-architecture |
| Rules SDK setup | https://docs.fluentcommerce.com/by-type/setup-your-development-environment-for-rules-sdk |
| Rules SDK writing rules | https://docs.fluentcommerce.com/by-type/rules-sdk-writing-rules-overview |
| Sourcing utilities | https://docs.fluentcommerce.com/essential-knowledge/sourcing-utilities-overview |
| Responsive Sourcing | https://docs.fluentcommerce.com/release-notes/responsive-sourcing-from-technical-setup-to-business-control |
| Order splitting | https://docs.fluentcommerce.com/by-type/split-orders-across-multiple-fulfilment-locations |
| Real-time availability | https://docs.fluentcommerce.com/by-type/display-real-time-stock-availability-online |
| SDKs overview | https://docs.fluentcommerce.com/explore-categories/sdks |
| Knowledge tracks | https://docs.fluentcommerce.com/landing/knowledge-tracks |
| Packages & modules | https://docs.fluentcommerce.com/landing/packages-modules |

---

## 4. Integration Patterns

### 4.1 Integration Methods

1. **GraphQL API** -- primary method for domain operations (orders, inventory, fulfillment)
2. **REST APIs** -- platform-level operations (auth, events, workflows, jobs, plugins)
3. **Webhooks** -- outbound event notifications with RSA-signed payloads
4. **Connect SDK** -- build custom Spring Boot connector microservices
5. **Event API** -- trigger workflow events programmatically
6. **Job API** -- batch data loading (jobs close at midnight UTC)
7. **Pre-built connectors** -- available for commercetools, Salesforce B2C Commerce, and others via partners like Patchworks

### 4.2 Pre-Built Integrations

| Platform | Type |
|----------|------|
| commercetools | Marketplace connector |
| Salesforce B2C Commerce | Cartridge on AppExchange |
| Patchworks | Pre-built connector via iPaaS |
| Prismatic | Component-based integration |
| AWS Marketplace | Deployment option |

### 4.3 API Retry Patterns

Documentation references "API Retries and Exponential Back-offs" and "Authentication Token Expiry" handling, though specific rate limits and threshold values are not publicly documented.

---

## 5. User Reviews and Feedback

### 5.1 G2 Reviews

**Pros (from verified G2 reviewers):**
- Workflows fit custom operational needs; highly extendable and flexible platform
- User-friendly dashboard enables easy support in retail stores
- Enables building end-to-end customer journeys with high personalization
- Strong features for D2C, Click & Collect, Vendor Drop Ship, global inventory visibility
- Scalable for any size B2C or B2B organization
- Account managers are knowledgeable and supportive during implementation

**Cons (from verified G2 reviewers):**
- Platform upgrades need better planning -- users want advance notice and timezone-appropriate scheduling outside business hours
- Tool described as "not very customizable" by some users; access configuration is difficult
- Lack of flexibility during contract negotiation

### 5.2 Gartner Peer Insights

Fluent Commerce is listed in Gartner's **Distributed Order Management Systems** market category. Fluent references the **2025 Gartner Market Guide for Distributed Order Management Systems** in their marketing materials. Detailed ratings require Gartner access.

- URL: https://www.gartner.com/reviews/market/distributed-order-management-systems/vendor/fluent-commerce/product/fluent-order-management

### 5.3 Forrester Recognition

Fluent Commerce is referenced in **The Forrester Wave: Order Management Systems, Q1 2025**, which noted: "Fluent Commerce's pricing is straightforward, without unpleasant surprises."

### 5.4 Capterra

Fluent Commerce has a Capterra listing at https://www.capterra.com/p/179809/Fluent-Commerce/ -- detailed review content requires direct access.

### 5.5 Reddit

No significant Reddit discussions found specifically about Fluent Commerce OMS.

---

## 6. Pricing

**Model:** Custom/quote-based pricing. No published tiers.

**Key facts:**
- All pricing unique to customer requirements and usage
- Contact info@fluentcommerce.com for quotes
- Private contract with custom EULA
- Available on AWS Marketplace (separate pricing)
- Salesforce AppExchange listing available
- Forrester noted pricing is "straightforward, without unpleasant surprises"
- Pricing page: https://fluentcommerce.com/pricing/

**Competitive context:** Compared to IBM Sterling ($500K+ implementations, 6-12 months), Fluent Commerce positions as more modern and faster to deploy due to its cloud-native SaaS model.

---

## 7. Competitive Positioning

### 7.1 Strengths vs. Competitors

| Strength | Detail |
|----------|--------|
| Cloud-native | Born in the cloud, no legacy baggage (vs. IBM Sterling, Manhattan) |
| API-first | GraphQL primary API with full schema introspection |
| Rules engine | 200+ built-in rules, extensible via Java SDK |
| Business user control | Responsive Sourcing UI for non-developers |
| Event-driven | Asynchronous microservices for scale |
| Performance | 675+ orders/sec, 1.2B inventory updates (Black Friday 2023) |
| AI sourcing | A/B testing of sourcing strategies (upcoming 2026) |
| Composable | Works alongside existing ERP/WMS without replacement |

### 7.2 Weaknesses / Gaps

| Weakness | Detail |
|----------|--------|
| Opaque pricing | No published tiers; requires sales engagement |
| Java-only SDKs | Rules SDK and Connect SDK are Java/Spring Boot only |
| Upgrade communication | Users report insufficient notice for platform upgrades |
| Documentation depth | Marketing-heavy; deep technical specs require consultant access |
| Rate limits undocumented | No public rate limit information |
| GraphQL-only domain API | REST domain APIs deprecated; teams must adopt GraphQL |
| AI sourcing not yet GA | A/B testing feature in pilot through H1 2026 |

### 7.3 Key Competitors

- **Manhattan Associates** -- enterprise-grade, complex, high cost, large dev team required
- **IBM Sterling Order Management** -- legacy leader, $500K+ implementations, 6-12 month deployments
- **Salesforce Order Management** -- strong for Salesforce ecosystem shops
- **commercetools** -- composable commerce partner (Fluent integrates with it)
- **Fabric OMS** -- newer cloud-native competitor
- **Pipe17** -- mid-market focused

---

## 8. Summary Assessment for Promise Sourcing

### What Makes Fluent Commerce Relevant

1. **Strong ATP/promising engine** with real-time inventory across all nodes, configurable safety stock, virtual pools, and customer-tier-based rules
2. **Sophisticated sourcing framework** with proximity, cost, speed, and inventory-based strategies configurable by business users
3. **GraphQL API** is well-designed for integration -- clients control exactly what data they retrieve
4. **Event-driven architecture** enables real-time inventory updates and webhook-based integrations
5. **Proven scale** -- 675+ orders/sec, 1.2B inventory updates on peak days
6. **Composable** -- designed to sit alongside existing systems, not replace them

### Integration Considerations

- **Authentication:** Standard OAuth 2.0 with access + refresh tokens
- **Primary API:** GraphQL for all domain operations
- **Webhooks:** RSA-signed outbound events for real-time notifications
- **SDKs:** Java-based (Rules SDK, Connect SDK); React for UI components
- **Batch:** Job API for bulk data loading

### Key Risks

- Custom pricing makes cost comparison difficult
- Java-only SDK stack limits polyglot development teams
- Some deeper technical documentation gated behind consultant relationships
- AI-powered A/B testing not yet generally available

---

## Sources

- [Fluent Commerce Homepage](https://fluentcommerce.com/)
- [Fluent Commerce Product Overview](https://fluentcommerce.com/product/)
- [Fluent Order Promising](https://fluentcommerce.com/product/fluent-order-promising/)
- [Fluent Order Orchestration](https://fluentcommerce.com/product/fluent-order-orchestration/)
- [Fluent Big Inventory](https://fluentcommerce.com/product/fluent-big-inventory/)
- [Fluent Commerce Pricing](https://fluentcommerce.com/pricing/)
- [Fluent Commerce Fulfillment Optimization](https://fluentcommerce.com/solutions/fulfillment-optimization/)
- [Fluent Commerce ATP Landing Page](https://fluentcommerce.com/available-to-promise/)
- [Fluent Commerce Docs Portal](https://docs.fluentcommerce.com/)
- [GraphQL API Docs](https://docs.fluentcommerce.com/essential-knowledge/graphql-api)
- [REST API Docs](https://docs.fluentcommerce.com/essential-knowledge/rest-api)
- [Authentication API Docs](https://docs.fluentcommerce.com/essential-knowledge/authentication-api)
- [APIs Overview](https://docs.fluentcommerce.com/essential-knowledge/apis-overview)
- [Connect SDK Overview](https://docs.fluentcommerce.com/essential-knowledge/connect-sdk-overview)
- [Sourcing Utilities Overview](https://docs.fluentcommerce.com/essential-knowledge/sourcing-utilities-overview)
- [Responsive Sourcing Release Notes](https://docs.fluentcommerce.com/release-notes/responsive-sourcing-from-technical-setup-to-business-control)
- [Order Splitting Docs](https://docs.fluentcommerce.com/by-type/split-orders-across-multiple-fulfilment-locations)
- [Real-Time Stock Availability Docs](https://docs.fluentcommerce.com/by-type/display-real-time-stock-availability-online)
- [Webhooks FAQ](https://docs.fluentcommerce.com/essential-knowledge/webhooks-frequently-asked-questions)
- [SDKs Overview](https://docs.fluentcommerce.com/explore-categories/sdks)
- [AI-Powered Sourcing A/B Testing Announcement](https://fluentcommerce.com/resources/news/fluent-commerce-launches-ai-powered-order-sourcing-logic-with-a-b-testing-giving-retailers-proof-not-assumptions-behind-fulfillment-decisions/)
- [G2 Reviews](https://www.g2.com/products/fluent-order-management/reviews)
- [Gartner Peer Insights](https://www.gartner.com/reviews/market/distributed-order-management-systems/vendor/fluent-commerce/product/fluent-order-management)
- [Capterra Listing](https://www.capterra.com/p/179809/Fluent-Commerce/)
- [Gartner 2025 Market Guide Reference](https://fluentcommerce.com/gartner-report-2025-market-guide-for-distributed-order-management-systems/)
- [Netguru Fluent Commerce Architecture](https://www.netguru.com/blog/fluent-commerce-architecture)
- [Netguru Essential Guide to Fluent OMS](https://www.netguru.com/blog/fluent-oms)
- [Pivotree Fluent Commerce Partner Page](https://www.pivotree.com/supply-chain/fluent-commerce-order-management-system-oms/)
- [Prismatic Fluent Commerce Component](https://prismatic.io/docs/components/fluent-commerce/)
- [Patchworks Fluent Commerce Connector](https://doc.wearepatchworks.com/product-documentation/connectors-and-instances/patchworks-connectors/fluent-commerce-prebuilt-connector)
- [commercetools Marketplace - Fluent Commerce](https://marketplace.commercetools.com/integration/fluent-commerce)
- [AWS Marketplace - Fluent Order Management](https://aws.amazon.com/marketplace/pp/prodview-eigdp3nk2ctri)
- [Salesforce AppExchange - Fluent Commerce](https://appexchange.salesforce.com/appxListingDetail?listingId=1d525ac3-58ff-4101-9baf-dc23c5132aea)
