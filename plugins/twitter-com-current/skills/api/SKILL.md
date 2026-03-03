---
name: x-api-v2
description: "X API v2 API skill. Use when working with X API v2 for 2. Covers 150 endpoints."
version: 1.0.0
generator: lapsh
---

# X API v2
API version: 2.158

## Auth
Bearer bearer | OAuth2 | Bearer OAuth

## Base URL
https://api.x.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /2/account_activity/subscriptions/count -- verify access
3. POST /2/account_activity/replay/webhooks/{webhook_id}/subscriptions/all -- create first all

## Endpoints

150 endpoints across 1 groups. See references/api-spec.lap for full details.

### 2
| Method | Path | Description |
|--------|------|-------------|
| POST | /2/account_activity/replay/webhooks/{webhook_id}/subscriptions/all | Create replay job |
| GET | /2/account_activity/subscriptions/count | Get subscription count |
| GET | /2/account_activity/webhooks/{webhook_id}/subscriptions/all | Validate subscription |
| POST | /2/account_activity/webhooks/{webhook_id}/subscriptions/all | Create subscription |
| GET | /2/account_activity/webhooks/{webhook_id}/subscriptions/all/list | Get subscriptions |
| DELETE | /2/account_activity/webhooks/{webhook_id}/subscriptions/{user_id}/all | Delete subscription |
| GET | /2/activity/stream | Activity Stream |
| GET | /2/activity/subscriptions | Get X activity subscriptions |
| POST | /2/activity/subscriptions | Create X activity subscription |
| DELETE | /2/activity/subscriptions/{subscription_id} | Deletes X activity subscription |
| PUT | /2/activity/subscriptions/{subscription_id} | Update X activity subscription |
| GET | /2/chat/conversations | Get Chat Conversations |
| GET | /2/chat/conversations/{conversation_id} | Get Chat Conversation |
| POST | /2/chat/conversations/{conversation_id}/messages | Send Chat Message |
| GET | /2/communities/search | Search Communities |
| GET | /2/communities/{id} | Get Community by ID |
| GET | /2/compliance/jobs | Get Compliance Jobs |
| POST | /2/compliance/jobs | Create Compliance Job |
| GET | /2/compliance/jobs/{id} | Get Compliance Job by ID |
| DELETE | /2/connections | Terminate multiple connections |
| GET | /2/connections | Get Connection History |
| DELETE | /2/connections/all | Terminate all connections |
| DELETE | /2/connections/{endpoint_id} | Terminate connections by endpoint |
| POST | /2/dm_conversations | Create DM conversation |
| GET | /2/dm_conversations/with/{participant_id}/dm_events | Get DM events for a DM conversation |
| POST | /2/dm_conversations/with/{participant_id}/messages | Create DM message by participant ID |
| POST | /2/dm_conversations/{dm_conversation_id}/messages | Create DM message by conversation ID |
| GET | /2/dm_conversations/{id}/dm_events | Get DM events for a DM conversation |
| GET | /2/dm_events | Get DM events |
| DELETE | /2/dm_events/{event_id} | Delete DM event |
| GET | /2/dm_events/{event_id} | Get DM event by ID |
| POST | /2/evaluate_note | Evaluate a Community Note |
| GET | /2/insights/28hr | Get 28-hour Post insights |
| GET | /2/insights/historical | Get historical Post insights |
| GET | /2/likes/compliance/stream | Stream Likes compliance data |
| GET | /2/likes/firehose/stream | Stream all Likes |
| GET | /2/likes/sample10/stream | Stream sampled Likes |
| POST | /2/lists | Create List |
| DELETE | /2/lists/{id} | Delete List |
| GET | /2/lists/{id} | Get List by ID |
| PUT | /2/lists/{id} | Update List |
| GET | /2/lists/{id}/followers | Get List followers |
| GET | /2/lists/{id}/members | Get List members |
| POST | /2/lists/{id}/members | Add List member |
| DELETE | /2/lists/{id}/members/{user_id} | Remove List member |
| GET | /2/lists/{id}/tweets | Get List Posts |
| GET | /2/media | Get Media by media keys |
| GET | /2/media/analytics | Get Media analytics |
| POST | /2/media/metadata | Create Media metadata |
| DELETE | /2/media/subtitles | Delete Media subtitles |
| POST | /2/media/subtitles | Create Media subtitles |
| GET | /2/media/upload | Get Media upload status |
| POST | /2/media/upload | Upload media |
| POST | /2/media/upload/initialize | Initialize media upload |
| POST | /2/media/upload/{id}/append | Append Media upload |
| POST | /2/media/upload/{id}/finalize | Finalize Media upload |
| GET | /2/media/{media_key} | Get Media by media key |
| GET | /2/news/search | Search News |
| GET | /2/news/{id} | Get news stories by ID |
| POST | /2/notes | Create a Community Note |
| GET | /2/notes/search/notes_written | Search for Community Notes Written |
| GET | /2/notes/search/posts_eligible_for_notes | Search for Posts Eligible for Community Notes |
| DELETE | /2/notes/{id} | Delete a Community Note |
| GET | /2/openapi.json | Get OpenAPI Spec. |
| GET | /2/spaces | Get Spaces by IDs |
| GET | /2/spaces/by/creator_ids | Get Spaces by creator IDs |
| GET | /2/spaces/search | Search Spaces |
| GET | /2/spaces/{id} | Get space by ID |
| GET | /2/spaces/{id}/buyers | Get Space ticket buyers |
| GET | /2/spaces/{id}/tweets | Get Space Posts |
| GET | /2/trends/by/woeid/{woeid} | Get Trends by WOEID |
| GET | /2/tweets | Get Posts by IDs |
| POST | /2/tweets | Create or Edit Post |
| GET | /2/tweets/analytics | Get Post analytics |
| GET | /2/tweets/compliance/stream | Stream Posts compliance data |
| GET | /2/tweets/counts/all | Get count of all Posts |
| GET | /2/tweets/counts/recent | Get count of recent Posts |
| GET | /2/tweets/firehose/stream | Stream all Posts |
| GET | /2/tweets/firehose/stream/lang/en | Stream English Posts |
| GET | /2/tweets/firehose/stream/lang/ja | Stream Japanese Posts |
| GET | /2/tweets/firehose/stream/lang/ko | Stream Korean Posts |
| GET | /2/tweets/firehose/stream/lang/pt | Stream Portuguese Posts |
| GET | /2/tweets/label/stream | Stream Post labels |
| GET | /2/tweets/sample/stream | Stream sampled Posts |
| GET | /2/tweets/sample10/stream | Stream 10% sampled Posts |
| GET | /2/tweets/search/all | Search all Posts |
| GET | /2/tweets/search/recent | Search recent Posts |
| GET | /2/tweets/search/stream | Stream filtered Posts |
| GET | /2/tweets/search/stream/rules | Get stream rules |
| POST | /2/tweets/search/stream/rules | Update stream rules |
| GET | /2/tweets/search/stream/rules/counts | Get stream rule counts |
| GET | /2/tweets/search/webhooks | Get stream links |
| DELETE | /2/tweets/search/webhooks/{webhook_id} | Delete stream link |
| POST | /2/tweets/search/webhooks/{webhook_id} | Create stream link |
| DELETE | /2/tweets/{id} | Delete Post |
| GET | /2/tweets/{id} | Get Post by ID |
| GET | /2/tweets/{id}/liking_users | Get Liking Users |
| GET | /2/tweets/{id}/quote_tweets | Get Quoted Posts |
| GET | /2/tweets/{id}/retweeted_by | Get Reposted by |
| GET | /2/tweets/{id}/retweets | Get Reposts |
| PUT | /2/tweets/{tweet_id}/hidden | Hide reply |
| GET | /2/usage/tweets | Get usage |
| GET | /2/users | Get Users by IDs |
| GET | /2/users/by | Get Users by usernames |
| GET | /2/users/by/username/{username} | Get User by username |
| GET | /2/users/compliance/stream | Stream Users compliance data |
| GET | /2/users/me | Get my User |
| GET | /2/users/personalized_trends | Get personalized Trends |
| GET | /2/users/reposts_of_me | Get Reposts of me |
| GET | /2/users/search | Search Users |
| GET | /2/users/{id} | Get User by ID |
| GET | /2/users/{id}/affiliates | Get affiliates |
| GET | /2/users/{id}/blocking | Get blocking |
| GET | /2/users/{id}/bookmarks | Get Bookmarks |
| POST | /2/users/{id}/bookmarks | Create Bookmark |
| GET | /2/users/{id}/bookmarks/folders | Get Bookmark folders |
| GET | /2/users/{id}/bookmarks/folders/{folder_id} | Get Bookmarks by folder ID |
| DELETE | /2/users/{id}/bookmarks/{tweet_id} | Delete Bookmark |
| POST | /2/users/{id}/dm/block | Block DMs |
| POST | /2/users/{id}/dm/unblock | Unblock DMs |
| GET | /2/users/{id}/followed_lists | Get followed Lists |
| POST | /2/users/{id}/followed_lists | Follow List |
| DELETE | /2/users/{id}/followed_lists/{list_id} | Unfollow List |
| GET | /2/users/{id}/followers | Get followers |
| GET | /2/users/{id}/following | Get following |
| POST | /2/users/{id}/following | Follow User |
| GET | /2/users/{id}/liked_tweets | Get liked Posts |
| POST | /2/users/{id}/likes | Like Post |
| DELETE | /2/users/{id}/likes/{tweet_id} | Unlike Post |
| GET | /2/users/{id}/list_memberships | Get List memberships |
| GET | /2/users/{id}/mentions | Get mentions |
| GET | /2/users/{id}/muting | Get muting |
| POST | /2/users/{id}/muting | Mute User |
| GET | /2/users/{id}/owned_lists | Get owned Lists |
| GET | /2/users/{id}/pinned_lists | Get pinned Lists |
| POST | /2/users/{id}/pinned_lists | Pin List |
| DELETE | /2/users/{id}/pinned_lists/{list_id} | Unpin List |
| GET | /2/users/{id}/public_keys | Get user public keys |
| POST | /2/users/{id}/public_keys | Add public key |
| POST | /2/users/{id}/retweets | Repost Post |
| DELETE | /2/users/{id}/retweets/{source_tweet_id} | Unrepost Post |
| GET | /2/users/{id}/timelines/reverse_chronological | Get Timeline |
| GET | /2/users/{id}/tweets | Get Posts |
| DELETE | /2/users/{source_user_id}/following/{target_user_id} | Unfollow User |
| DELETE | /2/users/{source_user_id}/muting/{target_user_id} | Unmute User |
| GET | /2/webhooks | Get webhook |
| POST | /2/webhooks | Create webhook |
| POST | /2/webhooks/replay | Create replay job for webhook |
| DELETE | /2/webhooks/{webhook_id} | Delete webhook |
| PUT | /2/webhooks/{webhook_id} | Validate webhook |

