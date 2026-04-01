# ShipHero

## Overview & History

ShipHero is a cloud-based warehouse management system (WMS) and fulfillment platform built for e-commerce brands and 3PL providers. Founded in 2013, headquartered in Garnersville, NY. ShipHero operates both as a SaaS WMS platform (brands run their own warehouses using ShipHero software) and as a fulfillment service provider (ShipHero-operated warehouses fulfill orders on behalf of brands).

ShipHero operates **seven fulfillment centers** across the United States and Canada, providing outsourced fulfillment services alongside its software product.

## What It Does

### Pick Methods

ShipHero supports all four major picking strategies:

- **Wave Picking**: Orders grouped into waves based on shipping deadlines, SKU type, or zone. Released at scheduled times throughout the day. Ideal for high-volume warehouses where precise timing and smooth workflow are essential.
- **Batch Picking**: Items from various orders grouped together by common similarity (e.g., same SKU across multiple orders). Reduces travel time by consolidating picks.
- **Zone Picking**: Warehouse divided into zones; pickers assigned to specific zones. Orders that span multiple zones are passed between zone pickers.
- **Discrete/Piece Picking**: One order at a time, picker retrieves all SKUs before moving to the next order. Best for small operations with limited SKUs.

### AI-Powered Picking Optimization

ShipHero AI Picking reduces walking time through AI path optimization and smart batching. Reported results:
- Pickers walk **20-30% less**
- Up to **33% savings** on travel time
- Increased pick density and workflow productivity

### Pack Optimization

- **Pack-to-Light**: LED-guided packing system that streamlines order packing, reduces errors, and boosts throughput up to **450%**
- Automated cartonization and box selection
- Barcode verification during packing to reduce mispicks

### Shipping & Carrier Selection

- **Real-Time Rate Shopping**: Compares shipping rates and estimated delivery times from all connected carriers for each order. Finds the cheapest label that meets delivery SLA.
- **Automated Label Generation**: Creates shipping labels by sending shipment details to the connected carrier's API during packing. Labels include addresses, tracking barcodes, and service details.
- **Shipping Method Mapping**: Maps store shipping methods to carrier services for automated carrier selection.

### Labor Management

- Integration with inVia Robotics WES provides intelligent labor orchestration
- 24/7 monitoring and support for both human and robotic labor
- Labor is managed throughout the day to ensure orders ship on time
- Workforce performance analytics and reporting

### Robotics Integration

**inVia Robotics Partnership** (since 2021):
- Native integration between inVia WES (Warehouse Execution System) and ShipHero WMS
- Autonomous Mobile Robots (AMRs) for picking and replenishment
- Deployed in Jacksonville FL, Allentown PA, and Las Vegas NV fulfillment centers
- inVia Logic WES coordinates daily movements of goods, people, and equipment

**Webster Robotics Integration**:
- Multi-year partnership documented in ShipHero case studies
- WMS-to-robotics integration for automated warehouse operations

### WCS/WES Interfaces

ShipHero's architecture positions it as the WMS layer that integrates with external WES (Warehouse Execution System) providers like inVia. The WMS handles order management, inventory, and fulfillment logic while the WES coordinates physical automation (robots, conveyors, sorters). The native inVia integration demonstrates ShipHero's capacity to interface with warehouse control/execution systems.

## Technical Documentation

### API Overview

ShipHero provides a **GraphQL Public API** for programmatic access to platform data and features.

- **GraphQL Endpoint**: `https://public-api.shiphero.com/graphql`
- **Auth Endpoint**: `https://public-api.shiphero.com/auth`
- **Developer Portal**: https://developer.shiphero.com/
- **Schema Reference**: https://developer.shiphero.com/schema/
- **Legacy REST API**: Documented at https://shipheropublic.docs.apiary.io/ (deprecated in favor of GraphQL)

### GraphQL Queries (Known)

| Query | Description |
|-------|-------------|
| `order` / `orders` | Retrieve order details and lists |
| `product` / `products` | Retrieve product/SKU information |
| `inventory` | Query inventory levels |
| `vendors` | List vendor records |
| `shipment` / `shipments` | Query shipment data |
| `inbound_shipment` | Query inbound shipment details |
| `inbound_shipments` | List inbound shipments |
| `inbound_shipment_images` | Retrieve images for inbound shipments |
| `inbound_shipment_summary` | Summary of inbound shipment data |
| `inbound_shipment_location_summary` | Location-level inbound summary |
| `purchase_order` / `purchase_orders` | PO queries |
| `return` / `returns` | Return/RMA queries |
| `warehouse` / `warehouses` | Warehouse configuration |
| `bill` / `bills` | Billing data (3PL) |
| `webhook` / `webhooks` | Webhook registration queries |

