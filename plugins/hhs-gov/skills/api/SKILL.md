---
name: hhs-media-services-api
description: "HHS Media Services API skill. Use when working with HHS Media Services for resources.json, resources. Covers 31 endpoints."
version: 1.0.0
generator: lapsh
---

# HHS Media Services API
API version: 2

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /resources.json -- verify access

## Endpoints

31 endpoints across 2 groups. See references/api-spec.lap for full details.

### resources.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /resources.json | Get Resources by search query |

### resources
| Method | Path | Description |
|--------|------|-------------|
| GET | /resources/campaigns.json | Get Campaigns |
| GET | /resources/campaigns/{id}.json | Get Campaign by ID |
| GET | /resources/campaigns/{id}/media.json | Get MediaItems by Campaign ID |
| GET | /resources/campaigns/{id}/syndicate.{format} | Get MediaItems for Campaign |
| GET | /resources/languages.json | Get Languages |
| GET | /resources/languages/{id}.json | Get Language by ID |
| GET | /resources/media.json | Get MediaItems |
| GET | /resources/media/featured.json | Get the list of featured content in the syndication system |
| GET | /resources/media/mostPopularMedia.{format} | Get MediaItems by popularity |
| GET | /resources/media/searchResults.json | Get MediaItems by search query |
| GET | /resources/media/{id}.json | Get MediaItem by ID |
| GET | /resources/media/{id}/content | Get content for MediaItem |
| GET | /resources/media/{id}/embed.json | Get embed code for MediaItem |
| GET | /resources/media/{id}/preview.jpg | Get Tag by ID |
| GET | /resources/media/{id}/relatedMedia.{format} | Get related MediaItems by ID |
| GET | /resources/media/{id}/syndicate.{format} | Get syndicated content for MediaItem |
| GET | /resources/media/{id}/thumbnail.jpg | Get JPG thumbnail for MediaItem |
| GET | /resources/media/{id}/youtubeMetaData.json | Get Youtube metadata for MediaItem |
| GET | /resources/mediaTypes.{format} | Get MediaTypes |
| GET | /resources/sources.json | Get Sources |
| GET | /resources/sources/{id}.json | Get Source by ID |
| GET | /resources/sources/{id}/syndicate.{format} | Get MediaItems for Source |
| GET | /resources/tags.{format} | Get Tags |
| GET | /resources/tags/tagLanguages.{format} | Get TagLanguages |
| GET | /resources/tags/tagTypes.{format} | Get MediaItems for Tag |
| GET | /resources/tags/{id}.{format} | Get Tag by ID |
| GET | /resources/tags/{id}/media.{format} | Get MediaItems for Tag |
| GET | /resources/tags/{id}/related.{format} | Get related Tags by ID |
| GET | /resources/tags/{id}/syndicate.{format} | Get MediaItems for Tag |
| GET | /resources/userMediaLists/{id}.json | Get UserMediaList by ID |

## Enhanced Skill Content
## Question Mapping

- "Search for health content about diabetes?" -> GET /resources.json
- "List all available campaigns?" -> GET /resources/campaigns.json
- "Get details for campaign 42?" -> GET /resources/campaigns/{id}.json
- "What media items belong to a specific campaign?" -> GET /resources/campaigns/{id}/media.json
- "Find media by keyword?" -> GET /resources/media/searchResults.json
- "What media types does HHS support?" -> GET /resources/mediaTypes.{format}
- "Show me featured health media?" -> GET /resources/media/featured.json
- "What are the most popular media items?" -> GET /resources/media/mostPopularMedia.{format}
- "Get the embed code for a media item?" -> GET /resources/media/{id}/embed.json
- "Download a thumbnail or preview image for media?" -> GET /resources/media/{id}/thumbnail.jpg
- "What languages are available for content?" -> GET /resources/languages.json
- "List all content sources (agencies/organizations)?" -> GET /resources/sources.json
- "Find media tagged with a specific topic?" -> GET /resources/tags/{id}/media.{format}
- "Get the syndicated HTML content for a media item with custom styling?" -> GET /resources/media/{id}/syndicate.{format}
- "What content was published in a specific date range?" -> GET /resources/media.json

