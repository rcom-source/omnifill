# ShipBob Fulfillment Platform - Comprehensive Research

## 1. What It Does

### Overview

ShipBob is a technology-first third-party logistics (3PL) provider offering outsourced fulfillment, warehousing, and shipping for e-commerce merchants. Founded in 2014, it operates a distributed network of fulfillment centers globally. ShipBob's core differentiator is its proprietary WMS (Warehouse Management System) that powers both its own fulfillment network and is available to merchants running their own warehouses via the "Merchant Plus" (WMS-as-a-service) product.

### Pick Methods

ShipBob's proprietary WMS supports multiple picking strategies:

- **Batch Picking**: Multiple similar orders are picked in a single trip. Orders can be identical (same SKU combination) or similar (overlapping SKUs). The WMS groups orders intelligently to minimize picker travel.
- **Auto-Cluster Picking**: Algorithmically groups orders into optimal pick clusters based on warehouse layout and SKU proximity.
- **Custom Cluster Picking**: Allows manual configuration of pick clusters for specific operational needs.
- **Single-Order (Discrete) Picking**: One picker handles one order at a time, used for complex or high-value orders.
- **Wave Picking**: Orders released in time-based waves aligned with carrier cutoffs, dock availability, or labor shifts. The WMS generates pick lists per wave based on optimal picking routes to reduce travel time.
- **Zone Picking**: Pickers assigned to specific physical areas/zones in the warehouse. Items are picked within zones and consolidated downstream.

### Pack Optimization

ShipBob uses **cartonization algorithms** powered by triple Cubiscan technology:

- Products are dimensionally scanned (length, width, height, weight) on intake
- The algorithm considers item size, weight, shape, material, and product type
- SKU-level packaging preferences are honored (not one-size-fits-all)
- Automatically recommends the optimal box size or poly mailer for each order
- Reduces dimensional weight charges and shipping costs
- Packing team receives data-driven box recommendations per order

### Shipping & Carrier Selection

- Integrated rate shopping across 60+ carriers including USPS, FedEx, UPS, DHL Express, Amazon Shipping
- Regional carriers: Australia Post, Canada Post, Royal Mail, and others
- Uses the **Shippo API** under the hood to connect with carriers, gather rates, and purchase labels
- Real-time rate comparison across carriers and service levels
- Automated label generation and printing
- Ship methods map to configurable "Ship Options": Standard, Expedited, 2-Day, etc.

### Labor Management

Through the WMS, ShipBob provides:

- Per-employee fulfillment rate tracking (orders completed per hour)
- Labor forecasting based on historical throughput metrics
- Staffing optimization tied to order volume forecasting
- Pilot customers reported **25% less time on fulfillment** and **35% reduction in error rates**

### Robotics & Automation

ShipBob has historically prioritized **software automation over physical robotics**:

- Co-founder Divey Gulati stated: "Physical automation is rigid... investing in engineering keeps paying off"
- Focus on algorithmic optimization (route planning, cartonization, order clustering) rather than warehouse robots
- No proprietary robotics platform; compatible with third-party solutions
- The WMS is designed to integrate with collaborative robots like 6 River Systems' Chuck (mobile picking robot), though ShipBob itself does not manufacture or mandate specific robotics

---

## 2. Technical Documentation

### Developer Portal

- **URL**: https://developer.shipbob.com/
- **Support email**: techspecialists@shipbob.com (1-business day first response)
- **OpenAPI spec**: `https://marketplaceapi.shipbob.com/docs/2026-01.json`

### Environments

| Environment | API Base URL | Auth URL | Dashboard |
|-------------|-------------|----------|-----------|
| Production | `https://api.shipbob.com` | `https://auth.shipbob.com` | `https://web.shipbob.com` |
| Sandbox | `https://sandbox-api.shipbob.com` | `https://authstage.shipbob.com` | `https://webstage.shipbob.dev` |

Sandbox is free with no expiration. Accounts are free until physical inventory arrives.

### API Versioning

Date-based versioning scheme. Current version: **2026-01**. Endpoints follow the pattern:
```
https://api.shipbob.com/{version}/{resource}
```

Action-style endpoints use colon notation: `/order:estimate`, `/shipment:batchUpdateTrackingUpload`

