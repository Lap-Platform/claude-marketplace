---
name: cis-automotive-api
description: "CIS Automotive API skill. Use when working with CIS Automotive for getToken, makeSubUserKey, revokeSubUserKey. Covers 35 endpoints."
version: 1.0.0
generator: lapsh
---

# CIS Automotive API
API version: 1.0

## Auth
ApiKey apiKey in query

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /getToken -- verify access
3. POST /getToken -- create first getToken

## Endpoints

35 endpoints across 34 groups. See references/api-spec.lap for full details.

### getToken
| Method | Path | Description |
|--------|------|-------------|
| GET | /getToken | Get a JWT from your API credentials |
| POST | /getToken | Get a JWT from your API credentials |

### makeSubUserKey
| Method | Path | Description |
|--------|------|-------------|
| POST | /makeSubUserKey | Generate a Sub User Key that can be used by your users to make API calls in frontend applications. |

### revokeSubUserKey
| Method | Path | Description |
|--------|------|-------------|
| PUT | /revokeSubUserKey | Revoke a Sub User Key associated with your account. |

### getSubUserKeys
| Method | Path | Description |
|--------|------|-------------|
| GET | /getSubUserKeys | Get all Sub User Keys associated with your account. |

### getRegions
| Method | Path | Description |
|--------|------|-------------|
| GET | /getRegions | Get a list of region names |

### getBrands
| Method | Path | Description |
|--------|------|-------------|
| GET | /getBrands | Get a list of brand names |

### getModels
| Method | Path | Description |
|--------|------|-------------|
| GET | /getModels | Get a list of model names |

### getInactiveModels
| Method | Path | Description |
|--------|------|-------------|
| GET | /getInactiveModels | Get a list of model names including discontinued models |

### daysToSell
| Method | Path | Description |
|--------|------|-------------|
| GET | /daysToSell | Days a vehicle takes to sell |

### daysSupply
| Method | Path | Description |
|--------|------|-------------|
| GET | /daysSupply | Days worth of supply left on dealer lots |

### listPrice
| Method | Path | Description |
|--------|------|-------------|
| GET | /listPrice | Stats on ask price of new vehicles |

### salePrice
| Method | Path | Description |
|--------|------|-------------|
| GET | /salePrice | Stats on sale price of new vehicles |

### salePriceHistogram
| Method | Path | Description |
|--------|------|-------------|
| GET | /salePriceHistogram | Histogram of sales price of new vehicles by model |

### modelYearDist
| Method | Path | Description |
|--------|------|-------------|
| GET | /modelYearDist | Used market share of model year by model |

### topModels
| Method | Path | Description |
|--------|------|-------------|
| GET | /topModels | Top models in a given region |

### getRegionBrandMarketShare
| Method | Path | Description |
|--------|------|-------------|
| GET | /getRegionBrandMarketShare | Market share of a brand in region |

### getRegionMarketShare
| Method | Path | Description |
|--------|------|-------------|
| GET | /getRegionMarketShare | Market share of all brands in region |

### getDealers
| Method | Path | Description |
|--------|------|-------------|
| GET | /getDealers | Premium. Dealers in a zip code. |

### getDealersByRegion
| Method | Path | Description |
|--------|------|-------------|
| GET | /getDealersByRegion | Premium. Dealers in a region. |

### getDealersByID
| Method | Path | Description |
|--------|------|-------------|
| GET | /getDealersByID | Premium. Dealers by ID |

### regionSales
| Method | Path | Description |
|--------|------|-------------|
| GET | /regionSales | Premium. Brand sales by region and month |

### regionDailySales
| Method | Path | Description |
|--------|------|-------------|
| GET | /regionDailySales | Brand sales by region and Day |

### vehicleHistory
| Method | Path | Description |
|--------|------|-------------|
| GET | /vehicleHistory | Premium. Simple Vehicle History Report |

### similarSalePrice
| Method | Path | Description |
|--------|------|-------------|
| GET | /similarSalePrice | Premium. Simple Vehicle Market Report |

