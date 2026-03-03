---
name: api-v100
description: "API v1.0.0 API skill. Use when working with API v1.0.0 for api. Covers 61 endpoints."
version: 1.0.0
generator: lapsh
---

# API v1.0.0
API version: v1

## Auth
ApiKey x-auth-key in header | ApiKey x-auth-secret in header

## Base URL
https://www.envoice.in

## Setup
1. Set your API key in the appropriate header
2. GET /api/client/all -- verify access
3. POST /api/client/new -- create first new

## Endpoints

61 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/client/all | Return all clients for the account |
| POST | /api/client/new | Create a client |
| POST | /api/client/update | Update an existing client |
| GET | /api/client/candelete | Check if the provided client can be deleted |
| POST | /api/client/delete | Delete an existing client |
| GET | /api/client/details | Return client details. Activities and invoices included. |
| GET | /api/estimation/all | Return all estimation for the account |
| POST | /api/estimation/new | Create an estimation |
| POST | /api/estimation/update | Update an existing estimation |
| POST | /api/estimation/delete | Delete an existing estimation |
| POST | /api/estimation/changestatus | Change estimation status |
| GET | /api/estimation/status | Retrieve the status of the estimation |
| GET | /api/estimation/details | Return estimation data |
| GET | /api/estimation/uri | Return the unique url to the client's invoice |
| POST | /api/estimation/convert | Convert the estimation to an invoice |
| POST | /api/estimation/sendtoclient | Send the provided estimation to the client |
| GET | /api/general/countries | Return all of the platform supported countries |
| GET | /api/general/currencies | Return all of the platform supported currencies |
| GET | /api/general/uilanguages | Return all of the platform supported UI languages |
| GET | /api/general/dateformats | Return all of the platform supported Date Formats |
| GET | /api/invoice/all | Return all invoices for the account |
| GET | /api/invoice/allcategories | Return all invoice categories for the account |
| POST | /api/invoice/new | Create an invoice |
| POST | /api/invoice/newcategory | Create an invoice category |
| POST | /api/invoice/update | Update an existing invoice |
| POST | /api/invoice/updatecategory | Update an existing invoice category |
| POST | /api/invoice/delete | Delete an existing invoice |
| POST | /api/invoice/deletecategory | Delete an existing invoice category |
| POST | /api/invoice/sendtoclient | Send the provided invoice to the client |
| POST | /api/invoice/sendtoaccountant | Send the provided invoice to the accountant |
| POST | /api/invoice/changestatus | Change invoice status |
| GET | /api/invoice/status | Retrieve the status of the invoice |
| GET | /api/invoice/details | Return invoice data |
| GET | /api/invoice/uri | Return the unique url to the client's invoice |
| GET | /api/invoice/pdf | Return the PDF for the invoice |
| GET | /api/order/all | Return all orders for the account |
| POST | /api/order/new | Create an order |
| POST | /api/order/delete | Delete an existing order |
| POST | /api/order/changeshippingdetails | Change order shipping details |
| POST | /api/order/changestatus | Change order status |
| GET | /api/order/details | Return order details |
| GET | /api/payment/supported | Return all supported payment gateways (no currencies means all are supported) |
| GET | /api/paymentlink/uri | Return the unique url to the client's payment link |
| GET | /api/paymentlink/all | Create a payment link |
| POST | /api/paymentlink/new | Create a payment link |
| POST | /api/paymentlink/delete | Delete an existing payment link |
| GET | /api/product/all | Return all products for the account |
| POST | /api/product/new | Create a product |
| POST | /api/product/update | Update an existing product |
| POST | /api/product/delete | Delete an existing product |
| GET | /api/product/details | Return product details |
| GET | /api/tax/all | Return all taxes for the account |
| POST | /api/tax/new | Create a tax |
| POST | /api/tax/update | Update an existing tax |
| POST | /api/tax/delete | Delete an existing tax |
| GET | /api/worktype/all | Return all work types for the account |
| GET | /api/worktype/search | Return all work types for the account that match the query param |
| POST | /api/worktype/new | Create a work type |
| POST | /api/worktype/update | Update an existing work type |
| POST | /api/worktype/delete | Delete an existing work type |
| GET | /api/worktype/details | Return work type details |

## Enhanced Skill Content
## Question Mapping

- "Show me all my clients" -> GET /api/client/all
- "Create a new client" -> POST /api/client/new
- "Can I safely delete this client?" -> GET /api/client/candelete
- "Get the details for a specific invoice" -> GET /api/invoice/details
- "List all invoices with pagination" -> GET /api/invoice/all
- "Send an invoice to my client" -> POST /api/invoice/sendtoclient
- "Download an invoice as PDF" -> GET /api/invoice/pdf
- "Convert an estimation into an invoice" -> POST /api/estimation/convert
- "Create a new estimation and send it to the client" -> POST /api/estimation/new + POST /api/estimation/sendtoclient
- "What payment methods are supported?" -> GET /api/payment/supported
- "Create a payment link for a client" -> POST /api/paymentlink/new
- "List all products in my catalog" -> GET /api/product/all
- "Search work types by name" -> GET /api/worktype/search
- "What tax rates do I have configured?" -> GET /api/tax/all
- "Change the status of an order" -> POST /api/order/changestatus

