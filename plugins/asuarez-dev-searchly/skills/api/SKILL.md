---
name: searchly-api-v1
description: "SearchLy API v1 API skill. Use when working with SearchLy API v1 for similarity, song. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# SearchLy API v1
API version: 1.0

## Auth
No authentication required.

## Base URL
https://searchly.asuarez.dev/api/v1

## Setup
1. No auth setup needed
2. GET /similarity/by_song -- verify access
3. POST /similarity/by_content -- create first by_content

## Endpoints

3 endpoints across 2 groups. See references/api-spec.lap for full details.

### similarity
| Method | Path | Description |
|--------|------|-------------|
| GET | /similarity/by_song | API endpoint to search similarity using a song identifier |
| POST | /similarity/by_content | API endpoint to search similarity using content |

### song
| Method | Path | Description |
|--------|------|-------------|
| GET | /song/search | API endpoint to search songs from the database given a query |

## Enhanced Skill Content
## Question Mapping

- "Find songs similar to this one?" -> GET /similarity/by_song
- "What songs sound like song ID 42?" -> GET /similarity/by_song
- "Get recommendations based on a specific song?" -> GET /similarity/by_song
- "Find similar songs from these lyrics?" -> POST /similarity/by_content
- "What songs match this text?" -> POST /similarity/by_content
- "Find songs with similar themes to this paragraph?" -> POST /similarity/by_content
- "Search for a song by name?" -> GET /song/search
- "Look up a song called 'Bohemian Rhapsody'?" -> GET /song/search
- "Find the song ID so I can get recommendations?" -> GET /song/search, then GET /similarity/by_song
- "What songs are similar to one matching these keywords?" -> GET /song/search, then GET /similarity/by_song
- "Find songs related to custom lyrics I wrote?" -> POST /similarity/by_content
- "Does a song exist in the database?" -> GET /song/search
- "Get a similarity list for multiple songs?" -> GET /similarity/by_song (repeated per song_id)
- "Compare two songs for similarity?" -> GET /similarity/by_song for each, then compare overlap in similarity_list

## Response Tips

- **All endpoints**: Check `error` (bool) first; if `true`, read `message` for the failure reason before accessing `response`.
- **Similarity endpoints**: Results live in `response.similarity_list` -- each entry is a map; expect fields like song ID, title, and a similarity score. An empty list means no matches, not an error.
- **Song search**: Results live in `response.results` -- each entry is a map representing a matched song. Use the song's ID from here to feed into `/similarity/by_song`.

## Anomaly Flags

- **`error: true` in response**: Surface the `message` field immediately -- the API uses soft errors (HTTP 200 with error flag) rather than HTTP status codes for most failures.
- **Empty similarity_list or results**: Proactively tell the user no matches were found rather than silently returning nothing.
- **Missing or null song_id**: Flag before calling `/similarity/by_song` -- the parameter is required and an invalid ID will waste a round-trip.
- **Large similarity_list**: If the list is unexpectedly large, summarize the top results rather than dumping everything.
- **POST with empty content**: Warn if `/similarity/by_content` is called with blank or very short content, as results may be meaningless.

## Playbook

### 1. Find Songs Similar to a Known Song

1. If you only have a song name, call `GET /song/search?query=<name>` to find it.
2. Pick the best match from `response.results` and note its `song_id`.
3. Call `GET /similarity/by_song?song_id=<id>`.
4. Present `response.similarity_list` ranked by similarity score.

### 2. Discover Songs from Lyrics or a Text Passage

1. Collect the lyrics or text from the user.
2. Call `POST /similarity/by_content` with `content` set to the text.
3. Return the `response.similarity_list`, highlighting the top matches.
4. If the user wants deeper exploration, take a result's song ID and call `GET /similarity/by_song` for second-degree recommendations.

### 3. Explore a Genre or Theme

1. Ask the user for a representative song or descriptive keywords.
2. Call `GET /song/search?query=<keywords>` to find seed songs.
3. For each promising result, call `GET /similarity/by_song?song_id=<id>`.
4. Merge and deduplicate the similarity lists to build a broader playlist.
5. Present the consolidated list, noting which seed song each recommendation came from.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
