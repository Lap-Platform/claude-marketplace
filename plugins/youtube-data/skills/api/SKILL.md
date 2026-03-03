---
name: youtube-data-api-v3
description: "YouTube Data API v3 API skill. Use when working with YouTube Data API v3 for youtube. Covers 76 endpoints."
version: 1.0.0
generator: lapsh
---

# YouTube Data API v3
API version: v3

## Auth
OAuth2 | OAuth2

## Base URL
https://youtube.googleapis.com/

## Setup
1. Configure auth: OAuth2 | OAuth2
2. GET /youtube/v3/activities -- verify access
3. POST /youtube/v3/abuseReports -- create first abuseReports

## Endpoints

76 endpoints across 1 groups. See references/api-spec.lap for full details.

### youtube
| Method | Path | Description |
|--------|------|-------------|
| POST | /youtube/v3/abuseReports | Inserts a new resource into this collection. |
| GET | /youtube/v3/activities | Retrieves a list of resources, possibly filtered. |
| DELETE | /youtube/v3/captions | Deletes a resource. |
| GET | /youtube/v3/captions | Retrieves a list of resources, possibly filtered. |
| POST | /youtube/v3/captions | Inserts a new resource into this collection. |
| PUT | /youtube/v3/captions | Updates an existing resource. |
| GET | /youtube/v3/captions/{id} | Downloads a caption track. |
| POST | /youtube/v3/channelBanners/insert | Inserts a new resource into this collection. |
| DELETE | /youtube/v3/channelSections | Deletes a resource. |
| GET | /youtube/v3/channelSections | Retrieves a list of resources, possibly filtered. |
| POST | /youtube/v3/channelSections | Inserts a new resource into this collection. |
| PUT | /youtube/v3/channelSections | Updates an existing resource. |
| GET | /youtube/v3/channels | Retrieves a list of resources, possibly filtered. |
| PUT | /youtube/v3/channels | Updates an existing resource. |
| GET | /youtube/v3/commentThreads | Retrieves a list of resources, possibly filtered. |
| POST | /youtube/v3/commentThreads | Inserts a new resource into this collection. |
| PUT | /youtube/v3/commentThreads | Updates an existing resource. |
| DELETE | /youtube/v3/comments | Deletes a resource. |
| GET | /youtube/v3/comments | Retrieves a list of resources, possibly filtered. |
| POST | /youtube/v3/comments | Inserts a new resource into this collection. |
| PUT | /youtube/v3/comments | Updates an existing resource. |
| POST | /youtube/v3/comments/markAsSpam | Expresses the caller's opinion that one or more comments should be flagged as spam. |
| POST | /youtube/v3/comments/setModerationStatus | Sets the moderation status of one or more comments. |
| GET | /youtube/v3/i18nLanguages | Retrieves a list of resources, possibly filtered. |
| GET | /youtube/v3/i18nRegions | Retrieves a list of resources, possibly filtered. |
| DELETE | /youtube/v3/liveBroadcasts | Delete a given broadcast. |
| GET | /youtube/v3/liveBroadcasts | Retrieve the list of broadcasts associated with the given channel. |
| POST | /youtube/v3/liveBroadcasts | Inserts a new stream for the authenticated user. |
| PUT | /youtube/v3/liveBroadcasts | Updates an existing broadcast for the authenticated user. |
| POST | /youtube/v3/liveBroadcasts/bind | Bind a broadcast to a stream. |
| POST | /youtube/v3/liveBroadcasts/cuepoint | Insert cuepoints in a broadcast |
| POST | /youtube/v3/liveBroadcasts/transition | Transition a broadcast to a given status. |
| DELETE | /youtube/v3/liveChat/bans | Deletes a chat ban. |
| POST | /youtube/v3/liveChat/bans | Inserts a new resource into this collection. |
| DELETE | /youtube/v3/liveChat/messages | Deletes a chat message. |
| GET | /youtube/v3/liveChat/messages | Retrieves a list of resources, possibly filtered. |
| POST | /youtube/v3/liveChat/messages | Inserts a new resource into this collection. |
| DELETE | /youtube/v3/liveChat/moderators | Deletes a chat moderator. |
| GET | /youtube/v3/liveChat/moderators | Retrieves a list of resources, possibly filtered. |
| POST | /youtube/v3/liveChat/moderators | Inserts a new resource into this collection. |
| DELETE | /youtube/v3/liveStreams | Deletes an existing stream for the authenticated user. |
| GET | /youtube/v3/liveStreams | Retrieve the list of streams associated with the given channel. -- |
| POST | /youtube/v3/liveStreams | Inserts a new stream for the authenticated user. |
| PUT | /youtube/v3/liveStreams | Updates an existing stream for the authenticated user. |
| GET | /youtube/v3/members | Retrieves a list of members that match the request criteria for a channel. |
| GET | /youtube/v3/membershipsLevels | Retrieves a list of all pricing levels offered by a creator to the fans. |
| DELETE | /youtube/v3/playlistItems | Deletes a resource. |
| GET | /youtube/v3/playlistItems | Retrieves a list of resources, possibly filtered. |
| POST | /youtube/v3/playlistItems | Inserts a new resource into this collection. |
| PUT | /youtube/v3/playlistItems | Updates an existing resource. |
| DELETE | /youtube/v3/playlists | Deletes a resource. |
| GET | /youtube/v3/playlists | Retrieves a list of resources, possibly filtered. |
| POST | /youtube/v3/playlists | Inserts a new resource into this collection. |
| PUT | /youtube/v3/playlists | Updates an existing resource. |
| GET | /youtube/v3/search | Retrieves a list of search resources |
| DELETE | /youtube/v3/subscriptions | Deletes a resource. |
| GET | /youtube/v3/subscriptions | Retrieves a list of resources, possibly filtered. |
| POST | /youtube/v3/subscriptions | Inserts a new resource into this collection. |
| GET | /youtube/v3/superChatEvents | Retrieves a list of resources, possibly filtered. |
| POST | /youtube/v3/tests | POST method. |
| DELETE | /youtube/v3/thirdPartyLinks | Deletes a resource. |
| GET | /youtube/v3/thirdPartyLinks | Retrieves a list of resources, possibly filtered. |
| POST | /youtube/v3/thirdPartyLinks | Inserts a new resource into this collection. |
| PUT | /youtube/v3/thirdPartyLinks | Updates an existing resource. |
| POST | /youtube/v3/thumbnails/set | As this is not an insert in a strict sense (it supports uploading/setting of a thumbnail for multiple videos, which doesn't result in creation of a single resource), I use a custom verb here. |
| GET | /youtube/v3/videoAbuseReportReasons | Retrieves a list of resources, possibly filtered. |
| GET | /youtube/v3/videoCategories | Retrieves a list of resources, possibly filtered. |
| DELETE | /youtube/v3/videos | Deletes a resource. |
| GET | /youtube/v3/videos | Retrieves a list of resources, possibly filtered. |
| POST | /youtube/v3/videos | Inserts a new resource into this collection. |
| PUT | /youtube/v3/videos | Updates an existing resource. |
| GET | /youtube/v3/videos/getRating | Retrieves the ratings that the authorized user gave to a list of specified videos. |
| POST | /youtube/v3/videos/rate | Adds a like or dislike rating to a video or removes a rating from a video. |
| POST | /youtube/v3/videos/reportAbuse | Report abuse for a video. |
| POST | /youtube/v3/watermarks/set | Allows upload of watermark image and setting it for a channel. |
| POST | /youtube/v3/watermarks/unset | Allows removal of channel watermark. |

## Enhanced Skill Content
## Question Mapping

- "How do I search for videos about a topic?" -> GET /youtube/v3/search
- "How do I get details for a specific video by ID?" -> GET /youtube/v3/videos
- "How do I upload a video to my channel?" -> POST /youtube/v3/videos
- "How do I list all playlists for a channel?" -> GET /youtube/v3/playlists
- "How do I add a video to a playlist?" -> POST /youtube/v3/playlistItems
- "How do I read comments on a video?" -> GET /youtube/v3/commentThreads
- "How do I post a comment on a video?" -> POST /youtube/v3/commentThreads
- "How do I like or dislike a video?" -> POST /youtube/v3/videos/rate
- "How do I subscribe to a channel?" -> POST /youtube/v3/subscriptions
- "How do I start a live broadcast?" -> POST /youtube/v3/liveBroadcasts + POST /youtube/v3/liveBroadcasts/transition
- "How do I get my channel's info?" -> GET /youtube/v3/channels (with `mine=true`)
- "How do I update my channel's branding or description?" -> PUT /youtube/v3/channels
- "How do I list captions for a video?" -> GET /youtube/v3/captions
- "How do I moderate comments (approve, hold, or reject)?" -> POST /youtube/v3/comments/setModerationStatus
- "How do I get the most popular videos in a region?" -> GET /youtube/v3/videos (with `chart=mostPopular`, `regionCode`)

## Response Tips

- **List endpoints** (videos, playlists, search, comments, subscriptions): All return `items[]` array with `nextPageToken`/`prevPageToken` and `pageInfo.totalResults`/`pageInfo.resultsPerPage` -- always check `nextPageToken` for more pages, and note `totalResults` is an estimate on search.
- **Mutation endpoints** (POST/PUT/DELETE): Return the created/updated resource directly; DELETE endpoints return an empty 200 body with no JSON.
- **Part parameter**: Controls which nested objects appear in `items[]` -- omitting a part means those fields are absent, not null. Request only the parts you need to conserve quota.
- **Error responses**: Return `{ error: { code, message, errors[] } }` where `errors[].reason` identifies the specific failure (e.g., `quotaExceeded`, `forbidden`, `videoNotFound`, `commentTextRequired`).
- **Numeric strings**: Statistics fields (`viewCount`, `likeCount`, `subscriberCount`) are returned as strings, not integers -- parse them explicitly.
- **Thumbnail maps**: Nested under `snippet.thumbnails` with keys `default`, `medium`, `high`, `standard`, `maxres` -- not all sizes are always present.

## Anomaly Flags

- **Quota exceeded**: Surface `quotaExceeded` or `rateLimitExceeded` error reasons immediately -- each API call has a quota cost and the daily limit (default 10,000 units) depletes fast with search (100 units) and uploads.
- **Deprecated fields**: `statistics.dislikeCount` returns `"0"` for all videos since the dislike count was hidden -- flag if the caller is trying to read dislike data.
- **Processing not complete**: When `processingDetails.processingStatus` is not `"succeeded"` after upload, flag that video metadata/thumbnails may be incomplete.
- **Made for Kids restrictions**: When `status.madeForKids` is true, flag that comments, notifications, live chat, and personalized ads are disabled by COPPA rules.
- **Privacy status mismatch**: Surface when a video or playlist has `privacyStatus: "private"` or `"unlisted"` in case the user expects it to be public.
- **Live broadcast health**: When `liveStream.status.healthStatus.status` is not `"good"` or `configurationIssues[]` is non-empty, surface the stream health warnings.
- **Empty result sets**: When `pageInfo.totalResults` is 0 or `items[]` is empty on a search or list call, proactively suggest refining filters or checking IDs.
- **403 with `forbidden` reason**: Often means the OAuth scope is insufficient -- flag the specific scope needed (e.g., `youtube.force-ssl` for comment writes).

## Playbook

### 1. Upload a Video and Add It to a Playlist

1. POST /youtube/v3/videos with `part=["snippet","status"]`, attach video file, set `snippet.title`, `snippet.description`, `snippet.categoryId`, and `status.privacyStatus`.
2. Note the returned `id` from the response.
3. POST /youtube/v3/playlistItems with `part=["snippet"]`, set `snippet.playlistId` to the target playlist and `snippet.resourceId.videoId` to the video ID from step 2.
4. Optionally POST /youtube/v3/thumbnails/set with `videoId` to upload a custom thumbnail.

### 2. Set Up and Go Live with a Broadcast

1. POST /youtube/v3/liveStreams with `part=["snippet","cdn"]`, set `snippet.title` and `cdn.ingestionType` (e.g., `"rtmp"`), `cdn.resolution`, `cdn.frameRate`.
2. Note the `cdn.ingestionInfo.ingestionAddress` and `cdn.ingestionInfo.streamName` from the response -- configure your encoder with these.
3. POST /youtube/v3/liveBroadcasts with `part=["snippet","contentDetails","status"]`, set `snippet.title`, `snippet.scheduledStartTime`, and `status.privacyStatus`.
4. POST /youtube/v3/liveBroadcasts/bind with the broadcast `id` and `streamId` from step 1.
5. Start streaming from your encoder, then POST /youtube/v3/liveBroadcasts/transition with `broadcastStatus=testing` to preview.
6. POST /youtube/v3/liveBroadcasts/transition with `broadcastStatus=live` to go live.
7. To end, POST /youtube/v3/liveBroadcasts/transition with `broadcastStatus=complete`.

### 3. Moderate Comments on a Video

1. GET /youtube/v3/commentThreads with `part=["snippet"]`, `videoId`, and `moderationStatus=heldForReview` to fetch pending comments.
2. Review each item's `snippet.topLevelComment.snippet.textDisplay` and `authorDisplayName`.
3. For approved comments: POST /youtube/v3/comments/setModerationStatus with `id` and `moderationStatus=published`.
4. For spam: POST /youtube/v3/comments/setModerationStatus with `moderationStatus=rejected` and optionally `banAuthor=true`.
5. Page through results using `nextPageToken` until all held comments are reviewed.

### 4. Build a Channel Analytics Dashboard

1. GET /youtube/v3/channels with `part=["snippet","statistics","contentDetails"]` and `mine=true` to get subscriber count, view count, and the uploads playlist ID.
2. GET /youtube/v3/playlistItems with `part=["snippet"]` and `playlistId` set to the uploads playlist ID from `contentDetails.relatedPlaylists.uploads` -- paginate to list all uploads.
3. GET /youtube/v3/videos with `part=["statistics","snippet"]` and `id` set to a comma-separated batch of video IDs (up to 50) to fetch per-video view/like/comment counts.
4. Aggregate statistics client-side. Repeat step 3 for each batch of 50 IDs.

### 5. Search and Subscribe to Channels by Topic

1. GET /youtube/v3/search with `part=["snippet"]`, `q` set to the topic, `type=["channel"]`, and `maxResults=10`.
2. Review `items[].snippet.title` and `items[].snippet.channelId` from the results.
3. For each desired channel: POST /youtube/v3/subscriptions with `part=["snippet"]` and `snippet.resourceId.channelId` set to the channel ID.
4. Confirm subscription via GET /youtube/v3/subscriptions with `mine=true` and `forChannelId` set to the subscribed channel ID.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