## Response Tips

- **Client endpoints**: Returns flat client objects; `candelete` returns a boolean check -- always call before `delete` to avoid orphan references.
- **Invoice/Estimation lists**: Paginated via `queryOptions.page` and `queryOptions.pageSize`; omitting these returns the first page with default size. Check response for total count to know if more pages exist.
- **Detail endpoints**: Return a single entity by `id` query parameter; a missing or invalid ID typically yields an empty body with 200 rather than 404.
- **Status endpoints**: Return the current status string/enum for an entity; `changestatus` accepts a `statusModel` map with the target state.
- **Delete endpoints**: Most accept a `deleteModel` map (not just an ID) -- include the full model as returned by the detail endpoint.
- **General reference data** (`countries`, `currencies`, `uilanguages`, `dateformats`): Static lists, safe to cache for the session lifetime.
- **204 responses** (`client/update`, `order/changestatus`, `order/changeshippingdetails`, `product/update`, `tax/update`, `worktype/update`): No response body on success -- treat any non-204 as an error.

## Anomaly Flags

- **Mixed response codes across similar operations**: Some updates return 200, others 204. Surface a warning if a 200-returning update suddenly returns 204 or vice versa, as this may indicate API version drift.
- **Delete without candelete check**: Only `client` has a `candelete` guard. Flag when deleting invoices, products, or orders without first verifying dependencies manually.
- **Estimation-to-invoice conversion**: `POST /api/estimation/convert` accepts `id` as `int(int32)` -- the only endpoint with a typed parameter. Flag if the estimation status is not in a convertible state.
- **Missing pagination parameters**: If a list response returns a suspiciously round number of items (e.g., exactly 10, 20, 50), warn that results may be truncated and suggest adding `queryOptions.page` / `queryOptions.pageSize`.
- **Auth header presence**: Both `x-auth-key` and `x-auth-secret` are required on every request. Flag immediately if either is missing or returns 401/403.
- **Typo in official spec**: The `updatecategory` endpoint uses `invoiceCateogry` (misspelled). Agents must use the misspelled key or the request will fail.

## Playbook

### 1. Create and Send an Invoice

1. Fetch client list: `GET /api/client/all` -- pick the target client ID.
2. Fetch products: `GET /api/product/all` -- select line items.
3. Fetch tax rates: `GET /api/tax/all` -- attach applicable taxes.
4. Create the invoice: `POST /api/invoice/new` with the `invoice` map including client, line items, and tax references.
5. Verify creation: `GET /api/invoice/details?id={newId}`.
6. Send to client: `POST /api/invoice/sendtoclient` with `deliveryOptions` (email, subject, message).
7. Confirm status: `GET /api/invoice/status?id={newId}` -- should reflect "sent".

### 2. Estimation to Invoice Workflow

1. Create an estimation: `POST /api/estimation/new` with the `estimation` map.
2. Send to client for approval: `POST /api/estimation/sendtoclient` with `deliveryOptions`.
3. Check status periodically: `GET /api/estimation/status?id={id}` -- wait for client approval.
4. Convert to invoice: `POST /api/estimation/convert` with the estimation `id` (int32).
5. Retrieve the new invoice: `GET /api/invoice/all` to find the converted invoice.
6. Send the invoice: `POST /api/invoice/sendtoclient`.

### 3. Manage Product Catalog

1. List current products: `GET /api/product/all` with pagination.
2. Add a new product: `POST /api/product/new` with the `product` map.
3. Update pricing or details: `POST /api/product/update` -- expects 204 (no body) on success.
4. Remove discontinued product: `POST /api/product/delete` with the full `product` map.
5. Verify removal: `GET /api/product/all` and confirm the product is gone.

### 4. Order Fulfillment

1. List all orders: `GET /api/order/all` with pagination.
2. View order details: `GET /api/order/details?id={id}`.
3. Update shipping info: `POST /api/order/changeshippingdetails` with `orderId` and `shippingDetails` map -- expects 204.
4. Advance order status: `POST /api/order/changestatus` with the `status` map -- expects 204.
5. Generate payment link: `POST /api/paymentlink/new` if payment is still needed.
6. Share payment link: `GET /api/paymentlink/uri?id={linkId}` to get the shareable URL.

### 5. Safe Client Cleanup

1. List all clients: `GET /api/client/all`.
2. Check deletion safety: `GET /api/client/candelete?id={clientId}` -- if false, the client has linked invoices or orders.
3. Review linked records: `GET /api/client/details?id={clientId}` to understand dependencies.
4. Delete if safe: `POST /api/client/delete` with the `deleteModel` map.
5. Verify: `GET /api/client/all` to confirm removal.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
