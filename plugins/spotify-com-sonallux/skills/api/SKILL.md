---
name: spotify-web-api-with-fixes-and-improvements-from-sonallux
description: "Spotify Web API with fixes and improvements from sonallux API skill. Use when working with Spotify Web API with fixes and improvements from sonallux for albums, artists, shows. Covers 97 endpoints."
version: 1.0.0
generator: lapsh
---

# Spotify Web API with fixes and improvements from sonallux
API version: 2025.5.18

## Auth
OAuth2

## Base URL
https://api.spotify.com/v1

## Setup
1. Configure auth: OAuth2
2. GET /albums -- verify access
3. POST /playlists/{playlist_id}/tracks -- create first tracks

## Endpoints

97 endpoints across 16 groups. See references/api-spec.lap for full details.

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
| GET | /me/top/artists | Get User's Top Artists |
| GET | /me/top/tracks | Get User's Top Tracks |

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

- "What songs are in this playlist?" -> GET /playlists/{playlist_id}/tracks
- "Who is this artist and what genres do they play?" -> GET /artists/{id}
- "What's currently playing on my Spotify?" -> GET /me/player/currently-playing
- "Add these tracks to my playlist" -> POST /playlists/{playlist_id}/tracks
- "What are my top artists this month?" -> GET /me/top/artists
- "Find songs similar to this track" -> GET /recommendations (with seed_tracks)
- "Skip to the next song" -> POST /me/player/next
- "What devices can I play music on?" -> GET /me/player/devices
- "Search for an artist or album" -> GET /search
- "Is this album in my library?" -> GET /me/albums/contains
- "What are the audio features of this track (danceability, energy, tempo)?" -> GET /audio-features/{id}
- "Create a new playlist for me" -> POST /me/playlists
- "Remove a track from my playlist" -> DELETE /playlists/{playlist_id}/tracks
- "What albums has this artist released?" -> GET /artists/{id}/albums
- "Show me new releases on Spotify" -> GET /browse/new-releases

## Response Tips

- **Paginated lists** (tracks, albums, playlists, episodes, shows): Responses include `limit`, `offset`, `total`, `next`, and `previous` fields. Use `offset` + `limit` to page through. Max `limit` is typically 50.
- **Batch endpoints** (GET /tracks, /albums, /artists, /episodes): Pass comma-separated IDs in the `ids` query param. Max 20 IDs for most, 50 for some. Returns an array; missing/unavailable items appear as `null` in the array.
- **Player endpoints**: GET /me/player returns 204 (no body) when nothing is active. PUT/POST player commands return 204 on success with no body -- absence of error means success.
- **Search**: Returns a map per requested `type` (tracks, artists, albums, etc.), each containing a paging object with `items`, `total`, `limit`, `offset`.
- **Library contains**: GET /me/{type}/contains returns a bare JSON array of booleans, positionally matching the input `ids`.
- **Playlist mutations**: POST/PUT/DELETE on playlist tracks return a `snapshot_id` string. Use this for optimistic concurrency -- pass it back on subsequent mutations to avoid conflicts.
- **Audio analysis**: Returns deeply nested timing arrays (`bars`, `beats`, `sections`, `segments`, `tatums`) that can be very large. Parse selectively.

## Anomaly Flags

- **429 Too Many Requests**: Every endpoint can return 429. Surface the `Retry-After` header value and pause all requests for that duration. Alert the user if 429s occur repeatedly.
- **204 from GET /me/player**: No active device or playback session. Proactively suggest the user open Spotify on a device before issuing playback commands.
- **Empty devices list**: GET /me/player/devices returning zero devices means no controllable targets. Flag before attempting play/pause/skip.
- **Null items in batch responses**: When fetching multiple IDs, null entries indicate unavailable or region-restricted content. Surface which IDs returned null.
- **Market-restricted content**: `is_playable: false` or missing `preview_url` on tracks signals regional restrictions. Suggest retrying with the user's `market` parameter.
- **Deprecated audio features**: Audio features and audio analysis endpoints may be deprecated in future API versions. Flag if responses return unexpected schemas or empty objects.
- **Playlist snapshot_id mismatch**: If a DELETE/PUT on playlist tracks fails, the playlist may have been modified concurrently. Surface the conflict and suggest refetching.
- **OAuth scope errors (403)**: A 403 typically means the token lacks the required scope (e.g., `user-modify-playback-state` for player controls). Surface the missing scope to the user.

## Playbook

### Build a Mood-Based Playlist

1. GET /recommendations/available-genre-seeds to discover valid genre names
2. GET /recommendations with `seed_genres`, `target_valence`, `target_energy`, and `target_danceability` tuned to the desired mood (e.g., high valence + high energy = upbeat)
3. POST /me/playlists with a descriptive `name` and `description` to create the playlist
4. POST /playlists/{playlist_id}/tracks with the `uris` array from the recommendations response
5. Optionally GET /playlists/{playlist_id} to confirm track count and share the link via `external_urls.spotify`

### Explore an Artist's Catalog

1. GET /search with `q` set to the artist name and `type=artist` to find the artist ID
2. GET /artists/{id} to retrieve genres, popularity, follower count, and images
3. GET /artists/{id}/top-tracks with `market` to get their most popular songs
4. GET /artists/{id}/albums with `include_groups=album,single` to browse their discography (paginate with `offset` if prolific)
5. GET /artists/{id}/related-artists to discover similar artists for further exploration

### Control Playback Across Devices

1. GET /me/player/devices to list available devices and their IDs
2. PUT /me/player with `device_ids` to transfer playback to the target device
3. PUT /me/player/play with `uris` or `context_uri` to start specific content, or omit to resume
4. Use PUT /me/player/volume, PUT /me/player/shuffle, and PUT /me/player/repeat to adjust playback settings
5. Monitor with GET /me/player to verify state (is_playing, progress_ms, current track)

### Audit and Clean Up Your Library

1. GET /me/tracks with pagination (`limit=50`, incrementing `offset`) to fetch all saved tracks
2. GET /audio-features with batches of track IDs (up to 100 comma-separated) to analyze your collection
3. GET /me/tracks/contains with specific `ids` to verify which tracks are saved
4. DELETE /me/tracks with `ids` of tracks you want to remove
5. Repeat for albums (GET /me/albums, DELETE /me/albums) and shows (GET /me/shows, DELETE /me/shows)

### Queue Up a Listening Session

1. GET /me/player to confirm an active playback session exists (watch for 204 = no session)
2. GET /search or GET /artists/{id}/top-tracks to find track URIs to queue
3. POST /me/player/queue with each `uri` to add tracks one at a time (the endpoint accepts one URI per call)
4. GET /me/player/queue to verify the queue contents and order
5. POST /me/player/next to skip ahead if the current track should be bypassed


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
