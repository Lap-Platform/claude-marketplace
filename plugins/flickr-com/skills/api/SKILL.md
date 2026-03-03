---
name: flickr-api-schema
description: "Flickr API Schema API skill. Use when working with Flickr API Schema for rest?method=flickr.favorites.getList, rest?method=flickr.people.getPhotos, rest?method=flickr.photosets.getList. Covers 25 endpoints."
version: 1.0.0
generator: lapsh
---

# Flickr API Schema
API version: 1.0.0

## Auth
ApiKey api_key in query

## Base URL
https://api.flickr.com/services

## Setup
1. Set your API key in the appropriate header
2. GET /rest?method=flickr.favorites.getList -- verify access
3. POST /upload -- create first upload

## Endpoints

25 endpoints across 24 groups. See references/api-spec.lap for full details.

### rest?method=flickr.favorites.getList
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.favorites.getList | Returns a list of the user's favorite photos. Only photos which the calling user has permission to see are returned. |

### rest?method=flickr.people.getPhotos
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.people.getPhotos | Return photos from the given user's photostream |

### rest?method=flickr.photosets.getList
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.photosets.getList | Returns the albums belonging to the specified user |

### rest?method=flickr.favorites.getContext
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.favorites.getContext | Returns next and previous favorites for a photo in a user's favorites |

### rest?method=flickr.groups.getInfo
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.groups.getInfo | Get information about a group |

### rest?method=flickr.groups.pools.getPhotos
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.groups.pools.getPhotos | Returns a list of pool photos for a given group |

### rest?method=flickr.groups.discuss.topics.getList
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.groups.discuss.topics.getList | Get a list of discussion topics in a group. |

### rest?method=flickr.groups.discuss.replies.getInfo
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.groups.discuss.replies.getInfo | Get information on a group topic reply |

### rest?method=flickr.groups.discuss.topics.getInfo
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.groups.discuss.topics.getInfo | Get information about a group discussion topic |

### rest?method=flickr.groups.pools.getContext
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.groups.pools.getContext | Returns next and previous photos for a photo in a group pool |

### rest?method=flickr.photolist.getContext
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.photolist.getContext | Returns next and previous photos in a photo list |

### rest?method=flickr.photos.getContext
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.photos.getContext | Returns next and previous photos for a photo in a photostream |

### rest?method=flickr.photos.licenses.getInfo
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.photos.licenses.getInfo | Fetches a list of available photo licenses for Flickr |

### rest?method=flickr.people.getInfo
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.people.getInfo | Returns a person |

### rest?method=flickr.photos.getExif
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.photos.getExif | Retrieves a list of EXIF/TIFF/GPS tags for a given photo. The calling user must have permission to view the photo. |

### rest?method=flickr.photos.getInfo
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.photos.getInfo | Returns a photo |

### rest?method=flickr.photos.getSizes
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.photos.getSizes | Returns photo sizes |

### rest?method=flickr.photosets.getContext
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.photosets.getContext | Returns next and previous photos for a photo in a set |

### rest?method=flickr.photosets.getPhotos
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.photosets.getPhotos | Returns a list of photos in an album. |

### rest?method=flickr.galleries.getPhotos
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.galleries.getPhotos | Returns a list of photos in a gallery. |

### rest?method=flickr.photos.search
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.photos.search | Return a list of photos matching some criteria. |

### upload
| Method | Path | Description |
|--------|------|-------------|
| POST | /upload | Uploads a new photo to Flickr |

### rest?method=flickr.test.echo
| Method | Path | Description |
|--------|------|-------------|
| GET | /rest?method=flickr.test.echo | Echos the input parameters back in the response |

### oauth
| Method | Path | Description |
|--------|------|-------------|
| GET | /oauth/request_token | Returns an oauth token and oauth token secret |
| GET | /oauth/access_token | Returns an access token |

## Enhanced Skill Content
## Question Mapping

- "What are a user's favorite photos?" -> GET /rest?method=flickr.favorites.getList
- "Show me photos uploaded by a specific user" -> GET /rest?method=flickr.people.getPhotos
- "List all photosets (albums) for a user" -> GET /rest?method=flickr.photosets.getList
- "Search for photos by keyword or tag" -> GET /rest?method=flickr.photos.search
- "Get detailed info about a specific photo" -> GET /rest?method=flickr.photos.getInfo
- "What sizes are available for a photo?" -> GET /rest?method=flickr.photos.getSizes
- "What EXIF data does a photo have?" -> GET /rest?method=flickr.photos.getExif
- "Get profile info for a Flickr user" -> GET /rest?method=flickr.people.getInfo
- "Upload a photo to Flickr" -> POST /upload
- "What photos are in a gallery?" -> GET /rest?method=flickr.galleries.getPhotos
- "Show photos in a group pool" -> GET /rest?method=flickr.groups.pools.getPhotos
- "Get info about a Flickr group" -> GET /rest?method=flickr.groups.getInfo
- "What are the available photo licenses?" -> GET /rest?method=flickr.photos.licenses.getInfo
- "Find photos taken within a geographic bounding box" -> GET /rest?method=flickr.photos.search (with bbox, lat, lon, radius params)
- "Is the API working? Test connectivity" -> GET /rest?method=flickr.test.echo

