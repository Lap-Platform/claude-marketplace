---
name: bc-gov-news-api-service-10
description: "BC Gov News API Service 1.0 API skill. Use when working with BC Gov News API Service 1.0 for api. Covers 27 endpoints."
version: 1.0.0
generator: lapsh
---

# BC Gov News API Service 1.0
API version: 1.0

## Auth
Requires API key (key parameter)

## Base URL
https://news.api.gov.bc.ca/

## Setup
1. Include your API key via the key parameter
2. GET /api/FacebookPosts/ByUri -- verify access

## Endpoints

27 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/FacebookPosts/ByUri | Get a Facebook post based on a Uri |
| GET | /api/Home | Returns the top level content for the home page |
| GET | /api/Ministries | Get all ministries |
| GET | /api/Ministries/{key} | Get the Ministry associated with the ministry key |
| GET | /api/Ministries/{key}/Minister | Get the Minister associated with the ministry key |
| GET | /api/Newsletters | Get all newsletters |
| GET | /api/Newsletters/{newsletterKey} | Get a specific newsletter |
| GET | /api/Newsletters/{newsletterKey}/Editions/{editionKey} | Returns a specific edition of a newsletter |
| GET | /api/Newsletters/{newsletterKey}/Editions/{editionKey}/Articles/{articleKey} | Get an article belonging to a Newsletter edition |
| GET | /api/Newsletters/Images/{guid} | Get the image object reference by of a Newsletter Edition associated with the image guid |
| GET | /api/Posts/{key} | Get the post associated with the key |
| GET | /api/Posts | Get the posts associated with the keys in the list passed in. |
| GET | /api/Posts/Latest/{indexKind}/{indexKey} | Get the latest posts of postKind for the specified index (default or category) |
| GET | /api/Posts/Keys/{indexKind}/{indexKey} | Get all keys for the specified index (newsroom or category) |
| GET | /api/Posts/Keys/{reference} | Get the post key associated with the reference. |
| GET | /api/Posts/LatestMediaUri/{mediaType} | Gets the latest Social Media post for the social media type passed in. |
| GET | /api/ResourceLinks | Get all resource links |
| GET | /api/Sectors | Get all Sectors |
| GET | /api/Sectors/{key} | Get the sector associated with the key |
| GET | /api/Services | Get all Services |
| GET | /api/Services/{key} | Get the service associated with the passed key |
| GET | /api/Slides/{id} | Get the slide associated to the id |
| GET | /api/Slides | Get all Slides |
| GET | /api/Tags | Get all Tags |
| GET | /api/Tags/{key} | Get the Tag associated with the key |
| GET | /api/Themes | Get all Themes |
| GET | /api/Themes/{key} | Get the Theme associated with the key |

## Enhanced Skill Content
## Question Mapping

- "What ministries are available in BC government news?" -> GET /api/Ministries
- "Who is the minister for a specific ministry?" -> GET /api/Ministries/{key}/Minister
- "What is the latest news post about a topic?" -> GET /api/Posts/Latest/{indexKind}/{indexKey}
- "Show me details for a specific news post" -> GET /api/Posts/{key}
- "What Facebook posts mention a given URI?" -> GET /api/FacebookPosts/ByUri
- "What newsletters does the BC government publish?" -> GET /api/Newsletters
- "Show me a specific newsletter edition" -> GET /api/Newsletters/{newsletterKey}/Editions/{editionKey}
- "What sectors does BC Gov News cover?" -> GET /api/Sectors
- "What services are listed in BC Gov News?" -> GET /api/Services
- "What tags are used to categorize news?" -> GET /api/Tags
- "What themes are currently active?" -> GET /api/Themes
- "What is on the BC Gov News homepage right now?" -> GET /api/Home
- "Get the latest media URI for a specific media type" -> GET /api/Posts/LatestMediaUri/{mediaType}
- "Find all post keys for a given index" -> GET /api/Posts/Keys/{indexKind}/{indexKey}
- "What resource links are available?" -> GET /api/ResourceLinks

## Response Tips

