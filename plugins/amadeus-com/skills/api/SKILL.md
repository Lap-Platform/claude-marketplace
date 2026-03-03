---
name: flight-offers-search
description: "Flight Offers Search API skill. Use when working with Flight Offers Search for shopping. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Flight Offers Search
API version: 2.2.0

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v2

## Setup
1. No auth setup needed
2. GET /shopping/flight-offers -- verify access
3. POST /shopping/flight-offers -- create first flight-offers

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### shopping
| Method | Path | Description |
|--------|------|-------------|
| POST | /shopping/flight-offers | Return list of Flight Offers based on posted searching criteria. |
| GET | /shopping/flight-offers | Return list of Flight Offers based on searching criteria. |

## Enhanced Skill Content
## Question Mapping

- "Search for flights from London to Paris on March 15?" -> GET /shopping/flight-offers
- "Find round-trip flights from JFK to LAX departing June 1 returning June 8?" -> GET /shopping/flight-offers
- "What are the cheapest nonstop flights from SFO to ORD?" -> GET /shopping/flight-offers
- "Search flights for 2 adults and 1 child in business class?" -> GET /shopping/flight-offers
- "Find flights under $500 from MIA to LHR?" -> GET /shopping/flight-offers
- "Show only Delta and United flights from BOS to DEN?" -> GET /shopping/flight-offers
- "Exclude budget carriers from my flight search?" -> GET /shopping/flight-offers
- "Get flight prices in EUR instead of USD?" -> GET /shopping/flight-offers
- "Limit results to the top 5 cheapest offers?" -> GET /shopping/flight-offers
- "Search flights for a family with an infant?" -> GET /shopping/flight-offers
- "Run an advanced multi-city or complex itinerary search?" -> POST /shopping/flight-offers
- "Search flights with specific cabin or fare restrictions using a request body?" -> POST /shopping/flight-offers
- "Find one-way economy flights from CDG to NRT for tomorrow?" -> GET /shopping/flight-offers
- "Compare nonstop vs connecting flights on a route?" -> GET /shopping/flight-offers (two calls: nonStop=true then nonStop=false)

## Response Tips

- **Flight offers**: Results are in `data[]` array; each offer contains `itineraries[]` with `segments[]` detailing legs, stops, and timing. Price lives under `price` with `grandTotal` as the bookable amount.
- **Dictionaries**: Response includes a `dictionaries` object mapping carrier codes to airline names, aircraft codes to models, and location codes to city/airport names -- always use these to resolve codes in the offers.
- **400 errors**: Returned as `errors[]` array with `detail` explaining the issue; common causes are invalid IATA codes, past dates, or infants exceeding adults count.
- **Pagination**: The `max` parameter caps results (default varies); there is no cursor-based pagination -- refine search parameters to narrow results instead.

## Anomaly Flags

- **Past departure dates**: Surface immediately if user requests a date that has already passed; the API will return 400.
- **Infants exceeding adults**: The API requires infants <= adults count; flag before sending the request.
- **Empty results**: If `data[]` is empty, proactively suggest relaxing filters (remove nonStop, drop airline restrictions, widen date range, increase maxPrice).
- **Currency mismatch**: If `currencyCode` is set but returned `price.currency` differs, flag the discrepancy.
- **High segment count**: Offers with 3+ segments per itinerary indicate long layover routes; surface these for user awareness.
- **Deprecated or missing dictionary entries**: If carrier/aircraft codes in offers have no matching dictionary entry, flag as potentially outdated data.
- **includedAirlineCodes + excludedAirlineCodes conflict**: These are mutually exclusive; flag if user attempts to set both.

## Playbook

### 1. Simple One-Way Flight Search

1. Collect origin (IATA code), destination (IATA code), departure date, and number of adults
2. Call `GET /shopping/flight-offers` with `originLocationCode`, `destinationLocationCode`, `departureDate`, `adults`
3. Parse `data[]` and sort by `price.grandTotal`
4. Resolve carrier codes using `dictionaries.carriers`
5. Present top results with airline name, departure/arrival times, stops, and price

### 2. Round-Trip with Filters

1. Gather origin, destination, departure date, return date, passenger counts, and preferences
2. Call `GET /shopping/flight-offers` with `returnDate`, `travelClass`, `nonStop=true`, and optionally `maxPrice` or `currencyCode`
3. If no results, retry with `nonStop=false` or increased `maxPrice`
4. Compare outbound and return itineraries within each offer
5. Present options highlighting total price, travel time, and number of stops

### 3. Advanced Multi-Criteria Search (POST)

1. Build a JSON request body with complex criteria (multi-city, specific fare classes, date flexibility)
2. Call `POST /shopping/flight-offers` with `X-HTTP-Method-Override` header and the body
3. Parse the richer response including any additional fare details
4. Cross-reference `dictionaries` for all code lookups
5. Filter and rank results based on user priorities (price, duration, airline preference)

### 4. Budget-Constrained Family Search

1. Collect passenger breakdown: adults, children, infants (validate infants <= adults)
2. Set `maxPrice` to budget ceiling and `currencyCode` to preferred currency
3. Call `GET /shopping/flight-offers` with `max=10` to limit results
4. Check each offer's `travelerPricings[]` for per-passenger cost breakdown
5. Flag any offers where infant pricing is missing or unusually high

### 5. Airline-Specific Comparison

1. Identify target airlines and collect their IATA carrier codes
2. Run `GET /shopping/flight-offers` with `includedAirlineCodes` set to the first airline
3. Run a second call with `includedAirlineCodes` set to the competing airline
4. Normalize results by route and date for side-by-side comparison
5. Present price, schedule, and stop differences between carriers


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
