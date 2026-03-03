---
name: name-generation-api
description: "Name Generation API skill. Use when working with Name Generation for name. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Name Generation API
API version: 1.5

## Auth
Bearer bearer

## Base URL
https://api.fungenerators.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /name/categories -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### name
| Method | Path | Description |
|--------|------|-------------|
| GET | /name/categories | Get available name generation categories. |
| GET | /name/generate | Generated names in the given category |

## Enhanced Skill Content
## Question Mapping

- "What name categories are available?" -> GET /name/categories
- "Show me the first 10 name categories" -> GET /name/categories (with limit=10)
- "Generate a random name" -> GET /name/generate (requires category)
- "Give me a fantasy name" -> GET /name/generate (with category=fantasy)
- "Generate 5 names in the sci-fi category" -> GET /name/generate (with category, limit=5)
- "Generate a name similar to 'Aria'" -> GET /name/generate (with category, suggest=Aria)
- "Get a variation of names in a category" -> GET /name/generate (with category, variation)
- "List categories starting from the 20th result" -> GET /name/categories (with start=20)
- "What kinds of names can I generate?" -> GET /name/categories
- "Generate a batch of baby names" -> GET /name/generate (with category=baby, limit)
- "Browse the next page of categories" -> GET /name/categories (with start=previous+limit)
- "Generate a name and then try a different variation" -> GET /name/generate twice (vary the variation param)
- "How many name categories exist?" -> GET /name/categories (inspect total in response)

## Response Tips

- **Categories** (`/name/categories`): Paginated via `start`/`limit` params. Check response for total count to know when you have fetched all pages.
- **Name Generation** (`/name/generate`): Results vary per call even with identical params. The `suggest` param biases output but does not guarantee exact matches. Multiple names may be returned when `limit` > 1.
- **Errors**: 401 on both endpoints means the Bearer token is missing or invalid. Prompt the user to check their API key.

## Anomaly Flags

- **401 Unauthorized on any call**: Surface immediately -- likely an expired or missing API key. Do not retry silently.
- **Empty category list**: If `/name/categories` returns zero results, the API may be experiencing issues. Flag to the user.
- **Zero names generated**: If `/name/generate` returns no results for a valid category, suggest trying without the `suggest` or `variation` params.
- **Unrecognized category value**: If the user requests a category not present in `/name/categories`, warn before calling generate -- the API may return an error or empty results.
- **Pagination exhausted**: When `start` exceeds total available results, flag that all items have been retrieved rather than showing empty results.

## Playbook

### 1. Browse and Generate Your First Name

1. Call `GET /name/categories` to see all available categories
2. Pick a category from the results
3. Call `GET /name/generate?category={chosen}` to get a name
4. If unsatisfied, call again with `variation` param for alternatives

### 2. Bulk Name Generation

1. Call `GET /name/generate?category={category}&limit=10` to get a batch
2. Review the results
3. Narrow down by adding `suggest={seed}` to bias toward a style
4. Increase or decrease `limit` as needed

### 3. Explore All Categories (Paginated)

1. Call `GET /name/categories?start=0&limit=20` for the first page
2. Note the total count in the response
3. Increment `start` by `limit` (e.g., `start=20`) for each subsequent page
4. Repeat until `start` >= total count

### 4. Guided Name Suggestion

1. Call `GET /name/categories` to present options to the user
2. Ask user to pick a category and optionally provide a seed name
3. Call `GET /name/generate?category={pick}&suggest={seed}`
4. If the result is close but not right, retry with `variation` param
5. Present final selection to the user


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
