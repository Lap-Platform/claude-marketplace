---
name: just-eat-api
description: "Just Eat API skill. Use when working with Just Eat for {tenant}, attempted-delivery-query-resolved, delivery-failed. Covers 98 endpoints."
version: 1.0.0
generator: lapsh
---

# Just Eat API
API version: 1.0.0

## Auth
ApiKey Authorization in header | Bearer basic | Bearer bearer | openIdConnect | Bearer bearer

## Base URL
https://uk.api.just-eat.io

## Setup
1. Set Authorization header with your Bearer token
2. GET /delivery/pools -- verify access
3. POST /{tenant}/orders/{orderId}/queries/attempteddelivery -- create first attempteddelivery

## Endpoints

98 endpoints across 33 groups. See references/api-spec.lap for full details.

### {tenant}
| Method | Path | Description |
|--------|------|-------------|
| POST | /{tenant}/orders/{orderId}/queries/attempteddelivery | Delivery Attempt Failed |
| POST | /{tenant}/orders/{orderId}/queries/attempteddelivery/resolution/redeliverorder | Request Redelivery of the Order |
| DELETE | /v1/{tenant}/restaurants/{id}/event/offline | Delete Offline Event |
| POST | /v1/{tenant}/restaurants/event/offline | Create Offline Event |

### attempted-delivery-query-resolved
| Method | Path | Description |
|--------|------|-------------|
| PUT | /attempted-delivery-query-resolved | Attempted delivery query resolved |

### delivery-failed
| Method | Path | Description |
|--------|------|-------------|
| PUT | /delivery-failed | Delivery Attempt Failed |

### checkout
| Method | Path | Description |
|--------|------|-------------|
| GET | /checkout/{tenant}/{checkoutId} | Get Checkout |
| PATCH | /checkout/{tenant}/{checkoutId} | Update Checkout |
| GET | /checkout/{tenant}/{checkoutId}/fulfilment/availabletimes | Get Available Fulfilment Times |

### orders
| Method | Path | Description |
|--------|------|-------------|
| POST | /orders/{tenant}/{orderId}/consumerqueries/lateorder/restaurantresponse | Response to Late Order Update Request |
| POST | /orders/{tenant}/{orderId}/consumerqueries/lateordercompensation/restaurantresponse | Update late order compensation request with Restaurant response |
| PUT | /orders/{orderId}/accept | Accept order |
| PUT | /orders/{orderId}/cancel | Cancel order |
| POST | /orders/{orderId}/complete | Complete order |
| PUT | /orders/{orderId}/duedate | Update order ETA |
| PUT | /orders/{orderId}/ignore | Ignore order |
| POST | /orders/{orderId}/readyforcollection | Mark order as ready for collection |
| PUT | /orders/{orderId}/reject | Reject order |
| PUT | /orders/{orderId}/deliverystate/atdeliveryaddress | Update order with driver at delivery address details |
| PUT | /orders/{orderId}/deliverystate/atrestaurant | Update order with driver at restaurant details |
| PUT | /orders/{orderId}/deliverystate/atrestauranteta | Update the driver's estimated time to arrive at the Restaurant |
| PUT | /orders/{orderId}/deliverystate/delivered | Update order with delivered details |
| PUT | /orders/{orderId}/deliverystate/driverassigned | Update order with driver assigned details |
| PUT | /orders/{orderId}/deliverystate/driverlocation | Update the driver's current location |
| PUT | /orders/{orderId}/deliverystate/driverunassigned | Update order with driver unassigned details |
| PUT | /orders/{orderId}/deliverystate/onitsway | Update order with driver on its way details |
| PUT | /orders/deliverystate/driverlocation | Update current driver locations (bulk upload) |
| POST | /orders | Create order |
| POST | /orders/{tenant}/{orderId}/restaurantqueries/compensation | Create Compensation requests |

### late-order-compensation-query
| Method | Path | Description |
|--------|------|-------------|
| POST | /late-order-compensation-query | late order compensation query, restaurant response required |

