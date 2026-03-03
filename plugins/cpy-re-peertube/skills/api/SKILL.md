---
name: peertube
description: "PeerTube API skill. Use when working with PeerTube for static, download, feeds. Covers 265 endpoints."
version: 1.0.0
generator: lapsh
---

# PeerTube
API version: 8.0.0

## Auth
OAuth2

## Base URL
https://peertube2.cpy.re

## Setup
1. Configure auth: OAuth2
2. GET /feeds/podcast/videos.xml -- verify access
3. POST /api/v1/config/instance-banner/pick -- create first pick

## Endpoints

265 endpoints across 4 groups. See references/api-spec.lap for full details.

### static
| Method | Path | Description |
|--------|------|-------------|
| GET | /static/web-videos/{filename} | Get public Web Video file |
| GET | /static/web-videos/private/{filename} | Get private Web Video file |
| GET | /static/streaming-playlists/hls/{filename} | Get public HLS video file |
| GET | /static/streaming-playlists/hls/private/{filename} | Get private HLS video file |

### download
| Method | Path | Description |
|--------|------|-------------|
| GET | /download/videos/generate/{videoId} | Download video file |

### feeds
| Method | Path | Description |
|--------|------|-------------|
| GET | /feeds/video-comments.{format} | Comments on videos feeds |
| GET | /feeds/videos.{format} | Common videos feeds |
| GET | /feeds/subscriptions.{format} | Videos of subscriptions feeds |
| GET | /feeds/podcast/videos.xml | Videos podcast feed |

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/v1/accounts/{name} | Get an account |
| GET | /api/v1/accounts/{name}/videos | List videos of an account |
| GET | /api/v1/accounts/{name}/followers | List followers of an account |
| GET | /api/v1/accounts | List accounts |
| GET | /api/v1/config | Get instance public configuration |
| GET | /api/v1/config/about | Get instance "About" information |
| GET | /api/v1/config/custom | Get instance runtime configuration |
| PUT | /api/v1/config/custom | Set instance runtime configuration |
| DELETE | /api/v1/config/custom | Delete instance runtime configuration |
| POST | /api/v1/config/instance-banner/pick | Update instance banner |
| DELETE | /api/v1/config/instance-banner | Delete instance banner |
| POST | /api/v1/config/instance-avatar/pick | Update instance avatar |
| DELETE | /api/v1/config/instance-avatar | Delete instance avatar |
| POST | /api/v1/config/instance-logo/{logoType}/pick | Update instance logo |
| DELETE | /api/v1/config/instance-logo/{logoType} | Delete instance logo |
| GET | /api/v1/custom-pages/homepage/instance | Get instance custom homepage |
| PUT | /api/v1/custom-pages/homepage/instance | Set instance custom homepage |
| POST | /api/v1/jobs/pause | Pause job queue |
| POST | /api/v1/jobs/resume | Resume job queue |
| GET | /api/v1/jobs/{state} | List instance jobs |
| GET | /api/v1/server/followers | List instances following the server |
| DELETE | /api/v1/server/followers/{handle} | Remove or reject a follower to your server |
| POST | /api/v1/server/followers/{handle}/reject | Reject a pending follower to your server |
| POST | /api/v1/server/followers/{handle}/accept | Accept a pending follower to your server |
| GET | /api/v1/server/following | List instances followed by the server |
| POST | /api/v1/server/following | Follow a list of actors (PeerTube instance, channel or account) |
| DELETE | /api/v1/server/following/{hostOrHandle} | Unfollow an actor (PeerTube instance, channel or account) |
| POST | /api/v1/users | Create a user |
| GET | /api/v1/users | List users |
| DELETE | /api/v1/users/{id} | Delete a user |
| GET | /api/v1/users/{id} | Get a user |
| PUT | /api/v1/users/{id} | Update a user |
| GET | /api/v1/oauth-clients/local | Login prerequisite |
| POST | /api/v1/users/token | Login |
| POST | /api/v1/users/revoke-token | Logout |
| GET | /api/v1/users/{id}/token-sessions | List token sessions |
| GET | /api/v1/users/{id}/token-sessions/{tokenSessionId}/revoke | List token sessions |
| POST | /api/v1/users/ask-send-verify-email | Resend user verification link |
| POST | /api/v1/users/registrations/ask-send-verify-email | Resend verification link to registration request email |
| POST | /api/v1/users/{id}/verify-email | Verify a user |
| POST | /api/v1/users/registrations/{registrationId}/verify-email | Verify a registration email |
| POST | /api/v1/users/ask-reset-password | Ask to reset password |
| POST | /api/v1/users/{id}/reset-password | Reset password |
| POST | /api/v1/users/{id}/two-factor/request | Request two factor auth |
| POST | /api/v1/users/{id}/two-factor/confirm-request | Confirm two factor auth |
| POST | /api/v1/users/{id}/two-factor/disable | Disable two factor auth |
| POST | /api/v1/users/{userId}/imports/import-resumable | Initialize the resumable user import |
| PUT | /api/v1/users/{userId}/imports/import-resumable | Send chunk for the resumable user import |
| DELETE | /api/v1/users/{userId}/imports/import-resumable | Cancel the resumable user import |
| GET | /api/v1/users/{userId}/imports/latest | Get latest user import |
| POST | /api/v1/users/{userId}/exports/request | Request user export |
| GET | /api/v1/users/{userId}/exports | List user exports |
| DELETE | /api/v1/users/{userId}/exports/{id} | Delete a user export |
| GET | /api/v1/users/me | Get my user information |
| PUT | /api/v1/users/me | Update my user information |
| GET | /api/v1/users/me/videos/comments | List comments on user's videos |
| GET | /api/v1/users/me/videos/imports | Get video imports of my user |
| GET | /api/v1/users/me/video-quota-used | Get my user used quota |
| GET | /api/v1/users/me/videos/{videoId}/rating | Get rate of my user for a video |
| GET | /api/v1/users/me/videos | List videos of my user |
| GET | /api/v1/users/me/subscriptions | List my user subscriptions |
| POST | /api/v1/users/me/subscriptions | Add subscription to my user |
| GET | /api/v1/users/me/subscriptions/exist | Get if subscriptions exist for my user |
| GET | /api/v1/users/me/subscriptions/videos | List videos of subscriptions of my user |
| GET | /api/v1/users/me/subscriptions/{subscriptionHandle} | Get subscription of my user |
| DELETE | /api/v1/users/me/subscriptions/{subscriptionHandle} | Delete subscription of my user |
| GET | /api/v1/users/me/notifications | List my notifications |
| POST | /api/v1/users/me/notifications/read | Mark notifications as read by their id |
| POST | /api/v1/users/me/notifications/read-all | Mark all my notification as read |
| PUT | /api/v1/users/me/notification-settings | Update my notification settings |
| POST | /api/v1/users/me/new-feature-info/read | Mark feature info as read |
| GET | /api/v1/users/me/history/videos | List watched videos history |
| DELETE | /api/v1/users/me/history/videos/{videoId} | Delete history element |
| POST | /api/v1/users/me/history/videos/remove | Clear video history |
| POST | /api/v1/users/me/avatar/pick | Update my user avatar |
| DELETE | /api/v1/users/me/avatar | Delete my avatar |
| POST | /api/v1/users/register | Register a user |
| POST | /api/v1/users/registrations/request | Request registration |
| POST | /api/v1/users/registrations/{registrationId}/accept | Accept registration |
| POST | /api/v1/users/registrations/{registrationId}/reject | Reject registration |
| DELETE | /api/v1/users/registrations/{registrationId} | Delete registration |
| GET | /api/v1/users/registrations | List registrations |
| GET | /api/v1/videos/ownership | List video ownership changes |
| POST | /api/v1/videos/ownership/{id}/accept | Accept ownership change request |
| POST | /api/v1/videos/ownership/{id}/refuse | Refuse ownership change request |
| POST | /api/v1/videos/{id}/give-ownership | Request ownership change |
| POST | /api/v1/videos/{id}/token | Request video token |
| POST | /api/v1/videos/{id}/studio/edit | Create a studio task |
| GET | /api/v1/videos | List videos |
| GET | /api/v1/videos/categories | List available video categories |
| GET | /api/v1/videos/licences | List available video licences |
| GET | /api/v1/videos/languages | List available video languages |
| GET | /api/v1/videos/privacies | List available video privacy policies |
| PUT | /api/v1/videos/{id} | Update a video |
| GET | /api/v1/videos/{id} | Get a video |
| DELETE | /api/v1/videos/{id} | Delete a video |
| GET | /api/v1/videos/{id}/description | Get complete video description |
| POST | /api/v1/videos/{id}/views | Notify user is watching a video |
| GET | /api/v1/videos/{id}/stats/overall | Get overall stats of a video |
| GET | /api/v1/videos/{id}/stats/user-agent | Get user agent stats of a video |
| GET | /api/v1/videos/{id}/stats/retention | Get retention stats of a video |
| GET | /api/v1/videos/{id}/stats/timeseries/{metric} | Get timeserie stats of a video |
| POST | /api/v1/videos/upload | Upload a video |
| POST | /api/v1/videos/upload-resumable | Initialize the resumable upload of a video |
| PUT | /api/v1/videos/upload-resumable | Send chunk for the resumable upload of a video |
| DELETE | /api/v1/videos/upload-resumable | Cancel the resumable upload of a video, deleting any data uploaded so far |
| POST | /api/v1/videos/imports | Import a video |
| POST | /api/v1/videos/imports/{id}/cancel | Cancel video import |
| POST | /api/v1/videos/imports/{id}/retry | Retry video import |
| DELETE | /api/v1/videos/imports/{id} | Delete video import |
| POST | /api/v1/videos/live | Create a live |
| GET | /api/v1/videos/live/{id} | Get information about a live |
| PUT | /api/v1/videos/live/{id} | Update information about a live |
| GET | /api/v1/videos/live/{id}/sessions | List live sessions |
| GET | /api/v1/videos/{id}/live-session | Get live session of a replay |
| GET | /api/v1/videos/{id}/source | Get video source file metadata |
| DELETE | /api/v1/videos/{id}/source/file | Delete video source file |
| POST | /api/v1/videos/{id}/source/replace-resumable | Initialize the resumable replacement of a video |
| PUT | /api/v1/videos/{id}/source/replace-resumable | Send chunk for the resumable replacement of a video |
| DELETE | /api/v1/videos/{id}/source/replace-resumable | Cancel the resumable replacement of a video |
| GET | /api/v1/users/me/abuses | List my abuses |
| GET | /api/v1/abuses | List abuses |
| POST | /api/v1/abuses | Report an abuse |
| PUT | /api/v1/abuses/{abuseId} | Update an abuse |
| DELETE | /api/v1/abuses/{abuseId} | Delete an abuse |
| GET | /api/v1/abuses/{abuseId}/messages | List messages of an abuse |
| POST | /api/v1/abuses/{abuseId}/messages | Add message to an abuse |
| DELETE | /api/v1/abuses/{abuseId}/messages/{abuseMessageId} | Delete an abuse message |
| POST | /api/v1/videos/{id}/blacklist | Block a video |
| DELETE | /api/v1/videos/{id}/blacklist | Unblock a video by its id |
| GET | /api/v1/videos/blacklist | List video blocks |
| GET | /api/v1/videos/{id}/storyboards | List storyboards of a video |
| GET | /api/v1/videos/{id}/captions | List captions of a video |
| POST | /api/v1/videos/{id}/captions/generate | Generate a video caption |
| PUT | /api/v1/videos/{id}/captions/{captionLanguage} | Add or replace a video caption |
| DELETE | /api/v1/videos/{id}/captions/{captionLanguage} | Delete a video caption |
| GET | /api/v1/videos/{id}/chapters | Get chapters of a video |
| PUT | /api/v1/videos/{id}/chapters | Replace video chapters |
| GET | /api/v1/videos/{id}/embed-privacy | Get video embed privacy |
| PUT | /api/v1/videos/{id}/embed-privacy | Update video embed privacy |
| GET | /api/v1/videos/{id}/embed-privacy/allowed | Check if embed is allowed |
| GET | /api/v1/videos/{id}/passwords | List video passwords |
| PUT | /api/v1/videos/{id}/passwords | Update video passwords |
| POST | /api/v1/videos/{id}/passwords | Add a video password |
| DELETE | /api/v1/videos/{id}/passwords/{videoPasswordId} | Delete a video password |
| GET | /api/v1/video-channels | List video channels |
| POST | /api/v1/video-channels | Create a video channel |
| GET | /api/v1/video-channels/{channelHandle} | Get a video channel |
| PUT | /api/v1/video-channels/{channelHandle} | Update a video channel |
| DELETE | /api/v1/video-channels/{channelHandle} | Delete a video channel |
| GET | /api/v1/video-channels/{channelHandle}/videos | List videos of a video channel |
| GET | /api/v1/video-channels/{channelHandle}/activities | List activities of a video channel |
| GET | /api/v1/video-channels/{channelHandle}/video-playlists | List playlists of a channel |
| POST | /api/v1/video-channels/{channelHandle}/video-playlists/reorder | Reorder channel playlists |
| GET | /api/v1/video-channels/{channelHandle}/followers | List followers of a video channel |
| POST | /api/v1/video-channels/{channelHandle}/avatar/pick | Update channel avatar |
| DELETE | /api/v1/video-channels/{channelHandle}/avatar | Delete channel avatar |
| POST | /api/v1/video-channels/{channelHandle}/banner/pick | Update channel banner |
| DELETE | /api/v1/video-channels/{channelHandle}/banner | Delete channel banner |
| POST | /api/v1/video-channels/{channelHandle}/import-videos | Import videos in channel |
| POST | /api/v1/video-channel-syncs | Create a synchronization for a video channel |
| DELETE | /api/v1/video-channel-syncs/{channelSyncId} | Delete a video channel synchronization |
| POST | /api/v1/video-channel-syncs/{channelSyncId}/sync | Triggers the channel synchronization job, fetching all the videos from the remote channel |
| GET | /api/v1/player-settings/videos/{id} | Get video player settings |
| PUT | /api/v1/player-settings/videos/{id} | Update video player settings |
| GET | /api/v1/player-settings/video-channels/{channelHandle} | Get channel player settings |
| PUT | /api/v1/player-settings/video-channels/{channelHandle} | Update channel player settings |
| GET | /api/v1/video-playlists/privacies | List available playlist privacy policies |
| GET | /api/v1/video-playlists | List video playlists |
| POST | /api/v1/video-playlists | Create a video playlist |
| GET | /api/v1/video-playlists/{playlistId} | Get a video playlist |
| PUT | /api/v1/video-playlists/{playlistId} | Update a video playlist |
| DELETE | /api/v1/video-playlists/{playlistId} | Delete a video playlist |
| GET | /api/v1/video-playlists/{playlistId}/videos | List videos of a playlist |
| POST | /api/v1/video-playlists/{playlistId}/videos | Add a video in a playlist |
| POST | /api/v1/video-playlists/{playlistId}/videos/reorder | Reorder playlist elements |
| PUT | /api/v1/video-playlists/{playlistId}/videos/{playlistElementId} | Update a playlist element |
| DELETE | /api/v1/video-playlists/{playlistId}/videos/{playlistElementId} | Delete an element from a playlist |
| GET | /api/v1/users/me/video-playlists/videos-exist | Check video exists in my playlists |
| GET | /api/v1/accounts/{name}/video-playlists | List playlists of an account |
| GET | /api/v1/accounts/{name}/video-channels | List video channels of an account |
| GET | /api/v1/accounts/{name}/video-channel-syncs | List the synchronizations of video channels of an account |
| GET | /api/v1/accounts/{name}/ratings | List ratings of an account |
| GET | /api/v1/videos/{id}/comment-threads | List threads of a video |
| POST | /api/v1/videos/{id}/comment-threads | Create a thread |
| GET | /api/v1/videos/{id}/comment-threads/{threadId} | Get a thread |
| GET | /api/v1/videos/comments | List instance comments |
| POST | /api/v1/videos/{id}/comments/{commentId} | Reply to a thread of a video |
| DELETE | /api/v1/videos/{id}/comments/{commentId} | Delete a comment or a reply |
| POST | /api/v1/videos/{id}/comments/{commentId}/approve | Approve a comment |
| PUT | /api/v1/videos/{id}/rate | Like/dislike a video |
| DELETE | /api/v1/videos/{id}/hls | Delete video HLS files |
| DELETE | /api/v1/videos/{id}/web-videos | Delete video Web Video files |
| POST | /api/v1/videos/{id}/transcoding | Create a transcoding job |
| GET | /api/v1/search/videos | Search videos |
| GET | /api/v1/search/video-channels | Search channels |
| GET | /api/v1/search/video-playlists | Search playlists |
| GET | /api/v1/blocklist/status | Get block status of accounts/hosts |
| GET | /api/v1/server/blocklist/accounts | List account blocks |
| POST | /api/v1/server/blocklist/accounts | Block an account |
| DELETE | /api/v1/server/blocklist/accounts/{accountName} | Unblock an account by its handle |
| GET | /api/v1/server/blocklist/servers | List server blocks |
| POST | /api/v1/server/blocklist/servers | Block a server |
| DELETE | /api/v1/server/blocklist/servers/{host} | Unblock a server by its domain |
| PUT | /api/v1/server/redundancy/{host} | Update a server redundancy policy |
| GET | /api/v1/server/redundancy/videos | List videos being mirrored |
| POST | /api/v1/server/redundancy/videos | Mirror a video |
| DELETE | /api/v1/server/redundancy/videos/{redundancyId} | Delete a mirror done on a video |
| GET | /api/v1/server/stats | Get instance stats |
| POST | /api/v1/server/logs/client | Send client log |
| GET | /api/v1/server/logs | Get instance logs |
| GET | /api/v1/server/audit-logs | Get instance audit logs |
| GET | /api/v1/plugins | List plugins |
| GET | /api/v1/plugins/available | List available plugins |
| POST | /api/v1/plugins/install | Install a plugin |
| POST | /api/v1/plugins/update | Update a plugin |
| POST | /api/v1/plugins/uninstall | Uninstall a plugin |
| GET | /api/v1/plugins/{npmName} | Get a plugin |
| PUT | /api/v1/plugins/{npmName}/settings | Set a plugin's settings |
| GET | /api/v1/plugins/{npmName}/public-settings | Get a plugin's public settings |
| GET | /api/v1/plugins/{npmName}/registered-settings | Get a plugin's registered settings |
| POST | /api/v1/metrics/playback | Create playback metrics |
| POST | /api/v1/runners/registration-tokens/generate | Generate registration token |
| DELETE | /api/v1/runners/registration-tokens/{registrationTokenId} | Remove registration token |
| GET | /api/v1/runners/registration-tokens | List registration tokens |
| POST | /api/v1/runners/register | Register a new runner |
| POST | /api/v1/runners/unregister | Unregister a runner |
| DELETE | /api/v1/runners/{runnerId} | Delete a runner |
| GET | /api/v1/runners | List runners |
| POST | /api/v1/runners/jobs/request | Request a new job |
| POST | /api/v1/runners/jobs/{jobUUID}/accept | Accept job |
| POST | /api/v1/runners/jobs/{jobUUID}/abort | Abort job |
| POST | /api/v1/runners/jobs/{jobUUID}/update | Update job |
| POST | /api/v1/runners/jobs/{jobUUID}/error | Post job error |
| POST | /api/v1/runners/jobs/{jobUUID}/success | Post job success |
| GET | /api/v1/runners/jobs/{jobUUID}/cancel | Cancel a job |
| DELETE | /api/v1/runners/jobs/{jobUUID} | Delete a job |
| GET | /api/v1/runners/jobs | List jobs |
| GET | /api/v1/automatic-tags/policies/accounts/{accountName}/comments | Get account auto tag policies on comments |
| PUT | /api/v1/automatic-tags/policies/accounts/{accountName}/comments | Update account auto tag policies on comments |
| GET | /api/v1/automatic-tags/accounts/{accountName}/available | Get account available auto tags |
| GET | /api/v1/automatic-tags/server/available | Get server available auto tags |
| GET | /api/v1/watched-words/accounts/{accountName}/lists | List account watched words |
| POST | /api/v1/watched-words/accounts/{accountName}/lists | Add account watched words |
| PUT | /api/v1/watched-words/accounts/{accountName}/lists/{listId} | Update account watched words |
| DELETE | /api/v1/watched-words/accounts/{accountName}/lists/{listId} | Delete account watched words |
| GET | /api/v1/watched-words/server/lists | List server watched words |
| POST | /api/v1/watched-words/server/lists | Add server watched words |
| PUT | /api/v1/watched-words/server/lists/{listId} | Update server watched words |
| DELETE | /api/v1/watched-words/server/lists/{listId} | Delete server watched words |
| POST | /api/v1/client-config/update-language | Update client language |
| GET | /api/v1/video-channels/{channelHandle}/collaborators | *List channel collaborators |
| POST | /api/v1/video-channels/{channelHandle}/collaborators/invite | Invite a collaborator |
| POST | /api/v1/video-channels/{channelHandle}/collaborators/{collaboratorId}/accept | Accept a collaboration invitation |
| POST | /api/v1/video-channels/{channelHandle}/collaborators/{collaboratorId}/reject | Reject a collaboration invitation |
| DELETE | /api/v1/video-channels/{channelHandle}/collaborators/{collaboratorId} | Remove a channel collaborator |