## Enhanced Skill Content
## Question Mapping

- "How do I post a tweet?" -> POST /2/tweets
- "How do I look up a user by their handle?" -> GET /2/users/by/username/{username}
- "How do I search for recent tweets about a topic?" -> GET /2/tweets/search/recent
- "How do I get my own profile info?" -> GET /2/users/me
- "How do I send a direct message to someone?" -> POST /2/dm_conversations/with/{participant_id}/messages
- "Who liked a specific tweet?" -> GET /2/tweets/{id}/liking_users
- "How do I follow or unfollow someone?" -> POST /2/users/{id}/following | DELETE /2/users/{source_user_id}/following/{target_user_id}
- "How do I get a user's timeline?" -> GET /2/users/{id}/timelines/reverse_chronological
- "How do I create a list and add members?" -> POST /2/lists then POST /2/lists/{id}/members
- "How do I upload media and attach it to a tweet?" -> POST /2/media/upload/initialize then POST /2/media/upload/{id}/append then POST /2/media/upload/{id}/finalize then POST /2/tweets
- "How do I set up filtered stream rules?" -> POST /2/tweets/search/stream/rules then GET /2/tweets/search/stream
- "What are the trending topics for a location?" -> GET /2/trends/by/woeid/{woeid}
- "How do I check my API usage and quota?" -> GET /2/usage/tweets
- "How do I bookmark or unbookmark a tweet?" -> POST /2/users/{id}/bookmarks | DELETE /2/users/{id}/bookmarks/{tweet_id}
- "How do I get tweet engagement analytics?" -> GET /2/tweets/analytics

