---
name: twitter-openapi
description: "Twitter OpenAPI API skill. Use when working with Twitter OpenAPI for 1.1, 2, graphql. Covers 39 endpoints."
version: 1.0.0
generator: lapsh
---

# Twitter OpenAPI
API version: 0.0.1

## Auth
ApiKey Accept in header | ApiKey Accept-Encoding in header | ApiKey Accept-Language in header | ApiKey x-twitter-active-user in header | ApiKey x-twitter-auth-type in header | Bearer bearer | ApiKey x-twitter-client-language in header | ApiKey x-client-transaction-id in header | ApiKey x-client-uuid in header | ApiKey auth_token in cookie | ApiKey ct0 in cookie | ApiKey gt0 in cookie | ApiKey x-csrf-token in header | ApiKey x-guest-token in header | ApiKey Priority in header | ApiKey Referer in header | ApiKey Sec-Ch-Ua in header | ApiKey Sec-Ch-Ua-Mobile in header | ApiKey Sec-Ch-Ua-Platform in header | ApiKey Sec-Fetch-Dest in header | ApiKey Sec-Fetch-Mode in header | ApiKey Sec-Fetch-Site in header | ApiKey user-agent in header

## Base URL
https://x.com/i/api

## Setup
1. Set Authorization header with your Bearer token
2. GET /1.1/friends/following/list.json -- verify access
3. POST /1.1/friendships/create.json -- create first create.json

## Endpoints

39 endpoints across 4 groups. See references/api-spec.lap for full details.

### 1.1
| Method | Path | Description |
|--------|------|-------------|
| GET | /1.1/friends/following/list.json | get friends following list |
| POST | /1.1/friendships/create.json | post create friendships |
| POST | /1.1/friendships/destroy.json | post destroy friendships |
| GET | /1.1/search/typeahead.json | get search typeahead |

### 2
| Method | Path | Description |
|--------|------|-------------|
| GET | /2/search/adaptive.json | get search adaptive |

### graphql
| Method | Path | Description |
|--------|------|-------------|
| GET | /graphql/{pathQueryId}/Bookmarks | get bookmarks |
| GET | /graphql/{pathQueryId}/CommunityAboutTimeline | get about of community |
| GET | /graphql/{pathQueryId}/CommunityMediaTimeline | get media list of community |
| GET | /graphql/{pathQueryId}/CommunityTweetsTimeline | get tweet list of community. rankingMode:[Recency, Relevance] |
| POST | /graphql/{pathQueryId}/CreateBookmark | create Bookmark |
| POST | /graphql/{pathQueryId}/CreateRetweet | create Retweet |
| POST | /graphql/{pathQueryId}/CreateTweet | create Tweet |
| POST | /graphql/{pathQueryId}/DeleteBookmark | delete Bookmark |
| POST | /graphql/{pathQueryId}/DeleteRetweet | delete Retweet |
| POST | /graphql/{pathQueryId}/DeleteTweet | delete Retweet |
| POST | /graphql/{pathQueryId}/FavoriteTweet | favorite Tweet |
| GET | /graphql/{pathQueryId}/Favoriters | get tweet favoriters |
| GET | /graphql/{pathQueryId}/Followers | get user list of followers |
| GET | /graphql/{pathQueryId}/FollowersYouKnow | get followers you know |
| GET | /graphql/{pathQueryId}/Following | get user list of following |
| GET | /graphql/{pathQueryId}/HomeLatestTimeline | get tweet list of timeline |
| GET | /graphql/{pathQueryId}/HomeTimeline | get tweet list of timeline |
| GET | /graphql/{pathQueryId}/Likes | get user likes tweets |
| GET | /graphql/{pathQueryId}/ListLatestTweetsTimeline | get tweet list of timeline |
| GET | /graphql/{pathQueryId}/NotificationsTimeline | get notification list. timeline_type:[All, Verified, Mentions] |
| GET | /graphql/{pathQueryId}/ProfileSpotlightsQuery | get user by screen name |
| GET | /graphql/{pathQueryId}/Retweeters | get tweet retweeters |
| GET | /graphql/{pathQueryId}/SearchTimeline | search tweet list. product:[Top, Latest, People, Photos, Videos] |
| GET | /graphql/{pathQueryId}/TweetDetail | get TweetDetail |
| GET | /graphql/{pathQueryId}/TweetResultByRestId | get TweetResultByRestId |
| POST | /graphql/{pathQueryId}/UnfavoriteTweet | unfavorite Tweet |
| GET | /graphql/{pathQueryId}/UserByRestId | get user by rest id |
| GET | /graphql/{pathQueryId}/UserByScreenName | get user by screen name |
| GET | /graphql/{pathQueryId}/UserHighlightsTweets | get user highlights tweets |
| GET | /graphql/{pathQueryId}/UserMedia | get user media tweets |
| GET | /graphql/{pathQueryId}/UserTweets | get user tweets |
| GET | /graphql/{pathQueryId}/UserTweetsAndReplies | get user replies tweets |
| GET | /graphql/{pathQueryId}/UsersByRestIds | get users by rest ids |