## Enhanced Skill Content
## Question Mapping

- "How do I search for videos?" -> GET /api/v1/search/videos
- "What videos has a specific user uploaded?" -> GET /api/v1/accounts/{name}/videos
- "How do I upload a video?" -> POST /api/v1/videos/upload
- "How do I get an OAuth token?" -> POST /api/v1/users/token (after GET /api/v1/oauth-clients/local)
- "What are the server stats like active users and video count?" -> GET /api/v1/server/stats
- "How do I subscribe to a channel?" -> POST /api/v1/users/me/subscriptions
- "How do I report an abusive video or comment?" -> POST /api/v1/abuses
- "How do I create a live stream?" -> POST /api/v1/videos/live
- "What plugins are installed on the instance?" -> GET /api/v1/plugins
- "How do I block a remote server?" -> POST /api/v1/server/blocklist/servers
- "How do I manage video captions?" -> GET /api/v1/videos/{id}/captions then PUT /api/v1/videos/{id}/captions/{captionLanguage}
- "What is my video quota usage?" -> GET /api/v1/users/me/video-quota-used
- "How do I register a new user?" -> POST /api/v1/users/register
- "How do I get the RSS feed for a channel?" -> GET /feeds/videos.{format}
- "How do I check viewer retention on my video?" -> GET /api/v1/videos/{id}/stats/retention

