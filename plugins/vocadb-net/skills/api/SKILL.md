---
name: vocadbweb
description: "VocaDbWeb API skill. Use when working with VocaDbWeb for api. Covers 134 endpoints."
version: 1.0.0
generator: lapsh
---

# VocaDbWeb
API version: 1.0

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /api/activityEntries -- verify access
3. POST /api/albums/comments/{commentId} -- create first comments

## Endpoints

134 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/activityEntries |  |
| DELETE | /api/albums/{id} |  |
| GET | /api/albums/{id} |  |
| DELETE | /api/albums/comments/{commentId} |  |
| POST | /api/albums/comments/{commentId} |  |
| GET | /api/albums/{id}/comments |  |
| POST | /api/albums/{id}/comments |  |
| GET | /api/albums |  |
| GET | /api/albums/names |  |
| GET | /api/albums/new |  |
| GET | /api/albums/{id}/reviews |  |
| POST | /api/albums/{id}/reviews |  |
| GET | /api/albums/{id}/user-collections |  |
| DELETE | /api/albums/{id}/reviews/{reviewId} |  |
| GET | /api/albums/top |  |
| GET | /api/albums/{id}/tracks |  |
| GET | /api/albums/{id}/tracks/fields |  |
| GET | /api/albums/{id}/related |  |
| DELETE | /api/artists/{id} |  |
| GET | /api/artists/{id} |  |
| DELETE | /api/artists/comments/{commentId} |  |
| POST | /api/artists/comments/{commentId} |  |
| GET | /api/artists/{id}/comments |  |
| POST | /api/artists/{id}/comments |  |
| GET | /api/artists |  |
| GET | /api/artists/names |  |
| DELETE | /api/comments/{entryType}-comments/{commentId} |  |
| POST | /api/comments/{entryType}-comments/{commentId} |  |
| GET | /api/comments/{entryType}-comments |  |
| POST | /api/comments/{entryType}-comments |  |
| GET | /api/comments/{entryType}-comments/{entryId}/locked |  |
| POST | /api/comments/{entryType}-comments/{entryId}/locked |  |
| GET | /api/comments |  |
| DELETE | /api/discussions/comments/{commentId} |  |
| POST | /api/discussions/comments/{commentId} |  |
| DELETE | /api/discussions/topics/{topicId} |  |
| GET | /api/discussions/topics/{topicId} |  |
| POST | /api/discussions/topics/{topicId} |  |
| GET | /api/discussions/folders |  |
| POST | /api/discussions/folders |  |
| GET | /api/discussions/topics |  |
| GET | /api/discussions/folders/{folderId}/topics |  |
| POST | /api/discussions/folders/{folderId}/topics |  |
| POST | /api/discussions/topics/{topicId}/comments |  |
| GET | /api/entries |  |
| GET | /api/entries/random |  |
| GET | /api/entries/names |  |
| GET | /api/entry-types/{entryType}/{subType}/tag |  |
| GET | /api/pvs/for-songs |  |
| GET | /api/pvs/thumbnail |  |
| DELETE | /api/releaseEvents/{id} |  |
| GET | /api/releaseEvents/{id} |  |
| GET | /api/releaseEvents/{eventId}/albums |  |
| GET | /api/releaseEvents/{eventId}/published-songs |  |
| GET | /api/releaseEvents |  |
| GET | /api/releaseEvents/names |  |
| POST | /api/releaseEvents/{eventId}/reports |  |
| DELETE | /api/releaseEventSeries/{id} |  |
| GET | /api/releaseEventSeries/{id} |  |
| GET | /api/releaseEventSeries |  |
| GET | /api/releaseEventSeries/{id}/for-edit |  |
| GET | /api/resources/{cultureCode} |  |
| DELETE | /api/songs/comments/{commentId} |  |
| POST | /api/songs/comments/{commentId} |  |
| DELETE | /api/songs/{id} |  |
| GET | /api/songs/{id} |  |
| GET | /api/songs/{id}/comments |  |
| POST | /api/songs/{id}/comments |  |
| GET | /api/songs/{id}/derived |  |
| GET | /api/songs/highlighted |  |
| GET | /api/songs/{id}/ratings |  |
| POST | /api/songs/{id}/ratings |  |
| GET | /api/songs/{id}/related |  |
| GET | /api/songs |  |
| GET | /api/songs/lyrics/{lyricsId} |  |
| GET | /api/songs/names |  |
| GET | /api/songs/byPv |  |
| GET | /api/songs/top-rated |  |
| DELETE | /api/songLists/{id} |  |
| DELETE | /api/songLists/comments/{commentId} |  |
| POST | /api/songLists/comments/{commentId} |  |
| GET | /api/songLists/{listId}/comments |  |
| POST | /api/songLists/{listId}/comments |  |
| GET | /api/songLists/featured |  |
| GET | /api/songLists/featured/names |  |
| GET | /api/songLists/{listId}/songs |  |
| POST | /api/songLists |  |
| DELETE | /api/tags/{id} |  |
| GET | /api/tags/{id} |  |
| DELETE | /api/tags/comments/{commentId} |  |
| POST | /api/tags/comments/{commentId} |  |
| GET | /api/tags/byName/{name} |  |
| GET | /api/tags/categoryNames |  |
| GET | /api/tags/{tagId}/children |  |
| GET | /api/tags/{tagId}/comments |  |
| POST | /api/tags/{tagId}/comments |  |
| GET | /api/tags |  |
| POST | /api/tags |  |
| GET | /api/tags/names |  |
| GET | /api/tags/top |  |
| POST | /api/tags/{tagId}/reports |  |
| DELETE | /api/users/current/followedTags/{tagId} |  |
| POST | /api/users/current/followedTags/{tagId} |  |
| DELETE | /api/users/profileComments/{commentId} |  |
| POST | /api/users/profileComments/{commentId} |  |
| GET | /api/users/{id}/albums |  |
| GET | /api/users/current |  |
| GET | /api/users/{id}/events |  |
| GET | /api/users/{id}/followedArtists |  |
| GET | /api/users |  |
| GET | /api/users/{id} |  |
| GET | /api/users/messages/{messageId} |  |
| GET | /api/users/{id}/messages |  |
| DELETE | /api/users/{id}/messages |  |
| POST | /api/users/{id}/messages |  |
| GET | /api/users/names |  |
| GET | /api/users/{id}/profileComments |  |
| POST | /api/users/{id}/profileComments |  |
| GET | /api/users/{id}/ratedSongs |  |
| GET | /api/users/{id}/songLists |  |
| GET | /api/users/{id}/ratedSongs/{songId} |  |
| GET | /api/users/current/ratedSongs/{songId} |  |
| POST | /api/users/current/albums/{albumId} |  |
| POST | /api/users/current/refreshEntryEdit |  |
| POST | /api/users/{id}/reports |  |
| POST | /api/users/current/songTags/{songId} |  |
| POST | /api/users/{id}/settings/{settingName} |  |
| GET | /api/users/{id}/followedArtists/{artistId} |  |
| GET | /api/users/current/followedArtists/{artistId} |  |
| GET | /api/users/{id}/album-collection-statuses/{albumId} |  |
| GET | /api/users/current/album-collection-statuses/{albumId} |  |
| DELETE | /api/venues/{id} |  |
| GET | /api/venues |  |
| POST | /api/venues/{id}/reports |  |

