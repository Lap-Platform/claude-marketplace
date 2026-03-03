---
name: getty-images-api
description: "Getty Images API skill. Use when working with Getty Images for affiliates, ai, artists. Covers 76 endpoints."
version: 1.0.0
generator: lapsh
---

# Getty Images API
API version: 3

## Auth
ApiKey Api-Key in header | OAuth2

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /v3/affiliates/search/images -- verify access
3. POST /v3/ai/image-generations -- create first image-generations

## Endpoints

76 endpoints across 19 groups. See references/api-spec.lap for full details.

### affiliates
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/affiliates/search/images |  |
| GET | /v3/affiliates/search/videos |  |

### ai
| Method | Path | Description |
|--------|------|-------------|
| POST | /v3/ai/image-generations | Generates images from a prompt |
| GET | /v3/ai/image-generations/{generationRequestId} | Get generated images from a previous generation request |
| POST | /v3/ai/image-generations/{generationRequestId}/images/{index}/variations | Get variations on a generated image |
| POST | /v3/ai/file-registrations | Register a client provided file for use with AIGenerator endpoints |
| GET | /v3/ai/file-registrations |  |
| GET | /v3/ai/file-registrations/{fileRegistrationId} | Get details on a registered file |
| DELETE | /v3/ai/file-registrations/{fileRegistrationId} | Archives a registered file |
| POST | /v3/ai/image-generations/refine | Refine an image |
| POST | /v3/ai/image-generations/extend | Extend an image |
| POST | /v3/ai/image-generations/background-removal | Remove a background |
| POST | /v3/ai/image-generations/object-removal | Remove object(s) |
| POST | /v3/ai/image-generations/background-replacement | Replace the background of an existing image |
| POST | /v3/ai/image-generations/influence-color-by-image | Influence the color of generated images using a reference image |
| POST | /v3/ai/image-generations/influence-composition-by-image | Influence the composition of generated images using a reference image |
| POST | /v3/ai/image-generations/background-generations | Add a background to a reference image |
| GET | /v3/ai/generation-history | Retrieve history of AI generations |
| GET | /v3/ai/generation-history/{generationRequestId} | Retrieve history item for an individual generation request |
| GET | /v3/ai/image-generations/{generationRequestId}/images/{index}/download-sizes | Get download sizes for a generated image |
| PUT | /v3/ai/image-generations/{generationRequestId}/images/{index}/download | Begin the download process |
| GET | /v3/ai/image-generations/{generationRequestId}/images/{index}/download | Once the download process has started, this endpoint can be used to check the status of the download and get the |
| POST | /v3/ai/redownloads | Re-download a previously downloaded item |
| POST | /v3/ai/enhance-prompt | Expands and enriches a short prompt to produce a more detailed and descriptive prompt which can then be used to generate images. |

### artists
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/artists/images | Search for images by a photographer |
| GET | /v3/artists/videos | Search for videos by a photographer |

### asset-changes
| Method | Path | Description |
|--------|------|-------------|
| PUT | /v3/asset-changes/change-sets | Get asset change notifications. |
| DELETE | /v3/asset-changes/change-sets/{change-set-id} | Confirm asset change notifications. |
| GET | /v3/asset-changes/channels | Get a list of asset change notification channels. |

### asset-licensing
| Method | Path | Description |
|--------|------|-------------|
| POST | /v3/asset-licensing/{assetId} | Endpoint for acquiring extended licenses with iStock credits for an asset. |

### boards
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/boards | Get all boards that the user participates in |
| POST | /v3/boards | Create a new board |
| GET | /v3/boards/{board_id} | Get assets and metadata for a specific board |
| DELETE | /v3/boards/{board_id} | Delete a board |
| PUT | /v3/boards/{board_id} | Update a board |
| PUT | /v3/boards/{board_id}/assets | Add assets to a board |
| DELETE | /v3/boards/{board_id}/assets | Remove assets from a board |
| PUT | /v3/boards/{board_id}/assets/{asset_id} | Add an asset to a board |
| DELETE | /v3/boards/{board_id}/assets/{asset_id} | Remove an asset from a board |
| POST | /v3/boards/{board_id}/assets/{asset_id}/comments | Add a comment to an asset on the specified board. |
| DELETE | /v3/boards/{board_id}/assets/{asset_id}/comments/{comment_id} | Delete a comment from an asset on the specified board. |
| GET | /v3/boards/{board_id}/comments | Get comments from a board |
| POST | /v3/boards/{board_id}/comments | Add a comment to a board |
| DELETE | /v3/boards/{board_id}/comments/{comment_id} | Delete a comment from a board |

### collections
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/collections | Gets collections applicable for the customer. |