### GraphQL Mutations (Known)

| Mutation | Description |
|----------|-------------|
| `order_create` | Create a new order |
| `order_fulfill` | Fulfill an order (returns shipment info) |
| `order_clear_tags` | Clear tags from an order |
| `product_update` | Update product details |
| `inventory_add` | Add inventory quantity |
| `inventory_subtract` | Subtract inventory quantity |
| `inventory_remove` | Remove inventory entirely |
| `inventory_replace` | Replace inventory count |
| `vendor_create` | Create a new vendor |
| `purchase_order_create` | Create a purchase order |
| `inbound_shipment_create` | Create inbound shipment (added March 2026) |
| `inbound_shipment_update` | Update inbound shipment |
| `webhook_create` | Register a new webhook |
| `webhook_update_url` | Change webhook destination URL |
| `bill_create` | Create a billing record |
| `bill_delete` | Delete a billing record |
| `bill_recalculate` | Recalculate a bill |
| `bill_submit` | Submit a bill |
| `bill_update` | Update a bill |

### SDKs and Client Libraries

ShipHero does **not** provide official SDKs. The API is accessed via standard GraphQL clients. Examples are provided in Python and JavaScript. Any HTTP client or GraphQL library works:
- Python: `requests`, `gql`, `graphql-client`
- JavaScript: `axios`, `apollo-client`, `graphql-request`
- No-code: n8n, Parabola, Pipedream all offer ShipHero connectors

**Public API Agents Skill** (March 2026): ShipHero published an AI agent skill for obtaining read-only access tokens for the Public API.

### Authentication

**Token-based authentication** (not OAuth2 authorization code flow):

1. Create a **Third-Party Developer user** in ShipHero account settings
2. Receive an **Access Token** and **Refresh Token** at creation time
3. Include the Access Token in all API requests:
   ```
   Authorization: Bearer <access_token>
   ```
4. When the access token expires, use the refresh token to obtain a new one via the `/auth` endpoint
5. Tokens expire (community reports suggest ~1 month lifetime for access tokens)

**Key details:**
- No OAuth2 authorization code grant or PKCE flow -- it is a simple token-based system
- Refresh tokens are long-lived; access tokens are short-lived
- The `/auth` endpoint handles token refresh
- 3PL accounts may have per-customer token scoping

### Rate Limiting

ShipHero uses a **credit-based throttle system**:

| Parameter | Value |
|-----------|-------|
| Initial credits | **4,004** |
| Credit restoration | **60 credits/second** |
| Max credits | **4,004** (cannot accumulate beyond initial) |
| Request limit | **7,000 requests per 5 minutes** |
| Throttle response | HTTP `429 Too Many Requests` |

- Each GraphQL operation has a calculated **complexity score** (cost in credits)
- Complexity depends on the fields requested and relationship depth
- Use `analyze: true` in queries to calculate complexity without executing
- The `complexity` field in responses shows the cost of each operation
- Credits are shared across all users on the same account

### Webhooks

**Registration**: Use the `webhook_create` GraphQL mutation with:
- `name`: Webhook event type (e.g., "Shipment Update")
- `url`: Destination URL
- `shop_name`: Associated shop

**Available Webhook Events**:

| Event | Trigger |
|-------|---------|
| Shipment Update | Order fulfilled (single or bulkship, or via API) |
| Inventory Update | Any inventory quantity change |
| Inventory Change | On Hand quantity change (reports delta) |
| Return Update | Return created or updated |
| PO Update | Purchase order created or updated |
| Order Canceled | Order cancellation |
| Capture Payment | Payment capture event |
| Order Packed Out | Order packing completed |
| Order Allocated | Order allocated to warehouse |
| Order Deallocated | Order deallocated |
| Package Added | Package added to order |
| Generate Label | Label generation event |
| Tote Complete | Tote picking completed |
| Tote Cleared | Tote cleared |
| Print Barcode | Barcode print event |
| Shipment ASN | Advanced Shipping Notification |
| Automation Rules | Automation rule triggered |

