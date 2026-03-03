---
name: travel-recommendations-api
description: "Travel Recommendations API skill. Use when working with Travel Recommendations for reference-data. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Travel Recommendations API
API version: 1.0.4

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /reference-data/recommended-locations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### reference-data
| Method | Path | Description |
|--------|------|-------------|
| GET | /reference-data/recommended-locations | GET recommended destinations |

## Enhanced Skill Content
## Question Mapping

- "Where should I travel from Paris?" -> GET /reference-data/recommended-locations
- "What destinations are recommended for someone in London and Berlin?" -> GET /reference-data/recommended-locations
- "Show me travel recommendations for a French traveler from Nice" -> GET /reference-data/recommended-locations
- "What are popular destinations from NYC for US travelers?" -> GET /reference-data/recommended-locations
- "Find recommended locations from multiple cities at once" -> GET /reference-data/recommended-locations
- "Where do people from Madrid typically travel to?" -> GET /reference-data/recommended-locations
- "Get destination suggestions filtered to European countries only" -> GET /reference-data/recommended-locations
- "What locations are recommended from Tokyo for Japanese travelers going to Southeast Asia?" -> GET /reference-data/recommended-locations
- "Show travel recommendations without specifying traveler country" -> GET /reference-data/recommended-locations
- "Compare recommended destinations from two different origin cities" -> GET /reference-data/recommended-locations (x2, compare results)
- "Which destinations overlap for travelers from both Paris and Rome?" -> GET /reference-data/recommended-locations (x2, intersect results)
- "Find recommendations from a city but only to specific destination countries" -> GET /reference-data/recommended-locations

## Response Tips

- **recommended-locations**: Expect an array of location objects. Each includes IATA city codes, relevance scores, and geo metadata. Results are not paginated -- the full set returns in one call. Watch for empty arrays when the origin city has insufficient travel data. Errors 400/500 return Amadeus standard error objects with `detail` and `source` fields.

## Anomaly Flags

- **Empty results**: If the response array is empty, surface this -- the city code may be too niche or misspelled. Suggest verifying the IATA code.
- **400 errors**: Likely an invalid or unrecognized `cityCodes` value. Flag the specific code and suggest looking up the correct IATA city code.
- **500 errors**: Amadeus server-side issue. Recommend retrying after a short delay; if persistent, flag as a service outage.
- **Low relevance scores**: If all returned locations have unusually low relevance, note that recommendations may be weak for that origin and suggest trying nearby major hubs instead.
- **travelerCountryCode defaulting to FR**: The default is France. If the user hasn't specified a country and results seem Euro-centric, proactively mention the default and suggest setting the parameter explicitly.

## Playbook

### 1. Get Basic Travel Recommendations from a City

1. Identify the IATA city code for the origin (e.g., PAR for Paris, LON for London)
2. Call `GET /reference-data/recommended-locations?cityCodes=PAR`
3. Parse the response array and present destinations sorted by relevance

### 2. Get Country-Filtered Recommendations

1. Determine the origin city IATA code and target destination country codes (ISO 3166-1 alpha-2)
2. Call `GET /reference-data/recommended-locations?cityCodes=NYC&travelerCountryCode=US&destinationCountryCodes=FR,ES,IT`
3. Review results -- only destinations in France, Spain, and Italy will appear
4. If results are empty, broaden the destination filter or remove it entirely

### 3. Compare Destinations Across Multiple Origins

1. Call `GET /reference-data/recommended-locations?cityCodes=PAR` for the first origin
2. Call `GET /reference-data/recommended-locations?cityCodes=ROM` for the second origin
3. Intersect the two result sets by destination city code to find overlapping recommendations
4. Present shared destinations with their respective relevance scores from each origin

### 4. Discover Trending Destinations for a Specific Nationality

1. Pick a major hub city as the origin (e.g., `cityCodes=LON`)
2. Set `travelerCountryCode` to the nationality of interest (e.g., `DE` for German travelers)
3. Call `GET /reference-data/recommended-locations?cityCodes=LON&travelerCountryCode=DE`
4. Compare against a second call with a different `travelerCountryCode` to see how preferences differ by nationality


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