### API Resources & Key Endpoints

#### Orders
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/2026-01/order` | Create order (D2C or B2B) |
| GET | `/2026-01/order` | List/filter orders |
| GET | `/2026-01/order?HasTracking=true&IsTrackingUploaded=false&Limit=250` | Poll for unsynced tracking |
| POST | `/2026-01/order:estimate` | Estimate order fulfillment |

**Required headers**: `Authorization: Bearer <token>`, `Content-Type: application/json`, `shipbob_channel_id: <id>`

**Order creation required fields**: shipping_method, recipient (name, address, city, country ISO Alpha-2), reference_id, products (via ReferenceId or ProductId model)

**Optional fields**: order_number, order_tags (name-value pairs for automation rules), location_id, sales_channel

**B2B-specific fields**: type="B2B", carrier_type (Parcel/Freight), payment_terms, purchase_order_number, retailer_program_type, quantity_unit_of_measure_code

#### Products
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/2026-01/product` | Create product (single, bulk, or bundle) |
| GET | `/2026-01/product` | List products |
| GET | `/2026-01/product/{productId}/variants` | Get product variants |
| POST | `/2026-01/product/{productId}/variants` | Create variants |
| PATCH | `/2026-01/product/{productId}/variants` | Update variants |
| POST | `/2026-01/product:moveVariants` | Move variants between products |
| POST | `/2026-01/variant/{variantId}:convertToBundle` | Convert variant to bundle |
| POST | `/2026-01/variant/{variantId}:merge` | Merge variants |
| DELETE | `/2026-01/product/{productId}` | Delete product |

**Product creation requires**: reference_id (typically SKU), name. Optional: barcode (recommended for receiving/stowing), type_id (2 for bundles), bundle_definition.

Products auto-create matching inventory items. The ReferenceId model auto-creates products if no match exists.

#### Inventory
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/2026-01/inventory` | Get all inventory levels |
| POST | `/2026-01/inventory/history:query` | Query historical inventory movement events (added 2026-01) |

**Key response field**: `total_sellable_quantity` = fulfillable_quantity - exception_quantity

Inventory tracked at component level, not bundle SKU level. Supports bundle/merge relationships.

#### Receiving (Warehouse Receiving Orders / WROs)
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/2026-01/receiving` | List WROs |
| POST | `/2026-01/receiving` | Create WRO |
| POST | `/2026-01/receiving/{id}/distributions` | Get IPP distribution details |
| POST | `/2026-01/receiving:setExternalSync` | Toggle external sync flag |

#### Returns
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/2026-01/return` | Create return |
| GET | `/2026-01/return` | List returns |
| PATCH | `/2026-01/return/{id}` | Edit return |
| DELETE | `/2026-01/return/{id}` | Cancel return |

#### Billing (added 2025-07)
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/2025-07/invoices` | Paginated invoice list |
| GET | `/2025-07/invoices/{invoiceId}/transactions` | Invoice transaction detail |
| GET | `/2025-07/transaction-fees` | Available fee types |
| POST | `/2025-07/transactions:query` | Advanced transaction querying |

#### Fulfillment Centers
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/2026-01/fulfillment-center` | List fulfillment centers |

#### Channels
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/2026-01/channel` | Get channels (required for write operations) |

#### Shipments
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/2026-01/shipment:batchUpdateTrackingUpload` | Mark tracking as synced |

#### Simulation (Sandbox Only)
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/2026-01/simulate/shipment` | Trigger shipment state transitions |
| GET | `/2026-01/simulate/status/{simulationId}` | Check simulation status |

### SDKs & Client Libraries

| Language | Source | Notes |
|----------|--------|-------|
| Go | https://github.com/stryd/shipbob-go | OpenAPI-generated |
| Rust | https://crates.io/crates/shipbob | OpenAPI-generated, docs at docs.rs/shipbob |
| Python | https://github.com/community-phone-company/shipbob-sdk-python | Community-maintained |
| Node.js | https://github.com/shipbobDev/DeveloperApiSampleNodeJs | Official sample app (OAuth demo) |

Official API docs repo: https://github.com/shipbobDev/ShipBobApi

