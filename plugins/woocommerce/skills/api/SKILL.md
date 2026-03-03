---
name: woocommerce-rest-api
description: "WooCommerce REST API skill. Use when working with WooCommerce REST for customers, products, orders. Covers 122 endpoints."
version: 1.0.0
generator: lapsh
---

# WooCommerce REST API
API version: v3

## Auth
Bearer basic

## Base URL
https://example-woocommerce-shop.com/wp-json/wc/v3

## Setup
1. Set Authorization header with your Bearer token
2. GET /customers -- verify access
3. POST /customers -- create first customers

## Endpoints

122 endpoints across 11 groups. See references/api-spec.lap for full details.

### customers
| Method | Path | Description |
|--------|------|-------------|
| POST | /customers | This API helps you to create a new customer. |
| GET | /customers | This API helps you to view all the customers. |
| GET | /customers/{customerId} | This API lets you retrieve and view a specific customer by ID. |
| PUT | /customers/{customerId} | This API lets you make changes to a customer. |
| DELETE | /customers/{customerId} | This API helps you delete a customer. |
| POST | /customers/batch | Batch create, update, and delete customers |

### products
| Method | Path | Description |
|--------|------|-------------|
| POST | /products | This API helps you to create a new product. |
| GET | /products | This API helps you to view all the products. |
| GET | /products/{productId} | This API lets you retrieve and view a specific product by ID. |
| PUT | /products/{productId} | This API lets you make changes to a product. |
| DELETE | /products/{productId} | This API helps you delete a product. |
| POST | /products/{productId}/duplicate | This API helps you to duplicate a product. |
| POST | /products/batch | Batch create, update, and delete products |
| POST | /products/{productId}/variations | This API helps you to create a new product variation. |
| GET | /products/{productId}/variations | This API helps you to view all the product variations. |
| GET | /products/{productId}/variations/{variationId} | This API lets you retrieve and view a specific product variation by ID. |
| PUT | /products/{productId}/variations/{variationId} | This API lets you make changes to a product variation. |
| DELETE | /products/{productId}/variations/{variationId} | This API helps you delete a product variation. |
| POST | /products/{productId}/variations/batch | Batch create, update, and delete product variations |
| GET | /products/attributes | List all product attributes |
| POST | /products/attributes | Create a product attribute |
| GET | /products/attributes/{attributeId} | Retrieve a product attribute |
| PUT | /products/attributes/{attributeId} | Update a product attribute |
| DELETE | /products/attributes/{attributeId} | Delete a product attribute |
| POST | /products/attributes/batch | Batch update product attributes |
| GET | /products/attributes/{attributeId}/terms | List all terms for a product attribute |
| POST | /products/attributes/{attributeId}/terms | Create an attribute term |
| GET | /products/attributes/{attributeId}/terms/{termId} | Retrieve an attribute term |
| PUT | /products/attributes/{attributeId}/terms/{termId} | Update an attribute term |
| DELETE | /products/attributes/{attributeId}/terms/{termId} | Delete an attribute term |
| POST | /products/attributes/{attributeId}/terms/batch | Batch update attribute terms |
| POST | /products/categories | This API helps you to create a new product category. |
| GET | /products/categories | This API lets you retrieve all product categories. |
| GET | /products/categories/{categoryId} | This API lets you retrieve a product category by ID. |
| PUT | /products/categories/{categoryId} | This API lets you make changes to a product category. |
| DELETE | /products/categories/{categoryId} | This API helps you delete a product category. |
| POST | /products/categories/batch | Batch create, update, and delete product categories |
| GET | /products/shipping-classes | List all shipping classes |
| POST | /products/shipping-classes | Create a shipping class |
| GET | /products/shipping-classes/{classId} | Retrieve a shipping class |
| PUT | /products/shipping-classes/{classId} | Update a shipping class |
| DELETE | /products/shipping-classes/{classId} | Delete a shipping class |
| POST | /products/shipping-classes/batch | Batch update shipping classes |
| POST | /products/tags | This API helps you to create a new product tag. |
| GET | /products/tags | This API lets you retrieve all product tags. |
| GET | /products/tags/{tagId} | This API lets you retrieve a product tag by ID. |
| PUT | /products/tags/{tagId} | This API lets you make changes to a product tag. |
| DELETE | /products/tags/{tagId} | This API helps you delete a product tag. |
| POST | /products/tags/batch | Batch create, update, and delete product tags |
| GET | /products/reviews | List all product reviews |
| POST | /products/reviews | Create a product review |
| GET | /products/reviews/{reviewId} | Retrieve a product review |
| PUT | /products/reviews/{reviewId} | Update a product review |
| DELETE | /products/reviews/{reviewId} | Delete a product review |
| POST | /products/reviews/batch | Batch update product reviews |