### valuation
| Method | Path | Description |
|--------|------|-------------|
| GET | /valuation | Premium. Simple Vehicle Market Report Over Arbitrary Locations and Vehicles. |

### vehicleSeen
| Method | Path | Description |
|--------|------|-------------|
| GET | /vehicleSeen | Checks if a VIN appeared on the market on or after a given date. |

### vinDecode
| Method | Path | Description |
|--------|------|-------------|
| GET | /vinDecode | Vin decoder and Recall Info |

### listings2
| Method | Path | Description |
|--------|------|-------------|
| GET | /listings2 | Flexible Listing Search |

### listings
| Method | Path | Description |
|--------|------|-------------|
| GET | /listings | Listings by Dealer ID |

### listingsByDate
| Method | Path | Description |
|--------|------|-------------|
| GET | /listingsByDate | Listings by Dealer ID and Date |

### listingsByRegion
| Method | Path | Description |
|--------|------|-------------|
| GET | /listingsByRegion | Listings by Region |

### listingsByRegionAndDate
| Method | Path | Description |
|--------|------|-------------|
| GET | /listingsByRegionAndDate | Listings by Region and Date |

### listingsByZipCode
| Method | Path | Description |
|--------|------|-------------|
| GET | /listingsByZipCode | Listings by ZipCode |

### listingsByZipCodeAndDate
| Method | Path | Description |
|--------|------|-------------|
| GET | /listingsByZipCodeAndDate | Listings by ZipCode and Date |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the CIS Automotive API?" -> GET /getToken
- "What car brands are available in the database?" -> GET /getBrands
- "What models does Toyota make?" -> GET /getModels
- "Which regions does the API cover?" -> GET /getRegions
- "How long does it take to sell a Ford in California?" -> GET /daysToSell
- "What is the current market value of my car?" -> GET /valuation
- "Decode this VIN number for me" -> GET /vinDecode
- "What are the sale prices for Honda vehicles in Texas?" -> GET /salePrice
- "Find car listings near zip code 90210" -> GET /listingsByZipCode
- "What dealers are in my area?" -> GET /getDealers
- "Has this VIN been seen on the market recently?" -> GET /vehicleSeen
- "What is the price history for similar vehicles to mine?" -> GET /similarSalePrice
- "Which models are selling the most in my region?" -> GET /topModels
- "What is Toyota's market share in California?" -> GET /getRegionBrandMarketShare
- "Show me a dealer's full inventory" -> GET /listings

## Response Tips

- **Auth endpoints** (`getToken`, `makeSubUserKey`): Store the returned `token` and check `expires` (epoch timestamp) before each subsequent call; all data endpoints require `jwt` from this token.
- **Reference data** (`getRegions`, `getBrands`, `getModels`): The `data` array contains the full list; `cacheTimeLimit` tells you how long to cache locally before refetching.
- **Market analytics** (`daysToSell`, `daysSupply`, `listPrice`, `salePrice`, `topModels`, market share): Always check `regionName` and `condition` in the envelope to confirm the scope of the returned `data`.
- **Histogram/distribution** (`salePriceHistogram`, `modelYearDist`): `data` is an array of maps representing buckets; iterate to build charts or summaries.
- **Listings** (`listings`, `listings2`, `listingsByRegion`, etc.): Paginated via `data.page` and `data.maxPages`; loop incrementing `page` until `page >= maxPages`. Check `startDate`/`endDate` in the response to confirm the date window applied.
- **Vehicle-specific** (`vinDecode`, `vehicleHistory`, `similarSalePrice`, `valuation`): `data` structure varies; `vinDecode` returns decoded fields, `vehicleHistory` nests under `data.data` as an array, `valuation`/`similarSalePrice` return statistical aggregates (`Avg`, `StdDev`, `Count`).
- **Dealer lookups** (`getDealers`, `getDealersByRegion`, `getDealersByID`): `getDealersByRegion` is paginated (`data.page`, `data.maxPages`); the other two return flat arrays.
- **All endpoints**: Every response shares a common envelope (`brandName`, `modelName`, `regionName`, `condition`, `msg`, `cacheTimeLimit`, `data`). Check `msg` for warnings or status notes. A 422 error indicates invalid or missing parameters.