**Webhook Security**:
- Each request includes an `x-shiphero-hmac-sha256` header
- HMAC-SHA256 signature generated using shared secret + request payload
- Shared secret is displayed **only once** at webhook registration time
- Verification process:
  1. Extract `x-shiphero-hmac-sha256` header
  2. Compute HMAC-SHA256 of the raw request body using the shared secret
  3. Base64-encode the result
  4. Use constant-time comparison to verify

**Webhook Management Mutations**:
- `webhook_create`: Register new webhook
- `webhook_update_url`: Change destination URL
- Enable/disable webhooks without deleting them
- Response fields: `enabled`, `health`, `created_at`, `updated_at`, `last_enabled_change`

## Ecommerce Platform Integrations

### Direct Store Integrations
- **Shopify** (including Shopify Plus and Shopify POS) -- one-click install
- **Amazon** (FBA/FBM)
- **BigCommerce** -- one-click install
- **WooCommerce** -- via WordPress plugin
- **eBay**
- **Etsy**
- **Walmart**
- **Google Shopping**
- **Magento 2.x**
- **Mystore.no**

### Alternative Connection Methods
- **CSV Upload**: Import orders via file upload
- **GraphQL API**: Build custom integrations for unsupported platforms

## Carrier Integration Capabilities

### Supported Carriers (Native Integrations)

| Carrier | Services |
|---------|----------|
| **USPS** | Via Endicia, USPS Modern (native), and Shippo |
| **UPS** | Full integration (rates, labels, tracking) |
| **FedEx** | Express, Ground, Ground Economy (SmartPost) |
| **DHL Express** | International shipping |
| **DHL eCommerce** | Lightweight international |
| **Canada Post** | Tracked Packet and other services |
| **Shippo** | Multi-carrier aggregator (extends to 85+ carriers) |

### Rate Shopping
- Real-time comparison across all connected carriers for each order
- Factors: cost, estimated delivery time, delivery SLA compliance
- Automatic selection of cheapest option meeting delivery requirements
- Configurable rules for carrier preference and service level

### Label Generation
- Automated during pack process
- Carrier API integration for real-time label creation
- Includes: addresses, tracking barcodes, service details, customs forms
- Bulk label generation supported (bulkship)

### Tracking
- Automatic tracking number capture at label generation
- Tracking info synced back to sales channels (Shopify, Amazon, etc.)
- **PostHero**: ShipHero's package tracking feature for end-customer visibility

## Help Centers, Knowledge Bases & Community

| Resource | URL | Description |
|----------|-----|-------------|
| Software Help Center | https://software-help.shiphero.com/hc/en-us | Main knowledge base for WMS software |
| Community Forum | https://community.shiphero.com/ | User forum for brands, 3PLs, developers |
| Developer Portal | https://developer.shiphero.com/ | API documentation and examples |
| FAQ | https://www.shiphero.com/faq | General product FAQ |
| Software FAQ | https://shiphero.com/software-faqs/ | Software-specific FAQ |
| Support Portal | https://www.shiphero.com/support | Ticketing system (24/7 access) |
| Blog | https://www.shiphero.com/blog | Product updates, warehouse tips |
| YouTube | ShipHero channel | Video tutorials and feature demos |

**Support tiers:**
- 24/7 access via ticketing system
- Tier 1 Support targets response within 1 hour of first contact
- Enterprise+ plan includes dedicated Account Manager

## Pricing

### Software Plans (WMS SaaS)

| Plan | Monthly Cost | Key Features |
|------|-------------|--------------|
| **Brand** | $1,850/mo | Warehouse routing, lot/expiration tracking, rate shopper, automation rules, up to 10 store connections, 5 user seats |
| **3PL** | $1,995/mo | All Brand features + customer portals, account manager, sandbox account, marketplace listing, 5 user seats |
| **Enterprise+** | $2,750/mo | All Brand features + dynamic slotting, account manager, increased API rate limits |

- Additional user seats: **$150/user/month**
- Custom pricing available for large deployments

### Fulfillment Service Pricing (ShipHero-operated warehouses)

- Starts at **$499/month** for up to 1,000 orders
- Additional orders: **$0.30/order** (reported, may vary)
- Storage, special handling, and other fees may apply
- Pricing not fully transparent upfront -- contact sales for detailed quotes