## Response Tips

- **List endpoints** (videos, accounts, channels, playlists, comments, jobs, runners, abuses, registrations): All return `{total, data}`. Use `start` and `count` (default 15) for pagination. Always check `total` to know if more pages exist.
- **Mutation endpoints** (create, update, delete): Most return 204 with no body. POST creation endpoints typically return the new resource ID nested one level deep (e.g., `{video: {id, uuid, shortUUID}}`).
- **Config endpoints**: GET /api/v1/config returns a deeply nested object. Navigate through `instance`, `signup`, `transcoding`, `import` sub-objects. GET /api/v1/config/custom is the admin-editable superset.
- **Stats endpoints**: Video stats (overall, retention, timeseries, user-agent) return different shapes. `overall` gives aggregates; `retention` and `timeseries` return `{data: [map]}` arrays for charting.
- **Feed endpoints**: Return XML/RSS/Atom/JSON based on the `{format}` path parameter, not JSON API objects. Content-Type varies accordingly.
- **Error responses**: 400 = bad input, 403 = missing auth or insufficient role, 404 = resource not found, 409 = conflict/duplicate, 413 = file too large, 429 = rate limited, 503 = service unavailable (plugin registry down).

## Anomaly Flags

- **429 on resumable upload PUT**: Rate limit hit during upload. Surface immediately -- the user may need to wait before retrying the chunk.
- **308 on resumable upload**: Not an error. This is the expected "send next chunk" response. Do not treat as a failure.
- **503 from /plugins/available**: The plugin registry is unreachable. Warn the user that plugin search is temporarily unavailable.
- **413 on any upload endpoint**: File exceeds server limit. Surface the instance's configured max sizes from GET /api/v1/config (`video.file.size.max`, `avatar.file.size.max`).
- **Video quota approaching**: After uploads, proactively check GET /api/v1/users/me/video-quota-used and compare against the quota from GET /api/v1/users/me. Alert if usage exceeds 90%.
- **Job queue backlog**: If GET /api/v1/jobs/waiting returns a high `total`, warn that transcoding or federation may be delayed.
- **Registration requires approval**: If GET /api/v1/config shows `signup.allowed: false`, user registration needs POST /api/v1/users/registrations/request instead of POST /api/v1/users/register. Flag this distinction.
- **Two-factor OTP required**: 401 on POST /users/token when `x-peertube-otp` header is missing. Prompt the user for their OTP code.
- **Redundancy conflicts (409)**: Attempting to add redundancy for a video that already has it. Surface the existing redundancy instead of retrying.

