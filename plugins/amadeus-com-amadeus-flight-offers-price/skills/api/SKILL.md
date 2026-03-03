---
name: flight-offers-price
description: "Flight Offers Price API skill. Use when working with Flight Offers Price for shopping. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Flight Offers Price
API version: 1.3.0

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
3. POST /shopping/flight-offers/pricing -- create first pricing

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### shopping
| Method | Path | Description |
|--------|------|-------------|
| POST | /shopping/flight-offers/pricing | Confirm pricing of given flightOffers. |

## Enhanced Skill Content
## Question Mapping

- "How much does this flight actually cost?" -> POST /shopping/flight-offers/pricing
- "Can you confirm the price for these flight offers?" -> POST /shopping/flight-offers/pricing
- "What's the final price including taxes and fees?" -> POST /shopping/flight-offers/pricing
- "Has the price changed since I searched for flights?" -> POST /shopping/flight-offers/pricing
- "What are the baggage fees for this flight offer?" -> POST /shopping/flight-offers/pricing (with include=bags)
- "Show me the fare breakdown with detailed fees" -> POST /shopping/flight-offers/pricing (with include=detailed-fare-rules)
- "Can I get pricing for multiple flight offers at once?" -> POST /shopping/flight-offers/pricing (multiple offers in body)
- "What's the price if I force a specific booking class?" -> POST /shopping/flight-offers/pricing (with forceClass=true)
- "Are there additional charges beyond the base fare?" -> POST /shopping/flight-offers/pricing (with include=bags,detailed-fare-rules)
- "Validate whether this flight offer is still bookable" -> POST /shopping/flight-offers/pricing
- "What payment options are available for this itinerary?" -> POST /shopping/flight-offers/pricing (with include=credit-card-fees,other-services)
- "Get the real-time price for a round-trip I found earlier" -> POST /shopping/flight-offers/pricing

## Response Tips

- **Pricing responses (200):** Contains `flightOffers` array with updated prices - compare `price.grandTotal` against original search results to detect fare changes. Check `price.fees` and `price.additionalServices` for hidden costs. The `travelerPricings` array breaks down per-passenger costs.
- **Validation errors (400):** Look at `errors[].detail` for specifics - common causes are expired offers (search results older than ~15 min), invalid flight-offer structure, or unavailable booking classes. The `errors[].source.pointer` field pinpoints the malformed field.
- **Include extras:** When `include` params are used, supplementary data appears in `dictionaries` and within each offer's `travelerPricings[].fareDetailsBySegment` - these are nested deeply, so drill into segment-level details.

## Anomaly Flags

- **Price drift:** Surface when `grandTotal` in the pricing response differs from the original search result - fare changes between search and pricing are common and time-sensitive.
- **Offer expiration:** Flag if the API returns 400 with an expired-offer error - the user needs to re-search before pricing again.
- **Booking class override:** When `forceClass=true` is used and the response returns a different cabin or class than requested, alert the user that their preferred class is unavailable.
- **Missing segments:** If the priced offer returns fewer segments or different routing than the original search offer, surface this as a schedule change.
- **Rate limiting (429):** Amadeus enforces per-second and per-month quotas - proactively warn when responses slow down or when nearing known limits.
- **Deprecated fields:** Watch for `warnings[]` in responses - Amadeus uses this array to signal deprecated parameters or upcoming breaking changes.

## Playbook

### 1. Price a Flight from Search Results

1. Obtain flight offers via the Flight Offers Search endpoint
2. Select one or more offers from the search results
3. POST to `/shopping/flight-offers/pricing` with the selected offers in `priceFlightOffersBody`
4. Set `X-HTTP-Method-Override: GET` in the header
5. Compare `price.grandTotal` in the response to the original search price
6. If price changed, decide whether to proceed or re-search

### 2. Get Full Cost Breakdown with Bags and Fees

1. Take a flight offer from search results
2. POST to `/shopping/flight-offers/pricing` with `include=bags,detailed-fare-rules,credit-card-fees`
3. Review `travelerPricings[].fareDetailsBySegment` for per-segment fare rules
4. Check `additionalServices` for optional bag pricing
5. Present total cost as `grandTotal` plus any selected extras

### 3. Force a Specific Booking Class

1. Identify the desired booking class (e.g., economy restricted vs flexible)
2. POST to `/shopping/flight-offers/pricing` with `forceClass=true`
3. Verify the response contains the expected `fareDetailsBySegment[].class`
4. If the class was overridden by the airline, compare pricing to decide whether the alternative is acceptable

### 4. Batch Price Multiple Itineraries for Comparison

1. Collect 2-5 flight offers from search results
2. Include all offers in a single `priceFlightOffersBody` array
3. POST to `/shopping/flight-offers/pricing`
4. Extract `price.grandTotal` from each returned offer
5. Rank by total cost and present side-by-side with fare conditions

### 5. Handle Expired Offers Gracefully

1. POST to `/shopping/flight-offers/pricing` with a previously found offer
2. If response is 400 with an expiration error, notify the user the fare is no longer available
3. Re-run the original Flight Offers Search with the same criteria
4. Price the new results immediately to minimize expiration risk
5. Present refreshed pricing to the user


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
