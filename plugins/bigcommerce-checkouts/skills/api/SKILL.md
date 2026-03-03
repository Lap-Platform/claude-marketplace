---
name: checkouts
description: "Checkouts API skill. Use when working with Checkouts for checkouts. Covers 19 endpoints."
version: 1.0.0
generator: lapsh
---

# Checkouts
API version: 3.0

## Auth
ApiKey X-Auth-Token in header

## Base URL
https://api.bigcommerce.com/stores/{store_hash}/v3

## Setup
1. Set your API key in the appropriate header
2. GET /checkouts/settings -- verify access
3. POST /checkouts/{checkoutId}/discounts -- create first discounts

## Endpoints

19 endpoints across 1 groups. See references/api-spec.lap for full details.

### checkouts
| Method | Path | Description |
|--------|------|-------------|
| GET | /checkouts/{checkoutId} | Get a Checkout |
| PUT | /checkouts/{checkoutId} | Update Customer Messages |
| POST | /checkouts/{checkoutId}/discounts | Add Discount to Checkout |
| POST | /checkouts/{checkoutId}/billing-address | Add Checkout Billing Address |
| PUT | /checkouts/{checkoutId}/billing-address/{addressId} | Update Checkout Billing Address |
| POST | /checkouts/{checkoutId}/consignments | Add Consignment to Checkout |
| PUT | /checkouts/{checkoutId}/consignments/{consignmentId} | Update Checkout Consignment |
| DELETE | /checkouts/{checkoutId}/consignments/{consignmentId} | Delete Checkout Consignment |
| POST | /checkouts/{checkoutId}/coupons | Add Coupon to Checkout |
| DELETE | /checkouts/{checkoutId}/coupons/{couponCode} | Delete Checkout Coupon |
| POST | /checkouts/{checkoutId}/fees | Add order level fees to a checkout |
| PUT | /checkouts/{checkoutId}/fees | Update order level fees in a checkout |
| DELETE | /checkouts/{checkoutId}/fees | Delete order level fees from a checkout. |
| POST | /checkouts/{checkoutId}/orders | Create an Order |
| GET | /checkouts/settings | Get Checkout Settings |
| PUT | /checkouts/settings | Update Checkout Settings |
| GET | /checkouts/settings/channels/{channelId} | Get Channel-Specific Checkout Settings |
| PUT | /checkouts/settings/channels/{channelId} | Update Channel-Specific Checkout Settings |
| POST | /checkouts/{checkoutId}/token | Create Checkout Token |

## Enhanced Skill Content
## Question Mapping

- "How do I get the details of a checkout?" -> GET /checkouts/{checkoutId}
- "How do I update the customer message on a checkout?" -> PUT /checkouts/{checkoutId}
- "How do I apply a discount to a checkout or specific line items?" -> POST /checkouts/{checkoutId}/discounts
- "How do I set the billing address for a checkout?" -> POST /checkouts/{checkoutId}/billing-address
- "How do I update an existing billing address?" -> PUT /checkouts/{checkoutId}/billing-address/{addressId}
- "How do I add shipping information (consignment) to a checkout?" -> POST /checkouts/{checkoutId}/consignments
- "How do I change the shipping option or address on a consignment?" -> PUT /checkouts/{checkoutId}/consignments/{consignmentId}
- "How do I remove a consignment from a checkout?" -> DELETE /checkouts/{checkoutId}/consignments/{consignmentId}
- "How do I apply a coupon code to a checkout?" -> POST /checkouts/{checkoutId}/coupons
- "How do I remove a coupon from a checkout?" -> DELETE /checkouts/{checkoutId}/coupons/{couponCode}
- "How do I add fees (like handling or surcharges) to a checkout?" -> POST /checkouts/{checkoutId}/fees
- "How do I convert a checkout into an order?" -> POST /checkouts/{checkoutId}/orders
- "How do I get the custom checkout script settings?" -> GET /checkouts/settings
- "How do I generate a checkout token for a headless or embedded flow?" -> POST /checkouts/{checkoutId}/token
- "How do I configure checkout settings for a specific channel?" -> PUT /checkouts/settings/channels/{channelId}

## Response Tips

