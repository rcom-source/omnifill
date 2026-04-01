# Radial (formerly GSI Commerce / eBay Enterprise)

## Overview & History

Radial is a multinational e-commerce fulfillment and omnichannel commerce company formed in 2016 through the merger of eBay Enterprise (formerly GSI Commerce, founded 1995 by Michael Rubin) and Innotrac Corporation. The lineage:

- **1995**: Global Sports Incorporated founded (renamed GSI Commerce in 2002)
- **2011**: eBay acquires GSI Commerce for $2.4 billion
- **2013**: Rebranded as eBay Enterprise
- **2015**: Sold to Permira-led consortium for $925 million, becomes independent
- **2016**: Merged with Innotrac to form **Radial**
- **2017**: Acquired by **bpostgroup** (Belgian postal/logistics) for $820 million

Headquartered in the Philadelphia area. Owned by bpostgroup. 40+ years of combined legacy in logistics and e-commerce.

## What It Does

### Operational Scale
- **30+ fulfillment centers** across North America and Europe
- **15M+ sq ft** of fulfillment capacity
- **139M units shipped** (2025); **18M units during peak season**
- Locations in: CA, GA, IN, KY, NJ, OH, PA, VA (US), plus Canada, Germany, Italy, Netherlands, Poland, UK

### Core Fulfillment Services
- **DTC (Direct-to-Consumer)** order fulfillment
- **B2B** distribution and order fulfillment
- **Returns management** (inspection, restocking)
- **Value-added services**: kitting, personalized packaging, bundling
- **Order orchestration/brokering**: AI/ML-driven intelligent routing to optimal fulfillment location
- **99.98% order accuracy** (reported by clients)

### Pick Methods & Pack Optimization
- Batch picking with mixed-SKU totes
- Pick-to-light systems integrated with WMS
- Manual putwalls (legacy) transitioning to robotic sortation
- AI-powered order sortation for batch-picked items

### Shipping / Carrier Selection
- Customizable **transportation management** solutions
- **Final mile network optimization** for fast, reliable delivery
- Zone-based pricing; rates depend on weight, size, destination, speed
- Works with major carriers (UPS, FedEx, USPS, regional carriers)
- Negotiated carrier rates passed through to clients

### Omnichannel / Store Fulfillment
- **Ship-from-Store**: Retail stores as fulfillment nodes
- **Buy Online Pick Up In-Store (BOPIS)**
- **Ship-to-Store**
- **Associate delivery**
- Intelligent order orchestration determines optimal fulfillment path based on speed, proximity, carrier availability

### Robotics Integration
- Deployed **12 Covariant AI Robotic U-Shaped Putwalls** at Trade Port 2 (Louisville, KY, 500,000 sq ft)
- Robots autonomously sort items from mixed-SKU totes into order cubbies
- AI-first solution that learns and adapts across wide SKU range
- Integrated with upstream/downstream material handling and existing WMS + pick-to-light systems
- Addresses labor shortage challenges during demand surges

### Labor Management
- Traditional labor-dependent operations transitioning to hybrid human+robot model
- Covariant deployment specifically addresses costly/unreliable labor sourcing during peak periods
- AI robotics reduce dependency on intensive seasonal hiring and training

### Payment & Fraud Services (Unique Differentiator)
- **Radial Fraud Zero**: Fully outsourced fraud management, works with existing payment providers
- **Radial Fraud Insights**: Real-time High/Medium/Low risk ratings per transaction
- **Payment processing**: Credit card, gift card, PayPal with client-side encryption
- **Tax compliance**: Worldwide indirect tax rate changes, customized tax reports
- **3D Secure v2** support

## Technical Documentation

### Developer Portal
- **Radial Integration Center**: `developer-apina.gsipartners.com` (requires login/account creation)
- **Payments & Fraud Docs**: `docs.radial.com` (being migrated to new portal)
- **Sandbox Environment**: `dev.radial.com` for Payments, Tax, and Fraud API testing

### API Architecture
- **REST-compliant** web services
- **XML messages** via HTTPS to defined URI endpoints (legacy)
- **JSON support** available via upgraded API integration option (newer)
- Each service defined by **.xsd schema files** with accompanying URI structure
- Public API behind an **API Security Layer**

### Authentication
- **API Key in HTTP header**: Radial generates the key and provides it to the client
- Key rotation: **new key every 6 months**
- Webhook endpoints use **username/password** authorization
- Client-side credit card encryption for payment APIs