### other
| Method | Path | Description |
|--------|------|-------------|
| GET | /other | This is not an actual endpoint |

## Enhanced Skill Content
## Question Mapping

- "Who is a user following?" -> GET /1.1/friends/following/list.json
- "How do I follow someone on Twitter?" -> POST /1.1/friendships/create.json
- "How do I unfollow a user?" -> POST /1.1/friendships/destroy.json
- "Search for users, topics, or events by name?" -> GET /1.1/search/typeahead.json
- "Search tweets with full metadata and cards?" -> GET /2/search/adaptive.json
- "How do I post a new tweet?" -> POST /graphql/{pathQueryId}/CreateTweet
- "How do I delete a tweet?" -> POST /graphql/{pathQueryId}/DeleteTweet
- "How do I like (favorite) a tweet?" -> POST /graphql/{pathQueryId}/FavoriteTweet
- "How do I unlike a tweet?" -> POST /graphql/{pathQueryId}/UnfavoriteTweet
- "How do I retweet a post?" -> POST /graphql/{pathQueryId}/CreateRetweet
- "How do I undo a retweet?" -> POST /graphql/{pathQueryId}/DeleteRetweet
- "How do I bookmark a tweet?" -> POST /graphql/{pathQueryId}/CreateBookmark
- "How do I get my bookmarks?" -> GET /graphql/{pathQueryId}/Bookmarks
- "How do I look up a user by username?" -> GET /graphql/{pathQueryId}/UserByScreenName
- "How do I get a user's tweets and media?" -> GET /graphql/{pathQueryId}/UserTweets, GET /graphql/{pathQueryId}/UserMedia
- "How do I view my home timeline?" -> GET /graphql/{pathQueryId}/HomeTimeline
- "How do I see the latest tweets on my timeline?" -> GET /graphql/{pathQueryId}/HomeLatestTimeline
- "Who liked or retweeted a specific tweet?" -> GET /graphql/{pathQueryId}/Favoriters, GET /graphql/{pathQueryId}/Retweeters
- "How do I get the full detail of a single tweet?" -> GET /graphql/{pathQueryId}/TweetDetail
- "How do I check my notifications?" -> GET /graphql/{pathQueryId}/NotificationsTimeline

## Response Tips

- **v1.1 endpoints**: Responses are flat JSON objects; follow/unfollow return the updated user object directly. The following list uses `cursor` for pagination -- pass the returned `next_cursor` value to page forward.
- **v2 search**: Returns an `adaptive` response with `globalObjects` containing `tweets` and `users` as ID-keyed maps, plus `timeline.instructions` for ordering. Check `spelling_corrections` in response for query corrections.
- **GraphQL timelines** (Home, Search, User, List, Community, Notifications): All return `data.*.timeline_v2.timeline.instructions[]` with entries nested under `itemContent.tweet_results.result`. Pagination uses `cursor` entries within instructions -- extract the `Bottom` cursor value and pass it as the `cursor` variable on the next request.
- **GraphQL mutations** (CreateTweet, FavoriteTweet, CreateRetweet, CreateBookmark, Delete*): Return `data.*_result` on success. Always check the `errors` array -- a 200 status does NOT guarantee success; errors may include rate limit or permission issues inline.
- **GraphQL user lookups** (UserByScreenName, UserByRestId, UsersByRestIds): User data is nested under `data.user.result` with `legacy` containing screen_name, follower counts, and profile metadata.
- **Session/other endpoint**: Returns account state including `country`, `language`, `guestId`, and feature flags. Use this to validate session health before making authenticated calls.

## Anomaly Flags

- **Rate limit errors in 200 responses**: GraphQL endpoints return HTTP 200 with `errors[].message` containing "Rate limit exceeded" -- surface these immediately since the status code alone is misleading.
- **`pathQueryId` drift**: The hardcoded query IDs (e.g., `IID9x6WsdMnTlXnzXGq8ng` for CreateTweet) can change when Twitter deploys updates. If you receive "Could not resolve query ID" errors, flag that the query IDs need refreshing.
- **Auth token expiry**: Watch for `errors` containing "Could not authenticate you" or 401-like messages inside 200 responses. The `ct0` cookie (CSRF token) and `auth_token` cookie expire independently -- surface when either fails.
- **`dark_request` flag misuse**: Several mutations include `dark_request: bool`. When set to `true`, the action is performed silently (no notifications). Flag if this is set unintentionally, as it changes expected behavior.
- **Suspended or protected accounts**: User lookups may return `result.__typename: "UserUnavailable"` instead of user data. Surface the `reason` field so the caller understands why data is missing.
- **Feature flag mismatches**: CreateTweet requires ~30 feature flags. Missing or outdated flags can cause silent failures or degraded responses. Flag when the response contains fewer fields than expected.
- **Guest token vs authenticated**: Some endpoints work with `x-guest-token` alone while others require full `auth_token`. Surface when a guest-mode request fails on an auth-required endpoint.

