---
name: event-export-api
description: "Event Export API skill. Use when working with Event Export for export. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Event Export API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /export -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### export
| Method | Path | Description |
|--------|------|-------------|
| GET | /export | Download Data |

## Enhanced Skill Content
## Question Mapping

- "How do I export events from a specific date range?" -> GET /export
- "Can I filter exported events by project?" -> GET /export (use project_id parameter)
- "How do I export only a specific event type?" -> GET /export (use event parameter)
- "How do I limit the number of exported events?" -> GET /export (use limit parameter)
- "Can I filter events with a custom expression?" -> GET /export (use where parameter)
- "How do I get timestamps in milliseconds instead of seconds?" -> GET /export (set time_in_ms=true)
- "How do I download a compressed export?" -> GET /export (set Accept-Encoding to gzip)
- "What's the largest export I can pull in one request?" -> GET /export (check limit parameter bounds)
- "How do I export all events for a single project last month?" -> GET /export (combine from_date, to_date, project_id)
- "Can I export events matching a specific property value?" -> GET /export (use where parameter with JQL/filter expression)
- "How do I do a daily export job?" -> GET /export (call repeatedly with rolling from_date/to_date windows)
- "How do I export everything and paginate through results?" -> GET /export (use limit + shifting from_date based on last event timestamp)

## Response Tips

- **Export responses**: Expect a potentially large payload; always set Accept-Encoding: gzip for non-trivial date ranges. The response is likely newline-delimited JSON or CSV -- check Content-Type headers. If limit is set, assume there may be more data beyond the returned batch; re-request with an adjusted from_date to paginate. Timestamps default to seconds unless time_in_ms=true. Watch for empty results when the date range or filters match nothing -- this is a 200 with an empty body, not an error.

## Anomaly Flags

- **Large date ranges without limit**: If from_date and to_date span more than 30 days with no limit set, warn the user about potential response size and timeout risk.
- **Missing compression**: If Accept-Encoding is not set on large exports, suggest enabling gzip to reduce transfer size.
- **Empty results on valid ranges**: If a 200 response returns zero events, surface this -- it may indicate a wrong project_id, overly restrictive where filter, or incorrect date format.
- **Rate limiting / 429 responses**: If the API returns 429, surface the retry-after header and pause automated export loops.
- **Timestamp ambiguity**: If time_in_ms is not explicitly set, flag that timestamps are in seconds by default -- mixing units is a common source of bugs downstream.
- **Deprecated or unexpected fields in response**: If the response payload contains fields not documented in the spec, flag them as potential deprecation candidates or schema drift.

## Playbook

### 1. Basic Date-Range Export

1. Determine the desired date range (e.g., 2025-01-01 to 2025-01-31).
2. Call `GET /export?from_date=2025-01-01&to_date=2025-01-31`.
3. Set `Accept-Encoding: gzip` header for compressed transfer.
4. Parse the response body according to its Content-Type.

### 2. Project-Scoped Filtered Export

1. Identify the target project_id.
2. Define the event type to filter (e.g., `signup`).
3. Call `GET /export?from_date=2025-01-01&to_date=2025-01-31&project_id=42&event=signup`.
4. Optionally add a `where` expression to narrow further (e.g., `where=properties["plan"]=="pro"`).
5. Process the filtered result set.

### 3. Paginated Full Export

1. Set an initial `from_date` and `to_date` covering the full desired range.
2. Call `GET /export?from_date=...&to_date=...&limit=10000`.
3. Record the timestamp of the last event in the response.
4. Shift `from_date` to just after that last timestamp.
5. Repeat until the response returns fewer events than the limit (indicating the final page).

### 4. Daily Automated Sync

1. Store the last successful export date in local state.
2. Set `from_date` to that date and `to_date` to today.
3. Call `GET /export?from_date=...&to_date=...&time_in_ms=true` for precision.
4. Ingest the response into your data warehouse or analytics pipeline.
5. Update the stored last-export date to `to_date` on success.

### 5. Debugging Missing Events

1. Start with a broad query: `GET /export?from_date=...&to_date=...&project_id=42`.
2. If empty, remove `project_id` to confirm events exist in the date range at all.
3. If events appear without the filter, verify the project_id is correct.
4. If still empty, widen the date range -- the events may have timestamps outside the expected window.
5. Check whether `time_in_ms` alignment matches your date format expectations.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
