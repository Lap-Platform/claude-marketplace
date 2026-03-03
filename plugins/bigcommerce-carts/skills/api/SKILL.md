---
name: carts
description: "Carts API skill. Use when working with Carts for carts. Covers 21 endpoints."
version: 1.0.0
generator: lapsh
---

# Carts

## Auth
ApiKey X-Auth-Token in header

## Base URL
https://api.bigcommerce.com/stores/{store_hash}/v3

## Setup
1. Set your API key in the appropriate header
2. GET /carts/settings -- verify access
3. POST /carts -- create first carts

## Endpoints

21 endpoints across 1 groups. See references/api-spec.lap for full details.

### carts
| Method | Path | Description |
|--------|------|-------------|
| POST | /carts | Create a Cart |
| POST | /carts/{cartId}/items | Add Cart Line Items |
| POST | /carts/{cartId}/redirect_urls | Create Cart Redirect URL |
| PUT | /carts/{cartId}/items/{itemId} | Update Cart Line Item |
| DELETE | /carts/{cartId}/items/{itemId} | Delete Cart Line Item |
| GET | /carts/{cartId} | Get a Cart |
| PUT | /carts/{cartId} | Update Customer ID |
| DELETE | /carts/{cartId} | Delete a Cart |
| GET | /carts/settings | Get Global Cart Settings |
| PUT | /carts/settings | Update Global Cart Settings |
| GET | /carts/settings/channels/{channel_id} | Get Channel Cart Settings |
| PUT | /carts/settings/channels/{channel_id} | Update Channel Cart Settings |
| GET | /carts/{cart_id}/metafields | Get Cart Metafields |
| POST | /carts/{cart_id}/metafields | Create a Cart Metafield |
| GET | /carts/{cart_id}/metafields/{metafield_id} | Get a Cart Metafield |
| PUT | /carts/{cart_id}/metafields/{metafield_id} | Update a Cart Metafield |
| DELETE | /carts/{cart_id}/metafields/{metafield_id} | Delete a Metafield |
| GET | /carts/metafields | Get All Cart Metafields |
| POST | /carts/metafields | Create multiple Metafields |
| PUT | /carts/metafields | Update multiple Metafields |
| DELETE | /carts/metafields | Delete multiple Metafields |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new shopping cart?" -> POST /carts
- "How do I add items to an existing cart?" -> POST /carts/{cartId}/items
- "How do I update the quantity of an item in a cart?" -> PUT /carts/{cartId}/items/{itemId}
- "How do I remove an item from a cart?" -> DELETE /carts/{cartId}/items/{itemId}
- "How do I get the current contents of a cart?" -> GET /carts/{cartId}
- "How do I assign a cart to a customer?" -> PUT /carts/{cartId}
- "How do I delete an entire cart?" -> DELETE /carts/{cartId}
- "How do I get a checkout URL for a cart?" -> POST /carts/{cartId}/redirect_urls
- "How do I add a gift certificate to a cart?" -> POST /carts/{cartId}/items
- "Can I disable purchasing on my store?" -> PUT /carts/settings
- "How do I check if purchasing is enabled for a specific channel?" -> GET /carts/settings/channels/{channel_id}
- "How do I attach custom metadata to a cart?" -> POST /carts/{cart_id}/metafields
- "How do I list all cart metafields across all carts?" -> GET /carts/metafields
- "How do I bulk update metafields across multiple carts?" -> PUT /carts/metafields
- "How do I add a custom line item with a custom price to a cart?" -> POST /carts/{cartId}/items (use `custom_items` field)

## Response Tips

