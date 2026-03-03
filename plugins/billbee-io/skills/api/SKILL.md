---
name: billbee-api
description: "Billbee API skill. Use when working with Billbee for api. Covers 87 endpoints."
version: 1.0.0
generator: lapsh
---

# Billbee API
API version: V1

## Auth
basic | ApiKey X-Billbee-Api-Key in header

## Base URL
https://app.billbee.io

## Setup
1. Set your API key in the appropriate header
2. GET /api/v1/apiusage -- verify access
3. POST /api/v1/customer-addresses -- create first customer-addresses

## Endpoints

87 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/v1/apiusage | Get summarised api usage statistics |
| GET | /api/v1/apiusage/detail | Get detailed api usage statistics |
| GET | /api/v1/cloudstorages | Gets a list of all connected cloud storage devices |
| GET | /api/v1/customer-addresses | Get a list of all customer addresses |
| POST | /api/v1/customer-addresses | Creates a new customer address |
| GET | /api/v1/customer-addresses/{id} | Queries a single customer address by id |
| PUT | /api/v1/customer-addresses/{id} | Updates a customer address by id |
| GET | /api/v1/customers | Get a list of all customers |
| POST | /api/v1/customers | Creates a new customer |
| GET | /api/v1/customers/{id} | Queries a single customer by id |
| PUT | /api/v1/customers/{id} | Updates a customer by id |
| GET | /api/v1/customers/{id}/orders | Queries a list of orders from a customer |
| GET | /api/v1/customers/{id}/addresses | Queries a list of addresses from a customer |
| POST | /api/v1/customers/{id}/addresses | Adds a new address to a customer |
| GET | /api/v1/customers/addresses/{id} | Queries a single address from a customer |
| PUT | /api/v1/customers/addresses/{id} | Updates all fields of an address |
| PATCH | /api/v1/customers/addresses/{id} | Updates one or more fields of an address |
| GET | /api/v1/enums/paymenttypes | Returns a list with all defined paymenttypes |
| GET | /api/v1/enums/shippingcarriers | Returns a list with all defined shippingcarriers |
| GET | /api/v1/enums/accountsyncstate | Returns a list with all defined account sync states |
| GET | /api/v1/enums/shopaccounttype | Returns a list with all defined account types |
| GET | /api/v1/enums/shipmenttypes | Returns a list with all defined shipmenttypes |
| GET | /api/v1/enums/orderstates | Returns a list with all defined orderstates |
| GET | /api/v1/events | Get a list of all events optionally filtered by date. This request is extra throttled to 2 calls per page per hour. |
| POST | /api/v1/orders/createmultiple |  |
| GET | /api/v1/orders | Get a list of all orders optionally filtered by date |
| POST | /api/v1/orders |  |
| PUT | /api/v1/orders/{id}/tags | Sets the tags attached to an order |
| POST | /api/v1/orders/{id}/tags | Attach one or more tags to an order |
| POST | /api/v1/orders/tags | Add one or more tags to multiple orders |
| GET | /api/v1/orders/{id} | Get a single order by its internal billbee id. This request is throttled to 6 calls per order in one minute |
| PATCH | /api/v1/orders/{id} | Updates one or more fields of an order |
| GET | /api/v1/orders/findbyextref/{extRef} | Get a single order by its external order number |
| PUT | /api/v1/orders/{id}/orderstate | Changes the main state of a single order |
| POST | /api/v1/orders/{id}/shipment | Add a shipment to a given order |
| GET | /api/v1/orders/invoices | Get a list of all invoices optionally filtered by date. This request ist throttled to 1 per 1 minute for same page and minInvoiceDate |
| GET | /api/v1/orders/find/{id}/{partner} | Find a single order by its external id (order number) |
| POST | /api/v1/orders/CreateDeliveryNote/{id} | Create an delivery note for an existing order. This request is extra throttled by order and api key to a maximum of 1 per 5 minutes. |
| POST | /api/v1/orders/CreateInvoice/{id} | Create an invoice for an existing order. This request is extra throttled by order and api key to a maximum of 1 per 5 minutes. |
| GET | /api/v1/orders/PatchableFields | Returns a list of fields which can be updated with the orders/{id} patch call |
| POST | /api/v1/orders/{id}/send-message | Sends a message to the buyer |
| POST | /api/v1/orders/{id}/trigger-event | Triggers a rule event |
| POST | /api/v1/orders/{id}/parse-placeholders | Parses a text and replaces all placeholders |
| POST | /api/v1/orders/{id}/message | Adds a message to the order |
| GET | /api/v1/layouts |  |
| POST | /api/v1/search | Search for products, customers and orders. |
| GET | /api/v1/products | Get a list of all products |
| POST | /api/v1/products | Creates a new product |
| GET | /api/v1/products/{id} | Queries a single article by id or by sku |
| DELETE | /api/v1/products/{id} | Deletes a product |
| PATCH | /api/v1/products/{id} | Updates one or more fields of a product |
| GET | /api/v1/products/stocks | Query all defined stock locations |
| GET | /api/v1/products/PatchableFields | Returns a list of fields which can be updated with the patch call |
| GET | /api/v1/products/category | GEts a list of all defined categories |
| POST | /api/v1/products/updatestock | Update the stock qty of an article |
| POST | /api/v1/products/stockmultiple | Retrieve the stock qty for multiple articles at once |
| POST | /api/v1/products/updatestockmultiple | Update the stock qty for multiple articles at once |
| GET | /api/v1/products/reservedamount | Queries the reserved amount for a single article by id or by sku |
| POST | /api/v1/products/updatestockcode | Update the stock code of an article |
| GET | /api/v1/products/custom-fields | Queries a list of all custom fields |
| GET | /api/v1/products/custom-fields/{id} | Queries a single custom field |
| GET | /api/v1/products/{productId}/images | Returns a list of all images of the product |
| PUT | /api/v1/products/{productId}/images | Add multiple images to a product or replace the product images by the given images |
| GET | /api/v1/products/{productId}/images/{imageId} | Returns a single image by id |
| PUT | /api/v1/products/{productId}/images/{imageId} | Add or update an existing image of a product |
| DELETE | /api/v1/products/{productId}/images/{imageId} | Deletes a single image from a product |
| GET | /api/v1/products/images/{imageId} | Returns a single image by id |
| DELETE | /api/v1/products/images/{imageId} | Deletes a single image by id |
| POST | /api/v1/products/images/delete |  |
| POST | /api/v1/automaticprovision/createaccount | Creates a new Billbee user account with the data passed |
| GET | /api/v1/automaticprovision/termsinfo | Returns infos about Billbee terms and conditions |
| POST | /api/v1/shipment/shipmentmultiple | Creates multiple shipments |
| POST | /api/v1/shipment/shipment | Creates a new shipment with the selected Shippingprovider |
| GET | /api/v1/shipment/shippingproviders | Query all defined shipping providers |
| POST | /api/v1/shipment/shipwithlabel | Creates a shipment for an order in billbee |
| POST | /api/v1/shipment/shipwithlabelmultiple | Creates shipments for a list of orders in billbee |
| GET | /api/v1/shipment/shippingcarriers | Queries the currently available shipping carriers. |
| GET | /api/v1/shipment/ping |  |
| GET | /api/v1/shipment/shipments | Get a list of all shipments optionally filtered by date. All parameters are optional. |
| GET | /api/v1/shopaccounts | Queries a list of avaible shop accounts |
| GET | /api/v1/webhooks | Gets all registered WebHooks for a given user. |
| POST | /api/v1/webhooks | Registers a new WebHook for a given user. |
| DELETE | /api/v1/webhooks | Deletes all existing WebHook registrations. |
| GET | /api/v1/webhooks/{id} | Looks up a registered WebHook with the given {id} for a given user. |
| PUT | /api/v1/webhooks/{id} | Updates an existing WebHook registration. |
| DELETE | /api/v1/webhooks/{id} | Deletes an existing WebHook registration. |
| GET | /api/v1/webhooks/filters | Returns a list of all known filters you can use to register webhooks |

