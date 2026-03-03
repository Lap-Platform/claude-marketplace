---
name: spotify-web-api
description: "Spotify Web API skill. Use when working with Spotify Web for albums, artists, shows. Covers 96 endpoints."
version: 1.0.0
generator: lapsh
---

# Spotify Web API
API version: 1.0.0

## Auth
OAuth2

## Base URL
https://api.spotify.com/v1

## Setup
1. Configure auth: OAuth2
2. GET /albums -- verify access
3. POST /playlists/{playlist_id}/tracks -- create first tracks

## Endpoints

96 endpoints across 16 groups. See references/api-spec.lap for full details.

### albums
| Method | Path | Description |
|--------|------|-------------|
| GET | /albums/{id} | Get Album |
| GET | /albums | Get Several Albums |
| GET | /albums/{id}/tracks | Get Album Tracks |

### artists
| Method | Path | Description |
|--------|------|-------------|
| GET | /artists/{id} | Get Artist |
| GET | /artists | Get Several Artists |
| GET | /artists/{id}/albums | Get Artist's Albums |
| GET | /artists/{id}/top-tracks | Get Artist's Top Tracks |
| GET | /artists/{id}/related-artists | Get Artist's Related Artists |

### shows
| Method | Path | Description |
|--------|------|-------------|
| GET | /shows/{id} | Get Show |
| GET | /shows | Get Several Shows |
| GET | /shows/{id}/episodes | Get Show Episodes |

### episodes
| Method | Path | Description |
|--------|------|-------------|
| GET | /episodes/{id} | Get Episode |
| GET | /episodes | Get Several Episodes |

### audiobooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /audiobooks/{id} | Get an Audiobook |
| GET | /audiobooks | Get Several Audiobooks |
| GET | /audiobooks/{id}/chapters | Get Audiobook Chapters |

### me
| Method | Path | Description |
|--------|------|-------------|
| GET | /me/audiobooks | Get User's Saved Audiobooks |
| PUT | /me/audiobooks | Save Audiobooks for Current User |
| DELETE | /me/audiobooks | Remove User's Saved Audiobooks |
| GET | /me/audiobooks/contains | Check User's Saved Audiobooks |
| GET | /me | Get Current User's Profile |
| GET | /me/playlists | Get Current User's Playlists |
| POST | /me/playlists | Create Playlist |
| PUT | /me/library | Save Items to Library |
| DELETE | /me/library | Remove Items from Library |
| GET | /me/library/contains | Check User's Saved Items |
| GET | /me/albums | Get User's Saved Albums |
| PUT | /me/albums | Save Albums for Current User |
| DELETE | /me/albums | Remove Users' Saved Albums |
| GET | /me/albums/contains | Check User's Saved Albums |
| GET | /me/tracks | Get User's Saved Tracks |
| PUT | /me/tracks | Save Tracks for Current User |
| DELETE | /me/tracks | Remove User's Saved Tracks |
| GET | /me/tracks/contains | Check User's Saved Tracks |
| GET | /me/episodes | Get User's Saved Episodes |
| PUT | /me/episodes | Save Episodes for Current User |
| DELETE | /me/episodes | Remove User's Saved Episodes |
| GET | /me/episodes/contains | Check User's Saved Episodes |
| GET | /me/shows | Get User's Saved Shows |
| PUT | /me/shows | Save Shows for Current User |
| DELETE | /me/shows | Remove User's Saved Shows |
| GET | /me/shows/contains | Check User's Saved Shows |
| GET | /me/top/{type} | Get User's Top Items |
| GET | /me/following | Get Followed Artists |
| PUT | /me/following | Follow Artists or Users |
| DELETE | /me/following | Unfollow Artists or Users |
| GET | /me/following/contains | Check If User Follows Artists or Users |
| GET | /me/player | Get Playback State |
| PUT | /me/player | Transfer Playback |
| GET | /me/player/devices | Get Available Devices |
| GET | /me/player/currently-playing | Get Currently Playing Track |
| PUT | /me/player/play | Start/Resume Playback |
| PUT | /me/player/pause | Pause Playback |
| POST | /me/player/next | Skip To Next |
| POST | /me/player/previous | Skip To Previous |
| PUT | /me/player/seek | Seek To Position |
| PUT | /me/player/repeat | Set Repeat Mode |
| PUT | /me/player/volume | Set Playback Volume |
| PUT | /me/player/shuffle | Toggle Playback Shuffle |
| GET | /me/player/recently-played | Get Recently Played Tracks |
| GET | /me/player/queue | Get the User's Queue |
| POST | /me/player/queue | Add Item to Playback Queue |