## Response Tips

- **Tweets & Users**: Core data lives in `data`; related objects (authors, media, polls, places) are in `includes` -- join on IDs manually. Always request `expansions` and relevant `.fields` params or you get minimal fields back.
- **Paginated lists** (followers, timelines, search, DM events, lists): Use `meta.next_token` as `pagination_token` in the next request. Stop when `next_token` is absent. `meta.result_count` tells you how many items arrived in the current page.
- **Errors**: Non-fatal errors appear in the `errors` array alongside `data` (e.g., a deleted tweet in a batch lookup). Fatal errors return HTTP 4xx/5xx with a top-level `errors` array and no `data`.
- **Streaming endpoints** (firehose, sample, filtered stream, compliance): Return newline-delimited JSON. Heartbeat blank lines keep the connection alive -- do not parse them as data.
- **Media upload**: Response includes `processing_info` with `state` (pending/in_progress/succeeded/failed) and `check_after_secs` -- poll GET /2/media/upload until state is `succeeded` before attaching to a tweet.
- **Write operations** (like, retweet, follow, bookmark, mute, block): Return a simple boolean confirmation object (e.g., `{data: {liked: true}}`). A `false` value means the action was reversed (unlike, unfollow, etc.).
- **Compliance & webhooks**: Job-based endpoints return `status` (created/in_progress/failed/complete) and expiring `download_url`/`upload_url` -- check expiration timestamps before downloading.

## Anomaly Flags