**ShipBob MCP Server**: AI assistant integration enabling natural language interaction with 27 tools for Orders, Products, Inventory, and Channels. Compatible with Claude Desktop, VS Code, and other MCP clients.

### Webhooks

#### Available Topics (Current Version)

| Topic | Trigger |
|-------|---------|
| `order.shipped` | Shipping labels purchased and printed |
| `order.shipment.delivered` | Customer delivery confirmed |
| `order.shipment.exception` | Exception (e.g., out-of-stock) |
| `order.shipment.on_hold` | Shipment paused (missing info, invalid address) |
| `order.shipment.cancelled` | Shipment cancelled |
| `return.created` | Return initiated |
| `return.updated` | Return details changed |
| `return.completed` | Return processing completed |

#### Legacy Topics (1.0/2.0)
`order_shipped`, `shipment_delivered`, `shipment_exception`, `shipment_onhold`, `shipment_cancelled`

#### Webhook Headers
- `x-webhook-topic` - Event topic
- `webhook-timestamp` - Event timestamp
- `webhook-signature` - HMAC signature for verification
- `webhook-id` - Unique webhook ID
- `content-type` - application/json

#### Subscription Management
- Dashboard: Integrations > Webhooks > Add Subscription
- API: `POST /api/webhooks/create-subscription`
- Retrieve: `GET /api/webhooks`

#### Retry Policy
Immediate, then: 5s, 5min, 30min, 2hr, 5hr, 10hr, 10hr. Endpoints disabled after 5 days of consecutive failures (12+ hour gap between first and last failure within 24 hours).

#### Security Requirements
- Subscription URLs **must** support SSL/HTTPS
- Static IP whitelist: `44.228.126.217`, `50.112.21.217`, `52.24.126.164`, `54.148.139.208`, `2600:1f24:64:8000::/56`
- Must return 2XX **before** heavy processing
- Webhook signatures provided for payload verification

### Status Reference

#### Order Statuses
Processing, Exception, On Hold, Completed, Cancelled, Partially Fulfilled, Fulfilled

#### Shipment Statuses
- **Exception**: Cannot be fulfilled (out of stock / inactive product)
- **On Hold**: Not ready for fulfillment even with stock available
- **Processing**: In the process of fulfillment
- **Completed**: Has left ShipBob (shipped)
- **Cancelled**: Will not be fulfilled
- **LabelCreated**: Shipping label purchased (transitions quickly to Completed)

#### Warehouse Receiving Order (WRO) Statuses
Awaiting, Processing, Arrived, PartiallyArrived, PartiallyArrivedAtHub, ArrivedAtHub, ProcessingAtHub, InternalTransfer, Completed, Cancelled

#### Return Statuses
AwaitingArrival, Arrived, Processing, Completed, Cancelled

---

## 3. Authentication Methods & Integration Patterns

### Personal Access Token (PAT)

Best for single-user custom integrations.

- **Generation**: Dashboard > Integrations > Token Management
  - Production: `https://web.shipbob.com/app/merchant/#/Integrations/token-management`
  - Sandbox: `https://webstage.shipbob.dev/app/merchant/#/Integrations/token-management`
- **Lifetime**: Never expires
- **Revocation**: Anytime from dashboard
- **Usage**: `Authorization: Bearer YOUR_API_TOKEN`
- Issued with auto-generated Single-Merchant Application (SMA) channel

### OAuth 2.0 (Authorization Code Flow)

Required for multi-user apps and ShipBob App Store listings.

#### Flow

1. **Create App**: Dashboard > Integrations > OAuth Apps > Create App. Receive `client_id` and `client_secret`.

2. **Authorization Request**:
   ```
   GET https://auth.shipbob.com/connect/authorize
     ?client_id=ExternalApplication_123
     &scope=orders_read orders_write inventory_read products_read webhooks_write offline_access
     &redirect_uri=https://yourapp.com/callback
     &response_mode=form_post
     &integration_name=YourApp
     &state=random_csrf_token
   ```

3. **User Authorizes**: Redirected to callback with `code`, `id_token`, `scope`, `session_state`.

