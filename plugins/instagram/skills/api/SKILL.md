---
name: instagram-api
description: "Instagram API skill. Use when working with Instagram for geographies, locations, media. Covers 27 endpoints."
version: 1.0.0
generator: lapsh
---

# Instagram API
API version: 1.0.0

## Auth
ApiKey access_token in query | OAuth2

## Base URL
https://api.instagram.com/v1

## Setup
1. Set your API key in the appropriate header
2. GET /locations/search -- verify access
3. POST /media/{media-id}/comments -- create first comments

## Endpoints

27 endpoints across 5 groups. See references/api-spec.lap for full details.

### geographies
| Method | Path | Description |
|--------|------|-------------|
| GET | /geographies/{geo-id}/media/recent | Get recent media from a custom geo-id. |

### locations
| Method | Path | Description |
|--------|------|-------------|
| GET | /locations/search | Search for a location by geographic coordinate. |
| GET | /locations/{location-id} | Get information about a location. |
| GET | /locations/{location-id}/media/recent | Get a list of recent media objects from a given location. |

### media
| Method | Path | Description |
|--------|------|-------------|
| GET | /media/popular | Get a list of currently popular media. |
| GET | /media/search | Search for media in a given area. |
| GET | /media/shortcode/{shortcode} | Get information about a media object. |
| GET | /media/{media-id} | Get information about a media object. |
| GET | /media/{media-id}/comments | Get a list of recent comments on a media object. |
| POST | /media/{media-id}/comments | Create a comment on a media object. |
| DELETE | /media/{media-id}/comments/{comment-id} | Remove a comment. |
| DELETE | /media/{media-id}/likes | Remove a like on this media by the current user. |
| GET | /media/{media-id}/likes | Get a list of users who have liked this media. |
| POST | /media/{media-id}/likes | Set a like on this media by the current user. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/search | Search for tags by name. |
| GET | /tags/{tag-name} | Get information about a tag object. |
| GET | /tags/{tag-name}/media/recent | Get a list of recently tagged media. |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/search | Search for a user by name. |
| GET | /users/self/feed | See the authenticated user's feed. |
| GET | /users/self/media/liked | See the list of media liked by the authenticated user. |
| GET | /users/self/requested-by | List the users who have requested this user's permission to follow. |
| GET | /users/{user-id} | Get basic information about a user. |
| GET | /users/{user-id}/followed-by | Get the list of users this user is followed by. |
| GET | /users/{user-id}/follows | Get the list of users this user follows. |
| GET | /users/{user-id}/media/recent | Get the most recent media published by a user. |
| GET | /users/{user-id}/relationship | Get information about a relationship to another user. |
| POST | /users/{user-id}/relationship | Modify the relationship between the current user and the target user. |

## Enhanced Skill Content
## Question Mapping

- "How do I search for users by name?" -> GET /users/search
- "What media is popular right now?" -> GET /media/popular
- "How do I get a user's recent posts?" -> GET /users/{user-id}/media/recent
- "How do I find media near a specific location?" -> GET /media/search
- "How do I look up a post by its shortcode from a URL?" -> GET /media/shortcode/{shortcode}
- "Who follows a given user?" -> GET /users/{user-id}/followed-by
- "Who does a user follow?" -> GET /users/{user-id}/follows
- "How do I like a post?" -> POST /media/{media-id}/likes
- "How do I comment on a post?" -> POST /media/{media-id}/comments
- "How do I delete a comment I left?" -> DELETE /media/{media-id}/comments/{comment-id}
- "How do I search for locations near coordinates?" -> GET /locations/search
- "What posts are tagged with a specific hashtag?" -> GET /tags/{tag-name}/media/recent
- "How do I follow or unfollow someone?" -> POST /users/{user-id}/relationship
- "What does my feed look like?" -> GET /users/self/feed
- "Who has requested to follow me?" -> GET /users/self/requested-by

## Response Tips