## Enhanced Skill Content
## Question Mapping

- "How many API calls have I made today?" -> GET /api/v1/apiusage
- "Show me detailed API usage breakdown" -> GET /api/v1/apiusage/detail
- "List all my orders from last week" -> GET /api/v1/orders
- "Find an order by its external reference number" -> GET /api/v1/orders/findbyextref/{extRef}
- "What is the current stock level for all products?" -> GET /api/v1/products/stocks
- "Update the stock quantity for a product" -> POST /api/v1/products/updatestock
- "Create a shipping label for an order" -> POST /api/v1/shipment/shipwithlabel
- "Generate an invoice PDF for order 12345" -> POST /api/v1/orders/CreateInvoice/{id}
- "What orders does customer 99 have?" -> GET /api/v1/customers/{id}/orders
- "Add a tag to an existing order" -> POST /api/v1/orders/{id}/tags
- "Change the state of an order to shipped" -> PUT /api/v1/orders/{id}/orderstate
- "Search across orders, products, and customers" -> POST /api/v1/search
- "Which shipping providers are available?" -> GET /api/v1/shipment/shippingproviders
- "List all available payment types" -> GET /api/v1/enums/paymenttypes
- "What fields can I patch on a product?" -> GET /api/v1/products/PatchableFields

## Response Tips

