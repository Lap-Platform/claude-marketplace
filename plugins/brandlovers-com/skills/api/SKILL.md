---
name: brandlovers-marketplace-api-v1
description: "BrandLovers Marketplace API V1 API skill. Use when working with BrandLovers Marketplace API V1 for products, product, orders. Covers 36 endpoints."
version: 1.0.0
generator: lapsh
---

# BrandLovers Marketplace API V1
API version: 1.0.0

## Auth
ApiKey authorization in header

## Base URL
https://api.brandlovers.com/marketplace/v1

## Setup
1. Set your API key in the appropriate header
2. GET /products -- verify access
3. POST /products -- create first products

## Endpoints

36 endpoints across 6 groups. See references/api-spec.lap for full details.

### products
| Method | Path | Description |
|--------|------|-------------|
| POST | /products | Allows new products from the seller to be loaded into the marketplace |
| GET | /products | Returns a list of products loaded into BrandLovers Marketplace |
| GET | /products/status | Returns seller products status in the marketplace |
| PUT | /products/status | Bulk enable/disable products in the marketplace |
| PUT | /products/prices | Allows bulk update of product prices. |
| PUT | /products/stocks | Bulk product stock update |
| GET | /products/status/selling | Returns products that are successfully listed for sale. |

### product
| Method | Path | Description |
|--------|------|-------------|
| GET | /product/{skuSellerId} | Returns details of a single product using the seller `skuSellerId` |
| PUT | /product/{skuSellerId} | Update product details |
| POST | /product | Create a new product to the marketplace |
| PUT | /product/{skuSellerId}/status | Enable/disable a single product in the Marketplace |
| PUT | /product/{skuSellerId}/stock | Update a single product stock |
| PUT | /product/{skuSellerId}/prices | Allows seller to update prices of a single SKU |

### orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /orders | Returns orders details |
| POST | /orders/shipments/delivered | Bulk update of order shipments |
| GET | /orders/shipments/delivered | Returns list of shipments |
| POST | /orders/shipments/shipped | Bulk update of order shipments |
| GET | /orders/shipments/shipped | Returns a list of shipments shipped |
| GET | /orders/status/approved | Return list of approved orders |
| GET | /orders/status/canceled | Returns lists of canceled orders |
| GET | /orders/status/delivered | Returns a list of orders successfully delivered associated with this seller. |
| GET | /orders/status/new | Returns a list of orders flagged as new. |
| GET | /orders/status/partiallyDelivered | Returns a list of partially deliverd orders |
| GET | /orders/status/partiallySent | Returns a list of orders partially fullfiled |
| GET | /orders/status/sent | Returns a list with orders fully sent |

### order
| Method | Path | Description |
|--------|------|-------------|
| GET | /order/{orderId} | Returns all details of a order |
| POST | /order/{orderId}/shipment/cancel | Confirm shipment canceletion (when requested by the customer) or failure to deliver |
| POST | /order/{orderId}/shipment/delivered | Confirms that a shipment was delivered |
| POST | /order/{orderId}/shipment/exchange | Confirm item exchange |
| POST | /order/{orderId}/shipment/return | Confirm order item return and refund |
| POST | /order/{orderId}/shipment/sent | Update new order to include shipment information |

### tickets
| Method | Path | Description |
|--------|------|-------------|
| GET | /tickets | Get customers trouble tickets |

### ticket
| Method | Path | Description |
|--------|------|-------------|
| POST | /ticket | Creates a new trouble ticket |
| GET | /ticket/{ticketId}/messages | Get trouble ticket messages |
| POST | /ticket/{ticketId}/message | Add new message to trouble ticket |
| PUT | /ticket/{ticketId}/status | Update trouble ticket status |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my products?" -> GET /products
- "How do I add a new product to the marketplace?" -> POST /product
- "How do I bulk upload multiple products at once?" -> POST /products
- "How do I check the status of my products?" -> GET /products/status
- "Which of my products are currently selling?" -> GET /products/status/selling
- "How do I update a specific product's details?" -> PUT /product/{skuSellerId}
- "How do I change the price of a single product?" -> PUT /product/{skuSellerId}/prices
- "How do I update stock for multiple products at once?" -> PUT /products/stocks
- "How do I bulk update prices across my catalog?" -> PUT /products/prices
- "How do I see all new orders waiting to be processed?" -> GET /orders/status/new
- "How do I mark an order as shipped?" -> POST /order/{orderId}/shipment/sent
- "How do I process a return for an order?" -> POST /order/{orderId}/shipment/return
- "How do I get the details of a specific order?" -> GET /order/{orderId}
- "How do I open a support ticket?" -> POST /ticket
- "How do I reply to an existing support ticket?" -> POST /ticket/{ticketId}/message

