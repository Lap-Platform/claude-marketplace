---
name: ecwid
description: "ecwid API skill. Use when working with ecwid for bulk, customers, objects. Covers 42 endpoints."
version: 1.0.0
generator: lapsh
---

# ecwid
API version: api-v2

## Auth
ApiKey Authorization in header

## Base URL
https://api.cloud-elements.com/elements/api-v2

## Setup
1. Set your API key in the appropriate header
2. GET /bulk/jobs -- verify access
3. POST /bulk/download -- create first download

## Endpoints

42 endpoints across 7 groups. See references/api-spec.lap for full details.

### bulk
| Method | Path | Description |
|--------|------|-------------|
| POST | /bulk/download | Create a new bulk download job (asynchronous) |
| GET | /bulk/jobs | Fetch all the bulk jobs for an instance |
| POST | /bulk/query | Create an asynchronous bulk query job. |
| PUT | /bulk/{id}/cancel | Cancel an asynchronous bulk query job. |
| GET | /bulk/{id}/errors | Retrieve the errors of a bulk job. |
| GET | /bulk/{id}/status | Retrieve the status of a bulk job. |
| GET | /bulk/{id}/{objectName} | Retrieve the results of an asynchronous bulk query. |
| POST | /bulk/{objectName} | Upload a file of objects to be bulk uploaded to the provider. |

### customers
| Method | Path | Description |
|--------|------|-------------|
| POST | /customers | Create a new customer in eCommerce system.With the exception of the 'id' field, the required fields indicated in the 'Customer' model are those required to create a new customer |
| GET | /customers | Find customers in the eCommerce system, using the provided CEQL search expression. If no search expression is provided, all records will be retrieved |
| PATCH | /customers/{id} | Update an customer associated with a given ID in the eCommerce system.The update API uses the PATCH HTTP verb, so only those fields provided in the customer object will be updated, and those fields not provided will be left alone. Updating a customer with a specified ID that does not exist will result in an error response |
| GET | /customers/{id} | Retrieve a customer associated with a given ID from the eCommerce system. Specifying a customer with an ID that does not exist will result in an error response |
| DELETE | /customers/{id} | Delete a customer associated with a given ID from your eCommerce system. Specifying a customer associated with a given ID that does not exist will result in an error message |
| GET | /customers/{id}/orders | Find orders in the customer associated with a given ID. If the customer does not exist, an error response will be returned. If no orders are found in the given customer then an empty array will be returned |

### objects
| Method | Path | Description |
|--------|------|-------------|
| GET | /objects | Get a list of all the available objects. |
| GET | /objects/{objectName}/docs | Get swagger docs for an object. |
| GET | /objects/{objectName}/metadata | Get a list of all the fields for an object. |

### orders
| Method | Path | Description |
|--------|------|-------------|
| POST | /orders | Create an order in the eCommerce system.With the exception of the 'id' field, the required fields indicated in the 'Order' model are those required to create a new order.The paymentStatus can only be AWAITING_PAYMENT or INCOMPLETE.The fulfillmentStatus can only be AWAITING_PROCESSING |
| GET | /orders | Find orders in the eCommerce system, using the provided CEQL search expression. If no search expression is provided, all records will be retrieved |
| PATCH | /orders/{id} | Update an order associated with a given ID in the eCommerce system. The update API uses the PATCH HTTP verb, so only those fields provided in the order object will be updated, and those fields not provided will be left alone. Updating an order with a specified ID that does not exist will result in an error response</strong> |
| GET | /orders/{id} | Retrieve an order associated with a given ID from the eCommerce system. Specifying an order with an ID that does not exist will result in an error response |
| DELETE | /orders/{id} | Delete an order associated with a given ID from your eCommerce system. Specifying an order associated with a given ID that does not exist will result in an error message |
| GET | /orders/{orderId}/payments | Retrieve the payments in the eCommerce system for the specified order |
| GET | /orders/{orderId}/refunds | Retrieve the refunds in the eCommerce system for the specified order |

### ping
| Method | Path | Description |
|--------|------|-------------|
| GET | /ping | Ping the element to confirm that the hub element has a heartbeat.  If the element does not have a heartbeat, an error message will be returned. |

### products
| Method | Path | Description |
|--------|------|-------------|
| POST | /products | Create a new product in eCommerce system.With the exception of the 'id' field, the required fields indicated in the 'Product' model are those required to create a new product |
| GET | /products | Find products in the eCommerce system, using the provided CEQL search expression. The search expression in CEQL is the WHERE clause in a typical SQL query, but without the WHERE keyword.  If no search expression is provided, all records will be retrieved |
| PATCH | /products/{id} | Update a product associated with a given ID in the eCommerce system. The update API uses the PATCH HTTP verb, so only those fields provided in the product object will be updated, and those fields not provided will be left alone. Updating a product with a specified ID that does not exist will result in an error response. <p><strong>Update supports the following fields: sku, quantity, trackQuantity, quantityDelta, warningLimit, name, price, weight, tangible, enabled, fixedShippingRateOnly, fixedShippingRate, description, wholesalePrices, compareAtPrice, productClassId</strong> |
| GET | /products/{id} | Retrieve a product associated with a given ID from the eCommerce system. Specifying a product with an ID that does not exist will result in an error response |
| DELETE | /products/{id} | Delete a product associated with a given ID from your eCommerce system. Specifying a product associated with a given ID that does not exist will result in an error message |