- **Orders/Customers/Products (list endpoints):** Paginated via `page` and `pageSize` params. Response wraps items in a data array with paging metadata. Always check if more pages exist before assuming complete results.
- **Enum endpoints (`/enums/*`):** Return flat arrays of id/name pairs. Cache these locally -- they rarely change.
- **Stock endpoints:** `reservedamount` returns reserved (not available) quantity. Subtract from total stock for sellable count. `lookupBy` controls whether `id` is a Billbee ID, SKU, or EAN.
- **Shipment/Invoice creation:** Returns the created resource. For PDF variants (`includePdf`, `includeInvoicePdf`), the response embeds base64-encoded PDF data.
- **Search (`POST /search`):** Accepts a model with search term and type filters. Results are grouped by entity type (orders, products, customers).
- **Events:** Filter by `typeId` to narrow to specific event categories. Date range filtering is essential for high-volume accounts.

## Anomaly Flags

- **API usage approaching limits:** After any write operation, proactively call `GET /api/v1/apiusage` and warn if daily quota is above 80%.
- **Empty paginated results with page > 1:** Likely means the client overshot. Surface a warning that total results may have changed between requests.
- **Order state mismatches:** If `PUT /orders/{id}/orderstate` returns 200 but a subsequent GET shows the old state, flag a potential rule conflict in Billbee's automation.
- **Stock going negative:** After `updatestock` or `updatestockmultiple`, if returned stock value is below zero, alert immediately -- this indicates overselling risk.
- **Shipment ping failures:** If `GET /shipment/ping` returns non-200, surface that the shipping subsystem may be degraded before attempting label creation.
- **Deprecated or unknown enum values:** If an order or product contains a payment type, carrier, or state ID not present in the corresponding `/enums/*` response, flag it as potentially deprecated or custom.
- **Bulk operation partial failures:** When using `createmultiple`, `updatestockmultiple`, or `shipmentmultiple`, inspect each item in the response array individually -- partial success is possible.

## Playbook

### 1. Fulfill an Order End-to-End

1. Retrieve the order: `GET /api/v1/orders/{id}`
2. Verify stock for each line item: `GET /api/v1/products/{id}` (use `lookupBy` if referencing by SKU)
3. Update order state to processing: `PUT /api/v1/orders/{id}/orderstate`
4. Create a shipping label: `POST /api/v1/shipment/shipwithlabel`
5. Add shipment to the order: `POST /api/v1/orders/{id}/shipment`
6. Generate the invoice: `POST /api/v1/orders/CreateInvoice/{id}` with `includeInvoicePdf: true`
7. Send confirmation message: `POST /api/v1/orders/{id}/send-message`

### 2. Bulk Stock Update from External System

1. Fetch current stock snapshot: `GET /api/v1/products/stocks`
2. Prepare delta models comparing external quantities to Billbee quantities
3. Push updates in batch: `POST /api/v1/products/updatestockmultiple`
4. Verify critical items: `GET /api/v1/products/reservedamount` for high-velocity SKUs
5. Check API usage after bulk operation: `GET /api/v1/apiusage`

### 3. Set Up Webhook Monitoring

1. List available webhook event filters: `GET /api/v1/webhooks/filters`
2. Register a new webhook: `POST /api/v1/webhooks` with target URL, secret, and selected filters
3. Verify registration: `GET /api/v1/webhooks/{id}`
4. Test by triggering a relevant event (e.g., create a test order)
5. To decommission: `DELETE /api/v1/webhooks/{id}` (use `DELETE /api/v1/webhooks` without ID to remove all)

### 4. Customer Lookup and Order History

1. Search for the customer: `POST /api/v1/search` with customer name or email
2. Retrieve full customer record: `GET /api/v1/customers/{id}`
3. Pull their order history: `GET /api/v1/customers/{id}/orders` (paginate through all pages)
4. List their addresses: `GET /api/v1/customers/{id}/addresses`
5. Update address if needed: `PUT /api/v1/customers/addresses/{id}`

### 5. Product Catalog Management

1. List all products: `GET /api/v1/products` (paginate with `page` and `pageSize`)
2. Check which fields are editable: `GET /api/v1/products/PatchableFields`
3. Update product details: `PATCH /api/v1/products/{id}` with only changed fields
4. Manage product images: `GET /api/v1/products/{productId}/images`, then `PUT` to add or `DELETE` to remove
5. Review custom fields: `GET /api/v1/products/custom-fields` for any extended attributes
6. Bulk delete unused images: `POST /api/v1/products/images/delete` with array of image IDs


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
