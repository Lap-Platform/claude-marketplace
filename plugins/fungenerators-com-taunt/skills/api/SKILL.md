---
name: taunt-as-a-service
description: "Taunt as a service API skill. Use when working with Taunt as a service for taunt. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Taunt as a service
API version: 1.5

## Auth
ApiKey X-Fungenerators-Api-Secret in header

## Base URL
https://api.fungenerators.com/

## Setup
1. Set your API key in the appropriate header
2. GET /taunt/categories -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### taunt
| Method | Path | Description |
|--------|------|-------------|
| GET | /taunt/categories | Get available taunt generation categories. |
| GET | /taunt/generate | Generated taunts in the given category |

## Enhanced Skill Content
## Question Mapping

- "What taunt categories are available?" -> GET /taunt/categories
- "Show me the first 5 taunt categories" -> GET /taunt/categories (limit=5)
- "List categories starting from the 10th result" -> GET /taunt/categories (start=10, limit=10)
- "Generate a taunt" -> GET /taunt/generate (category required)
- "Give me a taunt about movies" -> GET /taunt/generate (category=movies)
- "Generate 3 taunts in the sports category" -> GET /taunt/generate (category=sports, limit=3)
- "What kinds of insults can I generate?" -> GET /taunt/categories
- "Get me a random taunt from any category" -> GET /taunt/categories then GET /taunt/generate with a picked category
- "Page through all available categories" -> GET /taunt/categories (increment start by limit)
- "How many taunt categories exist?" -> GET /taunt/categories (inspect total in response)
- "Generate the maximum number of taunts at once" -> GET /taunt/generate (category required, set limit high)
- "Is there a category called 'nerdy'?" -> GET /taunt/categories (scan results for match)

## Response Tips

- **Categories** (`/taunt/categories`): Paginated via `start`/`limit` params. Check the total count in the response to know when you have fetched all pages.
- **Generate** (`/taunt/generate`): Returns one or more taunts depending on `limit`. The `category` param must match an existing category exactly -- fetch categories first if unsure.
- **Errors**: 401 means the API key is missing or invalid; verify `X-Fungenerators-Api-Secret` header is set correctly.

## Anomaly Flags

- **401 on any request**: Surface immediately -- the API key is missing, expired, or malformed. Prompt the user to check their `X-Fungenerators-Api-Secret` value.
- **Empty category list**: If `/taunt/categories` returns zero results, flag that the service may be temporarily unavailable.
- **Category mismatch**: If `/taunt/generate` fails after using a category from a previous listing, flag that the category may have been removed or renamed.
- **Pagination exhaustion**: If the user is paging through categories and `start` exceeds the total, surface that all categories have been retrieved.
- **Unexpectedly low taunt count**: If `limit` is set but fewer results return, note that the category may have limited content.

## Playbook

### Browse All Categories

1. Call `GET /taunt/categories` with `limit=20`
2. Note the total count in the response
3. If total exceeds 20, repeat with `start=20`, `start=40`, etc. until all fetched
4. Present the full category list to the user

### Generate a Taunt by Topic

1. Call `GET /taunt/categories` to retrieve available categories
2. Match the user's topic to the closest category name
3. Call `GET /taunt/generate` with `category={matched}` and `limit=1`
4. Return the generated taunt

### Batch Generate Taunts

1. Confirm the desired category with the user (list categories if needed)
2. Call `GET /taunt/generate` with `category={chosen}` and `limit={count}`
3. Return all generated taunts

### Random Taunt from Random Category

1. Call `GET /taunt/categories` with `limit=50`
2. Pick a random category from the results
3. Call `GET /taunt/generate` with `category={random_pick}` and `limit=1`
4. Present the taunt along with which category it came from

### Validate API Key Setup

1. Call `GET /taunt/categories` with `limit=1`
2. If 200, the key is valid -- confirm to the user
3. If 401, instruct the user to set the `X-Fungenerators-Api-Secret` header with a valid key


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
