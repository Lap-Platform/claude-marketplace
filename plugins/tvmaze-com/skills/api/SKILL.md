---
name: tvmaze-user-api
description: "TVmaze user API skill. Use when working with TVmaze user for user, scrobble, auth. Covers 42 endpoints."
version: 1.0.0
generator: lapsh
---

# TVmaze user API
API version: 1.0

## Auth
basic

## Base URL
https://api.tvmaze.com/v1

## Setup
1. Configure auth: basic
2. GET /user/episodes -- verify access
3. POST /user/tags -- create first tags

## Endpoints

42 endpoints across 3 groups. See references/api-spec.lap for full details.

### user
| Method | Path | Description |
|--------|------|-------------|
| GET | /user/episodes | List the marked episodes |
| GET | /user/episodes/{episode_id} | Check if an episode is marked |
| PUT | /user/episodes/{episode_id} | Mark an episode |
| DELETE | /user/episodes/{episode_id} | Unmark an episode |
| GET | /user/follows/shows | List the followed shows |
| GET | /user/follows/shows/{show_id} | Check if a show is followed |
| PUT | /user/follows/shows/{show_id} | Follow a show |
| DELETE | /user/follows/shows/{show_id} | Unfollow a show |
| GET | /user/follows/people | List the followed people |
| GET | /user/follows/people/{person_id} | Check if a person is followed |
| PUT | /user/follows/people/{person_id} | Follow a person |
| DELETE | /user/follows/people/{person_id} | Unfollow a person |
| GET | /user/follows/networks | List the followed networks |
| GET | /user/follows/networks/{network_id} | Check if a network is followed |
| PUT | /user/follows/networks/{network_id} | Follow a network |
| DELETE | /user/follows/networks/{network_id} | Unfollow a network |
| GET | /user/follows/webchannels | List the followed webchannels |
| GET | /user/follows/webchannels/{webchannel_id} | Check if a webchannel is followed |
| PUT | /user/follows/webchannels/{webchannel_id} | Follow a webchannel |
| DELETE | /user/follows/webchannels/{webchannel_id} | Unfollow a webchannel |
| GET | /user/tags | List all tags |
| POST | /user/tags | Create a new tag |
| DELETE | /user/tags/{tag_id} | Delete a specific tag |
| PATCH | /user/tags/{tag_id} | Update a specific tag |
| GET | /user/tags/{tag_id}/shows | List all shows under this tag |
| PUT | /user/tags/{tag_id}/shows/{show_id} | Tag a show |
| DELETE | /user/tags/{tag_id}/shows/{show_id} | Untag a show |
| GET | /user/votes/shows | List the shows voted for |
| GET | /user/votes/shows/{show_id} | Check if a show is voted for |
| PUT | /user/votes/shows/{show_id} | Vote for a show |
| DELETE | /user/votes/shows/{show_id} | Remove a show vote |
| GET | /user/votes/episodes | List the episodes voted for |
| GET | /user/votes/episodes/{episode_id} | Check if an episode is voted for |
| PUT | /user/votes/episodes/{episode_id} | Vote for an episode |
| DELETE | /user/votes/episodes/{episode_id} | Remove an episode vote |

### scrobble
| Method | Path | Description |
|--------|------|-------------|
| GET | /scrobble/shows/{show_id} | List watched and acquired episodes for a show |
| PUT | /scrobble/episodes/{episode_id} | Mark an episode as acquired or watched based on its ID |
| POST | /scrobble/shows | Mark episodes within a show as acquired or watched based on their attributes |
| POST | /scrobble/episodes | Mark episodes as acquired or watched based on their IDs |

### auth
| Method | Path | Description |
|--------|------|-------------|
| POST | /auth/start | Start an authentication request |
| POST | /auth/poll | Poll whether an authentication request was confirmed |
| GET | /auth/validate | Validate your authentication credentials |

## Enhanced Skill Content
## Question Mapping

- "What episodes has the user watched?" -> GET /user/episodes
- "Has the user watched a specific episode?" -> GET /user/episodes/{episode_id}
- "Mark an episode as watched" -> PUT /user/episodes/{episode_id}
- "Remove an episode from my watched list" -> DELETE /user/episodes/{episode_id}
- "What shows am I following?" -> GET /user/follows/shows
- "Follow a new show" -> PUT /user/follows/shows/{show_id}
- "Unfollow a show" -> DELETE /user/follows/shows/{show_id}
- "List all my custom tags" -> GET /user/tags
- "Create a new tag for organizing shows" -> POST /user/tags
- "Which shows have I tagged with a specific tag?" -> GET /user/tags/{tag_id}/shows
- "Tag a show" -> PUT /user/tags/{tag_id}/shows/{show_id}
- "What shows have I voted on?" -> GET /user/votes/shows
- "Rate a show" -> PUT /user/votes/shows/{show_id}
- "Bulk import my watch history" -> POST /scrobble/episodes
- "Is my API token still valid?" -> GET /auth/validate