## Response Tips

- **Search & listing endpoints** (`/resources.json`, `/media/searchResults.json`): Results are paginated via `max` (page size) and `offset` (starting index); always check total count in the response metadata to know if more pages exist.
- **Detail endpoints** (`/{id}.json`): Return a single nested object; look for the primary record inside a `results` wrapper array even for single-item responses.
- **Syndication endpoints** (`/syndicate.{format}`): Return rendered HTML or other formatted content, not JSON; the `{format}` path segment controls output type.
- **Image endpoints** (`/thumbnail.jpg`, `/preview.jpg`): Return binary image data with appropriate content-type headers, not JSON.
- **Error responses** (400, 500): Expect a JSON body with error message details; 400 typically means missing required parameters or invalid filter values.

## Anomaly Flags

- **Empty result sets on broad queries**: If `/resources/media.json` with no filters returns zero results, the upstream service may be experiencing issues -- surface this to the user.
- **500 errors on any endpoint**: HHS services can have intermittent availability; flag repeated 500s and suggest retrying after a delay.
- **Date filter mismatches**: If `InRange` parameters return fewer results than expected compared to `SinceDate`/`BeforeDate` equivalents, the range format may be incorrect -- alert the user to verify date format.
- **Missing YouTube metadata**: If `/media/{id}/youtubeMetaData.json` returns 400 for a video item, the media may not be YouTube-hosted -- flag this before the user builds a workflow around it.
- **Syndication content changes**: If syndicated content hash (available via `hash` filter on `/media.json`) differs from a previously cached value, flag that the source content was updated.
- **Pagination ceiling**: If responses consistently return exactly `max` items, warn the user there are likely more results and they should paginate.

## Playbook

### 1. Discover and embed health content by topic

1. Search for content: `GET /resources/media/searchResults.json?q=vaccination&max=10`
2. Review results and pick a media item by its `id`
3. Get embed code: `GET /resources/media/{id}/embed.json?width=600&height=400`
4. Use the returned embed snippet in your page or application

### 2. Build a multilingual content feed

1. List available languages: `GET /resources/languages.json`
2. Note the `id` for your target language (e.g., Spanish)
3. Fetch media filtered by language: `GET /resources/media.json?languageId={langId}&max=25&sort=-dateContentPublished`
4. Paginate through results using `offset` to collect the full set
5. For each item, fetch syndicated content: `GET /resources/media/{id}/syndicate.json`

### 3. Monitor a campaign's media inventory

1. List campaigns: `GET /resources/campaigns.json`
2. Get campaign details: `GET /resources/campaigns/{id}.json`
3. Fetch all media in the campaign: `GET /resources/campaigns/{id}/media.json?max=50&offset=0`
4. For each media item, check for updates using date filters: `GET /resources/media.json?contentUpdatedSinceDate={lastCheck}`
5. Compare content hashes to detect changes in syndicated material

### 4. Tag-based content curation

1. Browse available tags: `GET /resources/tags.json?max=50&sort=name`
2. Filter tags by type if needed: `GET /resources/tags.json?typeName=Topic`
3. Get media for a chosen tag: `GET /resources/tags/{tagId}/media.json?max=20`
4. Explore related tags: `GET /resources/tags/{tagId}/related.json`
5. Fetch thumbnails for display: `GET /resources/media/{mediaId}/thumbnail.jpg`

### 5. Source-specific content syndication

1. List all content sources: `GET /resources/sources.json`
2. Get source details: `GET /resources/sources/{id}.json`
3. Fetch media from that source: `GET /resources/media.json?sourceId={id}&max=25`
4. Generate syndication widget for the source: `GET /resources/sources/{id}/syndicate.json?displayMethod=feed`
5. For individual items, customize syndication: `GET /resources/media/{id}/syndicate.json?stripStyles=true&stripScripts=true&imageFloat=left`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
