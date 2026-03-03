---
name: ecommerce-api
description: "Ecommerce API skill. Use when working with Ecommerce for ecommerce. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# Ecommerce API
API version: 10.24.0

## Auth
ApiKey Authorization in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /ecommerce/orders -- verify access

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### ecommerce
| Method | Path | Description |
|--------|------|-------------|
| GET | /ecommerce/orders | List Orders |
| GET | /ecommerce/orders/{id} | Get Order |
| GET | /ecommerce/products | List Products |
| GET | /ecommerce/products/{id} | Get Product |
| GET | /ecommerce/customers | List Customers |
| GET | /ecommerce/customers/{id} | Get Customer |
| GET | /ecommerce/store | Get Store |

## Enhanced Skill Content
## Question Mapping

- "List all orders" -> GET /ecommerce/orders
- "Show me order details for a specific order" -> GET /ecommerce/orders/{id}
- "What is the payment status of order X?" -> GET /ecommerce/orders/{id}
- "List all products in the catalog" -> GET /ecommerce/products
- "Get product details including variants and inventory" -> GET /ecommerce/products/{id}
- "Is product X in stock?" -> GET /ecommerce/products/{id}
- "List all customers" -> GET /ecommerce/customers
- "Look up a customer by ID" -> GET /ecommerce/customers/{id}
- "What orders has customer X placed?" -> GET /ecommerce/customers/{id}
- "Get store info and URLs" -> GET /ecommerce/store
- "Show me the next page of orders" -> GET /ecommerce/orders (with cursor param)
- "Find orders with a specific fulfillment status" -> GET /ecommerce/orders (with filter param)
- "How much was refunded on order X?" -> GET /ecommerce/orders/{id}
- "What tracking info exists for an order?" -> GET /ecommerce/orders/{id}
- "List products filtered by status" -> GET /ecommerce/products (with filter param)

## Response Tips

- **All endpoints**: Responses wrap data in a standard envelope with `status_code`, `status`, `service`, `resource`, and `operation` -- always check `status` before reading `data`.
- **List endpoints** (orders, products, customers): Paginated via cursor-based navigation; read `meta.cursors.next` and pass it as `cursor` for the next page; `meta.items_on_page` tells you how many items were returned vs the `limit`.
- **Detail endpoints** (orders/{id}, products/{id}, customers/{id}): Return `data` as a single object, not an array; monetary values (`sub_total`, `total_amount`, `price`) are strings, not numbers -- parse them before doing arithmetic.
- **Orders**: `line_items`, `refunds`, `discounts`, and `tracking` are nested arrays inside `data`; `customer`, `billing_address`, and `shipping_address` are nested maps.
- **Products**: `variants` and `options` are arrays of maps; `categories` and `tags` provide classification; `images` may be null.
- **Customers**: `orders` is embedded as an array in the detail response, providing a quick way to see purchase history without a separate call.
- **Errors**: All endpoints share the same error codes (400, 401, 402, 404, 422) -- 402 indicates a payment/plan issue with the Apideck connector, not the ecommerce order.

## Anomaly Flags

- **402 Payment Required**: Surface immediately -- indicates the Apideck subscription or connector plan needs attention, not an ecommerce payment issue.
- **Empty cursor on paginated results**: If `meta.cursors.next` is null but `items_on_page` equals `limit`, data may have been truncated; warn the user.
- **Null monetary fields**: If `total_amount`, `sub_total`, or `price` return null on records that should have values, flag as potential data sync issue with the upstream provider.
- **Stale timestamps**: If `updated_at` is significantly older than expected on frequently changing resources (orders, inventory), the connector may not be syncing properly.
- **Missing `x-apideck-service-id`**: When omitted, Apideck auto-selects a service -- surface which service was used (from the `service` field in the response) so the user knows which integration handled the request.
- **Refunded amount exceeding total**: If `refunded_amount` > `total_amount` on an order, flag as a data anomaly for review.
- **422 Unprocessable Entity**: Usually means filter or sort parameters are malformed -- surface the specific field validation error to help the user correct their query.

## Playbook

### 1. Audit all orders with their line items

1. Call GET /ecommerce/orders with desired `limit` (max 20 per page)
2. For each order in `data`, note the `id` and summary fields (`total_amount`, `status`)
3. Call GET /ecommerce/orders/{id} for each order to retrieve full `line_items`, `discounts`, and `refunds`
4. If `meta.cursors.next` is not null, repeat step 1 with `cursor` set to that value
5. Aggregate results across all pages

### 2. Check inventory across the product catalog

1. Call GET /ecommerce/products to list all products
2. For each product, call GET /ecommerce/products/{id} to get `inventory_quantity` and `variants`
3. Flag any product where `inventory_quantity` is "0" or null
4. Paginate through all products using `meta.cursors.next` until null
5. Present a summary of low/out-of-stock items

### 3. Build a customer order history report

1. Call GET /ecommerce/customers to retrieve all customers
2. For each customer, call GET /ecommerce/customers/{id} to access the embedded `orders` array
3. For orders needing full detail (line items, shipping, refunds), call GET /ecommerce/orders/{id}
4. Compile per-customer totals by summing `total_amount` across their orders
5. Paginate customers using `cursor` until all are processed

### 4. Verify store configuration

1. Call GET /ecommerce/store to retrieve store metadata
2. Confirm `store_url` and `admin_url` are valid and accessible
3. Note the `service` field in the response to confirm which ecommerce platform is connected
4. Check `created_at` and `updated_at` to verify the integration is active and recently synced

### 5. Investigate a specific order issue

1. Call GET /ecommerce/orders/{id} with the order ID in question
2. Check `payment_status` and `fulfillment_status` for the current state
3. Review `tracking` array for shipment updates
4. Review `refunds` array for any partial or full refunds, comparing `refunded_amount` to `total_amount`
5. Cross-reference the `customer.id` by calling GET /ecommerce/customers/{id} for contact details and broader order history


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