### orders
| Method | Path | Description |
|--------|------|-------------|
| POST | /orders | This API helps you to create a new order. |
| GET | /orders | This API helps you to view all the orders. |
| GET | /orders/{orderId} | This API lets you retrieve and view a specific order. |
| PUT | /orders/{orderId} | This API lets you make changes to an order. |
| DELETE | /orders/{orderId} | This API helps you delete an order. |
| POST | /orders/batch | Batch create, update, and delete orders |
| GET | /orders/{orderId}/notes | This API helps you to view all notes for an order. |
| POST | /orders/{orderId}/notes | This API helps you to create a new order note. |
| GET | /orders/{orderId}/notes/{noteId} | This API lets you retrieve and view a specific order note by ID. |
| DELETE | /orders/{orderId}/notes/{noteId} | This API helps you delete an order note. |
| GET | /orders/{orderId}/refunds | This API helps you to view all refunds for an order. |
| POST | /orders/{orderId}/refunds | This API helps you to create a new order refund. |
| GET | /orders/{orderId}/refunds/{refundId} | This API lets you retrieve and view a specific order refund by ID. |
| DELETE | /orders/{orderId}/refunds/{refundId} | This API helps you delete an order refund. |

### reports
| Method | Path | Description |
|--------|------|-------------|
| GET | /reports | List all reports |
| GET | /reports/top_sellers | Retrieve top sellers report |
| GET | /reports/coupons/totals | Retrieve coupons totals report |
| GET | /reports/customers/totals | Retrieve customers totals report |
| GET | /reports/orders/totals | This API lets you retrieve and view orders totals report. |
| GET | /reports/products/totals | Retrieve products totals report |
| GET | /reports/reviews/totals | Retrieve reviews totals report |
| GET | /reports/sales | This API lets you retrieve and view a sales report. |

### coupons
| Method | Path | Description |
|--------|------|-------------|
| GET | /coupons | This API helps you to view all coupons. |
| POST | /coupons | This API helps you to create a new coupon. |
| GET | /coupons/{couponId} | This API lets you retrieve and view a specific coupon by ID. |
| PUT | /coupons/{couponId} | This API helps you to update a coupon. |
| DELETE | /coupons/{couponId} | This API helps you delete a coupon. |
| POST | /coupons/batch | Batch create, update, and delete coupons |

### settings
| Method | Path | Description |
|--------|------|-------------|
| GET | /settings | This API helps you to view all settings groups. |
| GET | /settings/{groupId} | This API helps you to view a specific settings group. |
| GET | /settings/{groupId}/{id} | This API helps you to view a specific setting. |
| PUT | /settings/{groupId}/{id} | This API helps you to update a specific setting. |

### shipping
| Method | Path | Description |
|--------|------|-------------|
| GET | /shipping/zones | This API helps you to view all shipping zones. |
| POST | /shipping/zones | This API helps you to create a new shipping zone. |
| GET | /shipping/zones/{id} | This API lets you retrieve and view a specific shipping zone by ID. |
| PUT | /shipping/zones/{id} | This API helps you to update a shipping zone. |
| DELETE | /shipping/zones/{id} | This API helps you delete a shipping zone. |
| GET | /shipping/zones/{id}/locations | This API helps you to view all locations for a shipping zone. |
| PUT | /shipping/zones/{id}/locations | This API helps you to update locations for a shipping zone. |
| GET | /shipping/zones/{id}/methods | This API helps you to view all shipping methods for a shipping zone. |
| POST | /shipping/zones/{id}/methods | This API helps you to create a new shipping method for a shipping zone. |
| GET | /shipping/zones/{id}/methods/{instanceId} | This API lets you retrieve and view a specific shipping zone method by instance ID. |
| PUT | /shipping/zones/{id}/methods/{instanceId} | This API helps you to update a shipping zone method. |
| DELETE | /shipping/zones/{id}/methods/{instanceId} | This API helps you delete a shipping zone method. |