## Enhanced Skill Content
## Question Mapping

- "What Vocaloid songs match a keyword?" -> GET /api/songs
- "Show me details for a specific album" -> GET /api/albums/{id}
- "Who is this artist and what are their popular songs?" -> GET /api/artists/{id} (with `relations` and `fields` params)
- "Find songs by a specific artist" -> GET /api/songs (with `artistId[]` filter)
- "What are the top-rated songs right now?" -> GET /api/songs/top-rated
- "Look up a song by its YouTube or Niconico video ID" -> GET /api/songs/byPv
- "What albums were released at a specific event?" -> GET /api/releaseEvents/{eventId}/albums
- "Show me a user's album collection" -> GET /api/users/{id}/albums
- "What songs has a user rated?" -> GET /api/users/{id}/ratedSongs
- "Get the lyrics for a song" -> GET /api/songs/lyrics/{lyricsId}
- "What artists am I following?" -> GET /api/users/{id}/followedArtists
- "Find events happening between two dates" -> GET /api/releaseEvents (with `afterDate`/`beforeDate`)
- "What are the most popular tags for a category?" -> GET /api/tags/top
- "Search across all entry types at once" -> GET /api/entries
- "Show me recent edits and activity on the database" -> GET /api/activityEntries

## Response Tips

- **List endpoints** (songs, albums, artists, tags, events, users, songLists, venues): All return `{items, term, totalCount}`. Set `getTotalCount=True` to get the total; default is `False` so `totalCount` may be 0. Paginate with `start` and `maxResults` (defaults vary: 10 for most, 50 for activity/comments, 25 for top-rated).
- **Detail endpoints** (single song/album/artist/tag/event): Deeply nested objects with optional expansions controlled by `fields` param (comma-separated). Omitting `fields` returns a minimal response; always request the fields you need.
- **Comment endpoints**: Comments across all entry types share the same structure (`author`, `message`, `created`, `entry`). The `entry` sub-object is polymorphic and includes fields for all entry types (many will be empty strings or defaults).
- **Delete endpoints**: Return bare 200 with no body. Some support `hardDelete` (events, tags, songLists, venues); albums, artists, and songs only soft-delete.
- **Name autocomplete** (`/names` variants): Return flat arrays of strings, not the standard `{items, totalCount}` wrapper.

