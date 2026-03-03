---
name: orders-v3
description: "Orders V3 API skill. Use when working with Orders V3 for orders. Covers 21 endpoints."
version: 1.0.0
generator: lapsh
---

# Orders V3

## Auth
ApiKey X-Auth-Token in header

## Base URL
https://api.bigcommerce.com/stores/{store_hash}/v3

## Setup
1. Set your API key in the appropriate header
2. GET /orders/payment_actions/refunds -- verify access
3. POST /orders/{order_id}/payment_actions/capture -- create first capture

## Endpoints

21 endpoints across 1 groups. See references/api-spec.lap for full details.

### orders
| Method | Path | Description |
|--------|------|-------------|
| POST | /orders/{order_id}/payment_actions/capture | Capture order payment |
| POST | /orders/{order_id}/payment_actions/void | Void |
| GET | /orders/{order_id}/transactions | Get Transactions |
| POST | /orders/{order_id}/payment_actions/refund_quotes | Create a Refund Quote |
| POST | /orders/{order_id}/payment_actions/refunds | Create a Refund |
| GET | /orders/{order_id}/payment_actions/refunds | Get Refunds for Order |
| GET | /orders/payment_actions/refunds/{refund_id} | Get a Refund |
| GET | /orders/payment_actions/refunds | Get All Refunds |
| GET | /orders/{order_id}/metafields | Get Order Metafields |
| POST | /orders/{order_id}/metafields | Create Metafields |
| GET | /orders/{order_id}/metafields/{metafield_id} | Get a Metafield |
| PUT | /orders/{order_id}/metafields/{metafield_id} | Update a Metafield |
| DELETE | /orders/{order_id}/metafields/{metafield_id} | Delete a Metafield |
| GET | /orders/settings | Get Global Order Settings |
| PUT | /orders/settings | Update Global Order Settings |
| GET | /orders/settings/channels/{channel_id} | Get Channel Order Settings |
| PUT | /orders/settings/channels/{channel_id} | Update Channel Order Settings |
| GET | /orders/metafields | Get All Order Metafields |
| POST | /orders/metafields | Create multiple Metafields |
| PUT | /orders/metafields | Update multiple Metafields |
| DELETE | /orders/metafields | Delete Multiple Metafields |

## Enhanced Skill Content
## Question Mapping

- "How do I capture payment for an order?" -> POST /orders/{order_id}/payment_actions/capture
- "How do I void a payment on an order?" -> POST /orders/{order_id}/payment_actions/void
- "What transactions exist for this order?" -> GET /orders/{order_id}/transactions
- "How much can I refund on this order?" -> POST /orders/{order_id}/payment_actions/refund_quotes
- "How do I issue a refund for an order?" -> POST /orders/{order_id}/payment_actions/refunds
- "What refunds have been made on this order?" -> GET /orders/{order_id}/payment_actions/refunds
- "Can I look up a specific refund by ID?" -> GET /orders/payment_actions/refunds/{refund_id}
- "Show me all refunds across orders within a date range" -> GET /orders/payment_actions/refunds
- "How do I add custom metadata to an order?" -> POST /orders/{order_id}/metafields
- "What metafields are set on this order?" -> GET /orders/{order_id}/metafields
- "How do I update or delete a metafield on an order?" -> PUT /orders/{order_id}/metafields/{metafield_id} or DELETE /orders/{order_id}/metafields/{metafield_id}
- "How do I change order notification email addresses?" -> PUT /orders/settings
- "What are the order notification settings for a specific channel?" -> GET /orders/settings/channels/{channel_id}
- "How do I bulk-create or bulk-update metafields across orders?" -> POST /orders/metafields or PUT /orders/metafields
- "How do I bulk-delete metafields?" -> DELETE /orders/metafields

## Response Tips