- **Rate limit headers**: Surface `x-rate-limit-remaining` and `x-rate-limit-reset` from response headers. Alert when remaining drops below 10% of the limit.
- **HTTP 429 Too Many Requests**: Back off using the `x-rate-limit-reset` timestamp. Flag to user with reset time.
- **Partial errors in batch lookups**: When `errors` array is non-empty alongside `data`, surface which IDs failed and why (suspended, deleted, not found).
- **Media processing failures**: If `processing_info.state` is `failed`, surface immediately with the error message rather than continuing to poll.
- **Usage cap approaching**: From GET /2/usage/tweets, alert when `project_usage` exceeds 80% of `project_cap`.
- **Stream disconnections**: If a streaming endpoint closes unexpectedly, flag the disconnect and suggest using `backfill_minutes` (up to 5) on reconnect to recover missed data.
- **Withheld content**: When `withheld` object appears on tweets or users, surface the `country_codes` and `scope` so the caller understands content restrictions.
- **Edit controls**: When `edit_controls.edits_remaining` is 0 or `editable_until` has passed, flag that the tweet can no longer be edited.
- **Pending follows**: When POST /2/users/{id}/following returns `pending_follow: true`, surface that the target account is protected and the follow is awaiting approval.
- **Deprecated fields**: Flag `nullcast`, `for_super_followers_only`, and any field returning null that previously had values -- these may indicate deprecated functionality.

## Playbook

### 1. Post a Tweet with Media

1. Initialize the upload: POST /2/media/upload/initialize with `total_bytes`, `media_type`, and `media_category` (e.g., `tweet_image`).
2. Upload chunks: POST /2/media/upload/{id}/append with binary segments (each up to 5MB).
3. Finalize: POST /2/media/upload/{id}/finalize. Note the `id` from the response.
4. Poll for processing: GET /2/media/upload?media_id={id} -- repeat every `check_after_secs` until `processing_info.state` is `succeeded`.
5. Optionally set alt text: POST /2/media/metadata with `alt_text`.
6. Post the tweet: POST /2/tweets with `media: {media_ids: ["{id}"]}` and your `text`.

### 2. Set Up a Filtered Stream

1. Check existing rules: GET /2/tweets/search/stream/rules.
2. Add rules: POST /2/tweets/search/stream/rules with body `{add: [{value: "keyword", tag: "my-label"}]}`. Use `dry_run: true` to validate first.
3. Verify rule counts: GET /2/tweets/search/stream/rules/counts to confirm you are within your cap.
4. Connect to the stream: GET /2/tweets/search/stream with desired `tweet.fields`, `expansions`, and `user.fields`.
5. Process each line of JSON. Ignore blank heartbeat lines. Use `matching_rules` in each payload to identify which rule triggered the match.

### 3. Monitor Tweet Performance

1. Post or identify the tweet ID.
2. For near-real-time metrics (last 28 hours): GET /2/insights/28hr with `tweet_ids`, `granularity: Hourly`, and `requested_metrics`.
3. For historical analytics: GET /2/tweets/analytics with `ids`, `start_time`, `end_time`, and `granularity: daily`.
4. For engagement breakdown: GET /2/tweets/{id} with `tweet.fields=public_metrics,non_public_metrics,organic_metrics`.
5. To see who engaged: GET /2/tweets/{id}/liking_users, GET /2/tweets/{id}/retweeted_by, and GET /2/tweets/{id}/quote_tweets. Paginate through all using `next_token`.

### 4. Build a User Profile Dashboard

1. Resolve username to user object: GET /2/users/by/username/{username} with `user.fields=public_metrics,created_at,description,profile_image_url,verified,verified_type`.
2. Get their recent tweets: GET /2/users/{id}/tweets with `max_results=100` and `tweet.fields=public_metrics,created_at`.
3. Get their followers: GET /2/users/{id}/followers -- paginate to build a full list or sample.
4. Get their following: GET /2/users/{id}/following.
5. Get lists they own: GET /2/users/{id}/owned_lists.
6. Check their mentions: GET /2/users/{id}/mentions with a time window via `start_time`/`end_time`.

### 5. Manage Webhooks for Real-Time Events

1. Register a webhook URL: POST /2/webhooks with your publicly accessible `url`. Save the returned `id`.
2. Verify it is valid: the response includes `valid: true`. If not, check your CRC implementation.
3. Subscribe to activity events: POST /2/activity/subscriptions with an `event_type` (e.g., `FollowFollow`) and optional `filter`.
4. List active subscriptions: GET /2/activity/subscriptions to confirm everything is wired up.
5. If you missed events, replay them: POST /2/webhooks/replay with `webhook_id`, `from_date`, and `to_date`.
6. To tear down: DELETE /2/activity/subscriptions/{subscription_id} then DELETE /2/webhooks/{webhook_id}.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