## Pros and Cons (Aggregated from G2, Capterra, TrustRadius, Shopify App Store)

### Pros

- **User-friendly interface** consistently praised; operators clearly involved in UX design
- **Comprehensive picking strategies** (wave, batch, zone, discrete) with AI optimization
- **Strong e-commerce integrations** (Shopify, Amazon, BigCommerce, etc.) with one-click setup
- **Real-time inventory tracking** with multi-location support
- **Rate shopping** finds cheapest carrier automatically
- **Pack-to-Light** system dramatically improves packing speed
- **Automation rules** (order batching, routing) reduce manual work
- **24/7 support** with fast initial response times
- **GraphQL API** is flexible and well-documented
- **Robotics integration** (inVia, Webster) for warehouse automation
- Mindful of operations on the floor -- built with operator input

### Cons

- **Steep learning curve** for advanced features; complex initial setup
- **Billing/invoicing limitations** -- manual invoice creation still required; QuickBooks integration lacks fee-to-revenue mapping
- **Buggy at times** -- random one-off issues that get fixed but cause disruptions
- **Confusing error messages** make troubleshooting difficult
- **Limited reporting dashboard** -- users want more insights and analytics
- **Fulfillment service complaints**: order errors, delayed shipments, inventory mismatches, SLA misses
- **Pricing transparency issues** -- unexpected costs and pricing changes after onboarding
- **Multi-location data issues** -- syncs ALL orders across ALL locations even when not needed, creating data protection concerns
- **Customer support inconsistency** -- fast Tier 1 response but sometimes slow on complex issues
- **Mobile experience** -- website/app performance issues on mobile reported
- **International shipping gaps** -- reports of packages going missing with international partner (Passport)
- **Limited customization** without developer support

### Review Ratings Summary

| Platform | Rating |
|----------|--------|
| G2 | Well-regarded (exact score varies by category) |
| Capterra | Positive overall, 4+ stars |
| TrustRadius | 6.7/10 |
| Shopify App Store | Mixed reviews |

## Key Differentiators

1. **Dual offering**: Both SaaS WMS software AND operated fulfillment centers
2. **AI-powered picking**: Path optimization and smart batching reduce labor costs
3. **Pack-to-Light**: LED-guided packing is a standout feature for throughput
4. **Native robotics integration**: Direct WMS-to-WES integration with inVia
5. **GraphQL-first API**: Modern API design with self-documenting schema
6. **Credit-based rate limiting**: More sophisticated than simple request-per-second limits

## Integration Considerations for Omnifill

### Adapter Architecture Notes
- **Protocol**: GraphQL (single endpoint, flexible queries)
- **Auth**: Bearer token with refresh flow (simpler than OAuth2 code grant)
- **Webhooks**: HMAC-SHA256 verified, JSON payloads, wide event coverage
- **Rate Limits**: Credit-based system requires complexity tracking; 4,004 credit pool, 60/sec restore
- **Pagination**: GraphQL cursor-based pagination (standard GraphQL pattern)
- **Real-time data**: Webhooks for push notifications; polling via GraphQL for pull
- **Key entities**: Orders, Products, Inventory, Shipments, Returns, Purchase Orders, Warehouses, Vendors, Bills
- **3PL considerations**: Multi-tenant support with customer portals; per-customer scoping possible

### Potential Challenges
- No official SDK -- adapter must handle raw GraphQL queries
- Credit-based throttling requires complexity estimation to avoid 429s
- Token refresh lifecycle must be managed (access tokens expire ~monthly)
- Webhook shared secret shown only once at registration -- must be captured and stored
- Some API features gated by plan tier (Enterprise+ gets higher API rate limits)

## Sources