## Anomaly Flags

- **Token expiration approaching**: Compare `expires` from `/getToken` against current epoch time; alert when less than 5 minutes remain.
- **Cache time exceeded**: If `cacheTimeLimit` indicates data staleness, surface a note that results may be outdated and a refresh is advisable.
- **Empty data arrays**: When `data` returns as an empty array or null for market/listing queries, flag that no results matched -- likely a region, brand, or date range issue rather than an API failure.
- **Pagination not exhausted**: If a listings response shows `page < maxPages` and the caller stopped fetching, warn that results are incomplete.
- **High standard deviation in valuations**: When `usedSaleStdDev` or `newSaleStdDev` from `/valuation` or `/similarSalePrice` is large relative to the average, flag that pricing is highly variable and the estimate may be unreliable.
- **Low comparable count**: When `newCount` or `usedCount` in valuation responses is below 5, warn that the sample size is too small for a confident estimate.
- **Sub-user key scope**: When creating sub-user keys, if `endPoints` is set to `['*']` (default), flag the broad access and suggest restricting to specific endpoints.
- **Inactive models returned**: If the caller uses `/getModels` but the model appears in `/getInactiveModels`, surface that the model may be discontinued with limited data availability.

## Playbook

### 1. First-time Setup and Authentication

1. Call `GET /getToken` with your `apiID` and `apiKey` to obtain a JWT.
2. Store the returned `token` and note the `expires` timestamp.
3. Use the `token` as the `jwt` parameter in all subsequent data calls.
4. Before each session, check if `expires` has passed; if so, re-authenticate.

### 2. Valuate a Specific Vehicle by VIN

1. Authenticate via `GET /getToken` to get a JWT.
2. Call `GET /vinDecode` with the VIN to confirm the vehicle details (brand, model, year, trim).
3. Call `GET /valuation` with the VIN and optional filters (`regionName`, `mileageLow`/`mileageHigh`, `daysBack`) for a market-based valuation.
4. If the valuation count is low, call `GET /similarSalePrice` with the same VIN, increasing `daysBack` or setting `sameYear=False` to widen the comparables.
5. Review `newSaleAvg`/`usedSaleAvg` and standard deviations to present a price range.

### 3. Competitive Market Analysis for a Brand in a Region

1. Authenticate via `GET /getToken`.
2. Call `GET /getRegions` to confirm available region identifiers.
3. Call `GET /getBrands` to list available brands.
4. Call `GET /getRegionBrandMarketShare` with the target brand and region for brand-level market share.
5. Call `GET /getRegionMarketShare` with the same region to compare against all brands.
6. Call `GET /topModels` for the same region to see which models dominate.
7. Call `GET /daysToSell` and `GET /daysSupply` for the brand/region to assess inventory velocity.

### 4. Search and Browse Dealer Inventory

1. Authenticate via `GET /getToken`.
2. To find dealers: call `GET /getDealers` with a zip code, or `GET /getDealersByRegion` with a region name (paginate through all pages).
3. Pick a `dealerID` from the results.
4. Call `GET /listings` with the `dealerID` to browse their current inventory (paginate via `page` parameter).
5. To filter by date range, use `GET /listingsByDate` with the same `dealerID` plus `startDate`/`endDate`.

### 5. Delegating Access with Sub-user Keys

1. Authenticate via `POST /getToken` with your master `apiID` and `apiKey`.
2. Call `POST /makeSubUserKey` with a `siteName` matching the consumer's domain and an `endPoints` array restricted to only the endpoints they need (avoid the `['*']` default).
3. Distribute the returned `token` and `uuid` to the sub-user.
4. To audit active sub-users, call `GET /getSubUserKeys`.
5. To revoke access, call `PUT /revokeSubUserKey` with the sub-user's `subUserKeyUUID`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
