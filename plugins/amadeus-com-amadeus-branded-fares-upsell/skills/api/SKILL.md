---
name: branded-fares-upsell
description: "Branded Fares Upsell API skill. Use when working with Branded Fares Upsell for shopping. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Branded Fares Upsell
API version: 1.2.0

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
3. POST /shopping/flight-offers/upselling -- create first upselling

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### shopping
| Method | Path | Description |
|--------|------|-------------|
| POST | /shopping/flight-offers/upselling | Return a list of upsell Flight Offers based on given Flight Offers |

## Enhanced Skill Content
## Question Mapping

- "How do I get branded fare options for a flight?" -> POST /shopping/flight-offers/upselling
- "Can I upsell a flight offer to a higher cabin class?" -> POST /shopping/flight-offers/upselling
- "What premium fare options are available for my booking?" -> POST /shopping/flight-offers/upselling
- "How do I compare economy vs business fares for a specific flight?" -> POST /shopping/flight-offers/upselling
- "What additional fare bundles can I offer a traveler?" -> POST /shopping/flight-offers/upselling
- "How do I retrieve upsell options from an existing flight search result?" -> POST /shopping/flight-offers/upselling
- "What branded fare families are available on this itinerary?" -> POST /shopping/flight-offers/upselling
- "Can I get baggage and seat selection upgrades for a flight offer?" -> POST /shopping/flight-offers/upselling
- "How do I pass a flight offer to get higher-tier alternatives?" -> POST /shopping/flight-offers/upselling
- "What does the X-HTTP-Method-Override header do for upselling?" -> POST /shopping/flight-offers/upselling
- "Why is my upsell request returning 400?" -> POST /shopping/flight-offers/upselling
- "How do I chain a flight search with upsell in one workflow?" -> Step 1: Flight Offers Search API, Step 2: POST /shopping/flight-offers/upselling

## Response Tips

- **Upsell offers (200):** Response contains an array of enriched flight offers with branded fare details, fare breakdowns, and included services (bags, seats, flexibility). Each upsell option references the original offer -- compare by `source` and `pricingOptions` fields. Price differences are absolute, not deltas; calculate savings client-side.
- **Validation errors (400):** Inspect `errors[].detail` for the specific field that failed. Common causes: malformed flight offer in the request body, missing required segments, or expired offer IDs from a prior search.

## Anomaly Flags

- **Expired flight offers:** If the input flight offer was retrieved more than 15-20 minutes ago, upsell results may be empty or stale. Surface a warning when no upsell options are returned.
- **Empty upsell array:** Some routes or carriers do not support branded fares. Flag when the response returns successfully but contains zero upsell alternatives.
- **X-HTTP-Method-Override required:** This header is mandatory. If omitted, the request may be silently misrouted. Flag any call missing this header before sending.
- **400 with no detail:** Occasionally the error response lacks granular field info. Surface the raw status and suggest validating the input flight offer structure.
- **Rate limiting (429):** Amadeus APIs enforce per-key rate limits. Surface `Retry-After` header value and queue subsequent requests accordingly.
- **Test vs production base URL:** The spec points to `test.api.amadeus.com`. Flag if the user intends production use, as test credentials return synthetic data.

## Playbook

### 1. Upsell a Flight Search Result

1. Obtain an OAuth2 token from `POST /v1/security/oauth2/token` using your Amadeus API key and secret.
2. Run a flight offers search (via the Flight Offers Search API) to get base flight offers.
3. Select one or more flight offers from the search results.
4. Send `POST /v1/shopping/flight-offers/upselling` with the selected offers in `upsellFlightOffersBody` and set `X-HTTP-Method-Override` header.
5. Parse the response to display branded fare alternatives sorted by price or included services.

### 2. Compare Branded Fare Tiers

1. Retrieve upsell options using the playbook above.
2. Group returned offers by `fareBasis` or branded fare family name.
3. Extract included services (checked bags, seat selection, rebooking flexibility) from each tier.
4. Present a side-by-side comparison table to the user with price deltas calculated from the original offer.

### 3. Handle Upsell Failures Gracefully

1. Send the upsell request and check the HTTP status code.
2. If 400: parse `errors[].detail`, validate that the input flight offer is well-formed and not expired, then retry with a fresh search result.
3. If 200 with an empty upsell array: inform the user that no branded fare upgrades are available for this route or carrier.
4. If 429: read the `Retry-After` header, wait the specified duration, and retry.

### 4. End-to-End Booking with Upsell

1. Search for flights using Flight Offers Search.
2. Call `POST /v1/shopping/flight-offers/upselling` to get premium alternatives.
3. Let the user select their preferred fare tier.
4. Confirm pricing with Flight Offers Price API using the selected upsell offer.
5. Create the booking via Flight Orders API with the confirmed and priced offer.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