### Webhooks & Async Messaging
- **Webhooks**: HTTP(S) endpoints for receiving async responses (fraud risk assessments, payment settlements)
- **AMQP (Advanced Message Queuing Protocol)**: Alternative queue-based event delivery
- Transaction responses are asynchronous -- must be collected from AMQP or pushed via webhooks
- Webhook payloads arrive as **XML strings**

### SDKs & Libraries
- **Node.js wrapper**: `node-radial` npm package (community, by giftnix) for Payments & Fraud REST APIs
- No official first-party SDKs found; integration is primarily REST API-based

### Platform Integrations
- **Shopify** (dedicated Shopify App Store app: "Radial Fulfillment")
- **Adobe Commerce** (Magento)
- **Salesforce Commerce Cloud**
- **Custom API** integrations
- **EDI** configurations
- Shopping cart integration options

### Fast Track Program
- Pay-as-you-go solution with pre-built integrations
- No upfront costs or long-term contracts
- Operational in as little as one week
- Connects to hundreds of commerce platforms and retail channels

## Help Center / Knowledge Base / Community

- **Radial Client Portal**: Enhanced version scheduled for mid-year release (comprehensive customer data insights)
- **Help Desk portal**: Dynamic FAQs and company policies for self-service
- **Customer care phone**: (877) 255-2857 (Mon-Fri business hours)
- **Sales inquiries**: sales@radial.com
- **Contact form**: radial.com/contact-us
- No public community forum or developer community found
- Documentation is gated behind login (Integration Center)

## User Reviews & Feedback

### G2 Reviews (Limited data -- few reviews available)
**Pros:**
- Great customer service, knowledgeable staff
- Good dashboard and interface
- Comprehensive order management covering all aspects (OMS, payments, fulfillment, customer care)
- Constantly working to improve UX

**Cons:**
- Platform is "very complicated within the user interface"
- Hard to find what you're looking for
- Still room for improvement despite ongoing updates

### Fulfill.com Profile
- **0 reviews** currently on the platform
- Listed as mid-market 3PL with 40+ years experience

### General Industry Sentiment
- Recognized as a leader in SPARK Matrix for Omnichannel Order Management Systems (2022)
- Strong reputation for enterprise-scale fulfillment
- Known for payment/fraud services as differentiator vs. pure 3PLs
- Criticism around complexity of integration and UI

## Pricing Model

Pricing is **not publicly disclosed** -- custom quotes required. Known fee categories:

| Category | Structure |
|----------|-----------|
| **Order Fulfillment** | Per-order; includes up to 4 picks, additional picks charged separately |
| **Storage** | Monthly; based on space (bins, shelves, pallets) |
| **Receiving** | Flat rate for first 2 hours, hourly thereafter |
| **Returns** | Variable based on inspection/restocking needs |
| **Implementation** | One-time setup fee; includes dashboard/analytics access |
| **Shipping** | Zone-based; by weight, size, destination, speed |
| **Custom Services** | Bundling, custom packaging charged separately |

- Volume-based pricing: costs per order decrease with higher shipment volume
- **Fast Track**: No upfront costs, no long-term contracts, pay-as-you-go

## Carrier Integration Capabilities

- Multi-carrier support (UPS, FedEx, USPS, regional carriers)
- Negotiated carrier rates leveraging Radial's volume
- Zone-based shipping rate optimization
- Transportation management system for carrier selection
- Final mile network optimization
- Store fulfillment integrates with carrier options for ship-from-store

## Summary: Strengths & Weaknesses

### Strengths
- Massive scale: 30+ FCs, 15M+ sq ft, 139M units/year
- Unique payment/fraud/tax services integrated with fulfillment
- True omnichannel: BOPIS, ship-from-store, ship-to-store
- Global presence (North America + Europe via bpostgroup)
- AI robotics deployment (Covariant) for automation
- Fast Track onboarding (1 week, no contracts)
- Pre-built integrations for major commerce platforms

### Weaknesses
- API documentation gated behind login; not developer-friendly for evaluation
- Legacy XML-first API design (JSON is newer addition)
- Complex UI/UX reported by users
- Limited public user reviews available
- No official SDKs beyond community Node.js wrapper
- No public community forum or developer ecosystem
- Pricing completely opaque; requires sales engagement


---

## Sources

- https://www.radial.com/
- https://www.radial.com/fulfillment
- https://www.radial.com/technology
- https://www.bpostgroup.com/ (parent company)
- https://www.g2.com/products/radial/reviews
- https://www.capterra.com/p/174483/Radial/reviews/
- Reddit r/ecommerce — Radial/GSI Commerce discussion threads
