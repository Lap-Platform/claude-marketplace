---
name: negotiation-api
description: "Negotiation API skill. Use when working with Negotiation for find_eligible_items, send_offer_to_interested_buyers. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Negotiation API
API version: v1.1.0

## Auth
OAuth2

## Base URL
https://api.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /find_eligible_items -- verify access
3. POST /send_offer_to_interested_buyers -- create first send_offer_to_interested_buyers

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### find_eligible_items
| Method | Path | Description |
|--------|------|-------------|
| GET | /find_eligible_items | This method evaluates a seller's current listings and returns the set of IDs that are eligible for a seller-initiated discount offer to a buyer.  <br><br>A listing ID is returned only when one or more buyers have shown an "interest" in the listing.  <br><br>If any buyers have shown interest in a listing, the seller can initiate a "negotiation" with them by calling <a href="/api-docs/sell/negotiation/resources/offer/methods/sendOfferToInterestedBuyers">sendOfferToInterestedBuyers</a>, which sends all interested buyers a message that offers the listing at a discount.  <br><br>For details about how to create seller offers to buyers, see <a href="/api-docs/sell/static/marketing/offers-to-buyers.html" title="Selling Integration Guide">Sending offers to buyers</a>. |

### send_offer_to_interested_buyers
| Method | Path | Description |
|--------|------|-------------|
| POST | /send_offer_to_interested_buyers | This method sends eligible buyers offers to purchase items in a listing at a discount.  <br><br>When a buyer has shown <i>interest</i> in a listing, they become "eligible" to receive a seller-initiated offer to purchase the item(s).  <br><br>Sellers use <a href="/api-docs/sell/negotiation/resources/offer/methods/findEligibleItems">findEligibleItems</a> to get the set of listings that have interested buyers. If a listing has interested buyers, sellers can use this method (<b>sendOfferToInterestedBuyers</b>) to send an offer to the buyers who are interested in the listing. The offer gives buyers the ability to purchase the associated listings at a discounted price.  <br><br>For details about how to create seller offers to buyers, see <a href="/api-docs/sell/static/marketing/offers-to-buyers.html" title="Selling Integration Guide">Sending offers to buyers</a>. |

## Enhanced Skill Content
## Question Mapping

- "What items can I send offers on?" -> GET /find_eligible_items
- "Show me my eligible negotiation items" -> GET /find_eligible_items
- "Which of my listings support buyer offers?" -> GET /find_eligible_items
- "Get the next page of eligible items" -> GET /find_eligible_items (with offset)
- "How many items are eligible for negotiation?" -> GET /find_eligible_items (check total field)
- "Send a discount offer to interested buyers" -> POST /send_offer_to_interested_buyers
- "Offer 10% off to watchers of my listing" -> POST /send_offer_to_interested_buyers
- "Send a price reduction to buyers watching item X" -> POST /send_offer_to_interested_buyers
- "Can I allow counter-offers on my negotiation?" -> POST /send_offer_to_interested_buyers (set allowCounterOffer)
- "Send offers on multiple listings at once" -> POST /send_offer_to_interested_buyers (multiple offeredItems)
- "Set a custom offer duration for buyers" -> POST /send_offer_to_interested_buyers (offerDuration field)
- "First check eligible items, then send offers to watchers" -> GET /find_eligible_items then POST /send_offer_to_interested_buyers

## Response Tips

- **Eligible items (GET):** Paginated via `limit`/`offset` params; follow `next`/`prev` URLs for navigation. A 204 means no eligible items exist -- not an error. The `total` field gives the full count regardless of page size.
- **Send offers (POST):** Returns an `offers` array with per-item results; inspect each entry for individual success/failure. A 409 Conflict means an offer already exists for that listing or buyer combination.

## Anomaly Flags

- **204 on eligible items**: No eligible items found. Surface this clearly -- the seller may need to adjust listing settings or wait for buyer interest.
- **409 Conflict on send offer**: An active offer already exists. Alert the user that they must wait for the prior offer to expire or be declined before resending.
- **400 errors on either endpoint**: Likely a missing or malformed `X-EBAY-C-MARKETPLACE-ID` header, or invalid listing IDs. Surface the specific error fields from the response body.
- **500 errors**: eBay platform issue. Recommend retry with backoff. Flag if it occurs more than once in succession.
- **Discount percentage sanity check**: If `discountPercentage` exceeds typical thresholds (e.g., >50%), warn the seller before sending.
- **Empty offeredItems array**: The POST will likely fail. Flag before making the call.

## Playbook

### 1. Send Offers to All Eligible Buyers

1. Call `GET /find_eligible_items` with `X-EBAY-C-MARKETPLACE-ID` header set to target marketplace (e.g., `EBAY_US`)
2. If 204, stop -- no eligible items available
3. Page through results using `next` URL until all items are collected
4. For each eligible item, build an entry in the `offeredItems` array with listing ID, desired discount or price, and quantity
5. Call `POST /send_offer_to_interested_buyers` with the constructed payload
6. Inspect each entry in the `offers` response array to confirm per-item success

### 2. Send a Targeted Offer on a Single Listing

1. Call `GET /find_eligible_items` to confirm the target listing ID appears in results
2. Build the POST body with a single entry in `offeredItems` containing the listing ID and desired price/discount
3. Optionally set `allowCounterOffer: true` and a custom `message` for the buyer
4. Set `offerDuration` (e.g., `{unit: "HOUR", value: 48}`) to control how long the offer stays open
5. Call `POST /send_offer_to_interested_buyers` and verify the response

### 3. Paginate Through Large Eligible Item Lists

1. Call `GET /find_eligible_items` with `limit=50&offset=0`
2. Read the `total` field to determine how many items exist overall
3. Follow the `next` URL in each response to advance through pages
4. Accumulate items from `eligibleItems` across all pages
5. Stop when `next` is absent or offset equals total

### 4. Handle Offer Conflicts Gracefully

1. Attempt `POST /send_offer_to_interested_buyers` with desired items
2. If 409 is returned, parse the error response to identify which listing(s) have active offers
3. Remove conflicting listings from the `offeredItems` array
4. Retry with the remaining items
5. Track conflicting listings for later retry once prior offers expire


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