## Playbook

### 1. Authenticate and get current user info

1. GET /api/v1/oauth-clients/local to retrieve `client_id` and `client_secret`
2. POST /api/v1/users/token with username, password, client_id, client_secret to get `access_token` and `refresh_token`
3. Use `Authorization: Bearer {access_token}` on all subsequent requests
4. GET /api/v1/users/me to verify identity and check quotas
5. When the access token expires, POST /api/v1/users/token with the refresh_token grant type

### 2. Upload a video with captions

1. POST /api/v1/videos/upload with the video file and metadata (name, channel, privacy, etc.) -- returns `{video: {id, uuid}}`
2. Wait for transcoding: poll GET /api/v1/videos/{id} until the video state indicates it is published
3. PUT /api/v1/videos/{id}/captions/{captionLanguage} with the subtitle file to attach captions
4. Optionally POST /api/v1/videos/{id}/captions/generate to auto-generate captions via transcription
5. PUT /api/v1/videos/{id}/chapters to add chapter markers with titles and timecodes

### 3. Set up a live stream

1. POST /api/v1/videos/live with channel ID, name, and privacy settings -- returns `{video: {id, uuid}}`
2. GET /api/v1/videos/live/{id} to retrieve the `rtmpUrl`, `rtmpsUrl`, and `streamKey`
3. Configure your streaming software (OBS, etc.) with the RTMP URL and stream key
4. Optionally PUT /api/v1/videos/live/{id} to enable `saveReplay`, set `latencyMode`, or configure `permanentLive`
5. After the stream ends, GET /api/v1/videos/{id}/live-session to check for errors and find the replay video ID