### countries
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/countries | Gets countries codes and names. |

### customers
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/customers/current | Returns information about the current user. |

### downloads
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/downloads | Returns information about a customer's downloaded assets. |
| POST | /v3/downloads/images/{id} | Download an image |
| POST | /v3/downloads/videos/{id} | Download a video |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/events | Get metadata for multiple events |
| GET | /v3/events/{id} | Get metadata for a single event |

### image-match
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/image-match/search | Searches for image matches using the provided URL. |

### images
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/images | Get metadata for multiple images by supplying multiple image ids |
| GET | /v3/images/{id} | Get metadata for a single image by supplying one image id |
| GET | /v3/images/{id}/downloadhistory | Returns information about a customer's download history for a specific asset |
| GET | /v3/images/{id}/same-series | Retrieve creative images from the same series |
| GET | /v3/images/{id}/similar | Retrieve similar images |

### orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/orders/{id} | Get order metadata |

### products
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/products | Get Products |

### purchased-assets
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/purchased-assets | Get Previously Purchased Images and Video |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/search/events | Search for events |
| GET | /v3/search/images/creative | Search for creative images only |
| GET | /v3/search/images/creative/by-image | Search for creative images based on url |
| GET | /v3/search/images/editorial | Search for editorial images only |
| GET | /v3/search/videos/creative | Search for creative videos |
| GET | /v3/search/videos/creative/by-image | Search for creative videos based on url |
| GET | /v3/search/videos/editorial | Search for editorial videos |
| PUT | /v3/search/by-image/uploads/{file-name} | Upload image for use by the search creative images/videos operations |
| GET | /v3/search/images | Search for both creative and editorial images - *** DEPRECATED *** |

### usage-batches
| Method | Path | Description |
|--------|------|-------------|
| PUT | /v3/usage-batches/{id} | Report usage of assets via a batch format. |

### videos
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/videos | Get metadata for multiple videos by supplying multiple video ids |
| GET | /v3/videos/{id} | Get metadata for a single video by supplying one video id |
| GET | /v3/videos/{id}/downloadhistory | Returns information about a customer's download history for a specific asset |
| GET | /v3/videos/{id}/same-series | Retrieve creative videos from the same series |
| GET | /v3/videos/{id}/similar | Retrieve similar videos |

## Enhanced Skill Content
## Question Mapping

- "Search for creative stock photos of sunsets?" -> GET /v3/search/images/creative
- "Find editorial news images from last week?" -> GET /v3/search/images/editorial
- "Generate an AI image from a text prompt?" -> POST /v3/ai/image-generations
- "Check the status of my AI image generation?" -> GET /v3/ai/image-generations/{generationRequestId}
- "Download a specific stock image?" -> POST /v3/downloads/images/{id}
- "Find videos similar to one I already have?" -> GET /v3/videos/{id}/similar
- "Create a board and add assets to it?" -> POST /v3/boards + PUT /v3/boards/{board_id}/assets
- "Remove the background from a generated image?" -> POST /v3/ai/image-generations/background-removal
- "Search for images using a reference photo?" -> GET /v3/search/images/creative/by-image
- "What products are available on my account?" -> GET /v3/products
- "View my recent download history?" -> GET /v3/downloads
- "Who am I authenticated as?" -> GET /v3/customers/current
- "Find all images by a specific artist?" -> GET /v3/artists/images
- "Report asset usage for compliance tracking?" -> PUT /v3/usage-batches/{id}
- "Get details and licensing info for a video clip?" -> GET /v3/videos/{id}

## Response Tips

- **Search endpoints** (`/search/*`): Always paginated via `page`/`page_size` with `result_count` for total. Check `auto_corrections.phrase` for spell-fix signals and `related_searches` for query refinement. Facets (`specific_people`, `events`, `locations`, `artists`, `entertainment`) are only populated when `include_facets=true`.
- **AI generation endpoints** (`/ai/*`): Return 202 Accepted with a `generation_request_id` for async polling. The GET status endpoint also returns 202 while processing and 200 when results are ready. Watch for 410 Gone on expired generations.
- **Download endpoints** (`/downloads/*`): May return 303 redirect to the actual file URL instead of the file body. The `auto_download` flag controls this behavior.
- **Board endpoints** (`/boards/*`): PUT for assets returns both `assets_added` and `assets_not_added` arrays -- always check the latter for partial failures. Board GET includes a `permissions` map governing what the current user can do.
- **Batch lookups** (`/images`, `/videos`, `/events` with `ids`): Return both a found array and a `*_not_found` array. Always check the not-found list rather than assuming all IDs resolved.
- **Asset detail endpoints** (`/images/{id}`, `/videos/{id}`): Deeply nested objects for `allowed_use`, `keywords`, `display_sizes`, and `download_sizes`. Use the `fields` parameter to limit payload size.

