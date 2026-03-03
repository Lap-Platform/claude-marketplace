---
name: seatmap-display
description: "Seatmap Display API skill. Use when working with Seatmap Display for shopping. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Seatmap Display
API version: 1.9.2

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /shopping/seatmaps -- verify access
3. POST /shopping/seatmaps -- create first seatmaps

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### shopping
| Method | Path | Description |
|--------|------|-------------|
| GET | /shopping/seatmaps | Returns all the seat maps of a given order. |
| POST | /shopping/seatmaps | Returns all the seat maps of a given flightOffer. |

## Enhanced Skill Content
## Question Mapping

- "What seats are available on my booked flight?" -> GET /shopping/seatmaps
- "Show me the seatmap for a flight order" -> GET /shopping/seatmaps
- "Can I see seat availability using my flight order ID?" -> GET /shopping/seatmaps
- "Get seatmap details for flight order {id}" -> GET /shopping/seatmaps
- "Which seats are free, occupied, or blocked?" -> GET /shopping/seatmaps
- "What seat classes and amenities are available?" -> GET /shopping/seatmaps
- "Show me seatmaps for flights I haven't booked yet" -> POST /shopping/seatmaps
- "Get a seatmap using raw flight offer data" -> POST /shopping/seatmaps
- "Preview seat availability before booking" -> POST /shopping/seatmaps
- "Can I check seatmaps for multiple flight segments at once?" -> POST /shopping/seatmaps
- "What does the cabin layout look like for this aircraft?" -> GET /shopping/seatmaps
- "Are there any premium or extra-legroom seats available?" -> GET /shopping/seatmaps
- "Why did my seatmap request return a 404?" -> GET /shopping/seatmaps (flight order not found or expired)
- "How do I get seatmaps without a flight order ID?" -> POST /shopping/seatmaps (pass flight offer data in body)

## Response Tips

- **Seatmap responses (200):** Results contain nested `decks` -> `seats` arrays; each seat has availability status, cabin class, coordinates, and pricing. Check `travelerPricing` for per-seat cost breakdowns.
- **GET errors (400):** Malformed or missing `flightOrderId` parameter. Verify the ID format matches the Amadeus order reference pattern.
- **GET errors (404):** Flight order not found, expired, or belongs to a different credential scope. Confirm the order exists and was created under the same API credentials.
- **POST errors (400):** Invalid or incomplete flight offer body. Ensure the payload matches the structure returned by Flight Offers Search, including all required segments and traveler info.
- **POST header:** The `X-HTTP-Method-Override` header is mandatory; omitting it produces a 400 even if the body is valid.

## Anomaly Flags

- **404 on GET requests:** Surface immediately -- the flight order may have expired, been cancelled, or the ID is incorrect. Suggest verifying with the Flight Orders API.
- **Empty seat arrays:** If a 200 response returns decks with zero available seats, flag that the flight may be fully booked or seatmap data is unavailable for that aircraft type.
- **X-HTTP-Method-Override missing:** If a POST returns 400, check whether this required header was omitted before investigating body issues.
- **Dual parameter names:** The GET endpoint accepts both `flightOrderId` and `flight-orderId`. Flag if both are sent simultaneously -- behavior may be undefined.
- **Test vs production base URL:** The spec points to `test.api.amadeus.com`. Surface a warning if the caller intends production use, as test data is synthetic.
- **Rate limiting (429):** Amadeus APIs enforce rate limits. If responses slow down or return 429, surface the limit status and recommend backoff.

## Playbook

### 1. View Seatmap for a Booked Flight

1. Obtain the `flightOrderId` from a prior booking via the Flight Orders API
2. Call `GET /shopping/seatmaps?flightOrderId={id}`
3. Parse the response `data` array -- each entry represents one flight segment
4. Iterate through `decks[].seats[]` to display available, occupied, and blocked seats
5. Check `travelerPricing` for seat upgrade costs if applicable

### 2. Preview Seatmap Before Booking

1. Run a flight search using the Flight Offers Search API to get offer data
2. Set the `X-HTTP-Method-Override` header (required by the endpoint)
3. Call `POST /shopping/seatmaps` with the flight offer JSON as the request body
4. Parse the returned seatmap to display available seats and pricing
5. Use seat selection data to inform the subsequent booking request

### 3. Compare Seat Options Across Segments

1. For a multi-segment itinerary, call `GET /shopping/seatmaps?flightOrderId={id}`
2. The response returns one seatmap entry per segment in the `data` array
3. For each segment, extract `aircraft.code` to identify the plane type
4. Compare `decks[].seats[]` across segments to find consistent seat preferences (e.g., window, extra legroom)
5. Note pricing differences between segments for the same seat category

### 4. Handle Seatmap Unavailability Gracefully

1. Call `GET /shopping/seatmaps?flightOrderId={id}`
2. If a 404 is returned, verify the order ID is correct and the booking is still active
3. If a 200 returns with empty seat data, inform the user that seatmap data is not available for that aircraft or carrier
4. Fall back to displaying cabin class information from the original flight offer
5. Suggest contacting the airline directly for seat selection on unsupported routes


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