- **List endpoints** (Ministries, Sectors, Services, Tags, Themes, Newsletters, Slides, Posts): Return bare arrays; iterate directly on the response body. No wrapper object or pagination envelope.
- **Detail endpoints** (single ministry, sector, service, tag, theme): Return flat objects with social media URIs (`twitterFeedUsername`, `flickrUri`, `youtubeUri`, `audioUri`) and an `isActive` boolean -- always check `isActive` before displaying.
- **Posts**: `publishDate` is ISO 8601 datetime; `ministryKeys`, `sectorKeys`, `serviceKeys` are string arrays referencing other entities by key. Documents and `azureAssets` are arrays of maps with varying shapes.
- **Paginated-style endpoints** (Posts/Latest, Posts/Keys): Use `count` and `skip` query params for manual pagination; there is no `next` cursor or total count in the response -- increment `skip` until an empty array is returned.
- **Newsletter deep paths**: Articles and editions are nested under newsletter keys; a 404 at any level means the parent key is invalid.
- **Images** (Newsletter images, Slides): `imageBytes` and `image` are base64-encoded byte strings; decode before rendering. Check `imageType` for the MIME type.
- **Home**: Returns live webcast URLs (`liveWebcastFlashMediaManifestUrl`, `liveWebcastM3uPlaylist`) that may be empty strings when no broadcast is active.

## Anomaly Flags

- **Empty live webcast URLs**: If `GET /api/Home` returns empty `liveWebcastFlashMediaManifestUrl` and `liveWebcastM3uPlaylist`, surface that no live broadcast is currently running.
- **Inactive entities**: When `isActive` is `false` on a ministry, sector, service, tag, or theme, flag it -- the user may be referencing stale data.
- **Missing contact info**: If a ministry's `contactUser` or `secondContactUser` has empty `phoneNumber` and `emailAddress`, warn that no contact route is available.
- **Empty documents or azureAssets**: When a post has `hasMediaAssets: true` but `documents` and `azureAssets` arrays are empty, flag the inconsistency.
- **Redirect posts**: If `redirectUri` is non-empty on a post, surface that this post redirects elsewhere and the current content may be a stub.
- **Pagination exhaustion**: When `Posts/Latest` or `Posts/Keys` returns fewer results than `count`, proactively note that the end of available posts has been reached.
- **api-version drift**: The common field `api-version` defaults to `1.0`; if a newer version becomes available, flag that requests are pinned to an older version.

## Playbook

### 1. Get All News Posts for a Ministry

1. Call `GET /api/Ministries` to list all ministries and find the target ministry key.
2. Call `GET /api/Posts/Latest/ministry/{ministryKey}?postKind=&count=25&skip=0` to fetch the first page of posts.
3. For each post of interest, call `GET /api/Posts/{key}` to retrieve full details including documents and media assets.
4. Increment `skip` by 25 and repeat step 2 until an empty array is returned.

### 2. Browse a Newsletter from Start to Finish

1. Call `GET /api/Newsletters` to list available newsletters.
2. Call `GET /api/Newsletters/{newsletterKey}` to get the newsletter details and its `editions` array.
3. Pick an edition and call `GET /api/Newsletters/{newsletterKey}/Editions/{editionKey}` to get the full HTML body.
4. If the edition contains article links, call `GET /api/Newsletters/{newsletterKey}/Editions/{editionKey}/Articles/{articleKey}` for individual article content.

### 3. Build a Ministry Profile Page

1. Call `GET /api/Ministries/{key}` to get ministry details, social links, contact info, and related topic/service/newsletter links.
2. Call `GET /api/Ministries/{key}/Minister` to get the minister's bio, photo, and headline.
3. Call `GET /api/Posts/Latest/ministry/{key}?count=5` to pull the five most recent posts for the ministry.
4. Combine the ministry metadata, minister profile, and recent posts into a unified profile view.

### 4. Search Across Sectors and Tags

1. Call `GET /api/Sectors` and `GET /api/Tags` in parallel to retrieve all available categories.
2. Identify the relevant sector or tag key from the lists.
3. Call `GET /api/Posts/Keys/{indexKind}/{indexKey}` (where `indexKind` is `sector` or `tag`) to get all post keys in that category.
4. Batch-fetch post details using `GET /api/Posts?postKeys={key1}&postKeys={key2}` with the collected keys.

### 5. Check for Live Webcasts and Featured Content

1. Call `GET /api/Home` to get the homepage state, including live webcast URLs and featured post keys.
2. If `liveWebcastM3uPlaylist` is non-empty, a live broadcast is active -- present the stream URL.
3. Call `GET /api/Posts/{topPostKey}` and `GET /api/Posts/{featurePostKey}` to load the featured content.
4. Call `GET /api/Slides` to get current homepage slide data for visual display.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
