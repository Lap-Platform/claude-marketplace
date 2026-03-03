---
name: flight-create-orders
description: "Flight Create Orders API skill. Use when working with Flight Create Orders for booking. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Flight Create Orders
API version: 1.10.0

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
3. POST /booking/flight-orders -- create first flight-orders

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### booking
| Method | Path | Description |
|--------|------|-------------|
| POST | /booking/flight-orders | Create Order associated to the Flight offers. |

## Enhanced Skill Content
## Question Mapping

- "How do I book a flight?" -> POST /booking/flight-orders
- "How do I create a flight order?" -> POST /booking/flight-orders
- "Can I book multiple passengers on one reservation?" -> POST /booking/flight-orders (include multiple traveler objects in body)
- "How do I add contact information to a booking?" -> POST /booking/flight-orders (include contact in traveler remarks)
- "How do I book a round-trip flight?" -> POST /booking/flight-orders (include outbound and return flight offers in body)
- "How do I specify payment for a flight booking?" -> POST /booking/flight-orders (include payment object in body)
- "Can I add special service requests like wheelchair or meal preference?" -> POST /booking/flight-orders (include SSR in remarks)
- "How do I book using a flight offer from the search results?" -> POST /booking/flight-orders (pass flightOffers array from Flight Offers Search response)
- "What happens if the price changed since I searched?" -> POST /booking/flight-orders (API validates pricing; returns 400 if offer expired)
- "How do I add frequent flyer numbers to a booking?" -> POST /booking/flight-orders (include loyaltyProgram in traveler object)
- "Can I book a one-way multi-city itinerary?" -> POST /booking/flight-orders (include multiple flight offers in the request body)
- "What fields are required to create a flight order?" -> POST /booking/flight-orders (body with flightOffers and travelers at minimum)

## Response Tips

- **201 Created**: Response contains the full flight order with `id`, `associatedRecords` (PNR locators), `travelers`, and `flightOffers` with confirmed pricing. Extract `data.id` for future reference and `data.associatedRecords[].reference` for airline confirmation codes.
- **400 Bad Request**: Check `errors[]` array -- each entry has `detail`, `code`, and `source.pointer` indicating which field failed. Common causes: expired offer, missing traveler info, invalid payment, or price mismatch since search.

## Anomaly Flags

- **Expired flight offers**: If a 400 error mentions offer validity or pricing, surface that the user should re-run Flight Offers Search before retrying.
- **Price discrepancies**: Compare `flightOffers[].price.grandTotal` in the response against the original search result; flag if the confirmed price differs.
- **Missing PNR references**: If `associatedRecords` is empty or missing in a 201 response, warn that the booking may not have been fully ticketed by the airline.
- **Partial traveler failures**: If the response includes `warnings[]`, surface them immediately -- they may indicate issues with specific passengers or segments.
- **Rate limiting (429)**: Although not declared in the spec, Amadeus test/production APIs enforce rate limits. Surface any 429 responses with retry-after guidance.

## Playbook

### 1. Book a Simple One-Way Flight

1. Obtain a valid OAuth token for the Amadeus API.
2. Search for flights using the Flight Offers Search endpoint to get available `flightOffers`.
3. Optionally price the selected offer using Flight Offers Price to confirm current pricing.
4. Call `POST /booking/flight-orders` with a body containing the selected `flightOffers` array, `travelers` (name, dateOfBirth, gender, contact), and `remarks`.
5. Extract `data.id` and `data.associatedRecords[].reference` from the 201 response for confirmation.

### 2. Book a Round-Trip for Multiple Passengers

1. Search for outbound and return flights, collecting the paired `flightOffers`.
2. Build the request body with both offers in the `flightOffers` array.
3. Add each passenger as a separate entry in the `travelers` array, each with unique `id`, full name, documents (passport), and contact info.
4. Call `POST /booking/flight-orders` with the assembled body.
5. Verify each traveler appears in the response and note individual PNR references if airlines differ per segment.

### 3. Handle a Failed Booking Gracefully

1. Attempt `POST /booking/flight-orders` with the desired flight offer and traveler data.
2. If a 400 error is returned, parse `errors[].detail` and `errors[].source.pointer` to identify the failing field.
3. If the error indicates an expired or repriced offer, re-run Flight Offers Search and Flight Offers Price.
4. Correct any traveler data issues (missing documents, invalid date formats, incomplete contact).
5. Retry the booking with the updated payload.

### 4. Add Loyalty Programs and Special Requests

1. Build the standard booking request with `flightOffers` and `travelers`.
2. For each traveler, include a `loyaltyPrograms` array with `programOwner` (airline code) and `id` (membership number).
3. Add special service requests under `remarks.general` with `subType: "GENERAL_MISCELLANEOUS"` and the request text.
4. Call `POST /booking/flight-orders` and confirm the loyalty and SSR details appear in the response.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
