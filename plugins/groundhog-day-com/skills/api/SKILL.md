---
name: groundhog-day-api
description: "Groundhog Day API skill. Use when working with Groundhog Day for api. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Groundhog Day API
API version: 1.2.1

## Auth
No authentication required.

## Base URL
https://virtserver.swaggerhub.com/pcraig3/groundhog-day-api/1.2.1

## Setup
1. No auth setup needed
2. GET /api/v1 -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/v1 | Root |
| GET | /api/v1/groundhogs | Get all groundhogs |
| GET | /api/v1/groundhogs/{slug} | Get a groundhog by slug |
| GET | /api/v1/predictions | Get predictions for a given year |
| GET | /api/v1/spec | Get JSON schema |

## Enhanced Skill Content
## Question Mapping

- "What groundhogs are in the database?" -> GET /api/v1/groundhogs
- "Show me only Canadian groundhogs" -> GET /api/v1/groundhogs?country=Canada
- "Which predictors are actual groundhogs vs. other animals?" -> GET /api/v1/groundhogs?isGroundhog=1
- "Which predictors are NOT real groundhogs?" -> GET /api/v1/groundhogs?isGroundhog=0
- "Tell me about Punxsutawney Phil" -> GET /api/v1/groundhogs/{slug}
- "What prediction did a specific groundhog make this year?" -> GET /api/v1/groundhogs/{slug} (check currentPrediction and predictions array)
- "What were all the predictions for 2024?" -> GET /api/v1/predictions?year=2024
- "Show me every prediction ever recorded" -> GET /api/v1/predictions
- "What endpoints does this API have?" -> GET /api/v1
- "Where can I find the OpenAPI spec?" -> GET /api/v1/spec
- "Is Wiarton Willie still active?" -> GET /api/v1/groundhogs/{slug} (check active field)
- "How many predictions has a groundhog made?" -> GET /api/v1/groundhogs/{slug} (check predictionsCount)
- "What types of animals predict the weather besides groundhogs?" -> GET /api/v1/groundhogs?isGroundhog=0 (inspect type field)
- "Where is a specific groundhog located?" -> GET /api/v1/groundhogs/{slug} (check city, region, country, coordinates)

## Response Tips

- **Root endpoint** (`/api/v1`): Returns HATEOAS `_links` -- use these hrefs for discovery rather than hardcoding paths.
- **Groundhog lists** (`/groundhogs`): Results are in the `groundhogs` array. No pagination -- the full list is returned. Filter server-side with `country` and `isGroundhog` params rather than client-side.
- **Single groundhog** (`/groundhogs/{slug}`): Nested under `groundhog` key. `isGroundhog` and `active` are binary integers (0/1), not booleans. `predictions` is an embedded array of maps -- no separate fetch needed.
- **Predictions** (`/predictions`): Results in the `predictions` array. A 302 redirect may occur -- follow it. 400 means invalid year parameter.
- **Spec** (`/spec`): Returns the raw OpenAPI spec document directly (not wrapped in a JSON envelope).

## Anomaly Flags

- **302 on predictions**: The predictions endpoint may redirect. Surface this if the client does not follow redirects automatically, as data will appear missing.
- **400 errors**: Flag malformed slug values or invalid year parameters immediately with the corrected format (slugs are lowercase-hyphenated, years are four-digit integers).
- **Inactive groundhogs**: When `active: 0`, proactively note that prediction data may be stale or incomplete -- the animal may be retired or deceased.
- **Non-groundhog predictors**: When `isGroundhog: 0`, surface the `type` field so the user knows what kind of animal or object it actually is.
- **Empty predictions array**: If a groundhog has `predictionsCount: 0` or an empty `predictions` array, flag that no historical data is available rather than returning silent empty results.
- **Missing contact/source**: If `contact` or `source` fields are empty strings, note that official verification channels are unavailable for that predictor.

## Playbook

### 1. Look Up a Specific Groundhog's Full Profile

1. GET /api/v1/groundhogs to browse the full list and find the slug
2. GET /api/v1/groundhogs/{slug} with the desired slug
3. Present name, location (city/region/country), active status, type, and description
4. Show currentPrediction for the latest call and predictionsCount for historical depth

### 2. Compare Predictions Across All Groundhogs for a Given Year

1. GET /api/v1/predictions?year={year} to fetch all predictions for the target year
2. Group results by prediction outcome (early spring vs. long winter)
3. Cross-reference with GET /api/v1/groundhogs to add location and type context
4. Summarize the consensus: what did the majority predict?

### 3. Find All Non-Groundhog Predictors

1. GET /api/v1/groundhogs?isGroundhog=0 to filter for alternative predictors
2. For each result, note the `type` field (e.g., lobster, owl, stuffed animal)
3. Optionally GET /api/v1/groundhogs/{slug} on interesting entries for full details and prediction history

### 4. Audit Active vs. Retired Predictors by Country

1. GET /api/v1/groundhogs?country=Canada (or USA, etc.)
2. Partition results by `active` field (1 = active, 0 = retired)
3. For retired entries, GET /api/v1/groundhogs/{slug} to check last prediction year from the predictions array
4. Report active count, retired count, and most recently retired predictor

### 5. Explore the API Programmatically via HATEOAS

1. GET /api/v1 to retrieve the root resource and its `_links`
2. Follow `_links.groundhogs.href` to list all groundhogs
3. Follow `_links.predictions.href` to list all predictions
4. Follow `_links.spec.href` to retrieve the machine-readable OpenAPI spec for client generation


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
