---
name: rawg-video-games-database-api
description: "RAWG Video Games Database API skill. Use when working with RAWG Video Games Database for creator-roles, creators, developers. Covers 30 endpoints."
version: 1.0.0
generator: lapsh
---

# RAWG Video Games Database API
API version: v1.0

## Auth
ApiKey (inferred from docs)

## Base URL
https://api.rawg.io/api

## Setup
1. Set your API key in the appropriate header
2. GET /creator-roles -- verify access

## Endpoints

30 endpoints across 9 groups. See references/api-spec.lap for full details.

### creator-roles
| Method | Path | Description |
|--------|------|-------------|
| GET | /creator-roles | Get a list of creator positions (jobs). |

### creators
| Method | Path | Description |
|--------|------|-------------|
| GET | /creators | Get a list of game creators. |
| GET | /creators/{id} | Get details of the creator. |

### developers
| Method | Path | Description |
|--------|------|-------------|
| GET | /developers | Get a list of game developers. |
| GET | /developers/{id} | Get details of the developer. |

### games
| Method | Path | Description |
|--------|------|-------------|
| GET | /games | Get a list of games. |
| GET | /games/{game_pk}/additions | Get a list of DLC's for the game, GOTY and other editions, companion apps, etc. |
| GET | /games/{game_pk}/development-team | Get a list of individual creators that were part of the development team. |
| GET | /games/{game_pk}/game-series | Get a list of games that are part of the same series. |
| GET | /games/{game_pk}/parent-games | Get a list of parent games for DLC's and editions. |
| GET | /games/{game_pk}/screenshots | Get screenshots for the game. |
| GET | /games/{game_pk}/stores | Get links to the stores that sell the game. |
| GET | /games/{id} | Get details of the game. |
| GET | /games/{id}/achievements | Get a list of game achievements. |
| GET | /games/{id}/movies | Get a list of game trailers. |
| GET | /games/{id}/reddit | Get a list of most recent posts from the game's subreddit. |
| GET | /games/{id}/suggested | Get a list of visually similar games, available only for business and enterprise API users. |
| GET | /games/{id}/twitch | Get streams on Twitch associated with the game, available only for business and enterprise API users. |
| GET | /games/{id}/youtube | Get videos from YouTube associated with the game, available only for business and enterprise API users. |

### genres
| Method | Path | Description |
|--------|------|-------------|
| GET | /genres | Get a list of video game genres. |
| GET | /genres/{id} | Get details of the genre. |

### platforms
| Method | Path | Description |
|--------|------|-------------|
| GET | /platforms | Get a list of video game platforms. |
| GET | /platforms/lists/parents | Get a list of parent platforms. |
| GET | /platforms/{id} | Get details of the platform. |

### publishers
| Method | Path | Description |
|--------|------|-------------|
| GET | /publishers | Get a list of video game publishers. |
| GET | /publishers/{id} | Get details of the publisher. |

### stores
| Method | Path | Description |
|--------|------|-------------|
| GET | /stores | Get a list of video game storefronts. |
| GET | /stores/{id} | Get details of the store. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags | Get a list of tags. |
| GET | /tags/{id} | Get details of the tag. |

## Enhanced Skill Content


## Question Mapping

- "What games are available for PlayStation?" -> GET /games?platforms={platform_id}
- "Search for a game by name" -> GET /games?search={query}
- "Get details about a specific game" -> GET /games/{id}
- "What platforms can I filter by?" -> GET /platforms
- "Show me all genres" -> GET /genres
- "What DLC or additions does this game have?" -> GET /games/{game_pk}/additions
- "Who developed this game?" -> GET /games/{game_pk}/development-team
- "What other games are in this series?" -> GET /games/{game_pk}/game-series
- "Show screenshots for a game" -> GET /games/{game_pk}/screenshots
- "Where can I buy this game?" -> GET /games/{game_pk}/stores
- "What are the top-rated games?" -> GET /games?ordering=-metacritic
- "List all publishers" -> GET /publishers
- "What achievements does this game have?" -> GET /games/{id}/achievements
- "Find games released in a date range" -> GET /games?dates={start},{end}
- "What tags are available for filtering?" -> GET /tags

## Response Tips

- **List endpoints** (`/games`, `/genres`, `/platforms`, etc.): Return paginated objects with `count`, `next`, `previous`, and `results` array. Follow `next` URL to paginate.
- **Detail endpoints** (`/games/{id}`, `/genres/{id}`, etc.): Return a flat object with nested arrays for related data (platforms, genres, tags, screenshots).
- **Sub-resource endpoints** (`/games/{id}/achievements`, `/screenshots`, etc.): Same paginated wrapper as list endpoints. The `game_pk` or `id` path param can be a slug or numeric ID.
- **Errors**: Expect `{"detail": "Not found."}` for invalid IDs. Auth failures return 401/403 when the API key is missing or invalid.

## Anomaly Flags

- **Missing API key**: All requests require a `key` query parameter. Surface a clear error if responses return 401 or 403.
- **Empty results**: If `count` is 0 and `results` is empty, flag that the search/filter may be too restrictive.
- **Pagination depth**: If `count` is very large (10,000+), warn the user that full iteration will require many requests.
- **Null nested fields**: Game detail responses may have `null` for `metacritic`, `reddit_url`, `website`, or `clip`. Do not assume these fields are always populated.
- **Slug vs ID ambiguity**: Path params accept both numeric IDs and string slugs. If a slug looks numeric, it may resolve to the wrong game. Prefer numeric IDs when available.
- **Rate limiting**: RAWG may throttle requests. If responses slow down or return 429, back off and retry with exponential delay.

## Playbook

### 1. Find and explore a specific game

1. `GET /games?search={name}&search_precise=true` to find the game
2. Pick the best match from `results` by checking `name` and `released`
3. `GET /games/{id}` for full details (description, metacritic, platforms, genres)
4. `GET /games/{id}/screenshots` for media
5. `GET /games/{game_pk}/stores` to find purchase links

### 2. Browse games by genre and platform

1. `GET /genres` to list available genres, note the `id` of the desired genre
2. `GET /platforms` to list platforms, note the `id` of the desired platform
3. `GET /games?genres={genre_id}&platforms={platform_id}&ordering=-rating` to get top-rated matches
4. Page through results using the `next` URL until you have enough entries

### 3. Discover a game series and its DLC

1. `GET /games/{id}` to get the base game details
2. `GET /games/{game_pk}/game-series` to find all entries in the series
3. `GET /games/{game_pk}/additions` to list DLC and expansions
4. `GET /games/{game_pk}/parent-games` to find the original if starting from a DLC

### 4. Research a game's community and media presence

1. `GET /games/{id}` for the base game info
2. `GET /games/{id}/reddit` for Reddit posts and discussions
3. `GET /games/{id}/youtube` for YouTube videos
4. `GET /games/{id}/twitch` for Twitch streams
5. `GET /games/{id}/movies` for trailers and gameplay videos

### 5. Explore developers and their game catalogs

1. `GET /developers?page_size=20` to browse developers
2. `GET /developers/{id}` for developer details including game count
3. `GET /games?developers={developer_id}&ordering=-added` to list their games sorted by popularity
4. Optionally filter further with `&metacritic=80,100` to show only highly-rated titles


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