## Anomaly Flags

- **429 Too Many Requests**: Nearly every AI endpoint returns 429. Surface rate limit warnings proactively and suggest backing off before retries. Track request cadence across generation, variation, and refinement calls.
- **410 Gone on AI generations**: Generated images expire. If a download or variation returns 410, alert the user that the generation has been purged and must be re-created.
- **409 Conflict on AI endpoints**: Signals a state conflict (e.g., generation still processing, duplicate request, or revoked product). Surface the specific generation_request_id so the user can investigate.
- **402 Payment Required on asset-licensing**: Insufficient credits. Proactively surface `credits_used` from successful licensing calls and warn when the operation requires `use_team_credits`.
- **`auto_corrections` in search results**: When the API silently corrects a search phrase, surface the original vs. corrected term so the user knows their exact query was not used.
- **`assets_not_added` / `*_not_found` arrays**: Partial failures on batch operations should always be surfaced, not silently ignored.
- **`product_revoked_date` in generation history**: If non-null, the product tied to a generation has been revoked. Alert the user that re-downloads may fail.
- **503 on `/customers/current`**: Service degradation. Surface this as a system health issue rather than an auth problem.

## Playbook

### 1. Generate an AI Image and Download It

1. Call `POST /v3/ai/image-generations` with your `prompt`, `aspect_ratio`, `media_type`, and `mood`.
2. Note the returned `generation_request_id`.
3. Poll `GET /v3/ai/image-generations/{generationRequestId}` until the response status changes from 202 to 200 and `results` is populated.
4. Pick a result by `index`. Call `GET /v3/ai/image-generations/{generationRequestId}/images/{index}/download-sizes` to see available sizes.
5. Initiate download with `PUT /v3/ai/image-generations/{generationRequestId}/images/{index}/download`, specifying `size_name` and `product_id`.
6. Poll `GET /v3/ai/image-generations/{generationRequestId}/images/{index}/download` until 200 returns a `url`.
7. Fetch the file from the returned URL.

### 2. Search, Preview, and License a Stock Image

1. Search with `GET /v3/search/images/creative` using `phrase`, desired `orientations`, `page_size`, and any filters (color, mood, ethnicity).
2. Review `result_count` and iterate pages if needed. Check `auto_corrections` for query rewrites.
3. For a candidate, call `GET /v3/images/{id}` with `fields` including `display_sizes` and `download_sizes` to inspect resolution options.
4. Download via `POST /v3/downloads/images/{id}` with the desired `file_type`, `height`, and `product_id`.
5. If extended licensing is needed, call `POST /v3/asset-licensing/{assetId}` with the required `extended_licenses` array.

### 3. Curate a Board with Comments

1. Create a board: `POST /v3/boards` with a `name` and optional `description`.
2. Note the returned board `id`.
3. Add assets in bulk: `PUT /v3/boards/{board_id}/assets` with an array of asset IDs in the body. Check `assets_not_added` for failures.
4. Add a comment on a specific asset: `POST /v3/boards/{board_id}/assets/{asset_id}/comments` with `Text`.
5. Add a board-level comment: `POST /v3/boards/{board_id}/comments` with `text`.
6. Retrieve all comments for review: `GET /v3/boards/{board_id}/comments`.

### 4. Iterate on an AI-Generated Image

1. Generate an initial image via `POST /v3/ai/image-generations` and poll until results are ready.
2. Create a variation: `POST /v3/ai/image-generations/{generationRequestId}/images/{index}/variations`.
3. Refine with inpainting: `POST /v3/ai/image-generations/refine` providing a `mask_url` and updated `prompt`.
4. Extend the canvas: `POST /v3/ai/image-generations/extend` with directional percentages (`left_percentage`, `right_percentage`, etc.).
5. Replace the background: `POST /v3/ai/image-generations/background-replacement` with a new `prompt` or `background_color`.
6. Each step returns a new `generation_request_id` -- poll each one before proceeding to the next refinement.

### 5. Track Downloads and Report Usage

1. Pull recent downloads: `GET /v3/downloads` with `date_from`/`date_to` and `company_downloads=true` for team-wide history.
2. For a specific asset, check its download history: `GET /v3/images/{id}/downloadhistory` or `GET /v3/videos/{id}/downloadhistory`.
3. Cross-reference with purchased assets: `GET /v3/purchased-assets` with date filters.
4. Report usage to Getty for compliance: `PUT /v3/usage-batches/{id}` with an array of `asset_usages` including `asset_id`, `quantity`, and `usage_date`.
5. Check `invalid_assets` in the response to catch any IDs that failed validation.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
