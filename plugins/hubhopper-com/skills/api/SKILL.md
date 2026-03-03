---
name: hubhopper-partner-integration-apis-production
description: "Hubhopper Partner Integration API(s) - Production API skill. Use when working with Hubhopper Partner Integration API(s) - Production for categories, podcasts, util. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# Hubhopper Partner Integration API(s) - Production
API version: v5

## Auth
ApiKey x-api-key in header | ApiKey hhPartnerId in header

## Base URL
https://apis.hubhopper.com/partner

## Setup
1. Set your API key in the appropriate header
2. GET /categories -- verify access

## Endpoints

7 endpoints across 3 groups. See references/api-spec.lap for full details.

### categories
| Method | Path | Description |
|--------|------|-------------|
| GET | /categories | Get the list of all content categories. |
| GET | /categories/{categoryId} | Get specific content category. |
| GET | /categories/{categoryId}/podcasts | Get a list of all podcasts under a category. |

### podcasts
| Method | Path | Description |
|--------|------|-------------|
| GET | /podcasts | Get the list of all podcasts. |
| GET | /podcasts/{podcastId} | Get a single Podcast. |
| GET | /podcasts/{podcastId}/episodes | Get a list of all episodes under a podcast. |

### util
| Method | Path | Description |
|--------|------|-------------|
| GET | /util/languages |  |

## Enhanced Skill Content
## Question Mapping

- "What podcast categories are available?" -> GET /categories
- "Show me category details for a specific category" -> GET /categories/{categoryId}
- "What podcasts are in the comedy category?" -> GET /categories/{categoryId}/podcasts
- "List all podcasts on the platform" -> GET /podcasts
- "Get details about a specific podcast" -> GET /podcasts/{podcastId}
- "Show me episodes for this podcast" -> GET /podcasts/{podcastId}/episodes
- "What languages does Hubhopper support?" -> GET /util/languages
- "Browse podcasts filtered by language or genre" -> GET /podcasts with filters param
- "Get the latest episodes from a podcast" -> GET /podcasts/{podcastId}/episodes with order param
- "How many podcasts are in each category?" -> GET /categories then GET /categories/{categoryId}/podcasts for each
- "Find podcasts page by page" -> GET /podcasts with page and pageSize params
- "What's on page 3 of the podcast listing?" -> GET /podcasts?page=3
- "Show me a small batch of categories" -> GET /categories?pageSize=5

## Response Tips

- **Categories** (`/categories`, `/categories/{categoryId}`): Expect paginated lists with `page` and `pageSize` controlling window. A 404 on a specific category means the ID is invalid or removed.
- **Podcasts** (`/podcasts`, `/categories/{categoryId}/podcasts`): Support `order` and `filters` params for sorting and narrowing results. Responses likely nest podcast metadata (title, description, artwork) inside each item.
- **Episodes** (`/podcasts/{podcastId}/episodes`): Paginated like podcasts; episode objects will contain media URLs, duration, and publish dates. Use `order` to get newest-first.
- **Languages** (`/util/languages`): A 204 means the list is empty (no content). A 401 here (unique to this endpoint) signals missing or invalid API key headers.
- **All endpoints**: 500 errors are server-side -- retry with backoff. Always send both `x-api-key` and `hhPartnerId` headers on every request.

## Anomaly Flags

- **401 on /util/languages**: Surface immediately -- indicates authentication is misconfigured. Verify both `x-api-key` and `hhPartnerId` headers are present and valid.
- **204 on /util/languages**: Flag that the languages list returned empty -- this may indicate a data issue upstream.
- **Repeated 500 errors**: If any endpoint returns 500 more than once consecutively, alert the user that the Hubhopper API may be experiencing downtime.
- **Empty paginated results**: If a paginated endpoint returns zero items on page 1, flag that the dataset or filter may be wrong rather than silently proceeding.
- **Category/podcast 404**: When browsing by ID and getting 404, proactively suggest refreshing the category or podcast list as IDs may have changed.
- **Missing pagination metadata**: If responses lack total count or next-page indicators, warn that iterating to completion requires checking for empty pages.

## Playbook

### 1. Discover and Browse All Podcasts by Category

1. Call `GET /categories` to retrieve the full category list (paginate if needed with `page` and `pageSize`)
2. Pick a category of interest and note its `categoryId`
3. Call `GET /categories/{categoryId}` to confirm category details
4. Call `GET /categories/{categoryId}/podcasts` to list podcasts in that category
5. Page through results by incrementing the `page` param until no more results

### 2. Fetch All Episodes for a Podcast

1. Call `GET /podcasts` (or search within a category) to find the target podcast
2. Note the `podcastId` from the results
3. Call `GET /podcasts/{podcastId}` to get full podcast metadata
4. Call `GET /podcasts/{podcastId}/episodes?order=desc` to get episodes newest-first
5. Continue paginating with `page` param until the response returns empty

### 3. Validate API Credentials

1. Call `GET /util/languages` with both `x-api-key` and `hhPartnerId` headers
2. If 200: credentials are valid and the API is reachable
3. If 401: one or both auth headers are missing or invalid -- check key values
4. If 500: the API is down -- retry later

### 4. Build a Filtered Podcast Directory

1. Call `GET /util/languages` to get available language codes
2. Call `GET /categories` to get all category IDs
3. For each category, call `GET /categories/{categoryId}/podcasts?filters={language}` to get podcasts matching the desired language
4. Aggregate results across categories, deduplicating by `podcastId`
5. For each podcast of interest, call `GET /podcasts/{podcastId}/episodes?pageSize=1` to preview the latest episode

### 5. Paginate Through Large Result Sets

1. Start with `page=1` and a reasonable `pageSize` (e.g., 20)
2. Call the target endpoint (e.g., `GET /podcasts?page=1&pageSize=20`)
3. Process the returned items
4. If the number of items equals `pageSize`, increment `page` and repeat
5. Stop when fewer items than `pageSize` are returned (indicates the final page)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