## Response Tips

- **Product listings** (`GET /products`, `/products/status`, `/products/status/selling`): Paginated via `offset`/`limit` params. Always check if result count equals `limit` to determine if more pages exist.
- **Order listings** (`GET /orders`, `/orders/status/*`, `/orders/shipments/*`): Same `offset`/`limit` pagination. Filter by status using the specific status endpoints rather than filtering client-side.
- **Single resource lookups** (`GET /product/{skuSellerId}`, `GET /order/{orderId}`): Return 404 when the resource does not exist. Distinguish from 403 (valid resource, no permission).
- **Bulk mutations** (`PUT /products/prices`, `/products/stocks`, `/products/status`): Accept arrays in the body. Check individual item results in the response for partial failures.
- **Shipment actions** (`POST /order/{orderId}/shipment/*`): Each action is a state transition. A 400 typically means the order is not in a valid state for that transition.
- **Tickets** (`GET /tickets`, `/ticket/{ticketId}/messages`): Support `status` filtering and `offset`/`limit` pagination. Message threads are per-ticket.

## Anomaly Flags

- **401 on any endpoint**: API key is missing, expired, or malformed. Surface immediately -- all subsequent calls will also fail.
- **403 on read endpoints**: The authenticated seller does not have permission to access this resource. May indicate a misconfigured account or attempting to access another seller's data.
- **404 on known SKU or order**: The resource may have been deleted or the ID format is wrong. Flag if a previously valid ID starts returning 404.
- **400 on bulk operations**: Likely partial validation failure. Surface which items in the batch were rejected so the user can fix and retry only the failures.
- **Repeated 400 on shipment state transitions**: The order is stuck in an unexpected state. Surface the current order status (via `GET /order/{orderId}`) so the user can understand why the transition is blocked.
- **Pagination returning zero results unexpectedly**: If `GET /orders/status/new` returns empty when orders are expected, flag a possible filter or date range issue.
- **Mixed partial delivery states**: If orders appear in both `partiallyDelivered` and `partiallySent`, surface these as needing attention -- they may require manual resolution.

## Playbook

### 1. Onboard a New Product Catalog

1. Prepare product data as an array of product objects.
2. Call `POST /products` with the full batch in `{products: [...]}`.
3. Check the response for any rejected items (400 errors per item).
4. Call `GET /products/status` to confirm all products are in the system.
5. Call `PUT /products/prices` to set initial pricing for all SKUs.
6. Call `PUT /products/stocks` to set initial inventory levels.
7. Call `PUT /products/status` to activate products for selling.
8. Verify with `GET /products/status/selling` that products are live.

### 2. Fulfill an Order End-to-End

1. Call `GET /orders/status/new` to retrieve unprocessed orders.
2. For each order, call `GET /order/{orderId}` to get full details (items, shipping address).
3. Prepare the shipment, then call `POST /order/{orderId}/shipment/sent` with tracking info.
4. Confirm the shipment appears via `GET /orders/shipments/shipped`.
5. Once delivery is confirmed, call `POST /order/{orderId}/shipment/delivered`.
6. Verify final state via `GET /orders/status/delivered`.

### 3. Handle a Return or Exchange

1. Call `GET /order/{orderId}` to review the order details and current status.
2. For a return: call `POST /order/{orderId}/shipment/return` with the return reason and items.
3. For an exchange: call `POST /order/{orderId}/shipment/exchange` with exchange details.
4. If the order must be canceled instead, call `POST /order/{orderId}/shipment/cancel`.
5. Monitor status via `GET /orders/status/canceled` or `GET /orders/status/delivered` as appropriate.

### 4. Monitor Order Pipeline Health

1. Call `GET /orders/status/new` to check the backlog of unprocessed orders.
2. Call `GET /orders/status/sent` and `GET /orders/shipments/shipped` to track in-transit orders.
3. Call `GET /orders/status/partiallySent` and `GET /orders/status/partiallyDelivered` to find orders needing attention.
4. Call `GET /orders/status/canceled` to review recent cancellations for patterns.
5. For any flagged orders, call `GET /order/{orderId}` for full details before taking action.

### 5. Manage Support Tickets

1. Call `GET /tickets` with `status` filter to see open tickets.
2. For each ticket needing attention, call `GET /ticket/{ticketId}/messages` to read the thread.
3. Reply with `POST /ticket/{ticketId}/message` including the response body.
4. When resolved, call `PUT /ticket/{ticketId}/status` to close the ticket.
5. To escalate or create a new issue, call `POST /ticket` with the details.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
