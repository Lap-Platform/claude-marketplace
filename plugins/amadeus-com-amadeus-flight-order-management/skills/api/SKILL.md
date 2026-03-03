---
name: flight-order-management
description: "Flight Order Management API skill. Use when working with Flight Order Management for booking. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Flight Order Management
API version: 1.10.0

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /booking/flight-orders/{flight-orderId} -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### booking
| Method | Path | Description |
|--------|------|-------------|
| GET | /booking/flight-orders/{flight-orderId} | Retrieve a given flight order |
| DELETE | /booking/flight-orders/{flight-orderId} | Cancel a given flight order |

## Enhanced Skill Content
## Question Mapping

- "How do I retrieve a flight order?" -> GET /booking/flight-orders/{flight-orderId}
- "Get the details of my booking" -> GET /booking/flight-orders/{flight-orderId}
- "Look up a flight order by ID" -> GET /booking/flight-orders/{flight-orderId}
- "What's the status of flight order ABC123?" -> GET /booking/flight-orders/{flight-orderId}
- "Show me passenger details for a booking" -> GET /booking/flight-orders/{flight-orderId}
- "Cancel a flight order" -> DELETE /booking/flight-orders/{flight-orderId}
- "Delete my booking" -> DELETE /booking/flight-orders/{flight-orderId}
- "How do I cancel a reservation?" -> DELETE /booking/flight-orders/{flight-orderId}
- "Remove flight order and confirm it's gone" -> DELETE /booking/flight-orders/{flight-orderId}, then GET /booking/flight-orders/{flight-orderId} (expect 404)
- "Check if a flight order exists" -> GET /booking/flight-orders/{flight-orderId} (200 = exists, 404 = not found)
- "Verify a cancellation went through" -> GET /booking/flight-orders/{flight-orderId} (expect 404 after DELETE)
- "What happens if I try to cancel a non-existent order?" -> DELETE /booking/flight-orders/{flight-orderId} (expect 404)

## Response Tips

- **GET /booking/flight-orders/{flight-orderId}**: Returns full order object on 200. Check nested `travelers`, `flightOffers`, and `ticketingAgreement` fields for complete booking details. A 404 means the order ID is invalid or the order has been cancelled.
- **DELETE /booking/flight-orders/{flight-orderId}**: Returns 204 with no body on success -- do not attempt to parse the response. A 400 typically means the order is in a state that prevents cancellation (e.g., already departed or partially used).
- **Error responses (400, 404)**: Amadeus errors return a JSON body with `errors[]` array. Each entry has `status`, `code`, `title`, and `detail` fields. Always surface `detail` to the user -- `title` alone is often too generic.

## Anomaly Flags

- **404 on GET after a recent booking**: The order may have been auto-cancelled due to ticketing deadline expiry. Surface this proactively.
- **400 on DELETE**: Likely means the order is non-cancellable (already flown, agency-restricted, or requires manual intervention). Flag the specific error `code` to the user.
- **Repeated 400 errors**: May indicate an expired or invalid OAuth token rather than a true client error. Suggest re-authenticating.
- **DELETE returning non-204 success codes**: Unexpected. Flag as a possible API version mismatch.
- **Missing fields in GET response**: If `ticketingAgreement` or `price` objects are absent, the order may be in an incomplete state. Alert the user.

## Playbook

### 1. Retrieve and Review a Flight Order

1. Call GET /booking/flight-orders/{flight-orderId} with the order ID
2. Check the response status -- 200 means the order exists
3. Extract key details: traveler names, itinerary segments, pricing, and ticketing deadline
4. Review `ticketingAgreement.dateTime` to confirm whether ticketing is still pending

### 2. Cancel a Flight Order

1. Call GET /booking/flight-orders/{flight-orderId} to confirm the order exists and review its current state
2. Verify the order is eligible for cancellation (check ticketing status and departure dates)
3. Call DELETE /booking/flight-orders/{flight-orderId}
4. Confirm a 204 response (no body expected)
5. Optionally call GET /booking/flight-orders/{flight-orderId} to verify it now returns 404

### 3. Verify a Cancellation

1. Call GET /booking/flight-orders/{flight-orderId} with the cancelled order's ID
2. Expect a 404 response confirming the order no longer exists
3. If a 200 is returned, the cancellation may not have been processed -- retry the DELETE or investigate the error

### 4. Handle a Failed Cancellation

1. Attempt DELETE /booking/flight-orders/{flight-orderId}
2. If a 400 is returned, parse the `errors[].detail` field for the reason
3. If the error indicates a non-cancellable state, call GET /booking/flight-orders/{flight-orderId} to check the order status
4. Surface the cancellation restriction to the user with the specific reason from the error detail
5. Advise contacting the airline or travel agency directly if programmatic cancellation is blocked


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
