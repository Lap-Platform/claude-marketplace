---
name: climate-fieldview-platform-apis
description: "Climate FieldView Platform APIs API skill. Use when working with Climate FieldView Platform APIs for fields, farmOrganizations, operations. Covers 28 endpoints."
version: 1.0.0
generator: lapsh
---

# Climate FieldView Platform APIs
API version: 4.0.11

## Auth
OAuth2 | ApiKey X-Api-Key in header

## Base URL
https://platform.climate.com/

## Setup
1. Set your API key in the appropriate header
2. GET /v4/fields -- verify access
3. POST /v4/boundaries/query -- create first query

## Endpoints

28 endpoints across 8 groups. See references/api-spec.lap for full details.

### fields
| Method | Path | Description |
|--------|------|-------------|
| GET | /v4/fields | Retrieve list of Fields |
| GET | /v4/fields/{fieldId} | Retrieve a specific Field by ID |

### farmOrganizations
| Method | Path | Description |
|--------|------|-------------|
| GET | /v4/farmOrganizations/{farmOrganizationType}/{farmOrganizationId} | Retrieve a specific farm organization by organization type and ID |

### operations
| Method | Path | Description |
|--------|------|-------------|
| GET | /v4/operations/all | Retrieve the operations accessible to a a given user. |

### resourceOwners
| Method | Path | Description |
|--------|------|-------------|
| GET | /v4/resourceOwners/{resourceOwnerId} | Retrieve a resource owner by ID |

### boundaries
| Method | Path | Description |
|--------|------|-------------|
| GET | /v4/boundaries/{boundaryId} | Retrieve a Boundary by ID |
| POST | /v4/boundaries/query | Retrieve Boundaries in batch |
| POST | /v4/boundaries | Upload a boundary |

### uploads
| Method | Path | Description |
|--------|------|-------------|
| POST | /v4/uploads | Initiate a new upload |
| PUT | /v4/uploads/{uploadId} | Chunked upload of data |
| GET | /v4/uploads/{uploadId}/status | Retrieve Upload status |
| POST | /v4/uploads/status/query | Retrieve Upload statuses in batch |

### exports
| Method | Path | Description |
|--------|------|-------------|
| POST | /v4/exports | Initiate a new export request. |
| GET | /v4/exports/{exportId}/status | Retrieve the status of an Export. |
| GET | /v4/exports/{exportId}/contents | Retrieve the binary contents of a processed export request. |

### layers
| Method | Path | Description |
|--------|------|-------------|
| GET | /v4/layers/scoutingObservations | Retrieve a list of scouting observations |
| GET | /v4/layers/scoutingObservations/{scoutingObservationId} | Retrieve individual scouting observation |
| GET | /v4/layers/scoutingObservations/{scoutingObservationId}/attachments | Retrieve attachments associated with a given scouting observation. |
| GET | /v4/layers/scoutingObservations/{scoutingObservationId}/attachments/{attachmentId}/contents | Retrieve the binary contents of a scouting observation’s attachment. |
| GET | /v4/layers/asPlanted | Retrieve a list of planting activities |
| GET | /v4/layers/asPlanted/{activityId}/contents | Retrieve the raw planting activity |
| GET | /v4/layers/asPlanted/{activityId} | Retrieve the summary of an activity as planted agronomic data |
| GET | /v4/layers/asApplied | Retrieve a list of application activities |
| GET | /v4/layers/asApplied/{activityId}/contents | Retrieve the raw application activity |
| GET | /v4/layers/asApplied/{activityId} | Retrieve the summary of an activity as applied agronomic data |
| GET | /v4/layers/asHarvested | Retrieve a list of harvest activities |
| GET | /v4/layers/asHarvested/{activityId}/contents | Retrieve the raw harvest activity |
| GET | /v4/layers/asHarvested/{activityId} | Retrieve the summary of an activity as harvested agronomic data |

## Enhanced Skill Content
## Question Mapping

- "What fields do I have access to?" -> GET /v4/fields
- "Show me details for a specific field" -> GET /v4/fields/{fieldId}
- "What is the boundary geometry for a field?" -> GET /v4/boundaries/{boundaryId}
- "Get boundaries for multiple fields at once" -> POST /v4/boundaries/query
- "Who owns this resource?" -> GET /v4/resourceOwners/{resourceOwnerId}
- "What farm organization does this field belong to?" -> GET /v4/farmOrganizations/{farmOrganizationType}/{farmOrganizationId}
- "List all operations for a grower" -> GET /v4/operations/all
- "Upload a GeoTIFF imagery layer" -> POST /v4/uploads
- "What is the status of my upload?" -> GET /v4/uploads/{uploadId}/status
- "Check status of multiple uploads at once" -> POST /v4/uploads/status/query
- "Export harvest data as GeoJSON" -> POST /v4/exports
- "Is my export ready to download?" -> GET /v4/exports/{exportId}/status
- "Download the exported file" -> GET /v4/exports/{exportId}/contents
- "What was planted in my fields this season?" -> GET /v4/layers/asPlanted
- "Show me harvest yield data for a specific activity" -> GET /v4/layers/asHarvested/{activityId}
- "What scouting observations were made this month?" -> GET /v4/layers/scoutingObservations

## Response Tips

