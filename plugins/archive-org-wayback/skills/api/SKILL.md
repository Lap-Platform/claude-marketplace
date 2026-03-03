---
name: wayback-api
description: "Wayback API skill. Use when working with Wayback for wayback. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Wayback API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
https://api.archive.org/

## Setup
1. No auth setup needed
2. GET /wayback/v1/available -- verify access
3. POST /wayback/v1/available -- create first available

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### wayback
| Method | Path | Description |
|--------|------|-------------|
| GET | /wayback/v1/available |  |
| POST | /wayback/v1/available |  |

## Enhanced Skill Content
## Question Mapping

- "Is this URL archived?" -> GET /wayback/v1/available
- "Check if a webpage has a snapshot" -> GET /wayback/v1/available
- "Find the closest archived version of a site to a specific date" -> GET /wayback/v1/available (with timestamp)
- "Was this page captured around 2020?" -> GET /wayback/v1/available (with timestamp=2020)
- "Get the most recent archive of example.com" -> GET /wayback/v1/available
- "Check availability with a specific HTTP status code filter" -> GET /wayback/v1/available (with status_code)
- "Look up multiple URLs for archival status" -> POST /wayback/v1/available (with availabilty_request)
- "Batch check whether several pages are in the Wayback Machine" -> POST /wayback/v1/available
- "Get a JSONP-wrapped availability response" -> GET /wayback/v1/available (with callback)
- "Find the nearest snapshot to a timestamp, preferring older captures" -> GET /wayback/v1/available (with closest=before)
- "Check if a URL was archived but set a short timeout" -> GET /wayback/v1/available (with timeout)
- "Find a tagged snapshot for a URL" -> GET /wayback/v1/available (with tag)
- "Is there a 200-status snapshot of this page near Jan 2019?" -> GET /wayback/v1/available (with timestamp=20190101, status_code=200)

## Response Tips

- **Availability responses**: The result nests under `archived_snapshots.closest` -- always check this object exists before reading `url`, `timestamp`, or `status`. A missing `closest` key means no snapshot was found, not an error.
- **Batch responses (POST)**: Each item in the request maps to a corresponding result; iterate by input URL to match results. Empty `archived_snapshots` objects indicate unarchived URLs.
- **JSONP (callback)**: When `callback` is set, the response body is wrapped in a function call -- parse accordingly or omit the parameter for raw JSON.

## Anomaly Flags

- **No snapshot found**: Surface immediately when `archived_snapshots` is empty or missing the `closest` key -- the user likely expects a result and should know the URL has no captures.
- **Stale snapshots**: If the returned `timestamp` is more than 2 years old, flag it -- the archived version may not reflect the current site.
- **Non-200 snapshot status**: When the snapshot's `status` field is not `200` (e.g., `301`, `404`), alert the user -- they may be viewing a redirect or error page capture, not the intended content.
- **Timeout behavior**: If using a short `timeout` value and getting empty results, suggest increasing it -- the CDX index lookup may need more time for obscure URLs.
- **Typo in spec field**: The API spec uses `availabilty_request` (misspelled) -- use this exact spelling in POST bodies or the parameter will be silently ignored.

## Playbook

### 1. Check if a Single URL is Archived

1. Call `GET /wayback/v1/available?url=https://example.com`
2. Inspect `archived_snapshots.closest` in the response
3. If present, read `url` for the Wayback link and `timestamp` for capture date
4. If absent, the URL has no known snapshots

### 2. Find the Nearest Snapshot to a Specific Date

1. Call `GET /wayback/v1/available?url=https://example.com&timestamp=20200315`
2. Check `archived_snapshots.closest.timestamp` to see how close the match is
3. Optionally add `closest=before` or `closest=after` to control direction preference
4. Compare the returned timestamp against your target to decide if the result is usable

### 3. Batch-Check Multiple URLs

1. Build a POST body with `url` set to the primary target and `availabilty_request` containing a list of URL maps
2. Send `POST /wayback/v1/available` with the payload
3. Iterate through each result and check for `archived_snapshots.closest`
4. Collect URLs with empty snapshots into a "not archived" list for the user

### 4. Filter Snapshots by HTTP Status

1. Call `GET /wayback/v1/available?url=https://example.com&status_code=200`
2. This restricts results to captures where the original page returned HTTP 200
3. Use this to avoid redirect or error-page snapshots
4. If no result is returned, retry without `status_code` to see if non-200 captures exist

### 5. Integrate with a Monitoring Workflow

1. For each monitored URL, call `GET /wayback/v1/available?url={target}`
2. Record the `timestamp` from `archived_snapshots.closest`
3. On subsequent runs, compare the new timestamp against the stored one
4. If the timestamp has not changed over a defined period, flag the URL as potentially stale or no longer being crawled


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