### chapters
| Method | Path | Description |
|--------|------|-------------|
| GET | /chapters/{id} | Get a Chapter |
| GET | /chapters | Get Several Chapters |

### tracks
| Method | Path | Description |
|--------|------|-------------|
| GET | /tracks/{id} | Get Track |
| GET | /tracks | Get Several Tracks |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search | Search for Item |

### playlists
| Method | Path | Description |
|--------|------|-------------|
| GET | /playlists/{playlist_id} | Get Playlist |
| PUT | /playlists/{playlist_id} | Change Playlist Details |
| GET | /playlists/{playlist_id}/tracks | Get Playlist Items [DEPRECATED] |
| POST | /playlists/{playlist_id}/tracks | Add Items to Playlist [DEPRECATED] |
| PUT | /playlists/{playlist_id}/tracks | Update Playlist Items [DEPRECATED] |
| DELETE | /playlists/{playlist_id}/tracks | Remove Playlist Items [DEPRECATED] |
| GET | /playlists/{playlist_id}/items | Get Playlist Items |
| POST | /playlists/{playlist_id}/items | Add Items to Playlist |
| PUT | /playlists/{playlist_id}/items | Update Playlist Items |
| DELETE | /playlists/{playlist_id}/items | Remove Playlist Items |
| PUT | /playlists/{playlist_id}/followers | Follow Playlist |
| DELETE | /playlists/{playlist_id}/followers | Unfollow Playlist |
| GET | /playlists/{playlist_id}/images | Get Playlist Cover Image |
| PUT | /playlists/{playlist_id}/images | Add Custom Playlist Cover Image |
| GET | /playlists/{playlist_id}/followers/contains | Check if Current User Follows Playlist |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/{user_id} | Get User's Profile |
| GET | /users/{user_id}/playlists | Get User's Playlists |
| POST | /users/{user_id}/playlists | Create Playlist for user |

### browse
| Method | Path | Description |
|--------|------|-------------|
| GET | /browse/featured-playlists | Get Featured Playlists |
| GET | /browse/categories | Get Several Browse Categories |
| GET | /browse/categories/{category_id} | Get Single Browse Category |
| GET | /browse/categories/{category_id}/playlists | Get Category's Playlists |
| GET | /browse/new-releases | Get New Releases |

### audio-features
| Method | Path | Description |
|--------|------|-------------|
| GET | /audio-features | Get Several Tracks' Audio Features |
| GET | /audio-features/{id} | Get Track's Audio Features |

### audio-analysis
| Method | Path | Description |
|--------|------|-------------|
| GET | /audio-analysis/{id} | Get Track's Audio Analysis |

### recommendations
| Method | Path | Description |
|--------|------|-------------|
| GET | /recommendations | Get Recommendations |
| GET | /recommendations/available-genre-seeds | Get Available Genre Seeds |

### markets
| Method | Path | Description |
|--------|------|-------------|
| GET | /markets | Get Available Markets |

## Enhanced Skill Content
## Question Mapping

- "What info do I have about a specific album?" -> GET /albums/{id}
- "Get details for multiple tracks at once?" -> GET /tracks
- "Search for an artist, album, or playlist by name?" -> GET /search
- "What are my saved/liked tracks?" -> GET /me/tracks
- "What's currently playing on my Spotify?" -> GET /me/player/currently-playing
- "Show me an artist's top tracks?" -> GET /artists/{id}/top-tracks
- "How do I create a new playlist?" -> POST /me/playlists
- "Add songs to an existing playlist?" -> POST /playlists/{playlist_id}/tracks
- "Remove tracks from a playlist?" -> DELETE /playlists/{playlist_id}/tracks
- "Get audio features like danceability and energy for a track?" -> GET /audio-features/{id}
- "What are my top artists or tracks?" -> GET /me/top/{type}
- "Skip to the next song?" -> POST /me/player/next
- "What devices are available for playback?" -> GET /me/player/devices
- "Get recommendations based on seed tracks or genres?" -> GET /recommendations
- "Do I follow a specific artist?" -> GET /me/following/contains

## Response Tips