4. **Token Exchange**:
   ```
   POST https://auth.shipbob.com/connect/token
   Content-Type: application/x-www-form-urlencoded

   redirect_uri=...&client_id=...&client_secret=...&code=...&grant_type=authorization_code
   ```

   Response:
   ```json
   {
     "access_token": "...",
     "expires_in": 3600,
     "token_type": "bearer",
     "refresh_token": "...",
     "scope": "..."
   }
   ```

5. **Token Refresh**:
   ```
   POST https://auth.shipbob.com/connect/token
   grant_type=refresh_token&refresh_token=...&client_id=...&client_secret=...
   ```

#### Token Lifetimes
- Access token: **1 hour**
- Refresh token: **30 days** (new one issued with each refresh)

### Available Scopes
`billing_read`, `channels_read`, `orders_read`, `orders_write`, `fulfillments_read`, `fulfillments_write`, `inventory_read`, `inventory_write`, `locations_read`, `pricing_read`, `products_read`, `products_write`, `receiving_read`, `receiving_write`, `returns_read`, `returns_write`, `webhooks_read`, `webhooks_write`, `offline_access`, `openid`

### Required Headers for All API Calls
```http
Authorization: Bearer <access_token>
Content-Type: application/json
shipbob_channel_id: <channel_id>   # Required for write operations
```

### Rate Limiting
- **150 requests per minute** per user per application (sliding window)
- HTTP 429 on exceed with message: "Rate limit is exceeded. Try again in 25 seconds."
- Response headers: `x-retry-after` (seconds to wait), `x-remaining-calls` (remaining quota)

### Integration Pattern: Channel Architecture

A **Channel** represents a vendor application installation for a specific merchant. Examples: "Kevin's Shopify Store #133432". Channels scope data access and are required for write operations. Retrieve via `GET /2026-01/channel`.

---

## 4. Help Centers, Knowledge Bases, Community Forums

### Official Support Resources

| Resource | URL | Description |
|----------|-----|-------------|
| Help Center / Knowledge Base | https://support.shipbob.com/ | Searchable articles, FAQs, how-to guides |
| Developer Portal | https://developer.shipbob.com/ | API docs, guides, release notes |
| Resource Library | https://resources.shipbob.com/ | Whitepapers, webinars, case studies |
| Jira Service Desk | https://shipbob.atlassian.net/servicedesk/customer | Customer ticket portal |
| Developer Support | techspecialists@shipbob.com | 1-business day first response |

### Support Channels
- **Live Chat**: Available during business hours via dashboard "Help" button
- **Phone Support**: Available for merchants
- **Email/Case Portal**: Contact form auto-routes to appropriate specialist
- **Dedicated Merchant Success Manager**: For larger merchants
- **On-site FC Representatives**: Warehouse floor support staff
- **Tech Pod**: Specialized technical issue resolution team

### Support Coverage
Representatives in US, Australia, UK, Europe, and India providing localized, country-specific hours.

### Community & Third-Party Resources
- **Shopify Community**: ShipBob discussions at community.shopify.com
- **ShipBob Partner Ecosystem**: https://partners.shipbob.com/directory/ (integration partner directory)
- **ShipBob Blog**: Extensive guides on fulfillment, shipping, inventory management

---

## 5. Pros and Cons from Real Users

### Pros

**Technology & Usability**
- Intuitive, plug-and-play dashboard with real-time visibility into inventory, orders, and costs
- Strong native integrations with 40+ platforms (Shopify, BigCommerce, Amazon, WooCommerce, eBay, Walmart, Squarespace, Wix, Square)
- Robust API for custom integrations
- Real-time inventory syncing across all channels

**Fulfillment Network**
- Distributed multi-location fulfillment centers enabling 2-day shipping
- Inventory distribution closer to customers reduces shipping costs and delivery times
- Global network spanning US, Canada, UK, EU, Australia

**Operational**
- Transparent fee structure with centralized cost dashboard
- Dedicated account managers for established brands
- ShipBob WMS available for hybrid/in-house fulfillment
- 2024 upgrades: real-time inventory, box-picking optimization, expanded partner ecosystem
- 2025: AI-powered inventory forecasting and network optimization

### Cons

**Customer Service**
- Slow and unresponsive support is the #1 complaint (48+ hour response times reported)
- Difficulty getting issues resolved satisfactorily
- Long wait times, especially for smaller accounts without dedicated managers