- **Cart CRUD** (`POST /carts`, `GET/PUT/DELETE /carts/{cartId}`): Response wraps cart in `data` with `meta`. Line items are nested under `data.line_items` split into `physical_items`, `digital_items`, `gift_certificates`, and `custom_items` -- always check the right sub-array.
- **Item operations** (`POST /PUT /DELETE items`): Returns the full updated cart, not just the item. On DELETE, response may be the cart object (200) or empty (204). Watch for 409 conflict errors indicating version mismatch.
- **Redirect URLs** (`POST redirect_urls`): Returns three distinct URLs -- `cart_url` (storefront cart page), `checkout_url` (direct checkout), and `embedded_checkout_url` (for iframe embedding). These are one-time use.
- **Settings** (`GET/PUT /carts/settings`): Simple `allow_purchasing` boolean. Channel-specific overrides return nullable `allow_purchasing` -- null means inheriting from global settings.
- **Metafields** (`GET /carts/metafields`): Supports both offset pagination (`meta.pagination`) and cursor pagination (`meta.cursor_pagination`). Use `before`/`after` params for cursor-based paging.
- **Bulk metafield operations** (`POST/PUT/DELETE /carts/metafields`): Return partial-success responses with `meta.total`, `meta.success`, `meta.failed` counts and an `errors` array -- always check both `data` and `errors`.

## Anomaly Flags

- **409 Conflict on item updates/deletes**: Indicates a cart version mismatch. Surface this immediately -- the client must re-fetch the cart and include the current `version` field to retry.
- **Partial bulk failures**: When `meta.failed > 0` on bulk metafield operations, proactively surface the `errors` array with details on which entries failed and why.
- **Null `allow_purchasing` on channel settings**: This means the channel inherits the global setting. Flag when a user expects an explicit override but gets inheritance.
- **Empty line item sub-arrays**: If all four line item categories are empty after an add/update, the cart may have silently rejected items. Alert the user to verify product IDs and availability.
- **204 vs 200 on item DELETE**: Two possible success codes. A 204 means the cart was emptied and deleted entirely. Surface this distinction so the caller knows the cart no longer exists.
- **Missing `include` query param**: Cart responses omit redirect URLs and promotions by default. Flag when a user expects these fields but did not pass `?include=redirect_urls` or similar.

## Playbook

### 1. Create a Cart and Proceed to Checkout

1. `POST /carts` with `line_items` (physical/digital products), optional `customer_id`, and `currency.code`
2. Note the returned `data.id` (cart UUID)
3. Optionally add gift certificates or custom items via `POST /carts/{cartId}/items`
4. `POST /carts/{cartId}/redirect_urls` to generate checkout links
5. Direct the customer to `checkout_url` or embed via `embedded_checkout_url`

### 2. Update Cart Item Quantities

1. `GET /carts/{cartId}` to retrieve current cart state
2. Find the target item ID in `data.line_items.physical_items` (or `digital_items`/`custom_items`)
3. Note the cart `version` from the response
4. `PUT /carts/{cartId}/items/{itemId}` with updated `line_item` and `version` field
5. If you receive a 409, re-fetch the cart and retry with the new version

### 3. Tag Carts with Custom Metadata

1. `POST /carts/{cart_id}/metafields` with `namespace`, `key`, `value`, and `permission_set`
2. Use `permission_set: "read_and_sf_access"` if the storefront needs to read the data
3. Verify with `GET /carts/{cart_id}/metafields?namespace={ns}&key={key}`
4. Update later via `PUT /carts/{cart_id}/metafields/{metafield_id}`

### 4. Manage Purchasing Availability per Channel

1. `GET /carts/settings` to check the global purchasing toggle
2. `GET /carts/settings/channels/{channel_id}` to check channel-specific override
3. If `allow_purchasing` is null, the channel uses the global setting
4. `PUT /carts/settings/channels/{channel_id}` with `{ "allow_purchasing": false }` to disable for that channel only
5. Verify by re-fetching channel settings

### 5. Bulk Manage Metafields Across All Carts

1. `GET /carts/metafields` with filters (`namespace`, `key:in`, `date_modified:min`) to find target metafields
2. Use cursor pagination (`after` param) if results span multiple pages
3. `PUT /carts/metafields` with an array of updates to modify in bulk
4. Check `meta.failed` in the response -- if non-zero, inspect `errors` array
5. To clean up, `DELETE /carts/metafields` with the list of metafield IDs


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