- **Single resource endpoints** (albums/{id}, tracks/{id}, artists/{id}): Return the object directly at the top level; key fields are `id`, `uri`, `name`, and `type`.
- **Batch endpoints** (GET /albums, /tracks, /artists with `ids`): Return an array wrapper (e.g., `{albums: [...]}`) -- entries may be `null` for invalid IDs, so always check each element.
- **Paginated lists** (me/tracks, me/playlists, playlist tracks, search): Use `limit` and `offset` params; responses include `next`, `previous`, `total`, and `items` fields inside a paging object.
- **Search**: Returns a map per content type requested (tracks, artists, albums, etc.) -- each is its own paging object; only requested `type` keys are present.
- **Player endpoints**: GET /me/player returns 204 (no content) when nothing is active -- treat 204 as "no active session," not an error.
- **Write operations** (PUT/POST/DELETE on playlists, library, following): Most return 200/201/204 with no body or just `{snapshot_id}`; use snapshot_id for conflict detection on subsequent modifications.
- **Audio features/analysis**: Numeric values (danceability, energy, valence) are floats 0.0-1.0; loudness is in dB (negative); tempo is BPM; key uses pitch-class notation (0=C, 1=C#, ..., 11=B).

## Anomaly Flags

- **429 Too Many Requests**: Every endpoint can return 429. Surface the `Retry-After` header value and pause all requests for that duration. Alert the user immediately when hit.
- **204 on player endpoints**: GET /me/player and GET /me/player/currently-playing return 204 when no device is active -- surface this as "no active playback session" rather than treating it as empty data.
- **Null entries in batch responses**: When fetching multiple IDs via /albums, /tracks, etc., null array entries indicate invalid or unavailable IDs. Flag which IDs returned null.
- **Market restrictions**: Tracks and episodes may have `is_playable: false` or missing `preview_url` (null) depending on the `market` parameter. Surface when content is region-locked.
- **Deprecated audio features**: Audio features and audio analysis endpoints may be deprecated in future API versions. Flag if response structure changes or endpoints begin returning errors.
- **Empty recommendations**: GET /recommendations can return zero tracks if seeds are too restrictive or conflicting min/max tuning params eliminate all candidates. Surface this with a suggestion to loosen constraints.
- **Snapshot ID drift**: If a playlist modification returns a `snapshot_id` different from what was sent, another user modified the playlist concurrently. Alert on potential conflicts.

## Playbook

### Build a Playlist from Recommendations

1. Call `GET /recommendations/available-genre-seeds` to see valid genre values
2. Pick seed artists, genres, or tracks (up to 5 seeds total across all three)
3. Call `GET /recommendations` with seeds and optional tuning params (e.g., `min_energy=0.7`, `target_danceability=0.8`)
4. Create a new playlist via `POST /me/playlists` with a name and optional description
5. Extract track URIs from the recommendations response
6. Call `POST /playlists/{playlist_id}/tracks` with the list of URIs to populate the playlist

### Analyze a Track's Musical Properties

1. Search for the track via `GET /search` with `q=<track name>&type=track`
2. Extract the track `id` from the first search result
3. Call `GET /audio-features/{id}` for high-level attributes (danceability, energy, valence, tempo, key, mode)
4. Optionally call `GET /audio-analysis/{id}` for granular timing data (bars, beats, sections, segments)
5. Cross-reference with `GET /tracks/{id}` for metadata like popularity, album, and artists

### Manage Your Library

1. Check current saved tracks with `GET /me/tracks` (paginate with `limit` and `offset` to retrieve all)
2. Check if specific tracks are already saved via `GET /me/tracks/contains` with comma-separated `ids`
3. Save new tracks with `PUT /me/tracks` passing an array of track IDs
4. Remove tracks with `DELETE /me/tracks` passing the IDs to unsave
5. Repeat the same pattern for albums (`/me/albums`), shows (`/me/shows`), and episodes (`/me/episodes`)

### Control Playback Across Devices

1. Call `GET /me/player/devices` to list available devices and their IDs
2. Transfer playback to a device with `PUT /me/player` providing `device_ids`
3. Start playback with `PUT /me/player/play`, optionally passing `context_uri` (album/playlist) or `uris` (specific tracks)
4. Use `PUT /me/player/volume`, `PUT /me/player/shuffle`, and `PUT /me/player/repeat` to adjust settings
5. Queue upcoming tracks with `POST /me/player/queue` passing a track or episode `uri`
6. Navigate with `POST /me/player/next`, `POST /me/player/previous`, or seek with `PUT /me/player/seek`

### Explore an Artist's Catalog

1. Search for the artist via `GET /search` with `q=<name>&type=artist`
2. Get full artist details with `GET /artists/{id}` (genres, popularity, followers, images)
3. Fetch their top tracks with `GET /artists/{id}/top-tracks` (optionally pass `market`)
4. Browse their discography with `GET /artists/{id}/albums` using `include_groups` to filter by album, single, compilation, or appears_on
5. Discover similar artists via `GET /artists/{id}/related-artists` and repeat the exploration


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
