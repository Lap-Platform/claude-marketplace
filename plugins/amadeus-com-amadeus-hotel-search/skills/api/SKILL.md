---
name: hotel-search-api
description: "Hotel Search API skill. Use when working with Hotel Search for shopping. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Hotel Search API
API version: 3.0.9

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v3

## Setup
1. No auth setup needed
2. GET /shopping/hotel-offers -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### shopping
| Method | Path | Description |
|--------|------|-------------|
| GET | /shopping/hotel-offers | getMultiHotelOffers |
| GET | /shopping/hotel-offers/{offerId} | getOfferPricing |

## Enhanced Skill Content
## Question Mapping

- "What hotels are available in Paris for next weekend?" -> GET /shopping/hotel-offers
- "Show me hotel offers for a specific hotel ID" -> GET /shopping/hotel-offers
- "What rooms are available for 2 adults?" -> GET /shopping/hotel-offers
- "Find hotels under $200 per night in USD" -> GET /shopping/hotel-offers
- "What board types (breakfast, all-inclusive) are available at this hotel?" -> GET /shopping/hotel-offers
- "Are there any hotels with free cancellation?" -> GET /shopping/hotel-offers
- "Show me the cheapest rate for hotel MCLONGHM" -> GET /shopping/hotel-offers
- "Get full details for a specific hotel offer I found" -> GET /shopping/hotel-offers/{offerId}
- "Is this offer still valid?" -> GET /shopping/hotel-offers/{offerId}
- "What's the cancellation policy on offer ABC123?" -> GET /shopping/hotel-offers/{offerId}
- "Search multiple hotels at once and compare prices" -> GET /shopping/hotel-offers
- "Find hotels that accept pay-at-property" -> GET /shopping/hotel-offers
- "Show me all offers including sold-out rooms" -> GET /shopping/hotel-offers
- "Get hotel prices in EUR instead of the default currency" -> GET /shopping/hotel-offers

## Response Tips

- **Hotel offers listing** (`GET /shopping/hotel-offers`): Returns an array of hotel objects, each containing nested `offers[]` with price, room, and policy details. When `bestRateOnly` is true (default), only the cheapest offer per hotel is returned. Check `dictionaries` in the response for decoded room type and board type codes.
- **Single offer detail** (`GET /shopping/hotel-offers/{offerId}`): Returns a single offer with full pricing breakdown, cancellation policies, and payment info. The `offerId` is ephemeral and expires -- a 404 means the offer is no longer available, not that the ID was wrong.
- **Errors (400)**: Typically malformed parameters -- check `errors[].detail` for which field failed validation. Common culprits: invalid date format (expects YYYY-MM-DD), `hotelIds` exceeding max batch size, or unsupported currency codes.
- **Errors (500)**: Upstream provider failures -- safe to retry with exponential backoff.

## Anomaly Flags

- **Offer expiration**: `offerId` values are short-lived. Surface a warning if a user tries to reference an offer retrieved more than 15 minutes ago, as it likely expired (will return 404).
- **Empty offers array**: If a hotel returns with zero offers, flag that the property may be sold out for the requested dates. Suggest setting `includeClosed: true` to confirm.
- **Currency mismatch**: If the user asks for prices in one currency but the response returns a different one, flag this -- it may indicate the hotel only prices in its local currency.
- **Rate limiting (429 or repeated 500s)**: Surface immediately and suggest spacing requests. Amadeus test environments have tight rate limits.
- **Price range filtering**: If `priceRange` returns zero results but the same search without it returns offers, flag that the budget may be unrealistic for the selected hotels.
- **bestRateOnly masking results**: When enabled (default), many offers are hidden. If the user seems to want comprehensive options, suggest setting `bestRateOnly: false`.

## Playbook

### 1. Search and Book Flow

1. Gather hotel IDs from a separate hotel list/search API (outside this spec's scope).
2. Call `GET /shopping/hotel-offers` with `hotelIds`, `checkInDate`, `checkOutDate`, and `adults`.
3. Parse the `offers[]` array from each hotel in the response.
4. Pick an offer and extract its `offerId`.
5. Call `GET /shopping/hotel-offers/{offerId}` to get full details and confirm availability before booking.

### 2. Price Comparison Across Hotels

1. Collect multiple hotel IDs (up to the API's batch limit).
2. Call `GET /shopping/hotel-offers` with all IDs, setting `bestRateOnly: true` and a target `currency`.
3. Extract `price.total` from each hotel's best offer.
4. Sort and present results by price.
5. For the top picks, call `GET /shopping/hotel-offers/{offerId}` to verify the rate is still live.

### 3. Finding Budget-Friendly Options

1. Call `GET /shopping/hotel-offers` with `hotelIds`, dates, and `priceRange` set (e.g., `100-200`).
2. Set `currency` to the user's preferred currency.
3. If zero results, retry without `priceRange` to see actual pricing and adjust expectations.
4. Set `paymentPolicy: NONE` to filter for pay-at-property options (no prepayment).
5. Review `boardType` values in results to find deals that include meals.

### 4. Checking Offer Validity

1. Retrieve the `offerId` from a previous search result.
2. Call `GET /shopping/hotel-offers/{offerId}`.
3. If 200: the offer is still available -- review updated price and policies.
4. If 404: the offer expired. Re-run the original `GET /shopping/hotel-offers` search to get fresh offers.
5. Compare the new price against the original to flag any changes.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