## Response Tips

- **Photo listings** (favorites, people.getPhotos, search, pools, galleries, photosets.getPhotos): Paginated via `page` and `per_page` params; response includes `pages` and `total` fields in the wrapper element. Default `per_page` is typically 100, max 500.
- **Single photo info** (getInfo, getExif, getSizes): Returns nested objects -- sizes are in `sizes.size[]` array, EXIF in `photo.exif[]` array. Check `stat` attribute for "ok" vs "fail".
- **Context endpoints** (getContext, pools.getContext, photosets.getContext): Return `prevphoto` and `nextphoto` objects for navigation; either may be `0` when at the boundary.
- **Group discussion** (topics.getList, topics.getInfo, replies.getInfo): Paginated topic lists; reply info returns a single reply object. Check `message` field on errors.
- **Upload**: Returns XML with `photoid` on success or `err` element with `code` and `msg` attributes on failure. Requires multipart/form-data encoding.
- **OAuth**: Returns URL-encoded key-value pairs (not JSON/XML). Parse `oauth_token` and `oauth_token_secret` from the response body.

## Anomaly Flags

- **Rate limiting**: Flickr enforces 3600 calls/hour per API key. Surface a warning when making rapid sequential calls (e.g., paginating through large result sets) and recommend batching with delays.
- **`stat: "fail"` responses**: All endpoints return HTTP 200 even on errors. Agents must check the `stat` field -- surface `err code` and `err msg` values immediately rather than treating 200 as success.
- **Empty result sets**: `total: 0` on search or listing calls may indicate an invalid `user_id`, overly restrictive filters, or a private account -- flag this to the user with suggestions.
- **Deprecated format param**: If `format=json` is used without `nojsoncallback=1`, the response is wrapped in a JSONP function call. Always flag when this param is missing.
- **Permission errors on EXIF**: `getExif` fails with code 2 ("Permission denied") when the photo owner has disabled EXIF viewing. Surface this as a permissions issue, not a bug.
- **OAuth token expiry**: If requests suddenly return auth errors after previously working, flag that the OAuth access token may have been revoked or expired.
- **Upload content_type mismatch**: If `content_type` param (1=photo, 2=screenshot, 3=other) doesn't match the actual file, Flickr may misclassify the upload. Flag when this param is omitted.

## Playbook

### 1. Search and Download Photos by Topic

1. Call GET /rest?method=flickr.photos.search with `text` or `tags` param and `per_page=10`
2. Parse the response for `photo` array; extract each photo's `id`, `server`, `secret`, and `farm`
3. For each photo of interest, call GET /rest?method=flickr.photos.getSizes with `photo_id`
4. Select the desired size from the `sizes.size[]` array and use its `source` URL to download
5. Check `license` via flickr.photos.getInfo if you need to verify usage rights

### 2. Browse a User's Complete Photo Library

1. Call GET /rest?method=flickr.people.getInfo with `user_id` to confirm the user exists and get their profile
2. Call GET /rest?method=flickr.photosets.getList with `user_id` and `per_page=500` to get all albums
3. For each photoset, call GET /rest?method=flickr.photosets.getPhotos with `photoset_id` to list contents
4. To see non-album photos, call GET /rest?method=flickr.people.getPhotos with `user_id`, paginating with `page` param
5. Use GET /rest?method=flickr.photos.getInfo on individual photos for full metadata

### 3. Upload a Photo with Metadata

1. Obtain an OAuth access token via GET /oauth/request_token then GET /oauth/access_token (user must authorize in browser between steps)
2. Call POST /upload with `photo` (binary), `title`, `description`, `tags` (space-separated, quote multi-word tags)
3. Parse the response XML for `photoid`
4. Call GET /rest?method=flickr.photos.getInfo with the returned `photo_id` to confirm upload and verify metadata
5. Optionally call GET /rest?method=flickr.photos.getSizes to confirm available resolutions

### 4. Explore a Group's Pool and Discussions

1. Call GET /rest?method=flickr.groups.getInfo with `group_id` or `group_path_alias` to get group details and member count
2. Call GET /rest?method=flickr.groups.pools.getPhotos with `group_id` to browse the photo pool
3. Call GET /rest?method=flickr.groups.discuss.topics.getList with `group_id` to see active discussion threads
4. For a specific thread, call GET /rest?method=flickr.groups.discuss.topics.getInfo with `topic_id` to read the opening post
5. Call GET /rest?method=flickr.groups.discuss.replies.getInfo with `topic_id` and `reply_id` for individual replies

### 5. Authenticate via OAuth (Full Flow)

1. Call GET /oauth/request_token with your consumer key, nonce, timestamp, signature method (HMAC-SHA1), version (1.0), signature, and callback URL
2. Parse `oauth_token` and `oauth_token_secret` from the URL-encoded response
3. Direct the user to `https://www.flickr.com/services/oauth/authorize?oauth_token={token}` to grant access
4. After authorization, Flickr redirects to your callback with `oauth_verifier` and `oauth_token`
5. Call GET /oauth/access_token with the verifier, token, and your consumer credentials to obtain the final access token and secret


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