### late-order-query
| Method | Path | Description |
|--------|------|-------------|
| POST | /late-order-query | late order query, restaurant response required |

### consumers
| Method | Path | Description |
|--------|------|-------------|
| POST | /consumers/{tenant} | Create consumer |
| GET | /consumers/{tenant} | Get consumers details |
| GET | /consumers/{tenant}/me/communication-preferences | Get communication preferences |
| GET | /consumers/{tenant}/me/communication-preferences/{type} | Get channel subscriptions for a given consumer's communication preference type |
| PUT | /consumers/{tenant}/me/communication-preferences/{type} | Set only the channel subscriptions for a given consumer's communication preference type |
| POST | /consumers/{tenant}/me/communication-preferences/{type}/subscribedChannels/{channel} | Subscribe to a specific communication preference channel |
| DELETE | /consumers/{tenant}/me/communication-preferences/{type}/subscribedChannels/{channel} | Remove subscription of a specific communication preference channel |

### delivery-fees
| Method | Path | Description |
|--------|------|-------------|
| GET | /delivery-fees/{tenant} | Get restaurant delivery fees |

### delivery
| Method | Path | Description |
|--------|------|-------------|
| GET | /delivery/pools | Get your delivery pools |
| POST | /delivery/pools | Create a new delivery pool |
| GET | /delivery/pools/{deliveryPoolId} | Get an individual delivery pool |
| DELETE | /delivery/pools/{deliveryPoolId} | Delete a delivery pool |
| PATCH | /delivery/pools/{deliveryPoolId} | Modify a delivery pool |
| PUT | /delivery/pools/{deliveryPoolId} | Replace an existing delivery pool |
| GET | /delivery/pools/{deliveryPoolId}/availability/relative | Get availability for pickup |
| PUT | /delivery/pools/{deliveryPoolId}/availability/relative | Set availability for pickup |
| PUT | /delivery/pools/{deliveryPoolId}/hours | Set the delivery pools daily start and end times |
| PUT | /delivery/pools/{deliveryPoolId}/restaurants | Add restaurants to an existing delivery pool |
| DELETE | /delivery/pools/{deliveryPoolId}/restaurants | Remove restaurants from a delivery pool |
| GET | /delivery/estimate | Get delivery estimate |

### acceptance-requested
| Method | Path | Description |
|--------|------|-------------|
| POST | /acceptance-requested | Acceptance requested |

### order-accepted
| Method | Path | Description |
|--------|------|-------------|
| POST | /order-accepted | Order accepted |

### order-cancelled
| Method | Path | Description |
|--------|------|-------------|
| POST | /order-cancelled | Order cancelled |

### order-rejected
| Method | Path | Description |
|--------|------|-------------|
| POST | /order-rejected | Order rejected |

### redelivery-requested
| Method | Path | Description |
|--------|------|-------------|
| PUT | /redelivery-requested | Customer Requested Redelivery |

### driver-assigned-to-delivery
| Method | Path | Description |
|--------|------|-------------|
| PUT | /driver-assigned-to-delivery | Driver Assigned to Delivery |

### driver-at-delivery-address
| Method | Path | Description |
|--------|------|-------------|
| PUT | /driver-at-delivery-address | Driver at delivery address |

### driver-at-restaurant
| Method | Path | Description |
|--------|------|-------------|
| PUT | /driver-at-restaurant | Driver at restaurant |

### driver-has-delivered-order
| Method | Path | Description |
|--------|------|-------------|
| PUT | /driver-has-delivered-order | Driver has delivered order |

### driver-location
| Method | Path | Description |
|--------|------|-------------|
| PUT | /driver-location | Driver Location |

### driver-on-their-way-to-delivery-address
| Method | Path | Description |
|--------|------|-------------|
| PUT | /driver-on-their-way-to-delivery-address | Driver on their way to delivery address |

### order-is-ready-for-pickup
| Method | Path | Description |
|--------|------|-------------|
| PUT | /order-is-ready-for-pickup | Order ready for pickup |

