---
name: hotel-booking
description: "Hotel Booking API skill. Use when working with Hotel Booking for booking. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Hotel Booking
API version: 1.1.3

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
3. POST /booking/hotel-bookings -- create first hotel-bookings

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### booking
| Method | Path | Description |
|--------|------|-------------|
| POST | /booking/hotel-bookings | Create Orders associated to the Hotel Offers |

## Enhanced Skill Content
## Question Mapping

- "How do I book a hotel?" -> POST /booking/hotel-bookings
- "How do I create a hotel reservation?" -> POST /booking/hotel-bookings
- "Can I book multiple rooms at once?" -> POST /booking/hotel-bookings (multiple roomAssociations in requestBody)
- "How do I specify guest details for a booking?" -> POST /booking/hotel-bookings (guests array in requestBody)
- "How do I pass payment information when booking?" -> POST /booking/hotel-bookings (payments array in requestBody)
- "What fields are required to complete a hotel booking?" -> POST /booking/hotel-bookings (requestBody is required; needs offerId, guests, payments)
- "How do I add special requests to a booking?" -> POST /booking/hotel-bookings (remarks field in requestBody)
- "Can I book using a previously retrieved offer ID?" -> POST /booking/hotel-bookings (reference offerId from Hotel Search/Shopping APIs)
- "What happens if my booking fails?" -> POST /booking/hotel-bookings (check 400/500 error responses)
- "How do I confirm a hotel reservation after shopping?" -> POST /booking/hotel-bookings (final step after offer search and price confirmation)
- "How do I associate guests with specific rooms?" -> POST /booking/hotel-bookings (roomAssociations maps guestReferences to hotelOfferId)
- "What payment methods does the booking API accept?" -> POST /booking/hotel-bookings (payments object with method, card details)
- "How do I book a hotel for someone else?" -> POST /booking/hotel-bookings (set guest name/contact different from payment holder)

## Response Tips

- **201 Created**: Successful booking returns a `data` array with booking confirmations including `id` (booking reference), `providerConfirmationId` (hotel's own reference), and `associatedRecords`. Always store both IDs for downstream operations.
- **400 Bad Request**: Returns structured error with `errors[]` array. Each error includes `code`, `title`, and `detail`. Common causes: expired offer ID, invalid payment data, missing required guest fields. Check `error.source.parameter` to identify the offending field.
- **500 Server Error**: Indicates upstream hotel system failure. The booking may or may not have been created on the hotel side. Retry with caution and verify with the provider before re-booking to avoid duplicates.

## Anomaly Flags

- **Expired Offer ID**: Hotel offers from the Shopping API are time-limited (typically 10-30 minutes). If a 400 error references an invalid or expired offer, surface this immediately and recommend re-running the hotel search flow.
- **Price Discrepancy**: If the booking response total differs from the quoted shopping price, flag the difference to the user before considering the booking final.
- **Missing Provider Confirmation**: A 201 response without a `providerConfirmationId` may indicate the hotel has not yet confirmed. Flag as "pending confirmation" and recommend follow-up.
- **Rate Limit Headers**: Monitor `X-RateLimit-Remaining` headers. Surface a warning when below 20% of the allowed quota to avoid mid-workflow failures.
- **Partial Booking Failures**: When booking multiple rooms, some may succeed while others fail. Flag any mismatch between requested rooms and confirmed bookings in the response.
- **500 with Ambiguous State**: After a server error, warn the user that the booking may have been partially processed upstream. Recommend checking booking status before retrying.

## Playbook

### 1. Complete Hotel Booking (End-to-End)

1. Retrieve a hotel offer ID from the Hotel Shopping API (separate API - hotel-offers)
2. Confirm the offer price is still valid using the Hotel Offer Price API
3. Build the request body with `offerId`, `guests` (name, contact, documents), and `payments` (method, card info)
4. Call `POST /booking/hotel-bookings` with the complete request body
5. Store the returned `id` and `providerConfirmationId` from the response
6. Confirm the booking status is active in the response data

### 2. Booking with Special Requests

1. Prepare the standard booking payload (offerId, guests, payments)
2. Add a `remarks` object with `comment` field containing the special request (e.g., "late check-in", "high floor")
3. Call `POST /booking/hotel-bookings`
4. Verify the response includes the remarks to confirm they were registered
5. Note: special requests are not guaranteed by the hotel - advise the user accordingly

### 3. Multi-Room Group Booking

1. Obtain multiple offer IDs from the Shopping API (one per room type/configuration)
2. Build `roomAssociations` array mapping each `hotelOfferId` to its `guestReferences`
3. Include all guests in the top-level `guests` array with unique `guestReference` IDs
4. Submit the single `POST /booking/hotel-bookings` request with all rooms
5. Validate the response contains confirmations for every requested room
6. If partial failure occurs, identify which rooms were confirmed and handle unconfirmed rooms separately

### 4. Handling Booking Errors and Recovery

1. Attempt `POST /booking/hotel-bookings` with the prepared payload
2. On 400: parse `errors[]` array, identify the failing field from `source.parameter`
3. For expired offers: return to the Shopping API, retrieve a fresh offer, and retry
4. For invalid payment: correct card details or payment method and resubmit
5. On 500: wait 30 seconds, then check if a booking was created before retrying to avoid duplicates


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