- **Payment actions** (capture, void, refunds): 201 on success; empty body for capture/void -- rely on status code, not response parsing.
- **Transactions**: Paginated via `meta.pagination`; 204 means no transactions exist (not an error), response body is a status object, not a data array.
- **Refund quotes**: `data.refund_methods` is a nested array of maps -- iterate the outer array for each payment method, inner maps for method details.
- **Refunds list** (all variants): `data` is always an array of maps; filter endpoints accept `order_id:in` and `id:in` as arrays for batch lookups.
- **Metafields** (per-order): Supports both offset pagination (`meta.pagination`) and cursor pagination (`meta.cursor_pagination`) -- prefer cursor for large sets using `before`/`after` params.
- **Bulk metafields**: Response includes `meta.total`, `meta.success`, `meta.failed` with partial-failure semantics -- always check `errors` array even on 200.
- **Settings**: Flat 200 response with no wrapping `data` key; 422 means validation failed on email addresses or notification structure.

## Anomaly Flags

- **502/503/504 on payment actions**: Payment gateway timeout -- surface immediately; the action may have been applied upstream even if the response failed. Advise checking transaction state before retrying.
- **422 on refund_quotes or refunds**: Refund exceeds available amount or order is in a non-refundable state -- surface the validation error details to the user.
- **204 on transactions**: No transactions recorded -- flag if the user expected payment activity; may indicate an incomplete or imported order.
- **409 on metafield creation**: Namespace/key combination already exists -- surface and suggest using PUT to update instead.
- **Partial failures in bulk metafield operations**: `meta.failed > 0` with a 200 status -- always surface `errors` array contents; a 200 does not mean full success.
- **Pagination totals shifting**: If `meta.pagination.total` changes between pages, surface that orders/refunds were created or deleted mid-pagination.
- **Missing `refund_methods` in quote**: Empty array in refund quote response means no refundable payment instruments -- flag before the user attempts a refund.

## Playbook

### 1. Full Refund Workflow

1. GET /orders/{order_id}/transactions to confirm a completed payment exists and note the transaction details.
2. POST /orders/{order_id}/payment_actions/refund_quotes with the items/amounts to refund -- review `total_refund_amount` and `refund_methods`.
3. POST /orders/{order_id}/payment_actions/refunds using the quote details to execute the refund.
4. GET /orders/{order_id}/payment_actions/refunds to verify the refund appears and matches the expected amount.

### 2. Capture and Settle an Authorized Order

1. GET /orders/{order_id}/transactions to confirm the order has an authorized (not yet captured) transaction.
2. POST /orders/{order_id}/payment_actions/capture with `Content-Type: application/json` to settle the payment.
3. GET /orders/{order_id}/transactions again to verify the transaction status changed to captured.
4. If capture returns 502/503/504, wait briefly, then check transactions before retrying -- the capture may have succeeded upstream.

### 3. Tag Orders with Custom Metafields

1. POST /orders/{order_id}/metafields with `namespace`, `key`, `value`, and `permission_set` to attach metadata (e.g., `namespace: "fulfillment"`, `key: "warehouse_id"`).
2. GET /orders/{order_id}/metafields with `namespace` filter to confirm the metafield was created.
3. To update later, PUT /orders/{order_id}/metafields/{metafield_id} with the new value.
4. To clean up, DELETE /orders/{order_id}/metafields/{metafield_id}.

### 4. Bulk Metafield Management Across Orders

1. GET /orders/metafields with `namespace` and optional date filters to audit existing metafields across all orders.
2. POST /orders/metafields with an array of metafield objects to create in batch.
3. Check the response `meta.failed` count and `errors` array -- handle any partial failures individually.
4. To update existing entries in bulk, PUT /orders/metafields with the metafield IDs and new values.
5. To remove in bulk, DELETE /orders/metafields with an array of metafield IDs; verify `meta.success` matches expected count.

### 5. Configure Order Notification Emails by Channel

1. GET /orders/settings to review the global default notification configuration.
2. GET /orders/settings/channels/{channel_id} to check channel-specific overrides.
3. PUT /orders/settings/channels/{channel_id} with updated `notifications.order_placed.email_addresses` and/or `notifications.forward_invoice.email_addresses`.
4. If 422 is returned, check that all email addresses are valid format -- the API validates strictly.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