## Response Tips

- **Episodes/Follows/Votes lists** (`GET /user/*`): Returns flat arrays; use the `embed` param on follows to inline full show/person/network objects and avoid extra lookups.
- **Single resource GETs** (`GET /user/*/{ id }`): Returns the object directly; a 404 means the user has no relationship with that resource (not watched, not followed, etc.) -- this is normal, not an error.
- **PUT/DELETE on resources**: 200 confirms the action; response body is the updated or removed relationship object.
- **Scrobble POST endpoints**: Watch for 207 Multi-Status -- this means partial success where some episodes were accepted and others rejected. Parse the per-item status in the response body.
- **Validation errors (422)**: Returned when a PUT/POST body is malformed or contains invalid values. The response body contains field-level error details.
- **Auth endpoints**: `POST /auth/start` initiates a device-auth flow; `POST /auth/poll` returns 403 while the user has not yet approved -- this is expected polling behavior, not a failure.

## Anomaly Flags

- **429 on auth endpoints**: Rate limit hit on `/auth/start` or `/auth/poll` -- back off exponentially and surface to the user that they are polling too frequently.
- **207 Multi-Status on scrobble**: Partial success -- agent should parse individual item results and report which episodes failed and why.
- **Repeated 404s on follows/votes**: May indicate stale show/episode IDs from a cached list -- suggest refreshing the resource list.
- **422 on PUT with body**: Likely a schema mismatch -- surface the validation error details so the user can correct their input.
- **401 on /auth/validate**: Token has expired or been revoked -- prompt re-authentication via the `/auth/start` flow.
- **Bulk scrobble with all failures**: If a `POST /scrobble/episodes` returns 422 rather than 207, the entire payload was rejected -- flag the format issue immediately.

## Playbook

### 1. Authenticate and validate a session

1. Call `POST /auth/start` with the required credentials body to initiate device auth.
2. Poll `POST /auth/poll` at intervals (respect 429 backoff) until a 200 response with a token is returned.
3. Confirm the token works with `GET /auth/validate` (expect 200).
4. Use the token as Basic auth credentials for all subsequent requests.

### 2. Track and organize shows with tags

1. List existing tags with `GET /user/tags`.
2. Create a new tag via `POST /user/tags` with a body containing the tag name.
3. Follow the show first with `PUT /user/follows/shows/{show_id}` if not already followed.
4. Assign the tag to a show with `PUT /user/tags/{tag_id}/shows/{show_id}`.
5. Verify by fetching `GET /user/tags/{tag_id}/shows` with `embed` to see full show details.

### 3. Bulk import watch history via scrobble

1. Identify the show using `GET /scrobble/shows/{show_id}` to confirm it exists and get episode structure.
2. Build an episodes array with episode identifiers and watch timestamps.
3. Submit via `POST /scrobble/episodes` with the episodes payload.
4. If 207 is returned, parse per-episode results and retry or fix failed entries.
5. Verify the import with `GET /user/episodes?show_id={show_id}` to confirm episodes are tracked.

### 4. Rate and review your watched shows

1. Fetch your watched episodes with `GET /user/episodes` to identify shows you have engaged with.
2. Check existing votes with `GET /user/votes/shows` to avoid duplicates.
3. Submit a vote with `PUT /user/votes/shows/{show_id}` including the vote value in the body.
4. Optionally vote on individual episodes with `PUT /user/votes/episodes/{episode_id}`.
5. To change a vote, call the same PUT endpoint with an updated body; to remove it, use DELETE.

### 5. Manage follows across all resource types

1. List current follows: `GET /user/follows/shows`, `/people`, `/networks`, `/webchannels` (use `embed` for full details).
2. Check a specific follow with `GET /user/follows/shows/{show_id}` -- 404 means not following.
3. Add a follow with `PUT /user/follows/shows/{show_id}` (same pattern for people, networks, webchannels).
4. Remove with `DELETE /user/follows/shows/{show_id}`.
5. Repeat across resource types as needed -- the API pattern is identical for shows, people, networks, and webchannels.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
