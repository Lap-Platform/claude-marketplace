---
name: catalog-products
description: "Catalog - Products API skill. Use when working with Catalog - Products for catalog. Covers 53 endpoints."
version: 1.0.0
generator: lapsh
---

# Catalog - Products

## Auth
ApiKey X-Auth-Token in header

## Base URL
https://api.bigcommerce.com/stores/{store_hash}/v3

## Setup
1. Set your API key in the appropriate header
2. GET /catalog/products -- verify access
3. POST /catalog/products -- create first products

## Endpoints

53 endpoints across 1 groups. See references/api-spec.lap for full details.

### catalog
| Method | Path | Description |
|--------|------|-------------|
| GET | /catalog/products | Get All Products |
| PUT | /catalog/products | Update Products (Batch) |
| POST | /catalog/products | Create a Product |
| DELETE | /catalog/products | Delete Products |
| GET | /catalog/products/{product_id} | Get a Product |
| PUT | /catalog/products/{product_id} | Update a Product |
| DELETE | /catalog/products/{product_id} | Delete a Product |
| GET | /catalog/products/{product_id}/images | Get All Product Images |
| POST | /catalog/products/{product_id}/images | Create a Product Image |
| GET | /catalog/products/{product_id}/images/{image_id} | Get a Product Image |
| PUT | /catalog/products/{product_id}/images/{image_id} | Update a Product Image |
| DELETE | /catalog/products/{product_id}/images/{image_id} | Delete a Product Image |
| GET | /catalog/products/{product_id}/videos | Get All Product Videos |
| POST | /catalog/products/{product_id}/videos | Create a Product Video |
| GET | /catalog/products/{product_id}/videos/{id} | Get a Product Video |
| PUT | /catalog/products/{product_id}/videos/{id} | Update a Product Video |
| DELETE | /catalog/products/{product_id}/videos/{id} | Delete a Product Video |
| GET | /catalog/products/{product_id}/complex-rules | Get Complex Rules |
| POST | /catalog/products/{product_id}/complex-rules | Create a Complex Rule |
| GET | /catalog/products/{product_id}/complex-rules/{complex_rule_id} | Get a Product Complex Rule |
| PUT | /catalog/products/{product_id}/complex-rules/{complex_rule_id} | Update a Product Complex Rule |
| DELETE | /catalog/products/{product_id}/complex-rules/{complex_rule_id} | Delete a Product Complex Rule |
| GET | /catalog/products/{product_id}/custom-fields | Get Product Custom Fields |
| POST | /catalog/products/{product_id}/custom-fields | Create a Product Custom Field |
| GET | /catalog/products/{product_id}/custom-fields/{custom_field_id} | Get a Product Custom Field |
| PUT | /catalog/products/{product_id}/custom-fields/{custom_field_id} | Update a Product Custom Field |
| DELETE | /catalog/products/{product_id}/custom-fields/{custom_field_id} | Delete a Product Custom Field |
| POST | /catalog/products/{product_id}/bulk-pricing-rules | Create a Bulk Pricing Rule |
| GET | /catalog/products/{product_id}/bulk-pricing-rules | Get all Bulk Pricing Rules |
| GET | /catalog/products/{product_id}/bulk-pricing-rules/{bulk_pricing_rule_id} | Get a Bulk Pricing Rule |
| PUT | /catalog/products/{product_id}/bulk-pricing-rules/{bulk_pricing_rule_id} | Update a Bulk Pricing Rule |
| DELETE | /catalog/products/{product_id}/bulk-pricing-rules/{bulk_pricing_rule_id} | Delete a Bulk Pricing Rule |
| GET | /catalog/products/{product_id}/metafields | Get Product Metafields |
| POST | /catalog/products/{product_id}/metafields | Create a Product Metafield |
| GET | /catalog/products/{product_id}/metafields/{metafield_id} | Get a Product Metafield |
| PUT | /catalog/products/{product_id}/metafields/{metafield_id} | Update a Product Metafield |
| DELETE | /catalog/products/{product_id}/metafields/{metafield_id} | Delete a Product Metafield |
| GET | /catalog/products/{product_id}/reviews | Get Product Reviews |
| POST | /catalog/products/{product_id}/reviews | Create a Product Review |
| GET | /catalog/products/{product_id}/reviews/{review_id} | Get a Product Review |
| PUT | /catalog/products/{product_id}/reviews/{review_id} | Update a Product Review |
| DELETE | /catalog/products/{product_id}/reviews/{review_id} | Delete a Product Review |
| GET | /catalog/products/channel-assignments | Get Products Channel Assignments |
| PUT | /catalog/products/channel-assignments | Create Products Channel Assignments |
| DELETE | /catalog/products/channel-assignments | Delete Products Channel Assignments |
| GET | /catalog/products/category-assignments | Get Products Category Assignments |
| PUT | /catalog/products/category-assignments | Create Products Category Assignments |
| DELETE | /catalog/products/category-assignments | Delete Products Category Assignments |
| GET | /catalog/summary | Get a Catalog Summary |
| GET | /catalog/products/metafields | Get All Product Metafields |
| POST | /catalog/products/metafields | Create multiple Metafields |
| PUT | /catalog/products/metafields | Update multiple Metafields |
| DELETE | /catalog/products/metafields | Delete Multiple Metafields |

## Enhanced Skill Content
## Question Mapping