### 4. Moderate content (abuse reports and blocklists)

1. GET /api/v1/abuses with optional `state`, `filter`, and `search` params to review pending reports
2. PUT /api/v1/abuses/{abuseId} with `state: 2` (accepted) or `state: 3` (rejected) and a `moderationComment`
3. If the video should be hidden: POST /api/v1/videos/{id}/blacklist to block it from public view
4. To block a repeat offender's instance: POST /api/v1/server/blocklist/servers with the `host`
5. To block a specific account: POST /api/v1/server/blocklist/accounts with the `accountName`
6. Review messages on a report: GET /api/v1/abuses/{abuseId}/messages, and reply with POST /api/v1/abuses/{abuseId}/messages

### 5. Set up remote runners for transcoding

1. POST /api/v1/runners/registration-tokens/generate to create a token
2. GET /api/v1/runners/registration-tokens to retrieve the generated token
3. On the runner machine: POST /api/v1/runners/register with the `registrationToken` and a `name` -- returns `runnerToken`
4. The runner polls POST /api/v1/runners/jobs/request with its `runnerToken` to pick up transcoding jobs
5. For each job: POST /api/v1/runners/jobs/{jobUUID}/accept, send progress updates via POST .../update, then POST .../success or .../error
6. Monitor all runner jobs from the admin side: GET /api/v1/runners/jobs with `stateOneOf` and `sort` filters


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