**Cost Issues**
- Hidden fees and inconsistent charges for warehousing/shipping
- Shipping markups not always transparent
- Confusing SLA wording giving ShipBob discretion on timing
- Higher costs for smaller businesses; recent order minimums exclude startups

**Operational Issues**
- Inventory check-in/receiving delays (can take weeks)
- Order inaccuracies (wrong items shipped)
- Polarized reviews: 73% five-star but 17% one-star on Trustpilot (963 reviews, 3.8/5)

### Review Platform Scores (Approximate)
| Platform | Rating |
|----------|--------|
| Trustpilot | 3.8/5 (963 reviews) |
| G2 | ~3.5-4.0/5 |
| Capterra | ~3.5-4.0/5 |
| Shopify App Store | Mixed (polarized) |

### User Sentiment Summary

ShipBob works best for **mid-market e-commerce brands** with stable order volumes (500+ orders/month) that benefit from distributed fulfillment and 2-day shipping. Smaller sellers and startups frequently report frustration with costs, support responsiveness, and receiving delays. Brands with dedicated account managers report significantly better experiences.

---

## 6. Pricing Model

### Pricing Structure

ShipBob uses **modular, usage-based pricing** (not a fixed monthly fee). Exact pricing now requires a custom quote from sales, but historically published rates include:

| Fee Category | Published Rate (Historical) | Notes |
|--------------|---------------------------|-------|
| **Setup/Onboarding** | $975 (waived on Startup Plan) | One-time |
| **Pick & Pack** | $0 for first 4 picks; $0.20/additional unit | Per order |
| **Storage - Bin** | $5/month | 0.77 cubic ft |
| **Storage - Shelf** | $10/month | 7.1 cubic ft |
| **Storage - Pallet** | $40/month | 60 cubic ft |
| **Receiving** | $35/hour | First 2 hours flat rate, then hourly |
| **Returns** | Flat fee per return | Applied when return physically arrives |
| **Shipping** | Negotiated carrier rates | Rate-shopped across 60+ carriers |

### Typical Total Cost
Most e-commerce businesses pay **$5-$10 per order** for fulfillment and shipping combined, varying by product dimensions, weight, destination zone, and volume.

### Important Notes
- ShipBob has removed standard pricing from their website; quotes are now required
- Volume discounts available for higher-order merchants
- Minimum order requirements have been introduced (exact thresholds undisclosed)
- No fixed monthly platform fee for outsourced fulfillment
- WMS (Merchant Plus) for in-house warehouses has separate pricing

---

## 7. Carrier Integration Capabilities

### Supported Carriers (60+)

**Major carriers**: USPS, FedEx, UPS, DHL Express, Amazon Shipping

**Regional/International**: Australia Post, Canada Post, Royal Mail, and dozens of other regional carriers

### Rate Shopping
- Real-time rate comparison across all integrated carriers
- Automatic selection of optimal carrier/service based on cost, delivery speed, and destination
- Powered by Shippo API integration under the hood
- Merchants can set shipping method preferences (Standard, Expedited, 2-Day)

### Label Generation
- Automated label purchase and printing at fulfillment time
- Labels generated instantly as orders enter processing
- Supports all integrated carriers' label formats
- Bulk label generation for high-volume operations

### Tracking
- Real-time tracking updates flow back to merchant dashboards and storefronts
- Each shipment includes: tracking number, carrier, service type, tracking URL
- **Webhook-based**: Subscribe to `order.shipped` and `order.shipment.delivered` events
- **Polling-based**: `GET /2026-01/order?HasTracking=true&IsTrackingUploaded=false&Limit=250`
- Tracking sync acknowledgment: `POST /2026-01/shipment:batchUpdateTrackingUpload`
- Automatic tracking email/SMS notifications to end customers

### Supported Shipping Methods
- Standard (ground)
- Expedited
- 2-Day
- B2B: Parcel and Freight options
- International shipping with customs documentation

---

## API Version History

| Version | Date | Key Changes |
|---------|------|-------------|
| 2026-01 | Feb 2026 | Inventory history query, sandbox simulation endpoints, MCP server |
| 2025-07 | Jul 2025 | Billing endpoints, product variants, product deletion, colon-style actions |
| 2.0 | Apr 2025 | New documentation portal, experimental version |
| 1.0 | 2019-2024 | Original API, incrementally expanded (receiving, returns, PAT auth, inventory) |