### {objectName}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{objectName} | Search for {objectName} |
| POST | /{objectName} | Create an {objectName} |
| DELETE | /{objectName}/{objectId} | Delete an {objectName} |
| GET | /{objectName}/{objectId} | Retrieve an {objectName} |
| PATCH | /{objectName}/{objectId} | Update an {objectName} |
| PUT | /{objectName}/{objectId} | Update an {objectName} |
| GET | /{objectName}/{objectId}/{childObjectName} | Search for {childObjectName} |
| POST | /{objectName}/{objectId}/{childObjectName} | Create an {objectName} |
| DELETE | /{objectName}/{objectId}/{childObjectName}/{childObjectId} | Delete an {childObjectName} |
| GET | /{objectName}/{objectId}/{childObjectName}/{childObjectId} | Retrieve an {childObjectName} |
| PATCH | /{objectName}/{objectId}/{childObjectName}/{childObjectId} | Update an {childObjectName} |
| PUT | /{objectName}/{objectId}/{childObjectName}/{childObjectId} | Update an {childObjectName} |

## Enhanced Skill Content
## Question Mapping

- "How do I check if the Ecwid API connection is working?" -> GET /ping
- "How do I list all customers?" -> GET /customers
- "How do I look up a specific customer by ID?" -> GET /customers/{id}
- "How do I create a new customer?" -> POST /customers
- "How do I update customer details?" -> PATCH /customers/{id}
- "How do I see all orders for a specific customer?" -> GET /customers/{id}/orders
- "How do I list all orders with filtering?" -> GET /orders
- "How do I check payment details for an order?" -> GET /orders/{orderId}/payments
- "How do I check refunds on an order?" -> GET /orders/{orderId}/refunds
- "How do I add a new product to the catalog?" -> POST /products
- "How do I search products with a filter?" -> GET /products
- "How do I start a bulk export of data?" -> POST /bulk/query
- "How do I check the status of a bulk job?" -> GET /bulk/{id}/status
- "How do I cancel a running bulk job?" -> PUT /bulk/{id}/cancel
- "What object types are available in this Ecwid instance?" -> GET /objects

## Response Tips

- **Customers, Orders, Products (list endpoints):** Paginated via `nextPage` and `pageSize` params. Iterate until `nextPage` is absent or the result set is smaller than `pageSize`.
- **Bulk jobs:** Status responses indicate job state -- poll `GET /bulk/{id}/status` until terminal. Errors are fetched separately via `GET /bulk/{id}/errors`.
- **Generic `/{objectName}` endpoints:** Response shape varies by object type. Use `GET /objects/{objectName}/metadata` to discover the schema before parsing.
- **All write operations (POST, PATCH, PUT):** Return the created/updated resource on 200. A 409 indicates a conflict (duplicate or concurrent edit).
- **Error responses (4xx/5xx):** All endpoints share the same error code set. The body typically contains a `message` field with details. 502 signals an upstream Ecwid failure, not a Cloud Elements issue.

## Anomaly Flags

- **401 on any call:** API key is invalid, expired, or the element instance is disconnected. Surface immediately -- all subsequent calls will also fail.
- **502 errors:** Upstream Ecwid is unreachable. Flag as a provider outage rather than a configuration problem.
- **Bulk job errors accumulating:** If `GET /bulk/{id}/errors` returns a non-empty result, surface the count and first few error messages proactively.
- **409 Conflict on writes:** Likely a duplicate record or concurrent modification. Flag the conflicting field if present in the response body.
- **Pagination loops:** If `nextPage` token repeats or total results don't decrease, flag a potential infinite pagination loop.
- **Empty object metadata:** If `GET /objects/{objectName}/metadata` returns no fields, the object type may not be supported by this Ecwid instance.
- **Slow bulk jobs:** If polling `GET /bulk/{id}/status` shows no progress over multiple checks, alert the user that the job may be stalled.

## Playbook

### 1. Export All Customers in Bulk

1. Call `POST /bulk/query` with `q` targeting the customers object.
2. Note the returned bulk job `id`.
3. Poll `GET /bulk/{id}/status` every 10-30 seconds until the job completes.
4. If errors exist, retrieve them with `GET /bulk/{id}/errors`.
5. Download results via `GET /bulk/{id}/{objectName}` using `objectName=customers`.

### 2. Fulfill an Order and Track Payment

1. Retrieve the order with `GET /orders/{id}`.
2. Update the order status with `PATCH /orders/{id}`, passing the `action` param (e.g., `action=fulfill`) and updated order body.
3. Verify payment was captured via `GET /orders/{orderId}/payments`.
4. If a refund is needed later, monitor with `GET /orders/{orderId}/refunds`.

### 3. Sync Product Catalog

1. List all products with `GET /products`, paginating with `nextPage` and `pageSize`.
2. For each product in your local catalog not found in results, create it with `POST /products`.
3. For existing products with changes, update with `PATCH /products/{id}`.
4. For products to remove, delete with `DELETE /products/{id}`.

### 4. Discover and Query Custom Objects

1. List available object types with `GET /objects`.
2. Inspect a specific object's schema via `GET /objects/{objectName}/metadata`.
3. Query records using the generic `GET /{objectName}` with `where` filters.
4. Create or update records via `POST /{objectName}` or `PATCH /{objectName}/{objectId}`.
5. Access child objects with `GET /{objectName}/{objectId}/{childObjectName}`.

### 5. Customer Order History Lookup

1. Search for the customer with `GET /customers` using a `where` filter (e.g., email match).
2. Retrieve the customer record with `GET /customers/{id}`.
3. Fetch their order history with `GET /customers/{id}/orders`, paginating as needed.
4. For each order of interest, get full details via `GET /orders/{id}`.
5. Check payment and refund status with the respective sub-endpoints.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
