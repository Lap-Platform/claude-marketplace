---
name: giphy-api
description: "Giphy API skill. Use when working with Giphy for gifs, stickers. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# Giphy API
API version: 1.0

## Auth
ApiKey api_key in query

## Base URL
https://api.giphy.com/v1

## Setup
1. Set your API key in the appropriate header
2. GET /gifs/search -- verify access

## Endpoints

10 endpoints across 2 groups. See references/api-spec.lap for full details.

### gifs
| Method | Path | Description |
|--------|------|-------------|
| GET | /gifs/search | Search GIFs |
| GET | /gifs/trending | Trending GIFs |
| GET | /gifs/translate | Translate phrase to GIF |
| GET | /gifs/random | Random GIF |
| GET | /gifs/{gifId} | Get GIF by Id |
| GET | /gifs | Get GIFs by ID |

### stickers
| Method | Path | Description |
|--------|------|-------------|
| GET | /stickers/search | Search Stickers |
| GET | /stickers/trending | Trending Stickers |
| GET | /stickers/translate | Translate phrase to Sticker |
| GET | /stickers/random | Random Sticker |

## Enhanced Skill Content
## Question Mapping

- "Search for GIFs about cats?" -> GET /gifs/search
- "What GIFs are trending right now?" -> GET /gifs/trending
- "Find a single GIF that best represents 'excited'?" -> GET /gifs/translate
- "Give me a random GIF?" -> GET /gifs/random
- "Get details for a specific GIF by ID?" -> GET /gifs/{gifId}
- "Fetch multiple GIFs by their IDs in one call?" -> GET /gifs
- "Search for stickers related to 'birthday'?" -> GET /stickers/search
- "What stickers are trending?" -> GET /stickers/trending
- "Find a sticker that means 'thank you'?" -> GET /stickers/translate
- "Get a random sticker with a specific tag?" -> GET /stickers/random
- "Search for GIFs but only show family-friendly results?" -> GET /gifs/search (use rating=g)
- "Get the next page of GIF search results?" -> GET /gifs/search (increment offset by limit)
- "Find GIFs in a specific language?" -> GET /gifs/search (use lang parameter)
- "Browse trending GIFs five at a time?" -> GET /gifs/trending (use limit=5, increment offset)

## Response Tips

- **Search & Trending** (`/gifs/search`, `/gifs/trending`, `/stickers/search`, `/stickers/trending`): Response wraps results in `data[]` with a `pagination` object containing `total_count`, `count`, and `offset`. Use `offset` + `count` for next page.
- **Translate** (`/gifs/translate`, `/stickers/translate`): Returns a single GIF object in `data` (not an array). This is Giphy's "weighted search" -- it picks one best match, not a list.
- **Random** (`/gifs/random`, `/stickers/random`): Returns a single object in `data`. Structure may differ slightly from search results (flattened fields).
- **By ID** (`/gifs/{gifId}`, `/gifs`): Single fetch returns `data` as object; bulk fetch via `ids` returns `data[]`. The `images` nested object contains renditions keyed by size (`original`, `fixed_height`, `downsized`, etc.).
- **All endpoints**: 403 means invalid or missing `api_key`. 429 means rate limit hit. `meta` object in every response carries `status`, `msg`, and `response_id` for debugging.

## Anomaly Flags

- **429 Too Many Requests**: Surface immediately -- the API key has hit its rate limit. Back off and retry after a delay. Warn the user about quota.
- **403 Forbidden**: API key is invalid, expired, or missing. Prompt the user to check their `api_key` value.
- **Empty `data` array on search**: Not an error, but worth flagging -- the query may be too specific or misspelled. Suggest broadening the search term.
- **`pagination.total_count` is 0**: Proactively tell the user no results exist rather than silently returning nothing.
- **Offset exceeds total_count**: The user has paginated past all results. Surface this instead of returning an empty page without explanation.
- **Rating filter mismatch**: If the user expects results but gets none, flag that a restrictive `rating` filter (e.g., `g`) may be excluding matches.
- **Deprecated or missing `images` renditions**: If an expected rendition key (e.g., `fixed_width_small`) returns null or is absent, flag it as a possible deprecation.

## Playbook

### 1. Search and paginate through GIF results

1. Call `GET /gifs/search?q=dogs&limit=25&offset=0&api_key=KEY`
2. Read `pagination.total_count` to know how many results exist
3. Display `data[]` results, extracting URLs from `data[].images.original.url`
4. To load next page, call again with `offset=25` (previous offset + limit)
5. Repeat until `offset >= pagination.total_count`

### 2. Get the perfect single GIF for a concept

1. Call `GET /gifs/translate?s=nervous+laughter&api_key=KEY`
2. Extract the GIF from `data.images.original.url`
3. If the result is not a good fit, fall back to `GET /gifs/search?q=nervous+laughter&limit=5` and let the user pick from multiple options

### 3. Build a "GIF of the day" feature

1. Call `GET /gifs/trending?limit=1&api_key=KEY` to get the top trending GIF
2. Extract `data[0].title`, `data[0].images.original.url`, and `data[0].id`
3. Optionally call `GET /gifs/{gifId}?api_key=KEY` with the ID to get full metadata including source, username, and import date

### 4. Curate a sticker pack by theme

1. Call `GET /stickers/search?q=celebration&limit=25&rating=g&api_key=KEY`
2. Collect IDs from `data[].id` that match the desired style
3. Store selected IDs, then batch-fetch details anytime via `GET /gifs?ids=id1,id2,id3&api_key=KEY`
4. Use `data[].images.fixed_height.url` for consistent display sizing

### 5. Random GIF with content filtering

1. Call `GET /gifs/random?tag=nature&rating=g&api_key=KEY`
2. If `data` is empty or unsatisfactory, retry without the `tag` to broaden: `GET /gifs/random?rating=g&api_key=KEY`
3. Extract the URL from `data.images.original.url`
4. If 429 is returned, wait 1-2 seconds and retry once before surfacing the rate limit to the user


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
