---
name: fulfillmentcom-apiv2
description: "Fulfillment.com APIv2 API skill. Use when working with Fulfillment.com APIv2 for users, returns, orders. Covers 15 endpoints."
version: 1.0.0
generator: lapsh
---

# Fulfillment.com APIv2
API version: 2.0

## Auth
OAuth2 | ApiKey x-api-key in header

## Base URL
https://api.fulfillment.com/v2

## Setup
1. Set your API key in the appropriate header
2. GET /users/me -- verify access
3. POST /orders -- create first orders

## Endpoints

15 endpoints across 7 groups. See references/api-spec.lap for full details.

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/me | About Me |

### returns
| Method | Path | Description |
|--------|------|-------------|
| GET | /returns | List Returns |
| PUT | /returns | Inform us of an RMA |

### orders
| Method | Path | Description |
|--------|------|-------------|
| PUT | /orders/{id}/status | Update Order Status |
| PUT | /orders/{id}/ship | Ship an Order |
| GET | /orders/{id} | Order Details |
| DELETE | /orders/{id} | Cancel an Order |
| GET | /orders | List of Orders |
| POST | /orders | New Order |
| GET | /orders/simple | List of Simplified Orders |

### oauth
| Method | Path | Description |
|--------|------|-------------|
| POST | /oauth/access_token | Generate an Access Token |

### inventory
| Method | Path | Description |
|--------|------|-------------|
| GET | /inventory | List of Item Inventories |
| GET | /inventory/full | List of Inventories |

### track
| Method | Path | Description |
|--------|------|-------------|
| GET | /track/{trackingNumber} | Tracking |

### accounting
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounting | List Order Accounting |

## Enhanced Skill Content
## Question Mapping

- "Who am I authenticated as?" -> GET /users/me
- "Show me all orders from last week" -> GET /orders
- "Get a simplified list of recent orders" -> GET /orders/simple
- "What's the status of order 12345?" -> GET /orders/{id}
- "Create a new fulfillment order" -> POST /orders
- "Cancel order 12345" -> DELETE /orders/{id}
- "Mark order 12345 as shipped with tracking" -> PUT /orders/{id}/ship
- "Put order 12345 on hold" -> PUT /orders/{id}/status
- "How much inventory do I have for SKU ABC?" -> GET /inventory
- "Get full inventory breakdown by warehouse" -> GET /inventory/full
- "Where is my shipment?" -> GET /track/{trackingNumber}
- "Show me returns from this month" -> GET /returns
- "Create an RMA return" -> PUT /returns
- "Pull accounting charges for Q1" -> GET /accounting
- "Get a new OAuth access token" -> POST /oauth/access_token

## Response Tips

- **Orders/Returns/Inventory/Accounting**: Paginated via `meta.pagination` -- check `totalPages` vs `currentPage` and loop with `page` param. Default limit is 80.
- **Single Order (GET /orders/{id})**: Use `hydrate` array to expand nested objects (e.g., status history, items) -- without it you get minimal references.
- **Order Creation (POST /orders)**: Returns full order object with `currentStatus` nested 3 levels deep (`status.stage`, `status.state`, `status.detail`). Parse `actionRequiredBy` to know who owns the next step.
- **Tracking (GET /track)**: `events` array is chronological. `status.code` gives machine-readable state; `status.description` is human-readable.
- **Returns (PUT /returns)**: May return 201 (created) or 202 (accepted for processing) -- handle both as success. 409 means duplicate RMA number.
- **Errors**: 404 across most endpoints means resource not found. POST /orders has richer error codes: 400 (bad payload), 409 (duplicate merchantOrderId), 422 (validation failure).

## Anomaly Flags

- **Rate limit on tracking**: GET /track returns 429 -- surface this immediately and suggest batching or backing off. No other endpoints document 429, so tracking is the bottleneck.
- **405 on order delete**: If DELETE /orders returns 405, the order is in a state that cannot be cancelled (likely already shipped). Surface the current status and suggest using PUT /orders/{id}/status instead.
- **Stale OAuth token**: Any 401 across endpoints should trigger a proactive suggestion to refresh via POST /oauth/access_token.
- **Order status actionRequiredBy**: When fetching orders, flag any where `currentStatus.status.actionRequiredBy` points to the merchant -- these need attention.
- **Pagination overflow**: If `currentPage` exceeds `totalPages` in any paginated response, flag it as a likely client bug (requesting beyond available data).
- **Missing tracking numbers**: On GET /orders or /orders/simple, flag orders where `trackingNumbers` is empty but `departDate` is set -- may indicate a fulfillment issue.

## Playbook

### 1. Place and Track a New Order

1. Call POST /orders with `merchantOrderId`, `shippingMethod`, `recipient` (address fields), and `items` (SKU, quantity, declaredValue).
2. Capture the returned `id` from the 201 response.
3. Poll GET /orders/{id} periodically (with `hydrate` for full status) until `currentStatus.status.stage.code` changes from intake to shipping.
4. Once `trackingNumbers` populates, call GET /track/{trackingNumber} to monitor delivery events.

### 2. Process a Return (RMA)

1. Call PUT /returns with `rmaNumber`, `recipient` (return-to address), and `items` (each with `sku` and `quantityExpected`).
2. If 201: return created. If 202: accepted but pending processing. If 409: RMA number already exists, use a different one.
3. Monitor returns with GET /returns using date range filters to check receiving progress.

### 3. Daily Inventory Audit

1. Call GET /inventory/full with desired `warehouseIds` to get per-warehouse stock levels.
2. Page through results using `page` param until `currentPage` equals `totalPages`.
3. Compare against your own catalog. Flag any SKUs with zero stock that have open orders (cross-reference with GET /orders filtered to active date range).

### 4. Bulk Order Export for Accounting

1. Call GET /accounting with `fromDate`, `toDate`, and `hydrate` set to include charge details.
2. Page through all results, collecting `data` arrays.
3. Optionally cross-reference with GET /orders/simple for the same date range to match `merchantOrderId` to accounting line items.
4. Filter by `warehouseIds` or `orderIds` if you only need a subset.

### 5. Cancel or Hold a Problematic Order

1. Call GET /orders/{id} to check current status. Inspect `currentStatus.status.isClosed` -- if true, the order cannot be modified.
2. To cancel: call DELETE /orders/{id}. If 405 is returned, the order has progressed too far.
3. To hold instead: call PUT /orders/{id}/status with `status.code` set to the hold code and a `reason` explaining why.
4. Verify the change by calling GET /orders/{id} again and confirming `currentStatus` reflects the update.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