- [ShipHero WMS](https://www.shiphero.com/shiphero-wms)
- [ShipHero Picking Guide](https://www.shiphero.com/blog/picking-in-a-warehouse-what-is-order-picking)
- [ShipHero Wave Picking](https://www.shiphero.com/blog/warehouse-wave-picking)
- [ShipHero Pick and Pack Guide](https://shiphero.com/blog/shiphero-pick-and-pack-guide-for-warehouses/)
- [Developer Resources](https://developer.shiphero.com/)
- [GraphQL Schema](https://developer.shiphero.com/schema/)
- [Getting Started](https://developer.shiphero.com/getting-started/)
- [GraphQL Primer](https://developer.shiphero.com/graphql-primer/)
- [API Examples](https://developer.shiphero.com/examples/)
- [Webhooks Documentation](https://developer.shiphero.com/webhooks/)
- [Shipment Update Webhook](https://developer.shiphero.com/webhooks/shipment-update-webhook/)
- [Inventory Update Webhook](https://developer.shiphero.com/webhooks/inventory-update-webhook/)
- [Inventory Change Webhook](https://developer.shiphero.com/webhooks/inventory-change-webhook/)
- [PO Update Webhook](https://developer.shiphero.com/webhooks/po-update-webhook/)
- [Return Update Webhook](https://developer.shiphero.com/webhooks/return-update-webhook/)
- [Order Fulfillment Flow](https://developer.shiphero.com/flows/order-fulfillment/)
- [Inventory Flow](https://developer.shiphero.com/flows/inventory/)
- [Purchase Orders Flow](https://developer.shiphero.com/flows/purchase-orders/)
- [Returns Flow](https://developer.shiphero.com/flows/returns/)
- [How to Obtain API Tokens](https://software-help.shiphero.com/hc/en-us/articles/4419362224781-How-to-Obtain-API-Access-Refresh-Tokens)
- [ShipHero API Developer Resources](https://software-help.shiphero.com/hc/en-us/articles/4419296860429-ShipHero-API-Developer-Resources)
- [Label Generation and Rate Shopping Overview](https://software-help.shiphero.com/hc/en-us/articles/41556301027725-Label-Generation-and-Rate-Shopping-Overview)
- [Rate Shopping](https://www.shiphero.com/software/rate-shopping)
- [Shipping Integrations](https://software-help.shiphero.com/hc/en-us/categories/4419329876621-Shipping-Integrations)
- [Specific Carriers](https://software-help.shiphero.com/hc/en-us/sections/4420180430605-Specific-Carriers)
- [Connecting UPS to ShipHero](https://software-help.shiphero.com/hc/en-us/articles/4419345121421-Connecting-UPS-to-ShipHero)
- [Connecting Canada Post to ShipHero](https://software-help.shiphero.com/hc/en-us/articles/42132551866125-Connecting-Canada-Post-to-ShipHero)
- [USPS Modern](https://software-help.shiphero.com/hc/en-us/articles/40656238832141-All-About-USPS-Modern-via-ShipHero)
- [PostHero Tracking](https://software-help.shiphero.com/hc/en-us/articles/4419362320013-PostHero)
- [DHL Express Integration](https://shiphero.com/integrations/dhl-express/)
- [Ecommerce Integrations](https://www.shiphero.com/integrations)
- [Store Integrations Help](https://software-help.shiphero.com/hc/en-us/categories/4419329898125-Store-Integrations)
- [BigCommerce Integration](https://shiphero.com/integrations/bigcommerce/)
- [Community Forum](https://community.shiphero.com/)
- [Webhook Verification Discussion](https://community.shiphero.com/t/webhook-request-verification/1328)
- [Token Refresh Discussion](https://community.shiphero.com/t/token-refresh-and-expired-after-a-month/923)
- [Credit Limit Discussion](https://community.shiphero.com/t/credit-usage-limit/278)
- [inVia Robotics Partnership - Robot Report](https://www.therobotreport.com/invia-robotics-to-automate-2-shiphero-fulfillment-centers/)
- [ShipHero + inVia - Robotics 24/7](https://www.robotics247.com/article/shiphero_implements_invia_automation_upgrades_ecommerce_fulfillment_warehouses_three_states)
- [Webster Robotics Integration](https://www.shiphero.com/videos/years-of-success-shiphero-wms-webster-robotics-integration)
- [G2 Reviews](https://www.g2.com/products/shiphero/reviews)
- [Capterra Reviews](https://www.capterra.com/p/166930/ShipHero/reviews/)
- [TrustRadius Reviews](https://www.trustradius.com/products/shiphero/reviews)
- [Capterra Pricing](https://www.capterra.com/p/166930/ShipHero/pricing/)
- [Shopify App Store](https://apps.shopify.com/shiphero)
- [ExploreWMS Profile](https://www.explorewms.com/shiphero-wms.html)
- [SoftwareConnect Review](https://softwareconnect.com/reviews/shiphero/)
- [Trustpilot Reviews](https://www.trustpilot.com/review/shiphero.com)