### order-requires-delivery-acceptance
| Method | Path | Description |
|--------|------|-------------|
| PUT | /order-requires-delivery-acceptance | Order requires delivery acceptance |

### order-ready-for-preparation-async
| Method | Path | Description |
|--------|------|-------------|
| POST | /order-ready-for-preparation-async | Order ready for preparation (async) |

### order-ready-for-preparation-sync
| Method | Path | Description |
|--------|------|-------------|
| POST | /order-ready-for-preparation-sync | Order ready for preparation (sync) |

### send-to-pos-failed
| Method | Path | Description |
|--------|------|-------------|
| POST | /send-to-pos-failed | Send to POS failed |

### restaurants
| Method | Path | Description |
|--------|------|-------------|
| GET | /restaurants/{tenant}/{restaurantId}/customerclaims | Get claims |
| GET | /restaurants/{tenant}/{restaurantId}/customerclaims/{id} | Get order claim |
| POST | /restaurants/{tenant}/{restaurantId}/customerclaims/{id}/restaurantresponse | Submit a restaurant response for the claim |
| PUT | /restaurants/{tenant}/{restaurantId}/customerclaims/{id}/restaurantresponse/justification | Add reason and comments to the response |
| GET | /restaurants/{tenant}/{restaurantId}/catalogue | Get product catalogue |
| GET | /restaurants/{tenant}/{restaurantId}/catalogue/availabilities | Get all availabilities |
| GET | /restaurants/{tenant}/{restaurantId}/catalogue/categories | Get all categories |
| GET | /restaurants/{tenant}/{restaurantId}/catalogue/categories/{categoryId}/items | Get all category item IDs |
| GET | /restaurants/{tenant}/{restaurantId}/catalogue/items | Get all menu items |
| GET | /restaurants/{tenant}/{restaurantId}/catalogue/items/{itemId}/dealgroups | Get all menu item deal groups |
| GET | /restaurants/{tenant}/{restaurantId}/catalogue/items/{itemId}/dealgroups/{dealGroupId}/dealitemvariations | Get all deal item variations for a deal group |
| GET | /restaurants/{tenant}/{restaurantId}/catalogue/items/{itemId}/modifiergroups | Get all menu item modifier groups |
| GET | /restaurants/{tenant}/{restaurantId}/catalogue/items/{itemId}/variations | Get all menu item variations |
| GET | /restaurants/{tenant}/{restaurantId}/fees | Get Restaurant Fees |
| PUT | /restaurants/{tenant}/{restaurantId}/fees | Create or Update Restaurant Fees |
| PUT | /restaurants/{tenant}/{restaurantId}/menu | Create or update a menu |
| GET | /restaurants/{tenant}/{restaurantId}/menu | Get the latest version of the restaurant's full menu |
| GET | /restaurants/{tenant}/{restaurantId}/ordertimes | Get the restaurant's delivery and collection lead times |
| PUT | /restaurants/{tenant}/{restaurantId}/ordertimes/{dayOfWeek}/{serviceType} | Update the restaurant's delivery and collection lead times |
| GET | /restaurants/{tenant}/{restaurantId}/servicetimes | Get service times |
| PUT | /restaurants/{tenant}/{restaurantId}/servicetimes | Create or update service times |
| GET | /restaurants/bylatlong | Get restaurants by location |
| GET | /restaurants/bypostcode/{postcode} | Get restaurants by postcode |
| PUT | /restaurants/driver/eta | Set ETA for pickup |

### restaurant-offline-status
| Method | Path | Description |
|--------|------|-------------|
| PUT | /restaurant-offline-status | Restaurant Offline Status |

### restaurant-online-status
| Method | Path | Description |
|--------|------|-------------|
| PUT | /restaurant-online-status | Restaurant Online Status |

### order-eligible-for-restaurant-compensation
| Method | Path | Description |
|--------|------|-------------|
| POST | /order-eligible-for-restaurant-compensation | Order Eligible For Restaurant Compensation |