### payment_gateways
| Method | Path | Description |
|--------|------|-------------|
| GET | /payment_gateways | This API helps you to view all payment gateways. |
| GET | /payment_gateways/{id} | This API lets you retrieve and view a specific payment gateway by ID. |
| PUT | /payment_gateways/{id} | This API helps you to update a payment gateway. |

### taxes
| Method | Path | Description |
|--------|------|-------------|
| GET | /taxes | This API helps you to view all taxes. |
| POST | /taxes | This API helps you to create a new tax. |
| GET | /taxes/{id} | This API lets you retrieve and view a specific tax by ID. |
| PUT | /taxes/{id} | This API helps you to update a tax. |
| DELETE | /taxes/{id} | This API helps you delete a tax. |
| POST | /taxes/batch | Batch create, update, and delete taxes |
| GET | /taxes/classes | This API helps you to view all tax classes. |
| POST | /taxes/classes | This API helps you to create a new tax class. |
| GET | /taxes/classes/{slug} | This API lets you retrieve and view a specific tax class by slug. |
| DELETE | /taxes/classes/{slug} | This API helps you delete a tax class. |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /webhooks | This API helps you to view all webhooks. |
| POST | /webhooks | This API helps you to create a new webhook. |
| GET | /webhooks/{id} | This API lets you retrieve and view a specific webhook by ID. |
| PUT | /webhooks/{id} | This API helps you to update a webhook. |
| DELETE | /webhooks/{id} | This API helps you delete a webhook. |
| POST | /webhooks/batch | Batch create, update, and delete webhooks |

### system_status
| Method | Path | Description |
|--------|------|-------------|
| GET | /system_status | This API helps you to view the system status. |
| GET | /system_status/tools | This API helps you to view all system status tools. |
| GET | /system_status/tools/{id} | This API lets you retrieve and view a specific system status tool by ID. |
| PUT | /system_status/tools/{id} | This API helps you to run a system status tool. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new customer account?" -> POST /customers
- "Show me all orders from the last month" -> GET /orders (with `after` and `before` params)
- "What products are currently on sale?" -> GET /products (with `on_sale=true`)
- "How do I issue a refund for an order?" -> POST /orders/{orderId}/refunds
- "What are my top selling products?" -> GET /reports/top_sellers
- "How do I apply a coupon code to restrict by email?" -> POST /coupons (with `email_restrictions`)
- "How do I update a product's stock quantity?" -> PUT /products/{productId} (set `manage_stock` and `stock_quantity`)
- "How do I add a note to a customer's order?" -> POST /orders/{orderId}/notes
- "How do I set up shipping zones and methods?" -> POST /shipping/zones then POST /shipping/zones/{id}/methods
- "What payment gateways are enabled?" -> GET /payment_gateways
- "How do I bulk update product prices?" -> POST /products/batch (with `update` array)
- "How do I add variations to a variable product?" -> POST /products/{productId}/variations
- "How do I check my store's system health?" -> GET /system_status
- "How do I create a product category with an image?" -> POST /products/categories (with `image` object)
- "How do I find a customer by email address?" -> GET /customers (with `email` param)

## Response Tips

