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

- "What information is available about a specific album?" -> GET /albums/{id}
- "Search for tracks, artists, or playlists by name" -> GET /search
- "What is currently playing on my Spotify?" -> GET /me/player/currently-playing
- "Show me my saved/liked tracks" -> GET /me/tracks
- "Add a song to my playlist" -> POST /playlists/{playlist_id}/tracks
- "What are an artist's most popular songs?" -> GET /artists/{id}/top-tracks
- "Get recommendations based on seed tracks or genres" -> GET /recommendations
- "What devices are available for playback?" -> GET /me/player/devices
- "Skip to the next track" -> POST /me/player/next
- "What are my top artists or tracks over time?" -> GET /me/top/artists
- "Remove tracks from a playlist" -> DELETE /playlists/{playlist_id}/tracks
- "Create a new playlist for a user" -> POST /users/{user_id}/playlists
- "Get the audio features (danceability, energy, tempo) of a track" -> GET /audio-features/{id}
- "Do I already follow this artist?" -> GET /me/following/contains
- "What genres are available for recommendations?" -> GET /recommendations/available-genre-seeds

## Response Tips

- **Albums/Artists/Tracks/Shows/Episodes**: Single-item GETs return the object directly; multi-item GETs (`?ids=`) wrap results in a keyed array (e.g., `{albums: [...]}`) where entries can be `null` for invalid IDs.
- **Paginated lists** (tracks in playlist, saved items, search results): Use `limit` and `offset` params; responses include `total`, `next`, and `previous` URLs -- follow `next` until it is `null` to exhaust pages.
- **Search**: Returns a map per requested `type` (tracks, artists, albums, etc.), each containing its own paginated object with `items`, `total`, `limit`, `offset`.
- **Player endpoints**: GET /me/player returns 204 (no body) when nothing is active; always check status code before parsing JSON.
- **Write/Delete operations on playlists**: Return a `snapshot_id` string -- store this to make subsequent operations idempotent and to detect concurrent edits.
- **Library endpoints** (`/me/tracks`, `/me/albums`, etc.): `contains` endpoints return a plain JSON array of booleans in the same order as the `ids` query param.
- **Recommendations**: `seeds` array in the response shows which seed values were actually used and how many results each contributed.

## Anomaly Flags

- **429 Too Many Requests**: Every endpoint can return 429. Surface the `Retry-After` header value and pause all requests for that duration. Alert the user if 429s occur more than twice in a session.
- **204 No Content from player**: GET /me/player returning 204 means no active device -- surface this clearly rather than treating it as an error.
- **Null entries in batch responses**: When fetching multiple IDs (`/albums?ids=`, `/tracks?ids=`), individual entries may be `null` for invalid or region-restricted IDs. Flag which IDs returned null.
- **Market restrictions**: Tracks with `is_playable: false` or non-empty `restrictions` indicate region-locked content. Proactively warn when a track is unavailable in the user's market.
- **Deprecated `preview_url`**: The `preview_url` field on tracks is nullable (`str?`) and increasingly returns `null`. Alert if a workflow depends on preview URLs and none are available.
- **Empty queue**: GET /me/player/queue may return `currently_playing: null` with an empty `queue` array when playback is inactive. Surface this state explicitly.
- **Snapshot drift**: If a playlist `snapshot_id` returned from a write differs from the one sent, another client modified the playlist concurrently. Flag this for the user.

## Playbook

### 1. Build a Personalized Recommendation Playlist

1. GET /me/top/tracks?time_range=short_term&limit=5 -- get the user's recent favorites
2. GET /recommendations?seed_tracks={ids}&target_energy=0.7&limit=20 -- generate recommendations
3. POST /users/{user_id}/playlists with `name` and `description` -- create a new playlist
4. POST /playlists/{playlist_id}/tracks with `uris` from the recommendations response -- populate the playlist

### 2. Analyze the Mood of a Playlist

1. GET /playlists/{playlist_id}/tracks?limit=50 -- fetch all tracks (paginate with `offset` if more than 50)
2. Collect all track IDs from the paginated results
3. GET /audio-features?ids={comma-separated-ids} -- batch fetch audio features (max 100 IDs per call)
4. Aggregate `valence`, `energy`, `danceability`, and `tempo` across all tracks to produce a mood profile

### 3. Transfer Playback and Start a Playlist

1. GET /me/player/devices -- list available devices
2. PUT /me/player with `device_ids` set to the target device -- transfer playback
3. PUT /me/player/play with `context_uri` set to the playlist/album URI -- start playing
4. GET /me/player -- confirm playback state on the new device

### 4. Curate a Playlist by Removing Unwanted Tracks

1. GET /playlists/{playlist_id} -- get current playlist details and `snapshot_id`
2. GET /playlists/{playlist_id}/tracks?limit=50 -- fetch all tracks (paginate as needed)
3. Identify tracks to remove based on criteria (e.g., low popularity, explicit content)
4. DELETE /playlists/{playlist_id}/tracks with `tracks: [{uri: "..."}]` and the current `snapshot_id`
5. Verify the returned `snapshot_id` to confirm the edit was applied cleanly

### 5. Discover and Follow Related Artists

1. GET /search?q={artist_name}&type=artist&limit=1 -- find the seed artist's ID
2. GET /artists/{id}/related-artists -- get up to 20 related artists
3. GET /me/following/contains?type=artist&ids={related_ids} -- check which ones the user already follows
4. PUT /me/following?type=artist&ids={unfollowed_ids} -- follow the new discoveries
5. GET /artists/{id}/top-tracks?market={user_market} for each new artist -- preview their best work


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
