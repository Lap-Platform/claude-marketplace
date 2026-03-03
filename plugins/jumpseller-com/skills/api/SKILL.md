---
name: jumpseller-api
description: "Jumpseller API skill. Use when working with Jumpseller for store, hooks.json, hooks. Covers 182 endpoints."
version: 1.0.0
generator: lapsh
---

# Jumpseller API
API version: 1.0.0

## Auth
Bearer basic | ApiKey login in query | ApiKey authtoken in query | ApiKey partner_code in query | ApiKey auth_token in query

## Base URL
https://api.jumpseller.com/v1

## Setup
1. Set Authorization header with your Bearer token
2. GET /store/info.json -- verify access
3. POST /hooks.json -- create first hooks.json

## Endpoints

182 endpoints across 42 groups. See references/api-spec.lap for full details.

### store
| Method | Path | Description |
|--------|------|-------------|
| GET | /store/info.json | Retrieve Store Information. |
| GET | /store/languages.json | Retrieve Store Languages. |
| POST | /store/create.json | Create a Partnered Store |
| GET | /store/check_status.json | Retrive store creation status. |

### hooks.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /hooks.json | Retrieve all Hooks. |
| POST | /hooks.json | Create a new Hook. |

### hooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /hooks/{id}.json | Retrieve a single Hook. |
| PUT | /hooks/{id}.json | Update a Hook. |
| DELETE | /hooks/{id}.json | Delete an existing Hook. |

### jsapps.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /jsapps.json | Retrieve all the Store's JSApps. |
| POST | /jsapps.json | Create a Store JSApp. |

### jsapps
| Method | Path | Description |
|--------|------|-------------|
| GET | /jsapps/{code}.json | Retrieve a JSApp. |
| DELETE | /jsapps/{code}.json | Delete an existing JSApp. |

### apps
| Method | Path | Description |
|--------|------|-------------|
| GET | /apps/{code}/install_status.json | Retrieve an OauthApplication installation status. |
| GET | /apps/{code}/install_status_by_store_id.json | Retrieve an OauthApplication installation status for a specific Store. |
| GET | /apps/{code}/billing_cycle_dates.json | Retrieve billing cycle start and billing cycle end for an OauthApplication. |
| GET | /apps/{code}/billing_cycle_orders.json | Retrieve billing cycle orders for an OauthApplication. |
| GET | /apps/{code}/check_billing_cycle_order.json | Retrieve a billing cycle order information for an OauthApplication. |

### products.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /products.json | Retrieve all Products. |
| POST | /products.json | Create a new Product. |

