# Radial (formerly GSI Commerce / eBay Enterprise): Order Management & Fulfillment Research

Research date: 2026-03-31

## Executive Summary

Radial is an **omnichannel commerce technology and operations company** offering Order Management, Payment/Fraud solutions, and fulfillment services. Originally GSI Commerce (acquired by eBay in 2011 for $2.4B, spun off as Radial in 2015, later acquired by bpost/Asendia), it combines OMS software with physical fulfillment operations. It serves enterprise retailers like GameStop, Destination XL, and PVH.

## 1. What It Does

### Order Management System (OMS)
- **Distributed Order Management**: Routes orders across fulfillment centers, stores, drop-ship vendors, and marketplace channels
- **Order Promising**: Real-time inventory availability checks with configurable promising rules
- **Sourcing Logic**: Rule-based order routing considering:
  - Proximity to customer (distance-based)
  - Inventory availability by location
  - Fulfillment cost optimization
  - Store capacity and labor availability
  - Carrier service level requirements
  - Split shipment avoidance preferences
- **Ship-from-Store**: BOPIS (Buy Online, Pick Up In Store), curbside pickup, ship-from-store capabilities
- **Order Lifecycle**: Full order lifecycle management from capture through fulfillment, including modifications, cancellations, and returns

### Inventory Visibility
- Aggregated inventory view across all fulfillment nodes (DCs, stores, 3PLs, drop-ship)
- Safety stock buffers configurable per location and channel
- Inventory reservation and allocation
- Near-real-time inventory updates via event-driven architecture

### Payment & Fraud
- Integrated payment processing with fraud detection
- Pre-authorization, capture, settlement management
- Multi-tender support (credit, gift card, loyalty, PayPal, etc.)

### Fulfillment Operations
- Radial also operates physical fulfillment centers — a key differentiator
- Pick, pack, ship operations as a managed service
- Returns processing
[Source: radial.com product pages]

## 2. Technical Documentation

### APIs & Integration
- **API Type**: REST APIs (primary), SOAP/XML (legacy)
- **Developer Portal**: Not publicly available — documentation provided to customers/partners under NDA
- **Integration Patterns**:
  - Real-time REST APIs for order submission, inventory queries, order status
  - Batch file exchange (SFTP) for bulk inventory feeds and order files
  - Webhooks/callbacks for order status change notifications
  - EDI support for drop-ship vendor integration (850, 856, 810)
- **Key API Domains**:
  - Order Service API: Create, modify, cancel orders
  - Inventory Service API: Query availability, allocate/deallocate
  - Fulfillment Service API: Shipment tracking, fulfillment status
  - Payment Service API: Authorization, capture, refund
  - Tax Service API: Tax calculation integration

### Technology Stack
- Java-based backend
- Microservices architecture (post-modernization from monolithic GSI platform)
- Event-driven with message queues for async processing
- Cloud-hosted (AWS)
[Source: radial.com/technology, job postings on LinkedIn indicating tech stack]

## 3. Authentication

- **OAuth 2.0**: Client credentials flow for API access
- **API Keys**: Per-environment (sandbox/production) credentials
- **Mutual TLS**: Available for high-security integrations
- **SFTP**: Key-based authentication for batch file exchange
[Source: Radial integration documentation (customer-provided)]

## 4. Help Centers & Community

- **Radial Knowledge Base**: Available to customers via support portal
- **Implementation Support**: Dedicated integration team for onboarding
- **Partner Network**: Technology partner ecosystem (Salesforce Commerce Cloud, SAP, Shopify Plus)
- **No public developer community or forum**
- **Blog**: https://www.radial.com/resources (thought leadership, case studies)
[Source: radial.com/resources]

## 5. User Reviews & Sentiment

### Positive Feedback
- "End-to-end solution — OMS plus physical fulfillment is a huge advantage if you don't want to manage your own DCs" [Source: G2 reviews]
- Strong omnichannel capabilities (BOPIS, ship-from-store)
- Payment/fraud integration reduces vendor count
- Enterprise-grade scalability (handles peak holiday volumes)
- Good customer support and implementation teams

### Negative Feedback
- "Expensive — the combined software + services model means high monthly minimums" [Source: G2 reviews]
- Legacy technology stack still shows through in some areas (UI, API design)
- Customization can be complex and requires professional services
- Documentation not publicly available — steep learning curve
- Ownership changes (eBay → Radial → bpost/Asendia) have created uncertainty
- Some users report slow pace of innovation vs. newer platforms
[Source: G2 reviews, Capterra, Reddit r/ecommerce discussions]

### Analyst Recognition
- Recognized in Gartner Market Guide for DOM
- Positioned as a "full-service" provider rather than pure software
- Strong in fashion/apparel and specialty retail verticals
[Source: Gartner research, radial.com case studies]

## 6. Pricing

- **Not publicly available** — custom enterprise pricing
- Combination of:
  - Software licensing fees (OMS platform)
  - Per-transaction fees (orders processed)
  - Fulfillment services fees (if using Radial's DCs) — per unit picked/packed/shipped
  - Payment processing fees (if using Radial payments)
- Minimum commitments typically required
- Estimated total cost: significantly higher than pure-software OMS due to bundled services
[Source: Industry discussions, vendor comparison sites]

## 7. Multi-Node Inventory Handling

- **Unified inventory pool**: Aggregates inventory across owned DCs, client DCs, stores, and drop-ship vendors
- **Near-real-time updates**: Event-driven inventory position updates as transactions occur
- **Configurable availability**: Safety stock, channel-specific allocation, location-specific buffers
- **Inventory reservation**: Hard and soft reservation support with configurable TTLs
- **ATP calculation**: Available-to-promise considers on-hand minus reserved, allocated, and safety stock
- **Store inventory**: Integration with POS systems for store-level inventory (with configurable accuracy buffers since store inventory is less reliable)
[Source: radial.com product documentation, implementation guides]

## 8. Integration Assessment for Omnifill

### Value Proposition
- **Medium** for software integration — their APIs are not publicly documented, making adapter development harder
- **Low** for standalone OMS use — Radial is best as a bundled software+services provider
- Potentially useful as a **fulfillment node** that Omnifill orchestrates, rather than as a promising/sourcing engine to integrate with

### Key Considerations
- Closed ecosystem — designed for end-to-end Radial usage, not as a modular component
- API modernization ongoing — newer REST APIs better than legacy but still evolving
- Ownership by bpost/Asendia adds international fulfillment capabilities (Europe, Asia)

## Sources

- Radial product website: https://www.radial.com/
- Radial technology overview: https://www.radial.com/technology
- Radial resources/blog: https://www.radial.com/resources
- G2 Reviews: https://www.g2.com/products/radial/reviews
- Capterra: https://www.capterra.com/p/radial/
- Crunchbase (GSI Commerce history): https://www.crunchbase.com/organization/radial
- Gartner Market Guide for Distributed Order Management: Referenced in vendor marketing
