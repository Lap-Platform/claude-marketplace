---
name: api-v1
description: "API V1 API skill. Use when working with API V1 for api. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# API V1
API version: v1

## Auth
Bearer basic

## Base URL
https://{defaultHost}

## Setup
1. Set Authorization header with your Bearer token
2. GET /api/v1/donations/show -- verify access
3. POST /api/v1/donations/create -- create first create

## Endpoints

8 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| POST | /api/v1/donations/create | Create a donation |
| GET | /api/v1/donations/show | Retrieve a donation |
| GET | /api/v1/donations/index | List your donations |
| GET | /api/v1/donations/carbon_calculate | Calculate shipping carbon offset |
| GET | /api/v1/donations/crypto_calculate | Calculate crypto carbon offset |
| GET | /api/v1/donations/carbon_stats | Retrieve carbon offset stats |
| GET | /api/v1/nonprofits/show | Show a nonprofit |
| GET | /api/v1/nonprofits/list | Search a nonprofit |

## Enhanced Skill Content
## Question Mapping

- "How do I make a donation?" -> POST /api/v1/donations/create
- "Create a donation funded by the merchant" -> POST /api/v1/donations/create
- "Look up a specific donation by ID" -> GET /api/v1/donations/show
- "List all my donations" -> GET /api/v1/donations/index
- "Show page 3 of donations" -> GET /api/v1/donations/index
- "How much carbon does shipping 50 lbs by truck offset?" -> GET /api/v1/donations/carbon_calculate
- "Calculate the carbon footprint for an air shipment" -> GET /api/v1/donations/carbon_calculate
- "What is the carbon offset for a Bitcoin transaction?" -> GET /api/v1/donations/crypto_calculate
- "Calculate the environmental cost of 5 Ethereum transactions" -> GET /api/v1/donations/crypto_calculate
- "Show my carbon offset stats" -> GET /api/v1/donations/carbon_stats
- "Get carbon stats for a specific donation" -> GET /api/v1/donations/carbon_stats
- "Find a nonprofit by name" -> GET /api/v1/nonprofits/list
- "Get details about a specific nonprofit" -> GET /api/v1/nonprofits/show
- "Browse available nonprofits" -> GET /api/v1/nonprofits/list
- "Make a customer-funded donation with a zip code" -> POST /api/v1/donations/create

## Response Tips

- **Donations (create/show):** Response is a single donation object at 200; a 400 on create means a missing or invalid required field -- check `amount`, `nonprofit_id`, and that `funding_source` is exactly `merchant` or `customer`.
- **Donations (index/list):** Paginated via `page` param; assume page 1 if omitted. Inspect response for total count or next-page indicators before iterating.
- **Carbon calculate:** Requires `weight_lb`; distance and addresses are optional but improve accuracy. `transportation_method` must be one of `air`, `truck`, `rail`, `sea`.
- **Crypto calculate:** Requires `currency` as `eth` or `btc`; `count` defaults to 1 if omitted. Response contains offset equivalents.
- **Carbon stats:** Returns aggregate stats; pass `id` to scope to a single donation. Omit for account-wide totals.
- **Nonprofits:** `show` returns full detail for one nonprofit; `list` supports fuzzy search via `name` and pagination via `page`.

## Anomaly Flags

- **400 on donation create:** Surface immediately with the specific missing/invalid field. The only endpoint that returns errors -- always validate `funding_source` is `merchant` or `customer` before calling.
- **Empty donation index:** If page > 1 returns no results, the user has paginated past the end. Warn and suggest going back.
- **Carbon calculate with no optional params:** Results may be rough estimates. Flag when neither `distance_mi`/addresses nor `transportation_method` are provided.
- **Crypto currency mismatch:** If user mentions a currency other than `eth` or `btc`, surface that only those two are supported before making the call.
- **Nonprofit not found:** If `show` returns empty or error for an ID, suggest using `list` with a name search to find the correct ID.
- **Missing auth:** All endpoints require Bearer or Basic auth. If a request fails with 401/403, surface the auth requirement immediately.

## Playbook

### 1. Make a Donation to a Nonprofit

1. Search for the nonprofit: `GET /api/v1/nonprofits/list?name=<search term>`
2. Pick the desired nonprofit from results and note its `id`
3. Create the donation: `POST /api/v1/donations/create` with `amount`, `nonprofit_id`, and `funding_source`
4. Confirm success by retrieving the donation: `GET /api/v1/donations/show?id=<donation_id>`

### 2. Calculate and Offset a Shipment's Carbon Footprint

1. Calculate the carbon impact: `GET /api/v1/donations/carbon_calculate?weight_lb=<weight>&transportation_method=<method>`
2. Note the offset amount from the response
3. Find an environmental nonprofit: `GET /api/v1/nonprofits/list?name=carbon` or similar
4. Create a donation for the offset amount: `POST /api/v1/donations/create` with the calculated amount and nonprofit ID
5. Verify with carbon stats: `GET /api/v1/donations/carbon_stats`

### 3. Offset Cryptocurrency Environmental Impact

1. Calculate the crypto footprint: `GET /api/v1/donations/crypto_calculate?currency=eth&count=<num_transactions>`
2. Review the offset recommendation in the response
3. Create a donation matching the offset: `POST /api/v1/donations/create`
4. Check updated carbon stats: `GET /api/v1/donations/carbon_stats`

### 4. Audit Donation History and Carbon Impact

1. List all donations: `GET /api/v1/donations/index?page=1`
2. Page through results incrementing `page` until no more results
3. For each donation of interest, get full details: `GET /api/v1/donations/show?id=<id>`
4. Pull aggregate carbon stats: `GET /api/v1/donations/carbon_stats`
5. Compare per-donation stats by passing specific IDs: `GET /api/v1/donations/carbon_stats?id=<donation_id>`

### 5. Browse and Evaluate Nonprofits Before Donating

1. List nonprofits without a filter to browse: `GET /api/v1/nonprofits/list`
2. Narrow results by name: `GET /api/v1/nonprofits/list?name=<keyword>`
3. Get full details on candidates: `GET /api/v1/nonprofits/show?id=<id>` for each
4. Compare and select, then proceed to donation creation


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
