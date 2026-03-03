---
name: art19-content-api-documentation
description: "ART19 Content API Documentation API skill. Use when working with ART19 Content API Documentation for classification_inclusions, classifications, credits. Covers 62 endpoints."
version: 1.0.0
generator: lapsh
---

# ART19 Content API Documentation
API version: 1.0.0

## Auth
ApiKey Authorization in header

## Base URL
https://art19.com/

## Setup
1. Set your API key in the appropriate header
2. GET /classification_inclusions -- verify access
3. POST /credits -- create first credits

## Endpoints

62 endpoints across 15 groups. See references/api-spec.lap for full details.

### classification_inclusions
| Method | Path | Description |
|--------|------|-------------|
| GET | /classification_inclusions | Get ClassificationInclusion records |
| GET | /classification_inclusions/{id} | Get a specific classification inclusion |

### classifications
| Method | Path | Description |
|--------|------|-------------|
| GET | /classifications | Get a list of classifications |
| GET | /classifications/{id} | Get a specific classification |

### credits
| Method | Path | Description |
|--------|------|-------------|
| GET | /credits | Get a list of credits |
| POST | /credits | Create a new credit |
| DELETE | /credits/{id} | Delete a specific credit |
| GET | /credits/{id} | Get a specific credit |
| PATCH | /credits/{id} | Update a specific credit |

### episode_versions
| Method | Path | Description |
|--------|------|-------------|
| GET | /episode_versions | Get a list of episode versions |
| POST | /episode_versions | Create a new episode version |
| DELETE | /episode_versions/{id} | Delete an episode version |
| GET | /episode_versions/{id} | Get a specific episode version |
| PATCH | /episode_versions/{id} | Update an episode version |

### episodes
| Method | Path | Description |
|--------|------|-------------|
| GET | /episodes | Get a list of episodes |
| POST | /episodes | Create a new episode |
| DELETE | /episodes/{id} | Delete a specific episode |
| GET | /episodes/{id} | Get a specific episode |
| PATCH | /episodes/{id} | Update a specific episode |
| GET | /episodes/{id}/next_sibling | Get the episode released right after the specified one |
| GET | /episodes/{id}/previous_sibling | Get the episode released right before the specified one |

### feed_items
| Method | Path | Description |
|--------|------|-------------|
| GET | /feed_items | Get a list of feed items |
| POST | /feed_items | Create a new feed item |
| DELETE | /feed_items/{id} | Delete a specific feed item |
| GET | /feed_items/{id} | Get a specific feed item |
| PATCH | /feed_items/{id} | Update a specific feed item |

### feeds
| Method | Path | Description |
|--------|------|-------------|
| GET | /feeds | Get a list of feeds |
| POST | /feeds | Create a new feed |
| DELETE | /feeds/{id} | Delete a specific feed |
| GET | /feeds/{id} | Get a specific feed |
| PATCH | /feeds/{id} | Update a specific feed |

### images
| Method | Path | Description |
|--------|------|-------------|
| GET | /images | Get a list of images |
| POST | /images | Create a new image |
| DELETE | /images/{id} | Delete an image |
| GET | /images/{id} | Get a specific image |

### marker_point_content_rules
| Method | Path | Description |
|--------|------|-------------|
| GET | /marker_point_content_rules | Get a list of marker point content rules |
| POST | /marker_point_content_rules | Create a new marker point content rule |
| DELETE | /marker_point_content_rules/{id} | Delete a marker point content rule |
| GET | /marker_point_content_rules/{id} | Get a specific marker point content rule |
| PATCH | /marker_point_content_rules/{id} | Update a marker point content rule |

### marker_points
| Method | Path | Description |
|--------|------|-------------|
| GET | /marker_points | Get a list of marker points |
| POST | /marker_points | Create a new marker point |
| DELETE | /marker_points/{id} | Delete a marker point |
| GET | /marker_points/{id} | Get a specific marker point |
| PATCH | /marker_points/{id} | Update a marker point |

### media_assets
| Method | Path | Description |
|--------|------|-------------|
| GET | /media_assets | Get a list of media assets |
| GET | /media_assets/{id} | Get a specific media asset |

### networks
| Method | Path | Description |
|--------|------|-------------|
| GET | /networks | Get a list of networks |
| GET | /networks/{id} | Get a specific network |
| PATCH | /networks/{id} | Update a specific network |

### people
| Method | Path | Description |
|--------|------|-------------|
| GET | /people | Get a list of people |
| POST | /people | Create a new person |
| GET | /people/{id} | Get a specific person |
| PATCH | /people/{id} | Update a specific person |

### seasons
| Method | Path | Description |
|--------|------|-------------|
| GET | /seasons | Get a list of seasons |
| POST | /seasons | Create a new season |
| DELETE | /seasons/{id} | Delete a specific season |
| GET | /seasons/{id} | Get a specific season |
| PATCH | /seasons/{id} | Update a specific season |

### series
| Method | Path | Description |
|--------|------|-------------|
| GET | /series | Get a list of series |
| GET | /series/{id} | Get a specific series |
| PATCH | /series/{id} | Update a specific series |

## Enhanced Skill Content
## Question Mapping