### menu-ingestion-complete
| Method | Path | Description |
|--------|------|-------------|
| POST | /menu-ingestion-complete | Menu ingestion complete |

### order-time-updated
| Method | Path | Description |
|--------|------|-------------|
| POST | /order-time-updated | Order time updated |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search/autocomplete/{tenant} | Get auto-completed search terms |
| GET | /search/restaurants/{tenant} | Search restaurants |

## Enhanced Skill Content
## Question Mapping

- "How do I search for restaurants near me?" -> GET /search/restaurants/{tenant}
- "What restaurants are available at this postcode?" -> GET /restaurants/bypostcode/{postcode}
- "How do I place a new order?" -> POST /orders
- "How do I accept an incoming order as a restaurant?" -> PUT /orders/{orderId}/accept
- "How do I register a new consumer account?" -> POST /consumers/{tenant}
- "Where is the driver right now?" -> PUT /orders/{orderId}/deliverystate/driverlocation
- "How do I get the full menu for a restaurant?" -> GET /restaurants/{tenant}/{restaurantId}/menu
- "How do I take a restaurant offline for an event?" -> POST /v1/{tenant}/restaurants/event/offline
- "How do I respond to a customer claim?" -> POST /restaurants/{tenant}/{restaurantId}/customerclaims/{id}/restaurantresponse
- "What are the delivery fees for a set of restaurants?" -> GET /delivery-fees/{tenant}
- "How do I get estimated delivery time?" -> GET /delivery/estimate
- "How do I update a restaurant's opening hours?" -> PUT /restaurants/{tenant}/{restaurantId}/servicetimes
- "How do I handle a late order complaint from a customer?" -> POST /orders/{tenant}/{orderId}/consumerqueries/lateorder/restaurantresponse
- "How do I set up delivery pool hours?" -> PUT /delivery/pools/{deliveryPoolId}/hours
- "How do I check available fulfilment times for a checkout?" -> GET /checkout/{tenant}/{checkoutId}/fulfilment/availabletimes

## Response Tips

- **Checkout endpoints**: Response includes `isFulfillable` boolean and `issues` array -- always check both; a 200 with `isFulfillable: false` is a soft failure, not success.
- **Order lifecycle endpoints** (accept, reject, cancel, complete): Most return bare 200/204 with no body; rely on status code alone. Watch for 409 Conflict indicating the order already transitioned state.
- **Restaurant catalogue endpoints**: All paginated via `limit` (required) and `after` cursor (optional); loop until response returns fewer items than `limit`.
- **Customer claims**: Nested `resolution` and `restaurantResponse` objects are nullable (`map?`); always nil-check before accessing inner fields like `justification.comments`.
- **Delivery state updates**: Return 200 with no documented body; these are fire-and-forget status pushes. A 400 on `driverunassigned` means malformed location data.
- **Search endpoints**: Results come in `restaurants` or `terms` arrays; 503 indicates the search service is temporarily down, not a client error.
- **Consumer registration**: 201 returns `{type, token}` -- store the token immediately as it is the session credential. 409 means the email is already registered.
- **Webhook-style event endpoints** (order-accepted, order-cancelled, driver-* events): All return bare 200; these are inbound notification receivers, not query APIs.

## Anomaly Flags

- **409 Conflict on order actions**: Surface immediately -- the order has already moved to a different state (e.g., already accepted, already cancelled). The agent should fetch current order state before retrying.
- **429 Too Many Requests on checkout**: The checkout endpoints explicitly list 429. Alert the user and implement exponential backoff before retry.
- **503 on search endpoints**: Search service degradation. Suggest the user retry after a short delay or fall back to `GET /restaurants/bypostcode/{postcode}`.
- **400 on order placement**: The order body is deeply nested (Items contain Items contain Items). Surface the exact validation error -- it almost always means a missing required field in a nested object.
- **301 redirect on menu GET**: `GET /restaurants/{tenant}/{restaurantId}/menu` can return 301. The agent should follow the redirect automatically and warn the user the menu endpoint has moved.
- **`isFulfillable: false` in checkout response**: This is a silent failure. Proactively surface the `issues` array contents so the user understands why the order cannot proceed.
- **Menu ingestion result `fail`**: When `POST /menu-ingestion-complete` arrives with `result: "fail"`, extract and surface the `fault.errors` array with codes and descriptions.
- **Tenant mismatch**: Many endpoints take `{tenant}` as path param (uk/dk/es/ie/it/no/au/nz). Flag if the tenant value doesn't match one of the known enum values.

