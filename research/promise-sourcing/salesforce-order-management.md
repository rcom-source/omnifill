# Salesforce Order Management (SOM) - Technical Research

> **Last updated:** 2026-03-31
> **Product:** Salesforce Order Management (part of Commerce Cloud)
> **Vendor:** Salesforce, Inc.

---

## Table of Contents

1. [Overview](#overview)
2. [Promising & Sourcing Capabilities](#promising--sourcing-capabilities)
3. [Multi-Node Inventory & Real-Time Availability](#multi-node-inventory--real-time-availability)
4. [Data Model](#data-model)
5. [APIs & Technical Integration](#apis--technical-integration)
6. [Authentication & Integration Patterns](#authentication--integration-patterns)
7. [Event-Driven Architecture](#event-driven-architecture)
8. [Flow Core Actions Reference](#flow-core-actions-reference)
9. [API Limits & Governor Limits](#api-limits--governor-limits)
10. [Pricing](#pricing)
11. [Pros & Cons (Real User Feedback)](#pros--cons-real-user-feedback)
12. [Competitive Positioning](#competitive-positioning)
13. [Help & Community Resources](#help--community-resources)
14. [Sources](#sources)

---

## Overview

Salesforce Order Management (SOM) is a cloud-based platform that manages the complete order lifecycle from purchase through delivery and returns. It is part of the Salesforce Commerce Cloud ecosystem and integrates natively with B2C Commerce, B2B Commerce, Service Cloud, and the broader Salesforce CRM platform.

**Two product variants exist:**

1. **Salesforce Order Management (OM)** - Standard solution for straightforward order processes with static rules for order acceptance, payment, invoicing, and shipment management. Primarily designed for B2C ecommerce with limited variation in fulfillment nodes.

2. **Industries Order Management (Industries OM / OM Plus)** - Advanced system for complex industries (telecommunications, energy, utilities) supporting dynamic rules and sophisticated order decomposition. Has its own API reference documentation set.

**Key capabilities:**
- Smart order orchestration and distributed order management (DOM)
- Omnichannel inventory visibility across all fulfillment locations
- Automated fulfillment routing with split-minimization and proximity logic
- Payment processing and invoicing
- Returns, cancellations, and refund management
- AI-powered return insights (Growth edition)
- BOPIS (Buy Online, Pick Up In Store), ship-from-store
- Native Service Cloud integration for customer service agents

---

## Promising & Sourcing Capabilities

### Distributed Order Management (DOM)

Salesforce OM includes a sample DOM flow package containing sample flows, Apex classes, custom objects, and custom fields demonstrating a flow-based system for routing order items to fulfillment locations. DOM optimizes fulfillment by intelligently routing orders across retail stores and distribution centers.

**Two automated routing approaches:**
1. **Connected Commerce Order Routing** - Limited to B2B Commerce environments
2. **Growth Order Routing** - Compatible with both B2B and B2C Commerce

### Sourcing Algorithms

#### 1. Find Routes with Fewest Splits

The primary routing algorithm that evaluates an order's product quantities against available inventory to determine the smallest set of locations that can combine to fulfill the order.

**Algorithm behavior:**
- Starts by looking for **single locations** with sufficient inventory to fulfill the entire order
- If none found, evaluates **pairs of locations** whose combined inventory can fulfill the order
- If no pairs found, evaluates **trios of locations**, and so on
- A configurable **maximum splits threshold** limits the search depth (e.g., max 2 splits = searches single, pairs, and trios)
- Prioritizes complete fulfillment from fewest locations to minimize shipping costs

#### 2. Order Routing Rank by Average Distance

Proximity-based ranking that evaluates location sets returned by the Fewest Splits action:
- Uses the **visitor address** (physical address) for each fulfillment location
- Calculates **straight-line (Euclidean) distance** from each location to the order recipient's postal code
- Computes the **average distance** for each location set
- Returns location sets **sorted by average distance** to the recipient
- Note: Uses physical distance, not carrier shipping zones

#### 3. Custom Routing Logic

Businesses can build custom routing logic in Salesforce Flows based on:
- Inventory location and levels
- Shipping speed requirements
- Product type
- Customer priority / SLA tier
- Lowest sell-through rate
- Oldest stock (FIFO)
- Highest discounts at location
- Store proximity to customer
- Cost optimization

### Promising Capabilities

**What Salesforce OM provides:**
- **Available-to-Fulfill (ATF)** and **Available-to-Order (ATO)** calculations via Omnichannel Inventory
- Real-time inventory availability checking during order routing
- Reservation management to guarantee fulfillment at checkout
- Configurable safety stock thresholds

**What Salesforce OM does NOT natively provide:**
- **Capable-to-Promise (CTP)** - No native manufacturing/production capacity planning
- **Profitable-to-Promise (PTP)** - No built-in margin/profitability optimization in routing decisions
- **Advanced ATP with supply chain planning** - ATP is inventory-based only, not production-pipeline-aware

These would require custom Apex/Flow development or third-party integration (e.g., SAP APO for CTP).

---

## Multi-Node Inventory & Real-Time Availability

### Omnichannel Inventory (OCI)

Salesforce Omnichannel Inventory is a **separate, multitenant microservice** that provides near-real-time inventory availability at the location level across all fulfillment channels. It is a collection of **headless APIs** for inventory data and reservation management.

**Important limitation:** OCI does NOT replace the inventory system of record, supply chain management, or warehouse management system. It is a **visibility and reservation layer** that sits on top of existing systems.

### Architecture

```
 WMS / ERP / POS  -->  [Omnichannel Inventory APIs]  -->  B2C Commerce
                              |                          B2B Commerce
                              |                          Order Management
                              v                          Service Cloud
                     [Inventory Store]
                     - Locations
                     - Location Groups
                     - Reservations
                     - Safety Stock
                     - Futures
```

### Location Hierarchy

- **Locations**: Individual fulfillment points (warehouses, DCs, retail stores, marketplaces)
- **Location Groups**: Aggregate related locations geographically or by brand
- Each location can belong to **multiple location groups**, enabling flexible inventory segmentation across storefronts
- **Location Graph**: Maps relationships between locations and groups

### Availability Calculations

Two key metrics, calculated per SKU per location:

| Metric | Formula | Use Case |
|--------|---------|----------|
| **Available to Fulfill (ATF)** | `Quantity on Hand - Reserved - Safety Stock` | Can we ship from this location right now? |
| **Available to Order (ATO)** | `Quantity on Hand + Future Inventory - Reserved - Safety Stock` | Can a customer place an order for this? |

**Example:**
- Allocation (on hand): 10
- Futures: 2
- Safety Stock: 1
- Reserved: 5
- **ATF** = 10 - 5 - 1 = **4**
- **ATO** = 10 + 2 - 5 - 1 = **6**

### Reservation Workflow

1. **Create Reservation** - Lock inventory when shopper adds items to cart or submits order
2. Reserved items are automatically removed from ATO/ATF at the location and its location groups
3. **Transfer Reservation** - Move reserved quantities between locations (re-routing)
4. **Release Reservation** - Cancel holds from abandoned carts
5. **Fulfill Reservation** - Complete the reservation, adjust on-hand counts

### Real-Time Sync

- Near-real-time inventory updates ingested from WMS, ERP, POS systems
- Delta-based retrieval (get changes since last sync token)
- Batch import for bulk inventory file uploads
- Import status monitoring for batch jobs

### Scalability

- Growth edition supports up to **500 locations**
- Multi-tenant architecture for horizontal scaling
- Headless API design for composable commerce architectures

---

## Data Model

Salesforce Order Management has one of the largest data models in the Salesforce ecosystem. Core objects organized by lifecycle stage:

### Core Objects

| Object | Description |
|--------|-------------|
| **Order** | Customer's original purchase intent. Becomes immutable after activation. |
| **OrderSummary** | Central hub - single aggregated view of complete order state (fulfillment, payments, returns, discounts). The "brain" of the order lifecycle. |
| **OrderItemSummary** | Line items on the order summary |
| **OrderDeliveryGroupSummary** | Defines delivery method and recipient for an order |
| **Change Order** | Tracks modifications (cancellations, returns, discounts) without altering original order |
| **FulfillmentOrder** | Group of products sharing same fulfillment location, delivery method, and recipient |
| **FulfillmentOrderLineItem** | Individual line items within a fulfillment order |
| **FulfillmentOrderItemAdjustment** | Price adjustments on fulfillment line items |
| **FulfillmentOrderItemTax** | Tax records for fulfillment line items |
| **OrderPaymentSummary** | Aggregates Payment and PaymentAuthorization records |
| **ReturnOrder** | RMA (Return Merchandise Authorization) tracking |
| **ReturnOrderLineItem** | Individual items being returned |
| **ProcessException** | Error/exception tracking (relates to nearly all objects) |
| **OrderSummaryRoutingSchedule** | Tracks routing attempts with status (Scheduled, Completed, Abandoned) and failure reasons |

### Object Relationships

- **Order** (1) --> (1) **OrderSummary** (created on activation)
- **OrderSummary** (1) --> (many) **OrderItemSummary**
- **OrderSummary** (1) --> (many) **OrderDeliveryGroupSummary**
- **OrderSummary** (1) --> (many) **FulfillmentOrder**
- **FulfillmentOrder** (1) --> (many) **FulfillmentOrderLineItem**
- **FulfillmentOrderLineItem** --> **OrderItemSummary**
- **OrderSummary** (1) --> (many) **OrderPaymentSummary**
- **OrderSummary** (1) --> (many) **ReturnOrder**

### Order Lifecycle Types

- **Managed**: System automatically processes orders, calculates financials, creates related records. Full OM core actions available.
- **Unmanaged**: Historical/read-only view. Core actions NOT available. Used for migrated legacy data.

### Custom Field Mapping

Custom fields with matching name and datatype between Order and OrderSummary auto-populate on summary creation.

---

## APIs & Technical Integration

### API Surface Areas

Salesforce OM exposes functionality through multiple API layers:

#### 1. Connect REST API (Primary)

Base URL: `/services/data/vXX.0/commerce/`

**Order Management Resources** - manage orders and fulfillment process:

| Resource Category | Key Operations |
|-------------------|---------------|
| **Order Summaries** | Create, preview cancel, submit cancel, preview return, submit return, adjust items, ensure funds/refunds |
| **Fulfillment Orders** | Create fulfillment orders, cancel items, create invoices |
| **Routing** | Find routes with fewest splits, rank by average distance |
| **Order Summary Creation** | Create OrderSummary from activated Order |

Example endpoint pattern:
```
POST /services/data/v66.0/commerce/order-management/order-summaries
POST /services/data/v66.0/commerce/order-management/order-summaries/{orderSummaryId}/actions/submit-cancel
POST /services/data/v66.0/commerce/order-management/fulfillment-orders
```

#### 2. Omnichannel Inventory APIs

Two collections:

**Salesforce Commerce APIs (Headless)**:
- Used by native B2C Commerce and OM integrations
- Access via Salesforce credentials or B2C Commerce Account Manager

**Salesforce Connect REST APIs**:
- Used by Platform app integrations (OM, B2B Commerce)
- Standard Salesforce authentication

| Endpoint Category | Operations |
|-------------------|-----------|
| **Availability** | Get inventory availability, get availability deltas (since token) |
| **Inventory Updates** | Update inventory counts from WMS/ERP/POS |
| **Import/Export** | Import inventory files, upload inventory, get import status |
| **Reservations** | Create, transfer, release, fulfill reservations |

#### 3. Composite REST API

Used for creating orders with multiple related records in a single transaction:
```
POST /services/data/v66.0/composite/sobjects
```
Supports reference IDs (`@{refOrder.id}`) for linking records within a single request.

#### 4. sObject REST API

Standard CRUD on all OM objects:
```
GET/POST/PATCH/DELETE /services/data/v66.0/sobjects/OrderSummary/{id}
GET/POST/PATCH/DELETE /services/data/v66.0/sobjects/FulfillmentOrder/{id}
```

#### 5. Place Order REST API

Dedicated API for order placement operations.
- Developer Guide: https://developer.salesforce.com/docs/atlas.en-us.api_placeorder.meta/api_placeorder/sforce_placeorder_rest_api_intro.htm

#### 6. Actions API

Invocable actions for OM operations, callable via REST:
```
POST /services/data/v66.0/actions/standard/orderManagement/{actionName}
```

### Apex Classes (ConnectApi Namespace)

All OM operations available as Apex classes for server-side logic:

| Class | Purpose |
|-------|---------|
| **ConnectApi.OrderSummary** | Order lifecycle operations (cancel, return, adjust, ensure funds/refunds) |
| **ConnectApi.FulfillmentOrder** | Fulfillment creation and management |
| **ConnectApi.OrderSummaryCreation** | `createOrderSummary()` - creates OrderSummary from Order |
| **ConnectApi.Routing** | DOM routing actions |
| **ConnectApi.OmniChannelInventory** | Inventory availability and reservation operations |

**OrderSummary creation example (Apex):**
```apex
ConnectApi.OrderSummaryCreationInput input = new ConnectApi.OrderSummaryCreationInput();
input.orderId = '801xx0000000001';
// OrderLifeCycleType defaults to "Managed"
ConnectApi.OrderSummaryCreationOutput output = ConnectApi.OrderSummaryCreation.createOrderSummary(input);
```

### SDKs and Developer Tools

- **Salesforce CLI (sf/sfdx)** - Deploy metadata, run Apex, manage orgs
- **Salesforce Extensions for VS Code** - IDE integration
- **Postman Collections** - Available for Salesforce APIs
- **Salesforce Mobile SDK** - For mobile app integrations
- No standalone OM-specific SDK; uses standard Salesforce platform SDKs

---

## Authentication & Integration Patterns

### OAuth 2.0 (Primary Method)

Salesforce uses **Connected Apps** (or the newer **External Client Apps**) as the OAuth client registration mechanism.

**Supported OAuth 2.0 Flows:**

| Flow | Use Case |
|------|----------|
| **Authorization Code** | Web apps with user interaction |
| **Authorization Code + PKCE** | Mobile and SPA apps |
| **Client Credentials** | Server-to-server (no user context) |
| **JWT Bearer Token** | Server-to-server with pre-authorized user |
| **Device Flow** | IoT / limited-input devices |
| **Refresh Token** | Long-lived access without re-authentication |
| **SAML Bearer Assertion** | SSO-integrated systems |
| **Username-Password** | Legacy (not recommended for production) |

**Setup process:**
1. Create a Connected App in Salesforce Setup
2. Enable OAuth Settings, configure callback URL
3. Obtain Consumer Key and Consumer Secret
4. Implement chosen OAuth flow
5. Use access token in `Authorization: Bearer {token}` header

**Token endpoint:** `https://{instance}.salesforce.com/services/oauth2/token`

### Integration Patterns

| Pattern | Description |
|---------|-------------|
| **Native Commerce Integration** | Pre-built connectors between B2C/B2B Commerce and OM |
| **REST API Integration** | External systems calling OM APIs with OAuth tokens |
| **Platform Events** | Event-driven async communication |
| **Change Data Capture** | Real-time change streaming to external systems |
| **Apex Callouts** | OM calling external systems (webhooks, WMS, shipping carriers) |
| **Middleware (MuleSoft)** | Salesforce-owned iPaaS for complex integrations |
| **Heroku Connect** | Bi-directional Postgres sync |

### External Client Apps (Modern Approach)

Salesforce is evolving toward External Client Apps as the modern replacement for Connected Apps:
- Optimized for ISV packaging
- Secure by default
- Built for contemporary DevOps practices
- Better suited for enterprise deployment pipelines

---

## Event-Driven Architecture

### Platform Events

Custom event channels for business-level notifications:
- Define custom Platform Events (e.g., `Order_Shipped__e`, `Payment_Captured__e`)
- Publish via REST API (`/services/data/v66.0/sobjects/Order_Shipped__e`), Apex, or Flows
- Subscribe via Apex Triggers, Flows, or external CometD/Pub/Sub API clients
- External apps can publish events via REST API or Pub/Sub API

### Change Data Capture (CDC)

Automatic change event streaming for OM objects:
- Publishes events on record creation, update, deletion, undeletion
- Subscribable via CometD or Pub/Sub API
- Enables real-time sync to external systems (data warehouses, analytics, downstream services)
- Per-object enablement in Setup

### Pub/Sub API

gRPC-based event bus for high-throughput, low-latency event streaming:
- Supports both Platform Events and CDC events
- Bi-directional: publish and subscribe
- Preferred over legacy CometD for new integrations

### Common OM Event Patterns

```
[Order Created] --> Platform Event --> External WMS notification
[FulfillmentOrder Updated] --> CDC --> Data warehouse sync
[Inventory Changed] --> OCI API callback --> Storefront availability update
[Return Submitted] --> Platform Event --> Returns processing system
```

---

## Flow Core Actions Reference

Salesforce OM operations are exposed as **Flow Core Actions** (invocable from Salesforce Flows, Apex, and REST API). Key actions include:

### Order Lifecycle Actions

| Action | Description |
|--------|-------------|
| Create Order Summary | Creates an OrderSummary from an activated Order |
| Preview Cancel | Previews cancellation outcome before applying |
| Submit Cancel | Applies cancellation to order item summaries |
| Preview Return | Previews return outcome |
| Submit Return | Applies return to order item summaries |
| Return Order Item Summaries Preview | Preview return for specific items |
| Adjust Order Item Summaries Preview | Preview price adjustment |
| Adjust Order Item Summaries Submit | Apply price adjustment |

### Fulfillment Actions

| Action | Description |
|--------|-------------|
| Create Fulfillment Order | Creates FulfillmentOrder(s) for order delivery group |
| Create Invoice from Fulfillment Order | Generates invoice for fulfilled orders |
| Ensure Funds Async | Asynchronously ensures payment funds are captured |
| Ensure Refunds Async | Asynchronously processes refunds |

### Routing Actions (DOM)

| Action | Description |
|--------|-------------|
| Find Routes with Fewest Splits | Evaluates inventory across locations to minimize shipment splits |
| Order Routing Rank by Average Distance | Ranks location sets by straight-line distance to recipient |

### Omnichannel Inventory Actions (in Flows)

| Action | Description |
|--------|-------------|
| Get Inventory Availability | Query product availability across locations |
| Create Reservation | Lock inventory for cart/order |
| Transfer Reservation | Move reservation between locations |
| Release Reservation | Cancel inventory holds |
| Fulfill Reservation | Complete reservation and adjust on-hand |
| Update Reservation | Modify SKU quantities in existing reservation |

---

## API Limits & Governor Limits

Salesforce OM operates within the standard Salesforce platform limits:

### API Request Limits

| Limit | Value |
|-------|-------|
| REST/SOAP/Connect API calls | 100,000 per 24-hour rolling period (Enterprise Edition base; increases with additional licenses) |
| Bulk API batches | 15,000 per 24 hours |
| Bulk API records per batch | 10,000 |
| Bulk API CPU time | 60,000 ms per transaction |

### Apex Governor Limits (per transaction)

| Limit | Value |
|-------|-------|
| SOQL queries | 100 (synchronous) / 200 (async) |
| SOQL rows returned | 50,000 |
| DML statements | 150 |
| DML rows | 10,000 |
| CPU time | 10,000 ms (sync) / 60,000 ms (async) |
| Heap size | 6 MB (sync) / 12 MB (async) |
| Callout timeout | 120 seconds |
| Callouts per transaction | 100 |

### OM-Specific Considerations

- The 24-hour API limit is a **soft limit** that Salesforce allows orgs to exceed, with a hard cap as a safety net
- High-volume order processing may require Bulk API 2.0 for operations exceeding 2,000 records
- DOM routing flows consume Flow interview limits
- Omnichannel Inventory is a separate microservice with its own rate limiting (not publicly documented in detail)

---

## Pricing

### Editions (as of 2026)

| Edition | Price Model | Key Features |
|---------|-------------|--------------|
| **Order Visibility** | **0.25% of GMV per order**, billed annually | Order visibility only, Service Cloud integration, B2C/B2B Commerce pre-integration, international localization. No advanced fulfillment. |
| **Growth** | **1% of GMV per order**, billed annually | Full order lifecycle, distributed order management, omnichannel inventory (up to 500 locations), AI-powered return insights, smart order orchestration |

**Notes:**
- GMV = Gross Merchandise Value
- Final pricing requires direct Salesforce sales engagement
- Success Plan add-ons: Standard (included), Premier (30% of net license fees), Signature (contact sales)
- Salesforce applied a ~6% price increase across most products in August 2025
- Some sources cite a starting price of ~$499/month for basic configurations

### Cost Considerations

- Per-order GMV-based pricing can become expensive at scale for high-AOV businesses
- Implementation costs (customization, consulting, training) are significant and separate
- Requires existing Salesforce ecosystem investment (Sales/Service Cloud licenses)
- Additional costs for MuleSoft if complex middleware needed

---

## Pros & Cons (Real User Feedback)

### Pros

**From G2, industry reviews, and analyst reports:**

1. **Deep Salesforce Ecosystem Integration** - Seamless connection with CRM, Commerce Cloud, Service Cloud provides unified customer view across all touchpoints
2. **Flexible Customization** - Flows, Apex, and custom objects allow tailoring to specific business requirements
3. **Omnichannel Support** - Consolidates online, in-store, and mobile orders into single system
4. **Real-Time Inventory Visibility** - Near-real-time availability across locations prevents overselling
5. **Mobile App** - Good UI for on-the-go order management access
6. **Quick Initial Setup** - Core setup is straightforward; more time available for custom logic
7. **Scalability** - Handles growing order volumes on multi-tenant cloud infrastructure
8. **Service Agent Integration** - Agents can manage orders directly within Service Cloud console
9. **BOPIS/Ship-from-Store** - Native omnichannel fulfillment scenarios out of the box
10. **Automation** - Einstein AI for return insights and order orchestration

### Cons

1. **Omnichannel Inventory is a Black Box** - Difficult to access debug logs and diagnose issues; limited visibility into OCI internals
2. **Steep Learning Curve** - Complex initial configuration; significant ramp-up time for developers
3. **High Total Cost of Ownership** - Licensing + customization + consulting + training costs add up rapidly
4. **Limited Payment Options** - Payment processing modes are limited; adding new payment methods is complex
5. **Customization Complexity** - While flexible, deep customization requires significant Apex/Flow expertise
6. **Relatively Simple DOM** - Compared to Manhattan Active Omni or IBM Sterling, routing logic is basic (fewest splits + distance only as out-of-box options)
7. **No Native CTP/PTP** - No built-in capable-to-promise or profitable-to-promise algorithms
8. **Primarily B2C-Focused** - Originally designed for single B2C ecommerce channel with limited fulfillment node variation
9. **Platform Lock-In** - Deep dependency on Salesforce ecosystem; migration is difficult
10. **Governor Limits** - Salesforce platform limits can constrain high-volume, complex routing operations
11. **In-House Expertise Required** - Successful operation requires dedicated Salesforce developers/admins

---

## Competitive Positioning

| Capability | Salesforce OM | Manhattan Active Omni | IBM Sterling | Fluent Commerce |
|-----------|--------------|----------------------|-------------|----------------|
| **Primary Strength** | CRM/Commerce integration | Supply chain optimization | Enterprise complexity | Multi-brand orchestration |
| **Routing Sophistication** | Basic (splits + distance) | Advanced (cost-to-serve) | Advanced (configurable rules) | Moderate (rule-based) |
| **Inventory Visibility** | Good (OCI microservice) | Excellent (WMS-native) | Excellent | Good |
| **CTP/PTP** | No | Partial | Yes | No |
| **Implementation Complexity** | Moderate | High | Very High | Moderate |
| **Best For** | Salesforce-native B2C/B2B | Large retail with stores+DCs | Complex supply chains | Multi-brand retailers |
| **Architecture** | Multi-tenant SaaS | Cloud-native microservices | Cloud or on-prem | Cloud-native SaaS |

**Key distinction:** Salesforce OM is primarily a **commerce-integrated order management system** rather than a full **supply chain planning/optimization** platform. Its strength is the unified customer experience across Commerce, Service, and CRM - not advanced fulfillment optimization.

---

## Help & Community Resources

### Official Documentation

| Resource | URL |
|----------|-----|
| Order Management Developer Guide | https://developer.salesforce.com/docs/atlas.en-us.order_management_developer_guide.meta/order_management_developer_guide/order_management_developer_guide_intro.htm |
| Connect REST API - OM Resources | https://developer.salesforce.com/docs/atlas.en-us.chatterapi.meta/chatterapi/connect_resources_order_management_resources.htm |
| OM Apex Classes | https://developer.salesforce.com/docs/atlas.en-us.order_management_developer_guide.meta/order_management_developer_guide/order_management_apex_classes.htm |
| Flow Core Actions List | https://help.salesforce.com/s/articleView?id=sf.flow_ref_elements_om_actions_list.htm&language=en_US&type=5 |
| Omnichannel Inventory APIs | https://help.salesforce.com/s/articleView?id=sf.inv_omnichannel_inventory_apis.htm&language=en_US&type=5 |
| OCI Connect REST API Resources | https://developer.salesforce.com/docs/atlas.en-us.chatterapi.meta/chatterapi/connect_resources_omnichannel_inventory_resources.htm |
| OM Actions API Reference | https://developer.salesforce.com/docs/atlas.en-us.api_action.meta/api_action/actions_obj_order_management.htm |
| Place Order REST API | https://developer.salesforce.com/docs/atlas.en-us.api_placeorder.meta/api_placeorder/sforce_placeorder_rest_api_intro.htm |
| Developer Guide PDF (v66.0) | https://resources.docs.salesforce.com/latest/latest/en-us/sfdc/pdf/order_management_developer_guide_html.pdf |
| OM Help Center | https://help.salesforce.com/s/articleView?id=commerce.om_order_management.htm&language=en_US&type=5 |
| DOM Help Article | https://help.salesforce.com/s/articleView?id=commerce.om_distributed_order_management.htm&language=en_US&type=5 |
| OM Licenses & Allocations | https://help.salesforce.com/s/articleView?id=commerce.om_licenses.htm&language=en_US&type=5 |

### Trailhead (Learning)

| Module | URL |
|--------|-----|
| Implement Distributed Order Management | https://trailhead.salesforce.com/content/learn/modules/om-salesforce-order-management/om-implement-distributed-order-management |
| Omnichannel Inventory Overview | https://trailhead.salesforce.com/content/learn/modules/omnichannel-inventory |
| Explore Omnichannel Inventory APIs | https://trailhead.salesforce.com/content/learn/modules/omnichannel-inventory/explore-omnichannel-inventory-apis |
| Get Started with Omnichannel Inventory | https://trailhead.salesforce.com/content/learn/modules/omnichannel-inventory/get-started-with-omnichannel-inventory |
| Optimize Fulfillment with Salesforce Inventory | https://trailhead.salesforce.com/content/learn/modules/omnichannel-inventory/integrate-omnichannel-inventory-with-salesforce-order-management |
| Customize Order Management Flows | https://trailhead.salesforce.com/content/learn/modules/b2c-order-management/b2c-som-customize-flows |
| Order Fulfillment & Payment Automation | https://trailhead.salesforce.com/content/learn/modules/om-salesforce-order-management/om-streamline-order-fulfillment-payment |

### Community & Reviews

| Resource | URL |
|----------|-----|
| G2 Reviews | https://www.g2.com/products/salesforce-order-management/reviews |
| G2 Pros and Cons | https://www.g2.com/products/salesforce-order-management/reviews?qs=pros-and-cons |
| Trailblazer Community | https://trailhead.salesforce.com/trailblazer-community |
| Salesforce StackExchange | https://salesforce.stackexchange.com/ |
| Salesforce Pricing Page | https://www.salesforce.com/commerce/order-management/pricing/ |

### Third-Party Technical Resources

| Resource | URL |
|----------|-----|
| OM Data Model Deep Dive | https://firatesmer.com/salesforce-order-management-data-model/ |
| Creating Orders & Order Summaries | https://firatesmer.com/salesforce-order-management-creating-order-order-summary/ |
| Cancel Order Items Walkthrough | https://firatesmer.com/salesforce-order-management-cancel-items/ |
| OCI Composable Architecture (Medium) | https://medium.com/@kanishk.khatter/salesforce-omnichannel-inventory-your-stepping-stone-to-a-composable-future-b4f99e18cc84 |

---

## Sources

All URLs referenced throughout this document. Primary sources:

- [Salesforce Order Management Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.order_management_developer_guide.meta/order_management_developer_guide/order_management_developer_guide_intro.htm)
- [Connect REST API - OM Resources](https://developer.salesforce.com/docs/atlas.en-us.chatterapi.meta/chatterapi/connect_resources_order_management_resources.htm)
- [OM Apex Classes Reference](https://developer.salesforce.com/docs/atlas.en-us.order_management_developer_guide.meta/order_management_developer_guide/order_management_apex_classes.htm)
- [Distributed Order Management - Trailhead](https://trailhead.salesforce.com/content/learn/modules/om-salesforce-order-management/om-implement-distributed-order-management)
- [Omnichannel Inventory APIs - Trailhead](https://trailhead.salesforce.com/content/learn/modules/omnichannel-inventory/explore-omnichannel-inventory-apis)
- [Omnichannel Inventory Help](https://help.salesforce.com/s/articleView?id=sf.inv_omnichannel_inventory.htm&language=en_US&type=5)
- [OM Flow Core Actions](https://help.salesforce.com/s/articleView?id=sf.flow_ref_elements_om_actions_list.htm&language=en_US&type=5)
- [Salesforce OM Pricing](https://www.salesforce.com/commerce/order-management/pricing/)
- [G2 Reviews - Salesforce Order Management](https://www.g2.com/products/salesforce-order-management/reviews)
- [Salesforce OAuth & Connected Apps](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_oauth_and_connected_apps.htm)
- [Platform Events Architecture - Trailhead](https://trailhead.salesforce.com/content/learn/modules/platform_events_basics/platform_events_architecture)
- [Salesforce API Limits Quick Reference](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm)
- [Salesforce Order Management 2026 - LitExtension](https://litextension.com/blog/salesforce-order-management/)
- [Salesforce OMS 2025 Review - Fynd](https://www.fynd.com/blog/salesforce-order-management)
- [OM Data Model - Firat Esmer](https://firatesmer.com/salesforce-order-management-data-model/)
- [Creating Orders - Firat Esmer](https://firatesmer.com/salesforce-order-management-creating-order-order-summary/)
- [IBM Sterling vs Salesforce OM - SelectHub](https://www.selecthub.com/order-management-software/ibm-sterling-vs-salesforce-order-management/)
- [Ecommerce OMS Platform Comparison](https://www.fullonecommerce.com/ecommerce-order-management-systems-software-vendors-2021.html)