### products
| Method | Path | Description |
|--------|------|-------------|
| GET | /products/count.json | Count all Products. |
| GET | /products/after/{id}.json | Retrieves Products after the given id. |
| GET | /products/status/{status}.json | Retrieve Products filtered by status. |
| GET | /products/category/{category_id}.json | Retrieve Products filtered by category. |
| GET | /products/status/{status}/count.json | Count Products filtered by status. |
| GET | /products/category/{category_id}/count.json | Count Products filtered by category. |
| GET | /products/{id}/reviews.json | Retrieve all reviews for a specific Product. |
| GET | /products/reviews/{review_id}.json | Retrieve a single Product Review. |
| GET | /products/reviews.json | Retrieve all Product Reviews. |
| GET | /products/{id}.json | Retrieve a single Product. |
| PUT | /products/{id}.json | Modify an existing Product. |
| DELETE | /products/{id}.json | Delete an existing Product. |
| GET | /products/search.json | Retrieve a Product List from a query. |
| GET | /products/{id}/options.json | Retrieve all Product Options. |
| POST | /products/{id}/options.json | Create a new Product Option. |
| GET | /products/{id}/options/count.json | Count all Product Options. |
| GET | /products/{id}/options/{option_id}.json | Retrieve a single Product Option. |
| PUT | /products/{id}/options/{option_id}.json | Modify an existing Product Option. |
| DELETE | /products/{id}/options/{option_id}.json | Delete a Product Option. |
| GET | /products/{id}/options/{option_id}/values.json | Retrieve all Product Option Values. |
| POST | /products/{id}/options/{option_id}/values.json | Create a new Product Option Value. |
| GET | /products/{id}/options/{option_id}/values/count.json | Count all Product Option Values. |
| GET | /products/{id}/options/{option_id}/values/{value_id}.json | Retrieve a single Product Option Value. |
| PUT | /products/{id}/options/{option_id}/values/{value_id}.json | Modify an existing Product Option Value. |
| DELETE | /products/{id}/options/{option_id}/values/{value_id}.json | Delete a Product Option Value. |
| GET | /products/{id}/variants/{variant_id}.json | Retrieve a single Product Variant. |
| PUT | /products/{id}/variants/{variant_id}.json | Modify an existing Product Variant. |
| GET | /products/{id}/variants.json | Retrieve all Product Variants. |
| POST | /products/{id}/variants.json | Create a new Product Variant. |
| GET | /products/{id}/variants/count.json | Count all Product Variants. |
| GET | /products/{id}/images.json | Retrieve all Product Images. |
| POST | /products/{id}/images.json | Create a new Product Image. |
| PUT | /products/{product_id}/images/{image_id}.json | Update a Product Image position. |
| GET | /products/{id}/images/count.json | Count all Product Images. |
| GET | /products/{id}/images/{image_id}.json | Retrieve a single Product Image. |
| DELETE | /products/{id}/images/{image_id}.json | Delete a Product Image. |
| GET | /products/{id}/attachments.json | Retrieve all Product Attachments. |
| POST | /products/{id}/attachments.json | Create a new Product Attachment. |
| GET | /products/{id}/attachments/count.json | Count all Product Attachments. |
| GET | /products/{id}/attachments/{attachment_id}.json | Retrieve a single Product Attachment. |
| DELETE | /products/{id}/attachments/{attachment_id}.json | Delete a Product Attachment. |
| GET | /products/{id}/digital_products.json | Retrieve all Product DigitalProducts. |
| POST | /products/{id}/digital_products.json | Create a new Product DigitalProduct. |
| GET | /products/{id}/digital_products/count.json | Count all Product DigitalProducts. |
| GET | /products/{id}/digital_products/{digital_product_id}.json | Retrieve a single Product DigitalProduct. |
| DELETE | /products/{id}/digital_products/{digital_product_id}.json | Delete a Product DigitalProduct. |
| GET | /products/{id}/fields.json | Retrieve all Product Custom Fields |
| POST | /products/{id}/fields.json | Add an existing Custom Field to a Product. |
| GET | /products/{id}/fields/count.json | Count all Product Custom Fields. |
| PUT | /products/{product_id}/fields/{field_id}.json | Update value of Product Custom Field |
| DELETE | /products/{product_id}/fields/{field_id}.json | Delete value of Product Custom Field |

### categories.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /categories.json | Retrieve all Categories. |
| POST | /categories.json | Create a new Category. |

### categories
| Method | Path | Description |
|--------|------|-------------|
| GET | /categories/count.json | Count all Categories. |
| GET | /categories/{id}.json | Retrieve a single Category. |
| PUT | /categories/{id}.json | Modify an existing Category. |
| DELETE | /categories/{id}.json | Delete an existing Category. |

### orders.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /orders.json | Retrieve all Orders. |
| POST | /orders.json | Create a new Order. |

### orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /orders/count.json | Count all Orders. |
| GET | /orders/status/{status}.json | Retrieve orders filtered by status. |
| GET | /orders/{id}.json | Retrieve a single Order. |
| PUT | /orders/{id}.json | Modify an existing Order. |
| GET | /orders/search.json | Retrieve an Orders List from a query. |
| GET | /orders/after/{id}.json | Retrieve orders filtered by Order Id. |
| GET | /orders/{id}/history.json | Retrieve all Order History. |
| POST | /orders/{id}/history.json | Create a new Order History Entry. |
| GET | /orders/{id}/documents.json | Retrieve all Documents from an  Order. |
| POST | /orders/{id}/documents.json | Create a new Order Document Entry. |
| PUT | /orders/{id}/documents/{public_id}.json | Update a Document from an Order. |
| DELETE | /orders/{id}/documents/{public_id}.json | Delete a Document from an Order. |

### fulfillments
| Method | Path | Description |
|--------|------|-------------|
| GET | /fulfillments/count.json | Count all Fulfillments. |
| POST | /fulfillments/rates.json | Rates for fulfillment. |
| GET | /fulfillments/{id}/label.json | Retrieve a presigned URL for the Fulfillment label |
| GET | /fulfillments/{id}.json | Retrieve a single Fulfillment. |
| PUT | /fulfillments/{id}.json | Modify an existing Fulfillment. |

### fulfillments.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /fulfillments.json | Retrieve all Fulfillments. |
| POST | /fulfillments.json | Create a new Fulfillment. |

### order
| Method | Path | Description |
|--------|------|-------------|
| GET | /order/{id}/fulfillments.json | Retrieve the Fulfillments associated with the Order. |

### pages.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /pages.json | Retrieve all Pages. |
| POST | /pages.json | Create a new Page. |

