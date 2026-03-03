---
name: api-v1
description: "API V1 API skill. Use when working with API V1 for api. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# API V1
API version: v1

## Auth
ApiKey apiKey in header

## Base URL
https://{defaultHost}

## Setup
1. Set your API key in the appropriate header
2. GET /api/v1/scans -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/v1/scans | Retrieves all scans |
| GET | /api/v1/scans/{id} | Retrieves a project scan result |
| GET | /api/v1/scans/{id}/files/{file_id} | Retrieves a file object, containing information about dependencies in the file |

## Enhanced Skill Content
## Question Mapping

- "List all scans" -> GET /api/v1/scans
- "Search for a scan by name" -> GET /api/v1/scans?name={name}
- "Show me the first 10 scans" -> GET /api/v1/scans?per_page=10
- "Get details for scan X" -> GET /api/v1/scans/{id}
- "What's the status of scan ABC?" -> GET /api/v1/scans/{id}
- "Show me the files in scan X" -> GET /api/v1/scans/{id}/files/{file_id}
- "Get file Y from scan X" -> GET /api/v1/scans/{id}/files/{file_id}
- "Paginate through files in a scan" -> GET /api/v1/scans/{id}/files/{file_id}?per_page={n}
- "Does a scan with this name exist?" -> GET /api/v1/scans?name={name}
- "How many scans are there?" -> GET /api/v1/scans
- "Find a scan and then retrieve one of its files" -> GET /api/v1/scans?name={name}, then GET /api/v1/scans/{id}/files/{file_id}
- "Get a specific file's content from a known scan" -> GET /api/v1/scans/{id}/files/{file_id}

## Response Tips

- **Scans list** (`GET /scans`): Results may be paginated via `per_page`. Check for total count or next-page indicators in the response body. A 404 means the resource path is wrong, not "no results" (empty list is 200).
- **Scan detail** (`GET /scans/{id}`): Returns a single scan object. A 404 means the scan ID does not exist -- confirm the ID before retrying.
- **Scan files** (`GET /scans/{id}/files/{file_id}`): Requires both scan and file IDs. Supports `per_page` for paginated file content. A 404 can mean either the scan or the file was not found -- check both IDs.

## Anomaly Flags

- **404 on scan detail**: Surface when a scan ID returns 404 -- it may have been deleted or the ID is malformed. Suggest listing scans to verify.
- **Empty scan list**: If `GET /scans` returns an empty set, flag that no scans exist yet or the name filter may be too restrictive.
- **Pagination exhaustion**: If `per_page` is set but the response contains fewer items than requested, surface that the final page has been reached.
- **Missing file ID**: If a user asks for "files in a scan" without a specific file_id, flag that this API requires a known file_id -- there is no list-all-files endpoint.
- **Auth failures**: If requests fail with 401/403, surface that the `apiKey` header may be missing or invalid.

## Playbook

### 1. Find a scan by name and inspect it

1. Call `GET /api/v1/scans?name={search_term}` to find matching scans
2. Extract the scan `id` from the results
3. Call `GET /api/v1/scans/{id}` to get full scan details

### 2. Retrieve a specific file from a scan

1. Identify the scan ID (list scans if unknown)
2. Identify the file ID from scan details or prior knowledge
3. Call `GET /api/v1/scans/{id}/files/{file_id}` to retrieve the file
4. If the response is paginated, repeat with `per_page` adjustments

### 3. Page through all scans

1. Call `GET /api/v1/scans?per_page=25` for the first page
2. Check the response for pagination metadata (next page token or offset)
3. Repeat with updated pagination parameters until all results are consumed

### 4. Verify a scan exists before accessing its files

1. Call `GET /api/v1/scans/{id}` with the target scan ID
2. If 404, stop and inform the user the scan does not exist
3. If 200, proceed to `GET /api/v1/scans/{id}/files/{file_id}` for the desired file


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
