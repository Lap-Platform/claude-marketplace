---
name: commerce-api
description: "Commerce API skill. Use when working with Commerce for commerce. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Commerce API
API version: v2

## Auth
ApiKey X-SSL-CERT-UID in header

## Base URL
https://www.ticketmaster.com/commerce/v2

## Setup
1. Set your API key in the appropriate header
2. GET /commerce/v2/events/{eventId}/offers -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### commerce
| Method | Path | Description |
|--------|------|-------------|
| GET | /commerce/v2/events/{eventId}/offers | Event Offers |

## Enhanced Skill Content
## Question Mapping

- "What offers are available for this event?" -> GET /commerce/v2/events/{eventId}/offers
- "Show me ticket prices for event X" -> GET /commerce/v2/events/{eventId}/offers
- "What ticket types can I buy for this concert?" -> GET /commerce/v2/events/{eventId}/offers
- "Are there any VIP packages for event {id}?" -> GET /commerce/v2/events/{eventId}/offers
- "What are the seating options and prices?" -> GET /commerce/v2/events/{eventId}/offers
- "Is this event sold out?" -> GET /commerce/v2/events/{eventId}/offers (check if offers array is empty)
- "What is the cheapest ticket for event X?" -> GET /commerce/v2/events/{eventId}/offers (sort/filter response by price)
- "Are there accessible seating offers for this event?" -> GET /commerce/v2/events/{eventId}/offers (filter for ADA/accessible offers)
- "What payment methods are accepted for this event?" -> GET /commerce/v2/events/{eventId}/offers (inspect payment fields in response)
- "How many tickets can I buy at once for event X?" -> GET /commerce/v2/events/{eventId}/offers (check quantity limits in offer details)
- "Are there any presale offers available?" -> GET /commerce/v2/events/{eventId}/offers (filter by offer type/access restrictions)
- "What are the fees on top of ticket price?" -> GET /commerce/v2/events/{eventId}/offers (inspect fee/charge breakdowns per offer)
- "Can I get a group discount for this event?" -> GET /commerce/v2/events/{eventId}/offers (look for group or bulk pricing tiers)

## Response Tips

- **Offers endpoint**: Response nests offer details inside an `offers` array -- each entry may contain price ranges, availability counts, seat maps, and fee breakdowns. Always check both `attributes` and nested `prices` objects for the full cost picture. An empty offers array typically means sold out or not yet on sale, not an error. A 200 with no offers is semantically different from a 404 (event not found).

## Anomaly Flags

- **Empty offers on a future event**: Surface when the event date is upcoming but zero offers are returned -- likely means tickets are not yet on sale or access is restricted.
- **Authentication failures (401/403)**: Flag immediately if X-SSL-CERT-UID or api-key is rejected -- the user may need to rotate credentials or check certificate configuration.
- **Unusual 200 with partial data**: If offers come back but critical fields (prices, availability) are null or missing, warn the user that the response may be incomplete.
- **Rate limiting (429)**: Surface proactively with retry-after timing so the caller can back off appropriately.
- **Deprecated fields in response**: If any offer object contains fields marked deprecated or legacy naming conventions, flag them so consumers can update integrations.
- **Event ID mismatch**: If the response event metadata does not match the requested eventId, flag as a potential routing or data integrity issue.

## Playbook

### 1. Check ticket availability for a specific event

1. Obtain the `eventId` from the Ticketmaster Discovery API or event URL
2. Call `GET /commerce/v2/events/{eventId}/offers` with your `X-SSL-CERT-UID` header
3. Inspect the `offers` array in the response
4. If empty, the event is sold out or not on sale -- check event status metadata
5. If populated, review each offer's availability count and price range

### 2. Find the best-priced ticket

1. Call `GET /commerce/v2/events/{eventId}/offers` with authentication headers
2. Iterate through all returned offers
3. For each offer, extract the base price and any fee/surcharge breakdowns
4. Compute total cost (base + fees) per offer
5. Sort by total cost ascending and present the lowest option to the user

### 3. Validate API credentials

1. Pick a known valid `eventId` (use a current, popular event)
2. Call `GET /commerce/v2/events/{eventId}/offers` with `X-SSL-CERT-UID` set
3. If 200: credentials are valid
4. If 401/403: check that the certificate UID is correct and not expired
5. Optionally test with `api-key` query param as a fallback auth method

### 4. Monitor offer changes over time

1. Call `GET /commerce/v2/events/{eventId}/offers` and store the full response
2. Wait a defined interval (e.g., 15 minutes)
3. Call the same endpoint again
4. Diff the two responses: compare offer counts, price changes, and availability shifts
5. Surface any new offers, removed offers, or significant price movements to the user

### 5. Retrieve offers with access token authentication

1. Obtain an `access_token` through the Ticketmaster OAuth flow
2. Call `GET /commerce/v2/events/{eventId}/offers` passing `X-TM-ACCESS-TOKEN` header or `access_token` query param
3. This may unlock presale or member-exclusive offers not visible with standard API key auth
4. Compare results against a standard API key call to identify access-restricted offers
5. Present exclusive offers separately with a note about their access requirements


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