- **Checkout responses**: All mutating checkout endpoints return the full checkout object under `data` -- use this to refresh local state rather than making a follow-up GET. The `version` field enables optimistic concurrency; always read it from the response for your next write.
- **Order creation**: POST /orders returns only `{data: {id: int}}`, not the full order -- use the Orders API with the returned ID to fetch details.
- **Settings endpoints**: Return a flat config object under `data`; channel-specific settings return `any` (schema varies by channel type).
- **Token endpoint**: Returns `{checkoutToken: str}` at the top level (not nested under `data`), which differs from every other endpoint in this API.
- **Error handling**: 409 (Conflict) is the dominant error across write operations -- this signals a version mismatch. Re-fetch the checkout, grab the latest `version`, and retry. 404 on GET means the checkout expired or was already converted to an order.

## Anomaly Flags

- **409 Conflict on writes**: Surface immediately -- indicates a concurrent modification. Advise the user to re-read the checkout and retry with the current `version` value.
- **`order_id` is non-null**: The checkout has already been converted to an order. Further mutations will likely fail; direct the user to the Orders API instead.
- **`grand_total` is 0 or negative**: Flag as unusual -- may indicate over-applied discounts or misconfigured fees.
- **Empty `consignments` array when physical items exist**: Shipping has not been configured; the checkout cannot be finalized until at least one consignment with a shipping option is set.
- **`tax_total` is 0 with tax_included=false**: Taxes may not be calculating -- check that billing/shipping addresses have valid country and state codes.
- **401 on token generation**: Authentication credentials are invalid or lack sufficient scope; verify X-Auth-Token permissions.
- **422 on channel settings**: The channel ID does not exist or the payload structure is invalid for that channel type.

## Playbook

### Complete a Standard Checkout (Cart to Order)

1. Retrieve the checkout: GET /checkouts/{checkoutId} to confirm cart contents and get the current `version`.
2. Set billing address: POST /checkouts/{checkoutId}/billing-address with `email`, `country_code`, and address fields.
3. Create a consignment for shipping: POST /checkouts/{checkoutId}/consignments with line item IDs and a shipping address. Use `?include=consignments.available_shipping_options` to get options in the response.
4. Select a shipping option: PUT /checkouts/{checkoutId}/consignments/{consignmentId} with the chosen `shipping_option_id`.
5. (Optional) Apply a coupon: POST /checkouts/{checkoutId}/coupons with the `coupon_code`.
6. Review the checkout: GET /checkouts/{checkoutId} to verify totals.
7. Create the order: POST /checkouts/{checkoutId}/orders. Capture the returned `order_id` for payment processing.

### Apply Discounts to Specific Line Items

1. Retrieve the checkout: GET /checkouts/{checkoutId} to get line item IDs from `cart.line_items.physical_items` (or digital_items).
2. Note the current `version` from the response.
3. Apply discounts: POST /checkouts/{checkoutId}/discounts with `cart.line_items` array containing each `{id, discounted_amount}` and set `version` to the value from step 2.
4. Verify the `discount_amount` and `grand_total` in the response to confirm correct application.

### Manage Fees on a Checkout

1. Add fees: POST /checkouts/{checkoutId}/fees with an array of fee objects, each specifying `type`, `name`, `display_name`, `cost`, and `source`.
2. Verify fees appear in the checkout response under the `fees` array and that `grand_total` reflects them.
3. To update fees: PUT /checkouts/{checkoutId}/fees with the revised fee array (this replaces all fees).
4. To remove specific fees: DELETE /checkouts/{checkoutId}/fees with the `ids` array of fee IDs to remove.

### Configure Custom Checkout Scripts

1. Get current settings: GET /checkouts/settings to see existing script URLs and SRI hashes.
2. Update settings: PUT /checkouts/settings with the new `custom_checkout_script_url` and optionally `custom_checkout_sri_hash` for integrity verification.
3. For channel-specific overrides: PUT /checkouts/settings/channels/{channelId} with channel-level configuration.
4. Verify: GET /checkouts/settings (or /channels/{channelId}) to confirm the changes took effect.

### Generate a Checkout Token for Embedded/Headless Use

1. Ensure the checkout is ready: GET /checkouts/{checkoutId} to confirm billing address and consignments are set.
2. Generate a token: POST /checkouts/{checkoutId}/token with optional `maxUses` (number of times the token can be redeemed) and `ttl` (time-to-live in seconds).
3. Use the returned `checkoutToken` string to construct your embedded checkout URL or pass it to your frontend payment flow.
4. If you receive a 401, verify your X-Auth-Token has the required OAuth scopes for checkout token generation.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