- "List all episodes for a series?" -> GET /episodes (with `series_id` filter)
- "How do I search for a podcast by name?" -> GET /series (with `q` parameter)
- "What feeds does a series have?" -> GET /feeds (with `series_id` filter)
- "How do I publish a new episode?" -> POST /episodes
- "How do I add someone as a credit on an episode?" -> POST /credits (with `creditable_id` and `creditable_type`)
- "What classifications or categories are available?" -> GET /classifications
- "How do I delete an episode?" -> DELETE /episodes/{id}
- "What episodes were released this month?" -> GET /episodes (with `year`, `month`, or `released_after`/`released_before`)
- "How do I update a series description or metadata?" -> PATCH /series/{id}
- "What is the next episode after this one?" -> GET /episodes/{id}/next_sibling
- "How do I upload an image for a series or episode?" -> POST /images
- "How do I set ad insertion marker points on an episode?" -> POST /marker_points
- "What networks exist and which series belong to them?" -> GET /networks then GET /series (with `network_id`)
- "How do I create a new season for a series?" -> POST /seasons
- "How do I assign a classification to an episode?" -> POST /classification_inclusions (with `classified_id`, `classified_type`, `classification_id`)

## Response Tips

- **List endpoints** (episodes, feeds, feed_items, marker_points, marker_point_content_rules): Require `page[number]` for pagination -- always pass page number starting at 1 and follow next-page links in response metadata.
- **Single-resource GETs**: Return the resource object directly; some support `include` param (episodes, seasons, series) to sideload related resources and reduce round trips.
- **POST/PATCH**: Expect JSON:API-style request bodies; 422 means validation failure -- check the `errors` array for field-level details. 415 means wrong Content-Type (must be `application/vnd.api+json`).
- **DELETE**: Returns 204 with no body on success; any other status indicates failure.
- **Search** (`q` param): Available on episodes, feed_items, classifications, networks, people, seasons, series -- returns matching results sorted by relevance unless `sort` overrides.
- **Media assets**: Read-only retrieval (no PATCH/DELETE); filter by `attachment_id` and `attachment_type` to find assets linked to a specific resource.

## Anomaly Flags

- **429 Too Many Requests**: Every endpoint can return 429. Surface rate limit headers (`Retry-After`, `X-RateLimit-Remaining`) proactively when approaching limits. Back off before hitting the wall.
- **507 Insufficient Storage**: Returned by all write operations (POST/PATCH/DELETE). Indicates a storage quota has been exceeded -- alert the user immediately as further writes will fail until resolved.
- **406 Not Acceptable**: All endpoints return this. Likely means the `Accept` header is missing or wrong -- flag if this appears on a previously-working integration as it suggests a client misconfiguration.
- **403 Forbidden on reads**: If a GET that previously worked starts returning 403, the API key's permissions may have been revoked or the resource moved to a different network. Surface this change immediately.
- **Missing pagination**: If a list endpoint returns fewer results than expected without a next-page link, flag that the result set may be truncated or filters may be too restrictive.
- **Stale episode versions**: If `GET /episode_versions` returns versions with no corresponding feed items, flag orphaned versions that may need cleanup.

## Playbook

### 1. Publish a New Episode to a Feed

1. `GET /series` with `q` to find the target series and note its `id`
2. `GET /seasons?series_id={series_id}` to find or verify the target season
3. `POST /episodes` with the episode metadata (title, description, season, series references)
4. `POST /images` to upload episode artwork, linking it to the new episode
5. `GET /feeds?series_id={series_id}` to find the target feed
6. `POST /feed_items` to add the episode to the feed (linking episode and feed)
7. `POST /episode_versions` to create a version of the episode for the feed item
8. Verify with `GET /episodes/{id}?include=feed_items` to confirm the episode appears correctly

### 2. Set Up Ad Insertion Marker Points

1. `GET /episodes/{id}` to retrieve the episode and confirm its duration and status
2. `POST /marker_points` to create pre-roll, mid-roll, and post-roll markers (specifying `episode_id`, `type`, and timestamp)
3. `POST /marker_point_content_rules` for each marker point to define what ad content fills each slot
4. `GET /marker_points?episode_id={id}` to verify all markers are correctly placed
5. `GET /marker_point_content_rules?marker_point_id={id}` to confirm content rules are attached

### 3. Manage Credits and People on an Episode

1. `GET /people?q={name}` to search for existing people records
2. If the person does not exist, `POST /people` to create them
3. `POST /credits` with `creditable_id` set to the episode ID, `creditable_type` set to `Episode`, and the person reference
4. `GET /credits?creditable_id={episode_id}&creditable_type=Episode` to list all credits and verify
5. To update a role, `PATCH /credits/{id}`; to remove, `DELETE /credits/{id}`

### 4. Organize Episodes by Season and Classification

1. `POST /seasons` to create a new season under the series (if needed)
2. `PATCH /episodes/{id}` to move episodes into the new season by updating `season_id`
3. `GET /classifications?type={type}` to find available classification categories (genres, topics, countries)
4. For each episode, `POST /classification_inclusions` with `classified_id` (episode), `classified_type` ("Episode"), and `classification_id`
5. Verify with `GET /classification_inclusions?classified_id={episode_id}&classified_type=Episode`

### 5. Audit and Clean Up a Series' Feed

1. `GET /feeds?series_id={series_id}` to list all feeds for the series
2. `GET /feed_items?feed_id={feed_id}&page[number]=1` and paginate through all items
3. For each feed item, `GET /episode_versions?feed_item_id={id}` to check version linkage
4. Identify orphaned or unpublished feed items (`published` filter) and remove with `DELETE /feed_items/{id}`
5. Remove unused episode versions with `DELETE /episode_versions/{id}`
6. `GET /feed_items?feed_id={feed_id}&sort=released_at` to verify the feed is clean and ordered correctly


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
