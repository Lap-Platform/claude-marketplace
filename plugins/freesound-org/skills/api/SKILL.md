---
name: freesound
description: "Freesound API skill. Use when working with Freesound for search, sounds. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Freesound
API version: 2.0.0

## Auth
No authentication required.

## Base URL
http://www.freesound.org/apiv2

## Setup
1. No auth setup needed
2. GET /search/text -- verify access

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search/text | Search sounds |

### sounds
| Method | Path | Description |
|--------|------|-------------|
| GET | /sounds/{soundId} | Details of a sound |

## Enhanced Skill Content
## Question Mapping

- "Search for rain sounds?" -> GET /search/text
- "Find ambient music loops?" -> GET /search/text
- "Get details about a specific sound?" -> GET /sounds/{soundId}
- "Search for sounds sorted by rating?" -> GET /search/text
- "Find drum samples under 5 seconds?" -> GET /search/text
- "What format and sample rate is sound #12345?" -> GET /sounds/{soundId}
- "Search for bird sounds and group results by pack?" -> GET /search/text
- "Get the license info for a sound?" -> GET /sounds/{soundId}
- "Browse page 3 of piano sound results?" -> GET /search/text
- "How many downloads does a sound have?" -> GET /sounds/{soundId}
- "Find Creative Commons sounds matching 'thunder'?" -> GET /search/text
- "Who uploaded sound #8821?" -> GET /sounds/{soundId}
- "Search for short notification sounds, 10 per page?" -> GET /search/text

## Response Tips

- **Search results** (`/search/text`): Paginated -- check `count` for total results, `next`/`previous` for page URLs. Default page size varies; set `page_size` explicitly for consistency. Empty queries may return broad results or 400 errors.
- **Sound details** (`/sounds/{soundId}`): Returns nested objects for user info, tags array, and file URLs. A 404 means the sound was deleted or the ID is invalid. Some fields (previews, analysis) may be absent depending on sound state.

## Anomaly Flags

- **400 on search**: Surface malformed `filter` syntax immediately -- Freesound uses a Solr-style filter language that is easy to get wrong
- **404 on sound detail**: Flag that the sound may have been removed by the uploader or moderated; suggest searching by name instead
- **Empty search results**: Proactively suggest relaxing filters or trying alternative keywords when `count` is 0
- **Large page_size values**: Warn if requesting >150 results per page, as the API may cap or reject oversized pages
- **Missing audio preview URLs**: Flag when a sound response lacks preview/download links, which can indicate processing-in-progress or restricted access

## Playbook

### 1. Find and inspect a sound

1. `GET /search/text?query=ocean waves&page_size=5` to find candidates
2. Pick a result and note its `id`
3. `GET /sounds/{soundId}` to retrieve full metadata (duration, tags, license, previews)

### 2. Browse sounds with filtering and pagination

1. `GET /search/text?query=guitar&filter=duration:[0 TO 10]&sort=rating_desc&page_size=10` for short, top-rated guitar sounds
2. Check `next` field in response for the next page URL
3. Continue fetching `next` until it is null or you have enough results

### 3. Search by pack grouping

1. `GET /search/text?query=footsteps&group_by_pack=1` to cluster results by sound pack
2. Review grouped results to find cohesive sound sets
3. `GET /sounds/{soundId}` on individual sounds within a pack for full details

### 4. Verify a sound exists before using it

1. `GET /sounds/{soundId}` with the known ID
2. If 404, fall back to `GET /search/text?query=<original name>` to find a replacement
3. Compare tags and duration of candidates to the original to pick the best match


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