### pages
| Method | Path | Description |
|--------|------|-------------|
| GET | /pages/count.json | Count all Pages. |
| GET | /pages/{id}.json | Retrieve a single Page by id. |
| PUT | /pages/{id}.json | Update a Page. |
| DELETE | /pages/{id}.json | Delete an existing Page. |
| GET | /pages/{id}/images.json | Retrieve all Page Images. |
| POST | /pages/{id}/images.json | Create a new Page Image. |
| GET | /pages/{id}/images/count.json | Count all Page Images. |
| GET | /pages/{id}/images/{image_id}.json | Retrieve a single Page Image. |
| PUT | /pages/{id}/images/{image_id}.json | Update a Page Image url. |
| DELETE | /pages/{id}/images/{image_id}.json | Delete a Page Image. |

### customers.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /customers.json | Retrieve all Customers. |
| POST | /customers.json | Create a new Customer. |

### customers
| Method | Path | Description |
|--------|------|-------------|
| GET | /customers/count.json | Count all Customers. |
| GET | /customers/email/{email}.json | Retrieve a single Customer by email. |
| GET | /customers/{id}/orders.json | Retrieve all orders of single Customer |
| GET | /customers/{id}/orders/status/{status}.json | Retrieve all orders of single Customer |
| GET | /customers/{id}.json | Retrieve a single Customer by id. |
| PUT | /customers/{id}.json | Update a new Customer. |
| DELETE | /customers/{id}.json | Delete an existing Customer. |
| GET | /customers/search.json | Retrieve a Customer List from a query. |
| GET | /customers/{id}/fields | Retrieves the Customer Additional Field of a Customer. |
| POST | /customers/{id}/fields | Adds Customer Additional Fields to a Customer. |
| GET | /customers/{id}/fields/{field_id} | Retrieve a single Customer Additional Field. |
| PUT | /customers/{id}/fields/{field_id} | Update a Customer Additional Field. |
| DELETE | /customers/{id}/fields/{field_id} | Delete a Customer Additional Field. |

### customer_categories.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /customer_categories.json | Retrieve all Customer Categories. |
| POST | /customer_categories.json | Create a new CustomerCategory. |

### customer_categories
| Method | Path | Description |
|--------|------|-------------|
| GET | /customer_categories/{id}.json | Retrieve a single CustomerCategory. |
| PUT | /customer_categories/{id}.json | Update a CustomerCategory. |
| DELETE | /customer_categories/{id}.json | Delete an existing CustomerCategory. |
| GET | /customer_categories/{id}/customers.json | Retrieves the customers in a CustomerCategory. |
| POST | /customer_categories/{id}/customers.json | Adds Customers to a CustomerCategory. |
| DELETE | /customer_categories/{id}/customers/{customer_id}.json | Delete Customer from an existing CustomerCategory. |

### promotions.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /promotions.json | Retrieve all Promotions. |
| POST | /promotions.json | Create a new Promotion. |

### promotions
| Method | Path | Description |
|--------|------|-------------|
| GET | /promotions/{id}.json | Retrieve a single Promotion. |
| PUT | /promotions/{id}.json | Update a Promotion. |
| DELETE | /promotions/{id}.json | Delete an existing Promotion. |

### payment_methods.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /payment_methods.json | Retrieve all Store's Payment Methods. |
| POST | /payment_methods.json | Creates an External Payment Method. |

### payment_methods
| Method | Path | Description |
|--------|------|-------------|
| GET | /payment_methods/{id}.json | Retrieve a single Payment Method. |

### shipping_methods.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /shipping_methods.json | Retrieve all Store's Shipping Methods. |
| POST | /shipping_methods.json | Creates a Shipping Method. |

### shipping_methods
| Method | Path | Description |
|--------|------|-------------|
| GET | /shipping_methods/{id}.json | Retrieve a single Shipping Method. |
| PUT | /shipping_methods/{id}.json | Update a Shipping Method. |
| DELETE | /shipping_methods/{id}.json | Delete an existing Shipping Method. |

### locations.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /locations.json | Retrieve all Store's Locations |
| POST | /locations.json | Create a Pickup Location |

### locations
| Method | Path | Description |
|--------|------|-------------|
| GET | /locations/{id}.json | Retrieve a Store's Locations by ID |
| PUT | /locations/{id}.json | Update a Pickup Location |
| DELETE | /locations/{id}.json | Delete a Store's Locations by ID |

### custom_fields.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /custom_fields.json | Retrieve all Store's Custom Fields. |
| POST | /custom_fields.json | Create a new Custom Field. |