- **List endpoints** (GET /products, /orders, /customers): Paginated via `page` and `per_page` (max 100). Check `X-WP-Total` and `X-WP-TotalPages` response headers to know total count and whether more pages exist.
- **Single resource endpoints** (GET /products/{id}, /orders/{id}): Return the full object directly (not wrapped in an array). A 404 means the ID does not exist or the resource was trashed.
- **Batch endpoints** (POST /*/batch): Return `{create: [], update: [], delete: []}` -- each array contains full objects or error objects per item. Partial failures are possible; check each entry individually.
- **Order financials**: Monetary fields (`total`, `discount_total`, `shipping_total`, `tax`) are returned as strings, not numbers. Always parse to float for calculations.
- **Nested objects**: `billing`/`shipping` are inline maps on customers and orders. `line_items`, `tax_lines`, `shipping_lines`, `fee_lines`, `coupon_lines` are arrays nested inside order objects.
- **Delete endpoints**: Require `force=true` for permanent deletion. Without it, products and orders are trashed (soft delete) rather than removed.

## Anomaly Flags

- **401 on any endpoint**: Auth credentials are invalid or missing. Surface immediately -- all subsequent calls will also fail. Verify Basic auth header format (`consumer_key:consumer_secret` base64-encoded).
- **Coupon nearing usage limit**: When `usage_count` is close to `usage_limit`, flag that the coupon will stop working soon.
- **Coupon expiration**: When `date_expires` is within 7 days or has passed, warn the user the coupon is expiring or already expired.
- **Stock status**: Products with `stock_status: "outofstock"` or `stock_quantity <= 0` when `manage_stock` is true should be surfaced during order creation workflows.
- **Order with refunds**: If an order has a non-empty `refunds` array, flag it as partially or fully refunded before further operations.
- **Disabled payment gateways**: If GET /payment_gateways returns all gateways with `enabled: false`, flag that no payment method is active.
- **System status warnings**: Flag database issues, outdated PHP/WP versions, or security concerns found in GET /system_status `environment` and `security` maps.
- **Batch partial failures**: When a batch response contains error objects mixed with success objects, surface the failures explicitly rather than reporting overall success.

## Playbook

### 1. Create a product with variations

1. POST /products with `type: "variable"`, `name`, `regular_price`, and `attributes` (e.g., `[{name: "Size", options: ["S","M","L"], variation: true, visible: true}]`)
2. Note the returned `id` (the parent product ID)
3. POST /products/{productId}/variations for each combination, setting `regular_price` and `attributes` (e.g., `[{name: "Size", option: "S"}]`)
4. Verify with GET /products/{productId}/variations to confirm all variations exist
5. Optionally use POST /products/{productId}/variations/batch to create multiple variations in one call

### 2. Process an order and issue a partial refund

1. GET /orders/{orderId} to review the order details, `line_items`, and `total`
2. PUT /orders/{orderId} with `status: "processing"` to mark it as being handled
3. When ready to refund a specific line item, POST /orders/{orderId}/refunds with `amount` (partial total) and `line_items` array specifying the `id`, `quantity`, and `total` to refund
4. Set `api_refund: true` if the payment gateway should process the refund automatically
5. GET /orders/{orderId}/refunds to confirm the refund was recorded

### 3. Set up shipping zones with methods

1. POST /shipping/zones with `name` (e.g., "Domestic") and `order`
2. Note the returned zone `id`
3. PUT /shipping/zones/{id}/locations with an array of location objects (`code`, `type: "country"` or `"state"` or `"postcode"`)
4. POST /shipping/zones/{id}/methods with `method_id` (e.g., `"flat_rate"`, `"free_shipping"`, `"local_pickup"`) and configure via `settings`
5. GET /shipping/zones/{id}/methods to verify the methods are enabled

### 4. Bulk import customers with batch operations

1. Prepare customer data arrays (max 100 per batch call)
2. POST /customers/batch with `create` array containing customer objects (each with `email`, `first_name`, `last_name`, `billing`, `shipping`)
3. Inspect the response `create` array -- each entry is either a full customer object (success) or an error object with `code` and `message`
4. For any failures (e.g., duplicate email), fix the data and retry with a second batch call
5. GET /customers with `orderby: "registered_date"` and `order: "desc"` to verify the imports

### 5. Create a time-limited sale with coupon

1. POST /products/batch with `update` array to set `sale_price` and `date_on_sale_from`/`date_on_sale_to` on target products
2. POST /coupons with `code`, `discount_type: "percent"`, `amount`, `date_expires`, and optionally `product_ids` to restrict to sale items
3. Set `usage_limit` and `usage_limit_per_user` to control redemption caps
4. GET /products with `on_sale: true` to verify sale prices are active
5. After the sale ends, POST /products/batch with `update` to clear `sale_price` fields, and DELETE /coupons/{couponId} to remove the coupon


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