## Playbook

### 1. Place an Order End-to-End

1. Search for restaurants: `GET /search/restaurants/{tenant}` with `searchTerm` and `latlong`
2. Browse the menu: `GET /restaurants/{tenant}/{restaurantId}/catalogue` then drill into categories and items using the catalogue sub-endpoints
3. Check delivery fees: `GET /delivery-fees/{tenant}` with the chosen `restaurantIds` and `deliveryTime`
4. Get delivery estimate: `GET /delivery/estimate` with `restaurantReference`, `toLat`, `toLon`
5. Create checkout: `GET /checkout/{tenant}/{checkoutId}` to verify fulfillability
6. Check available times: `GET /checkout/{tenant}/{checkoutId}/fulfilment/availabletimes`
7. Submit order: `POST /orders` with full order payload (Customer, Items, Payment, Fulfilment)
8. Confirm: Verify 201 response and store the returned `OrderId`

### 2. Handle an Incoming Order as a Restaurant

1. Receive the order notification via `POST /acceptance-requested` webhook
2. Review order details: check `Items`, `Fulfilment.DueDate`, `Customer` info
3. Accept: `PUT /orders/{orderId}/accept` with optional `TimeAcceptedFor` if adjusting the due time
4. Or reject: `PUT /orders/{orderId}/reject` with a `Message` explaining why
5. When food is ready: `POST /orders/{orderId}/readyforcollection`
6. When delivered: `POST /orders/{orderId}/complete`

### 3. Manage a Customer Claim

1. List claims: `GET /restaurants/{tenant}/{restaurantId}/customerclaims` with date range and pagination (`limit`, `offset`)
2. Review claim detail: `GET /restaurants/{tenant}/{restaurantId}/customerclaims/{id}` -- check `issueType`, `affectedItems`, `totalClaimed`
3. Respond: `POST /restaurants/{tenant}/{restaurantId}/customerclaims/{id}/restaurantresponse` with `decision` (Accepted/Rejected/PartiallyAccepted) and per-item decisions
4. Add justification if rejecting: `PUT /restaurants/{tenant}/{restaurantId}/customerclaims/{id}/restaurantresponse/justification` with `reason` and optional `comments`

### 4. Set Up and Manage Delivery Pools

1. Create pool: `POST /delivery/pools` with a `name` and optional list of restaurant IDs
2. Set operating hours: `PUT /delivery/pools/{deliveryPoolId}/hours` with per-day schedules (Monday through Sunday, each with `closed` flag and time slots)
3. Add restaurants: `PUT /delivery/pools/{deliveryPoolId}/restaurants` to assign restaurants to the pool
4. Set availability estimate: `PUT /delivery/pools/{deliveryPoolId}/availability/relative` with `bestGuess` time
5. Monitor: `GET /delivery/pools/{deliveryPoolId}` to verify configuration; `GET /delivery/pools` to list all pools

### 5. Take a Restaurant Offline and Back Online

1. Create offline event: `POST /v1/{tenant}/restaurants/event/offline` with `restaurantIds`, `name`, `reason`, `startDate`, and optional `endDate` or `duration`
2. Confirm: Store the returned `restaurantEventId` for later reference
3. To bring back online early: `DELETE /v1/{tenant}/restaurants/{id}/event/offline` with `X-JE-Requester` and `X-JE-User-Role` headers
4. Alternatively, use the status webhooks: `PUT /restaurant-offline-status` or `PUT /restaurant-online-status` to toggle state directly


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