### custom_fields
| Method | Path | Description |
|--------|------|-------------|
| GET | /custom_fields/{id}.json | Retrieve a single CustomField. |
| PUT | /custom_fields/{id}.json | Update a CustomField. |
| DELETE | /custom_fields/{id}.json | Delete an existing CustomField. |
| GET | /custom_fields/{id}/select_options.json | Retrieve all Store's Custom Fields. |
| POST | /custom_fields/{id}/select_options.json | Create a new Custom Field Select Option. |
| GET | /custom_fields/{id}/select_options/{custom_field_select_option_id}.json | Retrieve a single SelectOption from a CustomField. |
| PUT | /custom_fields/{id}/select_options/{custom_field_select_option_id}.json | Update a SelectOption from a CustomField. |
| DELETE | /custom_fields/{id}/select_options/{custom_field_select_option_id}.json | Delete an existing CustomFieldSelectOption. |

### checkout_custom_fields.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /checkout_custom_fields.json | Retrieve all Checkout Custom Fields. |
| POST | /checkout_custom_fields.json | Create a new CheckoutCustomField. |

### checkout_custom_fields
| Method | Path | Description |
|--------|------|-------------|
| GET | /checkout_custom_fields/{id}.json | Retrieve a single CheckoutCustomField. |
| PUT | /checkout_custom_fields/{id}.json | Update a CheckoutCustomField. |
| DELETE | /checkout_custom_fields/{id}.json | Delete an existing CheckoutCustomField. |

### countries.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /countries.json | Retrieve all Countries. |

### countries
| Method | Path | Description |
|--------|------|-------------|
| GET | /countries/{country_code}.json | Retrieve a single Country information. |
| GET | /countries/{country_code}/regions.json | Retrieve all Regions from a single Country. |
| GET | /countries/{country_code}/regions/{region_code}/municipalities.json | Retrieve all Municipalities from a single Region. |
| GET | /countries/{country_code}/regions/{region_code}.json | Retrieve a single Region information object. |

### taxes.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /taxes.json | Retrieve all Taxes. |
| POST | /taxes.json | Create a new Tax. |

### taxes
| Method | Path | Description |
|--------|------|-------------|
| GET | /taxes/{id}.json | Retrieve a single Tax information. |

### partners
| Method | Path | Description |
|--------|------|-------------|
| GET | /partners/stores.json | Retrieve statistics. |
| GET | /partners/subscriptions.json | Retrieve subscriptions and transactions. |

### carts
| Method | Path | Description |
|--------|------|-------------|
| GET | /carts/{id}.json | Obtain information for a cart. |

### documents.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /documents.json | Retrieve all Documents from a Store. |

### transaction_ledger
| Method | Path | Description |
|--------|------|-------------|
| GET | /transaction_ledger/balance.json | Store Balance |

### products_locations
| Method | Path | Description |
|--------|------|-------------|
| GET | /products_locations | Stock by Product and Location |
| PUT | /products_locations | Update Stock by Product and Location |

## Enhanced Skill Content
## Question Mapping

- "What are my store details?" -> GET /store/info.json
- "How many products do I have?" -> GET /products/count.json
- "Find products by SKU or barcode" -> GET /products/search.json
- "Show me all orders from the last 7 days" -> GET /orders.json (with dateFilter=last7days)
- "Which orders are still unfulfilled?" -> GET /orders.json (with fulfillment_filters=unfulfilled)
- "Look up a customer by email address" -> GET /customers/email/{email}.json
- "What orders has customer #42 placed?" -> GET /customers/{id}/orders.json
- "List all abandoned carts" -> GET /orders/status/abandoned.json
- "How do I update tracking info on an order?" -> PUT /orders/{id}.json (tracking_number, tracking_company, tracking_url fields)
- "Create a new product with variants" -> POST /products.json (include variants array in body)
- "What shipping methods are currently enabled?" -> GET /shipping_methods.json (with enabled=true)
- "Get shipping rates for a fulfillment" -> POST /fulfillments/rates.json
- "What promotions are active right now?" -> GET /promotions.json
- "How do I manage inventory across multiple locations?" -> PUT /products_locations (set stock per location)
- "What is my current transaction balance?" -> GET /transaction_ledger/balance.json

## Response Tips