- **Fields & Organizations**: Results wrapped in `{results: [...]}`. A 206 means partial content -- use `X-Next-Token` to paginate.
- **Boundaries**: Single boundary returns GeoJSON-like `{geometry, properties}`. Batch query via POST returns a FeatureCollection with `{type, features}`.
- **Uploads**: POST returns 201 with no body on initiation. PUT for chunked upload returns 204. Status polling returns `{id, status}` -- watch for terminal states.
- **Exports**: POST returns 201 with `{id}`. Status includes `error` (non-empty on failure), `size`, `checksum`, and `xNextToken`. Contents endpoint uses Range headers and returns 206 for partial downloads.
- **Layers (asPlanted/asApplied/asHarvested)**: Listing returns `{results: [...]}` with 200/206 pagination. Detail endpoints return rich metadata including `area`, `cropId`, `seasonCode`, timestamps, and layer-specific metrics (e.g., `moisturePct`, `wetMass` for harvest).
- **Scouting Observations**: Observations include `location`, `tags`, `fieldIds` arrays, and `status`. Attachments are fetched separately and downloaded via a contents sub-endpoint with Range headers.
- **Errors**: 429 appears on nearly every endpoint -- always implement backoff. 503 indicates temporary unavailability. 409/410/416 on export contents signal conflict, gone, or bad range respectively.

## Anomaly Flags

- **Rate limiting (429)**: Surface immediately when any endpoint returns 429. Nearly all endpoints declare this error -- the API enforces strict rate limits. Recommend exponential backoff.
- **Partial content (206)**: Flag when list endpoints return 206 instead of 200. This means results are truncated and `X-Next-Token` must be used to retrieve remaining data. Alert the user that they are seeing incomplete results.
- **Upload stuck states**: If `GET /v4/uploads/{uploadId}/status` returns the same non-terminal status after repeated polls, flag the upload as potentially stalled.
- **Export errors**: When `GET /v4/exports/{exportId}/status` returns a non-empty `error` field, surface the error message immediately rather than continuing to poll.
- **Gone exports (410)**: Export contents returning 410 means the export has expired and must be re-created. Surface this proactively.
- **Content-Type mismatch on uploads**: The POST /v4/uploads endpoint requires very specific MIME types (e.g., `image/vnd.climate.thermal.geotiff`). Flag if the user provides a generic MIME type like `image/tiff`.
- **Missing Accept header**: Layer content endpoints (asPlanted, asApplied, asHarvested contents) require an explicit `Accept` header. Flag if omitted.
- **304 Not Modified**: Several endpoints can return 304. Surface this so the agent knows to use cached data rather than retrying.

## Playbook

### 1. Inventory all fields and their boundaries

1. Call `GET /v4/fields` with a reasonable `X-Limit` (e.g., 100)
2. If response is 206, save `X-Next-Token` and repeat until you get 200
3. For each field, note the `boundaryId`
4. Batch-fetch boundaries with `POST /v4/boundaries/query` passing all collected boundary UUIDs
5. Pair each field with its GeoJSON geometry for mapping or analysis

### 2. Upload imagery and monitor processing

1. Prepare the file: compute MD5 hash, determine byte length, select the correct `contentType` (e.g., `image/vnd.climate.ndvi.geotiff`)
2. Initiate upload with `POST /v4/uploads` passing `{contentType, md5, length}`. Save the upload ID from the 201 response
3. Upload file contents in chunks using `PUT /v4/uploads/{uploadId}` with `Content-Range` headers
4. Poll `GET /v4/uploads/{uploadId}/status` until status reaches a terminal state
5. If uploading multiple files, use `POST /v4/uploads/status/query` with all upload IDs to check progress in bulk

### 3. Export and download harvest data

1. Create an export with `POST /v4/exports` specifying `contentType: "application/vnd.climate.harvest.geojson"` and any filter `definition`
2. Save the returned export `id`
3. Poll `GET /v4/exports/{exportId}/status` until `status` indicates completion. Check the `error` field on each poll
4. Once ready, use `size` and `checksum` from the status response to plan the download
5. Download with `GET /v4/exports/{exportId}/contents` using `Range` headers for chunked retrieval. Verify checksum after download

### 4. Review scouting observations with attachments

1. List observations with `GET /v4/layers/scoutingObservations`, optionally filtering with `occurredAfter`/`occurredBefore`
2. Paginate through results using `X-Next-Token` if response is 206
3. For each observation of interest, fetch full details via `GET /v4/layers/scoutingObservations/{id}`
4. List attachments with `GET /v4/layers/scoutingObservations/{id}/attachments`
5. Download each attachment using `GET /v4/layers/scoutingObservations/{id}/attachments/{attachmentId}/contents` with appropriate `Accept` and `Range` headers

### 5. Compare planting vs. harvest data for a season

1. List planting activities with `GET /v4/layers/asPlanted` filtered by `occurredAfter`/`occurredBefore` for the target season
2. List harvest activities with `GET /v4/layers/asHarvested` using the same date range
3. For each field (matched by `fieldId`), fetch planting details via `GET /v4/layers/asPlanted/{activityId}` to get `cropId`, `actualPopAvg`, `targetPopAvg`
4. Fetch corresponding harvest details via `GET /v4/layers/asHarvested/{activityId}` to get `wetMass`, `moisturePct`, `area`
5. Cross-reference by `fieldId` and `seasonCode` to analyze yield performance against planting inputs


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
