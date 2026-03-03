---
name: pos-api
description: "POS API skill. Use when working with POS for pos. Covers 46 endpoints."
version: 1.0.0
generator: lapsh
---

# POS API
API version: 10.24.0

## Auth
ApiKey Authorization in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /pos/orders -- verify access
3. POST /pos/orders -- create first orders

## Endpoints

46 endpoints across 1 groups. See references/api-spec.lap for full details.

### pos
| Method | Path | Description |
|--------|------|-------------|
| GET | /pos/orders | List Orders |
| POST | /pos/orders | Create Order |
| GET | /pos/orders/{id} | Get Order |
| PATCH | /pos/orders/{id} | Update Order |
| DELETE | /pos/orders/{id} | Delete Order |
| POST | /pos/orders/{id}/pay | Pay Order |
| GET | /pos/payments | List Payments |
| POST | /pos/payments | Create Payment |
| GET | /pos/payments/{id} | Get Payment |
| PATCH | /pos/payments/{id} | Update Payment |
| DELETE | /pos/payments/{id} | Delete Payment |
| GET | /pos/merchants | List Merchants |
| POST | /pos/merchants | Create Merchant |
| GET | /pos/merchants/{id} | Get Merchant |
| PATCH | /pos/merchants/{id} | Update Merchant |
| DELETE | /pos/merchants/{id} | Delete Merchant |
| GET | /pos/locations | List Locations |
| POST | /pos/locations | Create Location |
| GET | /pos/locations/{id} | Get Location |
| PATCH | /pos/locations/{id} | Update Location |
| DELETE | /pos/locations/{id} | Delete Location |
| GET | /pos/items | List Items |
| POST | /pos/items | Create Item |
| GET | /pos/items/{id} | Get Item |
| PATCH | /pos/items/{id} | Update Item |
| DELETE | /pos/items/{id} | Delete Item |
| GET | /pos/modifiers | List Modifiers |
| POST | /pos/modifiers | Create Modifier |
| GET | /pos/modifiers/{id} | Get Modifier |
| PATCH | /pos/modifiers/{id} | Update Modifier |
| DELETE | /pos/modifiers/{id} | Delete Modifier |
| GET | /pos/modifier-groups | List Modifier Groups |
| POST | /pos/modifier-groups | Create Modifier Group |
| GET | /pos/modifier-groups/{id} | Get Modifier Group |
| PATCH | /pos/modifier-groups/{id} | Update Modifier Group |
| DELETE | /pos/modifier-groups/{id} | Delete Modifier Group |
| GET | /pos/order-types | List Order Types |
| POST | /pos/order-types | Create Order Type |
| GET | /pos/order-types/{id} | Get Order Type |
| PATCH | /pos/order-types/{id} | Update Order Type |
| DELETE | /pos/order-types/{id} | Delete Order Type |
| GET | /pos/tenders | List Tenders |
| POST | /pos/tenders | Create Tender |
| GET | /pos/tenders/{id} | Get Tender |
| PATCH | /pos/tenders/{id} | Update Tender |
| DELETE | /pos/tenders/{id} | Delete Tender |

## Enhanced Skill Content
## Question Mapping

- "How do I list all orders?" -> GET /pos/orders
- "How do I create a new order for a specific location?" -> POST /pos/orders
- "How do I look up a specific order by ID?" -> GET /pos/orders/{id}
- "How do I mark an order as paid?" -> POST /pos/orders/{id}/pay
- "How do I void or cancel an order?" -> PATCH /pos/orders/{id} (set status to `voided`)
- "How do I delete an order?" -> DELETE /pos/orders/{id}
- "How do I record a payment against an order?" -> POST /pos/payments
- "How do I check payment details including card info?" -> GET /pos/payments/{id}
- "How do I add a new menu item with a price?" -> POST /pos/items
- "How do I set up modifier options like toppings or sizes?" -> POST /pos/modifiers (requires modifier_group_id from POST /pos/modifier-groups)
- "How do I list all store locations for a merchant?" -> GET /pos/locations
- "How do I configure which tender types accept tips?" -> POST /pos/tenders (set `allows_tipping`)
- "How do I paginate through a large list of items?" -> GET /pos/items (use `cursor` from `meta.cursors.next`)
- "How do I refund a payment?" -> PATCH /pos/payments/{id} (update `refunded` amount and `status`)
- "How do I hide a menu item without deleting it?" -> PATCH /pos/items/{id} (set `hidden: true`)

## Response Tips