---

## Key Domain Concepts

| Concept | Description |
|---------|-------------|
| **Channel** | Vendor app installation representing a merchant integration (e.g., "Store #133432") |
| **Product** | Virtual record created via a channel; auto-generates inventory items |
| **Inventory** | Physical goods; may relate to multiple products via merges |
| **Order** | External source data for fulfillment; can generate multiple shipments |
| **Shipment** | Fulfillment result; one order can produce many shipments |
| **WRO** | Warehouse Receiving Order (inbound ASN equivalent) |
| **Return** | RMA for unpacking returned items (restock, dispose, quarantine) |
| **Bundle** | Product resolving to multiple inventory items (gift packs, multipacks) |
| **Merge** | Multiple products from different channels resolving to one inventory item |
| **Lot Item** | FIFO-tracked items with expiration dates or batch numbers |
| **Fulfillment Center** | Physical ShipBob warehouse location |

---

## Platform Integrations

### Native Integrations
Shopify, Shopify Plus, BigCommerce, WooCommerce, Amazon, Walmart, eBay, Squarespace, Wix, Square, Magento

### Middleware Compatibility
ShipStation, OrderDesk, Pipe17, and other iPaaS/middleware platforms

### Partner Ecosystem
https://partners.shipbob.com/directory/ - Directory of technology and service partners

---

## Sources

- [ShipBob Developer Portal](https://developer.shipbob.com/)
- [ShipBob API Introduction](https://developer.shipbob.com/introduction)
- [ShipBob Authentication](https://developer.shipbob.com/auth)
- [ShipBob Rate Limits](https://developer.shipbob.com/rate-limit)
- [ShipBob Webhooks](https://developer.shipbob.com/webhooks)
- [ShipBob Status Reference](https://developer.shipbob.com/status-reference)
- [ShipBob API Release Notes](https://developer.shipbob.com/release-notes)
- [ShipBob Concepts](https://developer.shipbob.com/concepts)
- [ShipBob Orders Guide](https://developer.shipbob.com/guides/orders)
- [ShipBob Tracking Guide](https://developer.shipbob.com/guides/tracking)
- [ShipBob Inventory Guide](https://developer.shipbob.com/guides/inventory)
- [ShipBob Products Guide](https://developer.shipbob.com/guides/products)
- [ShipBob Pricing](https://www.shipbob.com/pricing/)
- [ShipBob Help Center](https://support.shipbob.com/)
- [ShipBob Resource Library](https://resources.shipbob.com/)
- [ShipBob Wave Picking Guide](https://www.shipbob.com/warehouse-management/wave-picking/)
- [ShipBob Cartonization](https://www.shipbob.com/blog/cartonization/)
- [ShipBob Box Selection Process](https://support.shipbob.com/s/article/Box-Selection-Process)
- [ShipBob WMS Announcement](https://www.businesswire.com/news/home/20220706005079/en/)
- [ShipBob WMS Support](https://support.shipbob.com/s/article/ShipBob-WMS)
- [ShipBob Go SDK](https://github.com/stryd/shipbob-go)
- [ShipBob Python SDK](https://github.com/community-phone-company/shipbob-sdk-python)
- [ShipBob Rust SDK](https://crates.io/crates/shipbob)
- [ShipBob Node.js Sample](https://github.com/shipbobDev/DeveloperApiSampleNodeJs)
- [Capterra ShipBob Reviews](https://www.capterra.com/p/166529/ShipBob/reviews/)
- [FitSmallBusiness ShipBob Review](https://fitsmallbusiness.com/shipbob-review/)
- [Speed Commerce ShipBob Review](https://www.speedcommerce.com/vs/shipbob-reviews/)
- [ShipBob Pricing Breakdown (Speed Commerce)](https://www.speedcommerce.com/vs/shipbob-pricing/)
- [ShipBob on Shopify App Store](https://apps.shopify.com/shipbob)
- [Prismatic ShipBob Component](https://prismatic.io/docs/components/shipbob/)
- [APITracker ShipBob](https://apitracker.io/a/shipbob)