- **Media endpoints**: Responses nest image/video data under `images` and `videos` objects with resolution variants (`low_resolution`, `standard_resolution`, `thumbnail`). Pagination uses `min_id`/`max_id` cursor fields in a top-level `pagination` object -- pass these as query params to page forward/backward.
- **User endpoints**: User profiles return `counts` with `media`, `follows`, `followed_by`. A 404 means the user ID is invalid or the account is deactivated. Relationship status is a separate call.
- **Location/Geography endpoints**: Location search supports multiple ID systems (Facebook Places, Foursquare v1/v2) -- only one is needed. Distance is in meters.
- **Tag endpoints**: Tag objects include `media_count`. Recent media under a tag paginates via `min_tag_id`/`max_tag_id`, not the standard `min_id`/`max_id`.
- **Comments/Likes**: Comment creation returns the new comment object. Like/unlike return a simple `meta` status. Likes list returns an array of user summary objects, not full profiles.

## Anomaly Flags

- **Rate limit headers**: Surface `X-Ratelimit-Remaining` when it drops below 20% of `X-Ratelimit-Limit`. Instagram's default is 500 requests/hour per token -- alert well before exhaustion.
- **Deprecated API version**: This spec targets v1, which Instagram has sunset in favor of the Instagram Graph API. Flag any 400/403 responses that indicate endpoint deprecation or migration requirements.
- **Empty pagination**: If `pagination` is present but contains no `next_url` or cursor IDs, the result set is complete -- do not retry or assume an error.
- **OAuth scope errors**: A 400 with `OAuthPermissionsException` means the token lacks required scopes (e.g., `public_content`, `comments`, `relationships`). Surface the missing scope name.
- **Sandbox mode restrictions**: If responses consistently return only a small fixed set of users/media, the app is likely in sandbox mode. Flag this so the user can submit for review.
- **Unusual 429/503 responses**: Instagram may throttle beyond standard rate limits during high traffic. Surface retry-after timing if present.

## Playbook

### 1. Explore a hashtag and save top posts

1. `GET /tags/{tag-name}` to confirm the tag exists and check `media_count`
2. `GET /tags/{tag-name}/media/recent` to fetch the first page of results
3. For each media item, extract `id`, `images.standard_resolution.url`, `likes.count`, and `caption.text`
4. Page through results using `max_tag_id` from the `pagination` object until you have enough posts or reach a `min_tag_id` boundary

### 2. Analyze a user's profile and recent activity

1. `GET /users/search?q={username}` to resolve a username to a `user-id`
2. `GET /users/{user-id}` to retrieve full profile including follower/following counts
3. `GET /users/{user-id}/media/recent?count=20` to pull their latest posts
4. `GET /users/{user-id}/followed-by` and `GET /users/{user-id}/follows` to examine their social graph
5. `GET /users/{user-id}/relationship` to check your relationship status with them

### 3. Engage with a specific post

1. `GET /media/shortcode/{shortcode}` to resolve a post URL (instagram.com/p/{shortcode}) to a `media-id` and view details
2. `GET /media/{media-id}/comments` to read existing comments
3. `POST /media/{media-id}/likes` to like the post
4. `POST /media/{media-id}/comments` with `text` to leave a comment
5. If needed, `DELETE /media/{media-id}/comments/{comment-id}` to remove your comment

### 4. Find and browse media near a place

1. `GET /locations/search?lat={lat}&lng={lng}&distance=1000` to find nearby location IDs
2. Pick a location and `GET /locations/{location-id}` for its name and coordinates
3. `GET /locations/{location-id}/media/recent` to browse recent posts from that spot
4. Use `min_timestamp`/`max_timestamp` to narrow results to a specific time window
5. Alternatively, `GET /media/search?lat={lat}&lng={lng}` for a coordinate-based media search without a specific location ID

### 5. Manage follow relationships

1. `GET /users/self/requested-by` to see pending follow requests
2. `POST /users/{user-id}/relationship` with `action=approve` or `action=ignore` to handle each request
3. To follow a new user: `POST /users/{user-id}/relationship` with `action=follow`
4. To unfollow: `POST /users/{user-id}/relationship` with `action=unfollow`
5. Verify the outcome with `GET /users/{user-id}/relationship` to confirm the updated status


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