- "How do I list all products in my store?" -> GET /catalog/products
- "How do I search for a product by name or keyword?" -> GET /catalog/products (use `keyword` or `name` param)
- "How do I get details for a specific product?" -> GET /catalog/products/{product_id}
- "How do I create a new physical product?" -> POST /catalog/products
- "How do I update a product's price or description?" -> PUT /catalog/products/{product_id}
- "How do I delete a product?" -> DELETE /catalog/products/{product_id}
- "How do I bulk update multiple products at once?" -> PUT /catalog/products
- "How do I bulk delete products by filter criteria?" -> DELETE /catalog/products (use filter params like `id:in`)
- "How do I add an image to a product?" -> POST /catalog/products/{product_id}/images
- "How do I get the catalog summary with inventory counts?" -> GET /catalog/summary
- "How do I find out-of-stock or low-inventory products?" -> GET /catalog/products (use `out_of_stock=1` or `inventory_low=1`)
- "How do I assign a product to a sales channel?" -> PUT /catalog/products/channel-assignments
- "How do I add custom fields to a product?" -> POST /catalog/products/{product_id}/custom-fields
- "How do I set up bulk pricing tiers for a product?" -> POST /catalog/products/{product_id}/bulk-pricing-rules
- "How do I store custom metadata on a product?" -> POST /catalog/products/{product_id}/metafields

## Response Tips

- **Product listings** (GET /catalog/products, images, videos, reviews, metafields): Response wraps results in `data` array with `meta.pagination` containing `total`, `total_pages`, `current_page`, and navigation `links` -- always check `total_pages` to know if more pages exist.
- **Single product** (GET /catalog/products/{product_id}): Response uses `data` as a single object (not array) with an empty `meta` map.
- **Bulk writes** (PUT /catalog/products, POST/PUT/DELETE /catalog/products/metafields): Return 200 with `meta.total`, `meta.success`, `meta.failed` counters and an `errors` array -- always check `errors` even on 200.
- **Partial success** (207 responses on POST/PUT products): Mix of succeeded and failed items in `data` plus an `errors` map with `status`, `title`, and `type` -- treat 207 as a partial failure requiring item-level inspection.
- **Deletes** (all DELETE endpoints): Return 204 No Content with empty body on success.
- **Catalog summary** (GET /catalog/summary): Returns a flat `data` object with inventory and variant stats -- note `lowest_variant_price` is a string, not a number.

## Anomaly Flags

- **207 Multi-Status on batch operations**: Surface each failed item from the `errors` object with its `status` and `title` -- partial failures are easy to miss.
- **409 Conflict errors**: Indicate duplicate SKU, slug collision, or concurrent modification -- surface the conflict details and suggest checking for existing resources.
- **422 Validation errors**: The `errors` map contains field-level details -- surface the specific field names and validation messages.
- **Inventory thresholds**: When `inventory_level` drops to or below `inventory_warning_level`, flag the product as low stock proactively.
- **Bulk delete without filters**: DELETE /catalog/products with no filter params could delete the entire catalog -- warn before executing unfiltered bulk deletes.
- **413 Payload Too Large**: On PUT /catalog/products batch updates, the payload exceeded limits -- suggest splitting into smaller batches.
- **Inconsistent type quirks**: `lowest_variant_price` in catalog summary is a string while other prices are numbers; `is_featured` and `is_free_shipping` accept int (1/0) as filters but bool on create -- flag type mismatches in request construction.
- **Pagination beyond total_pages**: If `current_page` exceeds `total_pages`, results will be empty -- surface when the requested page is out of range.

## Playbook

### 1. Create a Product with Images and Custom Fields

1. POST /catalog/products with required fields: `name`, `type` ("physical"), `weight`, `price`, plus optional `sku`, `description`, `categories`, `brand_id`, `is_visible`.
2. Capture the `product_id` from `data.id` in the response.
3. POST /catalog/products/{product_id}/images for each product image (primary image first).
4. POST /catalog/products/{product_id}/custom-fields for each custom field, providing `name` and `value`.
5. Optionally POST /catalog/products/{product_id}/bulk-pricing-rules to add volume discounts.

### 2. Audit Inventory Levels Across the Catalog

1. GET /catalog/summary to get total `inventory_count` and `inventory_value` as a quick health check.
2. GET /catalog/products with `inventory_low=1` to find products below their warning threshold.
3. GET /catalog/products with `out_of_stock=1` to find products with zero inventory.
4. For each flagged product, GET /catalog/products/{product_id} with `include=variants` to check variant-level stock.
5. PUT /catalog/products/{product_id} to update `inventory_level` or `inventory_warning_level` as needed.

### 3. Bulk Update Products and Verify Results

1. GET /catalog/products with appropriate filters to identify target products and collect their IDs.
2. PUT /catalog/products with a JSON array of objects, each containing `id` and the fields to update.
3. Check the response status: 200 means full success, 207 means partial success.
4. On 207, iterate through the `errors` map to identify which products failed and why.
5. Fix validation issues and retry failed items in a second PUT /catalog/products call.

### 4. Manage Multi-Channel Product Distribution

1. GET /catalog/products/channel-assignments to see current product-to-channel mappings.
2. PUT /catalog/products/channel-assignments with an array of `{product_id, channel_id}` objects to assign products to new channels.
3. Verify assignments with GET /catalog/products/channel-assignments filtered by `channel_id:in`.
4. To remove products from a channel, DELETE /catalog/products/channel-assignments with `product_id:in` and `channel_id:in` filters.

### 5. Set Up Product Metafields for App-Specific Data

1. POST /catalog/products/{product_id}/metafields with `key`, `value`, `namespace`, and `permission_set` (use "app_only" for private data, "read_and_sf_access" for storefront-visible data).
2. To query across all products, GET /catalog/products/metafields filtered by `namespace` and/or `key`.
3. To update, PUT /catalog/products/{product_id}/metafields/{metafield_id} with the full set of required fields (key, value, namespace, permission_set).
4. For bulk operations, POST /catalog/products/metafields with an array -- check `meta.failed` and `errors` in the response for partial failures.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