- **List endpoints** (orders, payments, items, etc.): Data is in `data[]` array; paginate using `meta.cursors.next` as the `cursor` param on the next request; `links.next` is `null` when you've reached the last page.
- **Create endpoints** (POST): Return only `data.id` on 201; fetch the full record with a subsequent GET if you need the complete object.
- **Single-resource GET**: Full object is in `data`; nullable fields (marked `?`) may be absent -- always null-check `currency`, `custom_mappings`, timestamps, and address sub-fields.
- **Update/Delete endpoints**: Return only `data.id` on 200; a successful PATCH does not echo the updated fields back.
- **Errors**: All endpoints share error codes 400 (bad request), 401 (unauthorized), 402 (payment required -- check Apideck subscription), 404 (not found), 422 (unprocessable entity -- validation failure); inspect the response body for `message` and `detail` fields.

## Anomaly Flags

- **402 Payment Required**: Surface immediately -- indicates the Apideck connector or plan does not cover this operation; user action required.
- **Voided orders**: If `voided: true` or `status: "voided"` appears on a fetched order, warn the user before attempting modifications or payments.
- **Currency mismatch**: Flag when an order's `currency` differs from the merchant or location default currency -- may indicate a data entry error.
- **Empty cursors on large datasets**: If `meta.items_on_page` equals the `limit` but `meta.cursors.next` is null, the upstream POS connector may be truncating results silently.
- **Missing `x-apideck-consumer-id` or `x-apideck-app-id`**: These common headers are required on every call; surface auth errors early if either is absent from the request context.
- **Refund exceeds payment**: When `refunded` on a payment exceeds `amount`, flag as a potential accounting anomaly.
- **Stale version conflicts**: If a PATCH returns 422, check for `version` field conflicts -- the upstream POS may require optimistic concurrency control.

## Playbook

### 1. Place and Pay for a New Order

1. GET /pos/merchants to find your `merchant_id`
2. GET /pos/locations to find the target `location_id`
3. GET /pos/items to browse the menu and collect item IDs and prices
4. POST /pos/orders with `merchant_id`, `location_id`, and `line_items` array containing selected items, quantities, and unit prices
5. Note the returned order `id`
6. POST /pos/orders/{id}/pay with payment and tender details to mark the order as paid
7. GET /pos/orders/{id} to confirm `payment_status` is `paid`

### 2. Set Up a Menu with Modifiers

1. POST /pos/modifier-groups to create a group (e.g., "Size" with `selection_type: "single"`, `minimum_required: 1`, `maximum_allowed: 1`)
2. Note the returned modifier group `id`
3. POST /pos/modifiers for each option (e.g., "Small", "Medium", "Large") using the `modifier_group_id` and a `price_amount`
4. POST /pos/items with `name`, `price_amount`, `pricing_type: "fixed"`, and link the modifier group via `modifier_groups`
5. GET /pos/items/{id} to verify the item shows the linked modifiers

### 3. Process a Refund

1. GET /pos/orders/{id} to review the order, its `tenders`, and `payments`
2. GET /pos/payments/{id} to confirm the original payment amount and status
3. PATCH /pos/payments/{id} with updated `refunded` amount and `status: "refunded"` (or `"partially_refunded"`)
4. PATCH /pos/orders/{id} with `payment_status: "refunded"` and add an entry to the `refunds` array with `amount`, `reason`, and `status`
5. GET /pos/orders/{id} to verify `total_refund` and `payment_status` reflect the change

### 4. Onboard a New Location

1. GET /pos/merchants to identify (or POST /pos/merchants to create) the parent merchant
2. POST /pos/locations with `name`, `business_name`, `address`, `merchant_id`, `currency`, and `status: "active"`
3. POST /pos/order-types to define order types for this location (e.g., "Dine-in", "Takeout") if not already configured
4. POST /pos/tenders to configure accepted payment methods (e.g., cash with `opens_cash_drawer: true`, card with `allows_tipping: true`)
5. GET /pos/items and PATCH any items to remove the new location ID from `absent_at_location_ids` or set `present_at_all_locations: true`

### 5. Daily Sales Reconciliation

1. GET /pos/orders with `location_id` filter, paginating through all results using `cursor`
2. For each order, sum `total_amount`, `total_tax`, `total_tip`, `total_discount`, and `total_refund`
3. GET /pos/payments, paginating through all results, and cross-reference each payment's `order_id` against collected orders
4. Flag any orders where `payment_status` is not `paid` or `refunded`
5. Compare tender-level breakdowns (`tenders[].total_amount`) against payment records to identify discrepancies


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
