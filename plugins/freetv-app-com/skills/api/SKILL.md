---
name: mixerbox-freecabletv
description: "MixerBox FreecableTV API skill. Use when working with MixerBox FreecableTV for services?funcs=GetShowsForChatGPT&mobile=0, services?funcs=GetMoviesForChatGPT&mobile=0, services?funcs=GetChannelsForChatGPT&mobile=0. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# MixerBox FreecableTV
API version: v1

## Auth
No authentication required.

## Base URL
https://api.freetv-app.com

## Setup
1. No auth setup needed
2. GET /services?funcs=GetShowsForChatGPT&mobile=0 -- verify access

## Endpoints

3 endpoints across 3 groups. See references/api-spec.lap for full details.

### services?funcs=GetShowsForChatGPT&mobile=0
| Method | Path | Description |
|--------|------|-------------|
| GET | /services?funcs=GetShowsForChatGPT&mobile=0 | Get the latest or trending TV shows for a specific country. |

### services?funcs=GetMoviesForChatGPT&mobile=0
| Method | Path | Description |
|--------|------|-------------|
| GET | /services?funcs=GetMoviesForChatGPT&mobile=0 | Get the latest or trending movies for a specific country. |

### services?funcs=GetChannelsForChatGPT&mobile=0
| Method | Path | Description |
|--------|------|-------------|
| GET | /services?funcs=GetChannelsForChatGPT&mobile=0 | Get specific type of channels, including news channels, sports channels and live channels. |

## Enhanced Skill Content


## Question Mapping

- "What TV shows are available?" -> GET /services?funcs=GetShowsForChatGPT&mobile=0
- "Show me trending movies" -> GET /services?funcs=GetMoviesForChatGPT&mobile=0&category=trending
- "What live TV channels can I watch?" -> GET /services?funcs=GetChannelsForChatGPT&mobile=0
- "Find horror movies" -> GET /services?funcs=GetMoviesForChatGPT&mobile=0&category=horror
- "What kids shows are available in the US?" -> GET /services?funcs=GetShowsForChatGPT&mobile=0&country=us&category=kids
- "Show me news channels in Japan" -> GET /services?funcs=GetChannelsForChatGPT&mobile=0&country=jp&category=news
- "What are the latest shows?" -> GET /services?funcs=GetShowsForChatGPT&mobile=0&category=latest
- "Find comedy movies in Taiwan" -> GET /services?funcs=GetMoviesForChatGPT&mobile=0&country=tw&category=comedy
- "Are there any sports channels?" -> GET /services?funcs=GetChannelsForChatGPT&mobile=0&category=sports
- "Show me page 2 of drama shows" -> GET /services?funcs=GetShowsForChatGPT&mobile=0&category=drama&offset=10&limit=10
- "What documentaries can I watch?" -> GET /services?funcs=GetShowsForChatGPT&mobile=0&category=documentary
- "Find sci-fi movies and shows" -> GET /services?funcs=GetMoviesForChatGPT&mobile=0&category=sci-fi + GET /services?funcs=GetShowsForChatGPT&mobile=0&category=sci-fi
- "What political news channels are available?" -> GET /services?funcs=GetChannelsForChatGPT&mobile=0&category=politics
- "Show me the first 5 trending shows" -> GET /services?funcs=GetShowsForChatGPT&mobile=0&category=trending&limit=5

## Response Tips

- **Shows/Movies/Channels**: All responses wrap in a top-level key matching the function name (e.g., `GetShowsForChatGPT`). Access `.items` for the content array and `.rules` for display/usage rules the agent must follow.
- **Pagination**: Use `offset` and `limit` query params manually; responses do not include next-page cursors, so track offset client-side and increment by `limit` to paginate.
- **Errors**: No error schema is documented; expect standard HTTP status codes. A 200 with an empty `items` array means no results for that filter combination, not an error.

## Anomaly Flags

- **Empty results for broad queries**: If a request with no category or country filter returns zero items, the API may be experiencing issues -- surface this to the user.
- **Rules array content**: Always read and follow the `rules` strings returned in each response; these may contain usage restrictions, attribution requirements, or content warnings that must be surfaced.
- **Country availability gaps**: Some country codes beyond `tw`, `us`, `jp` may be accepted by movies but not by shows/channels (shows and channels explicitly restrict to those three). Flag when a user requests an unsupported country.
- **Category mismatch across endpoints**: Show categories (e.g., `reality`, `variety`, `animation`, `crime`, `sports`) do not exist for movies, and channel categories (e.g., `news`, `live`, `business`, `review`) are entirely different. Flag if a user asks for a category on the wrong content type.
- **Large offset with no results**: If paginating and items suddenly return empty, the user has passed the end of available content -- notify them rather than continuing to paginate.

## Playbook

### 1. Browse content by category

1. Decide content type: shows, movies, or channels
2. Call the corresponding endpoint with `category` set (e.g., `category=horror`)
3. Optionally add `country` to narrow by region
4. Read the `rules` array and follow any display instructions
5. Present items from the `items` array to the user

### 2. Paginate through a large catalog

1. Make an initial request with `limit=10&offset=0`
2. Display the returned `items`
3. If the user wants more, increment offset by the limit value (e.g., `offset=10`)
4. Repeat until `items` returns empty, indicating no more results
5. Inform the user when the end of the catalog is reached

### 3. Cross-content discovery (find a genre across types)

1. Call GetShowsForChatGPT with the desired category (e.g., `category=action`)
2. Call GetMoviesForChatGPT with the same category in parallel
3. Merge and present results, clearly labeling which are shows vs. movies
4. Note: channels use different categories (news, sports, etc.) so skip if the genre does not apply

### 4. Region-specific content exploration

1. Set `country` param to the user's region (`us`, `tw`, or `jp` for shows/channels; freeform for movies)
2. Call all three endpoints in parallel with that country filter
3. Aggregate results into a unified "What's available in [country]" view
4. Flag any endpoint that returns empty -- content availability varies by region

### 5. Quick recommendations for a new user

1. Call GetShowsForChatGPT with `category=trending&limit=5`
2. Call GetMoviesForChatGPT with `category=trending&limit=5`
3. Call GetChannelsForChatGPT with `category=live&limit=5`
4. Present a curated "Start here" list combining the top trending shows, movies, and live channels
5. Read and respect all `rules` in each response before displaying


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
