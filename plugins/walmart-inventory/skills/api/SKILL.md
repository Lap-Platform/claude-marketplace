---
name: inventory-management
description: "Inventory Management API skill. Use when working with Inventory Management for inventory, inventories, feeds. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# Inventory Management

## Auth
ApiKey WM_SEC.ACCESS_TOKEN in header

## Base URL
https://marketplace.walmartapis.com

## Setup
1. Set your API key in the appropriate header
2. GET /v3/inventory -- verify access
3. POST /v3/feeds -- create first feeds

## Endpoints

7 endpoints across 4 groups. See references/api-spec.lap for full details.

### inventory
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/inventory | Inventory |
| PUT | /v3/inventory | Update inventory |

### inventories
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/inventories/{sku} | Single Item Inventory by Ship Node |
| PUT | /v3/inventories/{sku} | Update Item Inventory per Ship Node |
| GET | /v3/inventories | Multiple Item Inventory for All Ship Nodes |

### feeds
| Method | Path | Description |
|--------|------|-------------|
| POST | /v3/feeds | Bulk Item Inventory Update |

### fulfillment
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/fulfillment/inventory | WFS Inventory |

## Enhanced Skill Content
## Question Mapping

- "What's the current inventory for this SKU?" -> GET /v3/inventory
- "How do I update the stock quantity for a product?" -> PUT /v3/inventory
- "What's the inventory at a specific ship node?" -> GET /v3/inventory (with shipNode param)
- "Show me inventory across all fulfillment nodes for a SKU" -> GET /v3/inventories/{sku}
- "How do I set inventory quantities at multiple ship nodes at once?" -> PUT /v3/inventories/{sku}
- "How do I bulk update inventory for many SKUs?" -> POST /v3/feeds (feedType=inventory)
- "List all my inventory across the catalog" -> GET /v3/inventories
- "Get the next page of inventory results" -> GET /v3/inventories (with nextCursor)
- "What inventory changed since yesterday?" -> GET /v3/fulfillment/inventory (with fromModifiedDate/toModifiedDate)
- "Show me fulfillment center inventory for a SKU" -> GET /v3/fulfillment/inventory (with sku)
- "Filter fulfillment inventory by node type" -> GET /v3/fulfillment/inventory (with shipNodeType)
- "How many total items are in my inventory?" -> GET /v3/inventories (read meta.totalCount)
- "Did my inventory feed upload succeed?" -> POST /v3/feeds (check feedId vs errors in response)
- "How do I zero out stock for a product at a specific warehouse?" -> PUT /v3/inventories/{sku} (set inputQty amount to 0 for that shipNode)

## Response Tips

- **inventory (single SKU):** Response returns flat `quantity` map with `unit` (e.g., "EACH") and `amount` -- no nesting beyond that.
- **inventories (multi-node):** Response `nodes` is an array of maps; each node contains its own ship node ID and quantity -- iterate to find a specific location.
- **inventories (list all):** Cursor-based pagination -- use `meta.nextCursor` for the next page; stop when nextCursor is absent or empty. Default limit is 10.
- **fulfillment:** Offset-based pagination -- use `headers.totalCount`, `limit`, and `offset` to calculate pages. Default limit 10, offset 0.
- **feeds:** A successful POST returns `feedId` for tracking; if `errors` is present in the response, the submission had issues even with a 200 status.

## Anomaly Flags

- **Feed errors on 200:** `POST /v3/feeds` can return 200 with an `errors` map -- always check for its presence and surface it, since the HTTP status alone is misleading.
- **Zero quantity results:** Flag when `GET /v3/inventory` returns `amount: 0` as this may indicate an out-of-stock condition the user should act on.
- **Missing nextCursor mid-pagination:** If `meta.totalCount` suggests more results but `nextCursor` is absent, flag the inconsistency.
- **Ship node mismatches:** When updating via `PUT /v3/inventories/{sku}`, flag if the response `nodes` array does not include all ship nodes that were sent in the request.
- **Authentication headers:** All requests require `WM_SEC.ACCESS_TOKEN`, `WM_QOS.CORRELATION_ID`, `WM_SVC.NAME`, and `WM_CONSUMER.CHANNEL.TYPE` -- flag immediately if any are missing before making a call.

## Playbook

### 1. Check and Update Stock for a Single SKU

1. Call `GET /v3/inventory?sku={sku}` to retrieve current quantity.
2. Note the returned `quantity.amount` and `quantity.unit`.
3. Call `PUT /v3/inventory` with the SKU and new `quantity: {unit: "EACH", amount: <new_amount>}`.
4. Verify the response reflects the updated amount.

### 2. Manage Multi-Node Inventory

1. Call `GET /v3/inventories/{sku}` to see inventory across all ship nodes.
2. Identify the target nodes and their current quantities from the `nodes` array.
3. Call `PUT /v3/inventories/{sku}` with an `inventories.nodes` array containing each `shipNode` and its `inputQty`.
4. Confirm the response `nodes` array reflects the changes at each location.

### 3. Bulk Inventory Update via Feed

1. Prepare an inventory feed file with all SKUs and quantities to update.
2. Call `POST /v3/feeds?feedType=inventory` with the feed payload (optionally scope to a `shipNode`).
3. Capture the `feedId` from the response.
4. Check the response for an `errors` map -- if present, review and correct the feed data.

### 4. Audit Inventory Changes Over a Date Range

1. Call `GET /v3/fulfillment/inventory?fromModifiedDate={start}&toModifiedDate={end}&limit=50` to fetch the first page.
2. Read `headers.totalCount` to understand the full result set size.
3. If `totalCount` exceeds `limit`, increment `offset` by `limit` and repeat the call.
4. Aggregate results from `payload.inventory` across all pages for the complete change log.

### 5. Full Catalog Inventory Scan

1. Call `GET /v3/inventories?limit=50` to fetch the first page.
2. Read `meta.totalCount` for the full catalog size.
3. Use the returned `meta.nextCursor` value in subsequent calls: `GET /v3/inventories?limit=50&nextCursor={cursor}`.
4. Continue until `nextCursor` is absent or empty in the response.
5. Collect all entries from `elements.inventories` across pages.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