## Anomaly Flags

- **Deleted or merged entries**: Surface `deleted: true` or non-zero `mergedTo` fields immediately -- the user is likely looking at stale data and should follow the merge target.
- **Empty `releaseDate`**: When `releaseDate.isEmpty` is `true` on an album, flag that release date is unknown rather than silently omitting it.
- **High `maxResults` requests**: Default page sizes are intentionally small (10-25). If a workflow requires iterating many pages, warn about potential slowness and suggest narrowing filters.
- **Missing PV services**: When `pvServices` is empty on a song, the entry has no linked videos -- flag this as the song may be incomplete or the videos may have been taken down.
- **Status values**: Entries with status `Draft` or `Locked` indicate incomplete or restricted items. Surface the status when it is not `Approved`/`Finished`.
- **Language parameter inconsistency**: Some endpoints use `lang`, others use `languagePreference`. If a user sets one and gets untranslated names, suggest the alternate parameter.
- **Comment lock state**: Check `GET /api/comments/{entryType}-comments/{entryId}/locked` before attempting to post a comment -- locked entries will reject new comments silently or with an unhelpful error.

## Playbook

### 1. Research a Vocaloid producer's discography

1. Search for the artist: `GET /api/artists?query=ProducerName&artistTypes=Producer&fields=MainPicture,Tags`
2. Pick the matching artist and note their `id`
3. Fetch full profile with relations: `GET /api/artists/{id}?fields=Description,Tags,WebLinks&relations=PopularSongs,PopularAlbums,LatestSongs,LatestAlbums`
4. For each album of interest, get track listings: `GET /api/albums/{id}/tracks?fields=ThumbUrl,Artists`
5. Optionally get comments and community discussion: `GET /api/artists/{id}/comments`

### 2. Build a playlist from a tag

1. Find the tag: `GET /api/tags?query=electronic&fields=Description`
2. Note the tag `id` from results
3. Search songs with that tag: `GET /api/songs?tagId[]=123&sort=RatingScore&maxResults=50&getTotalCount=True&fields=ThumbUrl,PVs`
4. For each song, extract PV URLs from the `pvs` array (filter by `service` for YouTube/NicoNico)
5. Optionally create a song list: `POST /api/songLists` with the song IDs linked via `songLinks`

### 3. Track new album releases

1. Query recent albums: `GET /api/albums/new?fields=MainPicture,ReleaseDate,Tags`
2. For deeper filtering, use: `GET /api/albums?releaseDateAfter=2026-01-01T00:00:00Z&sort=ReleaseDate&getTotalCount=True&fields=ReleaseDate,Artists,Tags`
3. For each album, check its event: inspect `releaseEvent` or `releaseEvents` in the response
4. Get full event details if relevant: `GET /api/releaseEvents/{id}?fields=Artists,MainPicture,Venue`
5. Check the event's other albums: `GET /api/releaseEvents/{eventId}/albums`

### 4. Manage your collection and ratings

1. Get current user profile: `GET /api/users/current?fields=MainPicture,KnownLanguages`
2. Check collection status for an album: `GET /api/users/current/album-collection-statuses/{albumId}`
3. Add an album to your collection: `POST /api/users/current/albums/{albumId}` with `collectionStatus`, `mediaType`, and `rating`
4. Rate a song: `POST /api/songs/{id}/ratings` with `rating` set to `Like`, `Favorite`, or `Nothing`
5. Review rated songs: `GET /api/users/{id}/ratedSongs?sort=RatingDate&groupByRating=True&getTotalCount=True`

### 5. Moderate content and handle reports

1. Review recent activity: `GET /api/activityEntries?editEvent=Created&maxResults=50&getTotalCount=True`
2. Check if comments are locked on an entry: `GET /api/comments/{entryType}-comments/{entryId}/locked`
3. Lock comments if needed: `POST /api/comments/{entryType}-comments/{entryId}/locked`
4. Report problematic entries: `POST /api/tags/{tagId}/reports`, `POST /api/releaseEvents/{eventId}/reports`, `POST /api/venues/{id}/reports`, or `POST /api/users/{id}/reports` with `reportType` and `notes`
5. Soft-delete content: `DELETE /api/songs/{id}` (or albums/artists) with `notes` explaining the reason


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