## Playbook

### 1. Post a Tweet and Verify It

1. Confirm session is valid by calling `GET /other` and checking `Session.user_id` is present.
2. Call `POST /graphql/{pathQueryId}/CreateTweet` with `pathQueryId=IID9x6WsdMnTlXnzXGq8ng`, setting `tweet_text` in `variables` and all required `features` flags to their defaults.
3. Extract `data.create_tweet.tweet_results.result.rest_id` from the response as the new tweet ID.
4. Verify the tweet exists by calling `GET /graphql/{pathQueryId}/TweetResultByRestId` with `pathQueryId=7xflPyRiUxGVbJd4uWmbfg` and `variables.tweetId` set to the new tweet ID.
5. Check the `errors` array is empty in both responses to confirm success.

### 2. Search and Bookmark Interesting Tweets

1. Call `GET /graphql/{pathQueryId}/SearchTimeline` with `pathQueryId=VhUd6vHVmLBcw0uX-6jMLA` and set `variables.rawQuery` to your search terms.
2. Parse `data.search_by_raw_query.search_timeline.timeline.instructions` to extract tweet entries.
3. For each tweet of interest, extract its `rest_id` from `itemContent.tweet_results.result.rest_id`.
4. Call `POST /graphql/{pathQueryId}/CreateBookmark` with `pathQueryId=aoDbu3RHznuiSkQ9aNM67Q` and `variables.tweet_id` set to the tweet's `rest_id`.
5. Confirm bookmarks saved by calling `GET /graphql/{pathQueryId}/Bookmarks` with `pathQueryId=2neUNDqrrFzbLui8yallcQ`.

### 3. Follow a User by Username

1. Look up the user by calling `GET /graphql/{pathQueryId}/UserByScreenName` with `pathQueryId=1VOOyvKkiI3FMmkeDNxM9A` and `variables.screen_name` set to the target username.
2. Extract `data.user.result.rest_id` as the numeric user ID.
3. Call `POST /1.1/friendships/create.json` with the `user_id` parameter set to the extracted ID.
4. Verify the follow by calling `GET /graphql/{pathQueryId}/Following` with `pathQueryId=zx6e-TLzRkeDO_a7p4b3JQ` and your own user ID, then check that the target appears in results.

### 4. Explore a User's Profile and Engagement

1. Resolve the user via `GET /graphql/{pathQueryId}/UserByScreenName` to get their `rest_id`, follower/following counts, and bio from `result.legacy`.
2. Fetch their tweets with `GET /graphql/{pathQueryId}/UserTweets` using `pathQueryId=q6xj5bs0hapm9309hexA_g` and `variables.userId`.
3. Fetch their media posts with `GET /graphql/{pathQueryId}/UserMedia` using `pathQueryId=1H9ibIdchWO0_vz3wJLDTA`.
4. Check mutual connections via `GET /graphql/{pathQueryId}/FollowersYouKnow` with `pathQueryId=pNK460VRQKGuLfDcesjNEQ`.
5. View their highlights with `GET /graphql/{pathQueryId}/UserHighlightsTweets` using `pathQueryId=70Yf8aSyhGOXaKRLJdVA2A`.

### 5. Engage with a Tweet (Like, Retweet, Reply)

1. Fetch the full tweet via `GET /graphql/{pathQueryId}/TweetDetail` with `pathQueryId=xd_EMdYvB9hfZsZ6Idri0w` and `variables.focalTweetId` set to the tweet ID. Confirm the tweet exists and is not from a suspended account.
2. Like the tweet by calling `POST /graphql/{pathQueryId}/FavoriteTweet` with `pathQueryId=lI07N6Otwv1PhnEgXILM7A` and `variables.tweet_id`.
3. Retweet it by calling `POST /graphql/{pathQueryId}/CreateRetweet` with `pathQueryId=ojPdsZsimiJrUGLR1sjUtA`, `variables.tweet_id`, and `variables.dark_request=false`.
4. Reply by calling `POST /graphql/{pathQueryId}/CreateTweet` with `variables.reply.in_reply_to_tweet_id` set to the original tweet ID and `variables.tweet_text` containing your reply.
5. Check `errors` arrays in all responses -- a failed like or retweet (e.g., already liked) returns 200 with an error message, not an HTTP error.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