- **Paginated lists** (products, orders, customers, hooks, pages, documents): Default 50 per page. Increment `page` param until results come back empty. No total-pages header -- use the companion `/count.json` endpoint to calculate pages upfront.
- **Single-resource responses**: Wrapped in a root key matching the resource type (e.g., `{product: {...}}`, `{order: {...}}`). Always unwrap before accessing fields.
- **Orders**: Deeply nested -- `source`, `shipping_address`, `billing_address`, `pickup_address`, and `billing_information` are all sub-objects. The `products` array inside an order is separate from top-level products.
- **404 errors**: Returned for any invalid ID across all resource types. Treat as "not found," not a server error.
- **Products search**: The `fields` param controls which fields are searched (sku, barcode, brand, name, etc.), not which fields are returned.
- **Fulfillments**: The `order` field is triple-nested (`order.order.order`) -- likely a serialization quirk; dig into the innermost object for actual order data.

## Anomaly Flags

- **Promotion nearing max usage**: If `times_used` is approaching `max_times_used` on a promotion, surface a warning before it silently stops applying.
- **Stock below threshold**: When `stock` drops at or below `stock_threshold` and `stock_unlimited` is false, flag the product/variant as low inventory.
- **Expired or expiring promotions**: If `expires_at` is in the past or within 24 hours, alert that the promotion will stop working.
- **Subscription status changes**: If `GET /store/info.json` returns a `subscription_status` other than active, surface immediately -- API access may degrade.
- **Order status mismatch**: If `fulfillment_status` says "fulfilled" but `shipment_status` is still pending, flag the inconsistency.
- **Missing tracking on fulfilled orders**: Orders marked as paid/completed but with empty `tracking_number` and `tracking_url` should be flagged for follow-up.
- **Duplicate webhook URLs**: When creating hooks, warn if an identical `event` + `url` combination already exists to prevent double-firing.
- **Digital product expiration**: `expiration_seconds` on digital products set to very low values may cause customer access issues -- flag if under 3600.

## Playbook

### 1. Create a Product with Options and Variants

1. `POST /products.json` with name, price, and status to create the base product. Note the returned `product.id`.
2. `POST /products/{id}/options.json` for each option axis (e.g., "Size", "Color"). Note each `option.id`.
3. `POST /products/{id}/options/{option_id}/values.json` to add values to each option (e.g., "S", "M", "L").
4. `POST /products/{id}/variants.json` for each combination, specifying price, sku, stock, and `options` array linking option names to values.
5. `POST /products/{id}/images.json` to attach product images. Optionally set `image_id` on variants to assign variant-specific images.

### 2. Process and Fulfill an Order

1. `GET /orders/{id}.json` to retrieve full order details including products, shipping address, and current status.
2. `PUT /orders/{id}.json` with `{order: {status: "paid"}}` if confirming payment manually.
3. `POST /fulfillments.json` with `order_id`, `type`, `location_id`, `shipping_address`, and package dimensions to create the fulfillment.
4. `PUT /fulfillments/{id}.json` to update `tracking_number`, `tracking_company`, and `tracking_url` once the carrier provides them.
5. `PUT /orders/{id}.json` with `{order: {shipment_status: "shipped"}}` to sync the order-level status.
6. `POST /orders/{id}/history.json` to log a message like "Shipped via FedEx, tracking #12345" for audit trail.

### 3. Bulk Inventory Check Across Locations

1. `GET /locations.json` to list all warehouse/store locations. Note each `location.id`.
2. `GET /products.json` paginating through all pages (use `GET /products/count.json` first to calculate total pages).
3. `GET /products_locations` with arrays of `location_ids` and `product_ids` to fetch stock levels per location.
4. For any product where `stock <= stock_threshold` and `stock_unlimited` is false, flag for restocking.
5. `PUT /products_locations` to update stock at a specific location when new inventory arrives.

### 4. Set Up a Promotion with Coupon Codes

1. `GET /categories.json` to find category IDs for targeting (or `GET /products.json` for specific product IDs).
2. `POST /promotions.json` with promotion details: set `discount_target`, `discount_amount_percent` or `discount_amount_fix`, `begins_at`, `expires_at`, and `max_times_used`.
3. Include a `coupons` array with objects like `{code: "SAVE20", usage_limit: 100}` to attach codes.
4. Optionally scope to specific `categories`, `products`, `customer_categories`, or `countries` arrays.
5. `GET /promotions/{id}.json` to verify the promotion was created correctly and `status` is active.

### 5. Customer Lookup and Order History

1. `GET /customers/search.json?query=john` to find a customer by name, email, or other details.
2. `GET /customers/{id}.json` to retrieve full customer profile including addresses and custom fields.
3. `GET /customers/{id}/orders.json` to list all their orders (paginated, default 50).
4. `GET /customers/{id}/orders/status/Paid.json` to filter to only completed orders.
5. `GET /customers/{id}/fields` to check any additional custom fields stored on the customer record.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
