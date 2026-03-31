# WMS & Fulfillment System API Landscape

Research date: 2026-03-30

## Manhattan Associates

- **API Types:** REST + GraphQL (Active platform), SOAP/XML (legacy WMOS/SCALE), EDI, message queues (IBM MQ/JMS)
- **Auth:** OAuth 2.0 / OIDC + JWT (Active); LDAP/DB auth (legacy)
- **Docs:** Fully gated — no public developer portal. Requires licensing or partnership (NDA).
- **Products:** Active WM, Active Omni, Active Allocation, WMOS, SCALE
- **Capabilities:**
  - Order management (PO create/update, sales order ingestion, allocation, wave planning)
  - Inventory (real-time inquiry, adjustments, cycle counts, lot/serial tracking)
  - Fulfillment (wave management, pick/pack/ship, task/labor management, cartonization)
  - Shipping (carrier integration, rate shopping, label gen, manifest/BOL, tracking)
  - Receiving (ASN processing, receipt confirmation, put-away, cross-docking)
  - Returns, slotting, yard management, labor management
- **Access path:** Customer license, Partner Program (manh.com/partners), or sales engagement with NDA

## Blue Yonder (JDA)

- **API Types:** MOCA (proprietary layered architecture), SOAP; limited REST on newer components
- **Auth:** Not publicly documented (WS-Security for SOAP)
- **Docs:** Gated behind Blue Yonder Success Portal (customer/partner login required)
- **Capabilities:** Warehouse ops, inventory, order fulfillment, ERP integration via MOCA scripting
- **URL:** https://success.blueyonder.com (login required)

## SAP Extended Warehouse Management (EWM)

- **API Types:** OData/REST via SAP Business Accelerator Hub; also RFC, IDocs, ABAP OO interfaces
- **Auth:** OAuth 2.0 (SAP BTP standard)
- **Docs:** Partially public
  - API specs browsable: https://api.sap.com/api/WAREHOUSEORDER_0001/overview
  - EWM integration: https://api.sap.com/api/sapdme_ewm_integration/overview
  - Full API list: https://userapps.support.sap.com/sap/support/knowledge/en/3115182 (login required)
  - Help docs: https://help.sap.com/docs/SAP_EXTENDED_WAREHOUSE_MANAGEMENT
- **Capabilities:** Warehouse order/task management, goods movement, task confirmation, physical inventory, handling unit management
- **Licensing:** API specs free to browse; usage requires S/4HANA or EWM license

## Oracle WMS Cloud

- **API Types:** REST (comprehensive)
- **Auth:** BasicAuth + OAuth 2.0
- **Docs:** Fully public
  - REST API Guide: https://docs.oracle.com/en/cloud/saas/warehouse-management/26a/owmre/index.html
  - Integration API Guide: https://docs.oracle.com/en/cloud/saas/warehouse-management/20d/owmap/wms-web-service-apis.html
  - Auth guide: https://docs.oracle.com/en/cloud/saas/warehouse-management/22a/owmms/authentication.html
- **Capabilities:** Data integration (inbound/outbound), inventory, order ops, `lgfapi` module for CRUD on WMS resources

## Korber/Infios (HighJump)

- **API Types:** No public API. Integration via SFTP, SQL Server stored procedures + REST endpoints, ERP connectors
- **Auth:** Not publicly documented
- **Docs:** Fully gated — no public developer portal
- **Capabilities:** WMS ops, ERP integration (Dynamics, SAP, NetSuite, Infor), e-commerce connectors

## ShipBob

- **API Types:** REST
- **Auth:** Personal Access Token (PAT, no expiration) or OAuth 2.0 (multi-user apps)
- **Docs:** Fully public — https://developer.shipbob.com/
  - Quickstart: https://developer.shipbob.com/quickstart
  - Auth: https://developer.shipbob.com/auth
  - API base: https://api.shipbob.com/2026-01/
  - Free sandbox: https://sandbox-api.shipbob.com/
- **Capabilities:** Orders (read/write), inventory, products, fulfillment ops, receiving, returns, shipping/billing, channels, locations, webhooks

## ShipHero

- **API Types:** GraphQL
- **Auth:** JWT Bearer tokens (28-day expiry, refresh tokens available)
- **Docs:** Fully public — https://developer.shiphero.com/
  - GraphQL schema: https://developer.shiphero.com/schema/
  - Endpoint: https://public-api.shiphero.com/graphql
- **Rate Limiting:** Credit-based (4,004 initial, 60/sec restore)
- **Capabilities:** Inventory, order fulfillment, returns, POs, 3PL billing, inbound shipments, wholesale, webhooks, recurring exports

## Deposco

- **API Types:** REST
- **Auth:** Basic Auth (Tenant Code + API Username + API Password, from account manager)
- **Docs:** Partially public
  - Developer portal: https://developer.deposco.com/
  - Full docs: https://doc.deposco.com/ (login required)
  - Community client: https://github.com/launched-la/deposco-api
- **Capabilities:** Inventory (by facility/location), customer order import/update, POs, organizations

## Extensiv (3PL Central / Skubana)

- **API Types:** REST (8 separate APIs)
- **Auth:** OAuth 2.0 client credentials (Client ID + Secret, Base64-encoded, tokens expire 30-60 min)
  - Token endpoint: https://secure-wms.com/AuthServer/api/Token
- **Docs:** Fully public
  - Main hub: https://developer.extensiv.com/
  - 3PL Warehouse Manager: https://developer.3plcentral.com/
  - Order Manager (Skubana): https://documentation.skubana.com/
  - Access guide: https://help.extensiv.com/rest-api/providing-rest-api-access
- **APIs:** Hub, Billing, Fulfillment Marketplace, Parcel, Integration Manager (CartRover), 3PL Warehouse Manager, Warehouse Manager (TopShelf/Scout), Order Manager (Skubana)
- **Capabilities:** Billing/invoicing, inventory, orders, customers, multi-carrier parcel, sales channels, eCommerce integrations

## Logiwa

- **API Types:** REST (Swagger/OpenAPI)
- **Auth:** Client ID / Client Secret (API User + API Key), token-based
- **Docs:** Fully public
  - Swagger UI: https://myapi.logiwa.com/swagger/index.html
  - Open API guide: https://logiwa.my.site.com/logiwahelp/s/article/Logiwa-Open-API
- **Rate Limiting:** 60 req/min (standard), 530 req/min (enterprise)
- **Capabilities:** Product management, order operations, warehouse tasks (pick/sort/pack), store connections, POs, webhooks

---

## Accessibility Summary

| System | Public Docs | API Type | Auth | Sandbox |
|--------|------------|----------|------|---------|
| Manhattan Associates | No | REST/GraphQL/SOAP | OAuth 2.0 | No |
| Blue Yonder | No | MOCA/SOAP | WS-Security | No |
| SAP EWM | Partial | OData/REST | OAuth 2.0 | No |
| Oracle WMS Cloud | Yes | REST | BasicAuth/OAuth | No |
| Korber/Infios | No | N/A | N/A | No |
| ShipBob | Yes | REST | PAT/OAuth 2.0 | Yes |
| ShipHero | Yes | GraphQL | JWT | No |
| Deposco | Partial | REST | BasicAuth | No |
| Extensiv | Yes | REST (x8) | OAuth 2.0 | No |
| Logiwa | Yes | REST | Client creds | No |
