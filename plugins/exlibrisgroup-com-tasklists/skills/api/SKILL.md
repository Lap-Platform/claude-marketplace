---
name: ex-libris-apis
description: "Ex Libris APIs API skill. Use when working with Ex Libris APIs for almaws. Covers 11 endpoints."
version: 1.0.0
generator: lapsh
---

# Ex Libris APIs
API version: 1.0

## Auth
ApiKey apikey in query

## Base URL
https://api-eu.hosted.exlibrisgroup.com

## Setup
1. Set your API key in the appropriate header
2. GET /almaws/v1/task-lists/printouts -- verify access
3. POST /almaws/v1/task-lists/printouts -- create first printouts

## Endpoints

11 endpoints across 1 groups. See references/api-spec.lap for full details.

### almaws
| Method | Path | Description |
|--------|------|-------------|
| GET | /almaws/v1/task-lists/printouts | Retrieve Printouts |
| POST | /almaws/v1/task-lists/printouts | Act on Printouts |
| POST | /almaws/v1/task-lists/printouts/create | Create a Printout |
| GET | /almaws/v1/task-lists/printouts/{printout_id} | Retrieve a Printout |
| POST | /almaws/v1/task-lists/printouts/{printout_id} | Printout Service |
| GET | /almaws/v1/task-lists/requested-resources | Get Requested Resources |
| POST | /almaws/v1/task-lists/requested-resources | Act on Requested Resources |
| GET | /almaws/v1/task-lists/rs/lending-requests | Get Lending Requests |
| POST | /almaws/v1/task-lists/rs/lending-requests | Act on Lending Requests |
| GET | /almaws/v1/task-lists/test | GET Task-lists Test API |
| POST | /almaws/v1/task-lists/test | POST Task-lists Test API |

## Enhanced Skill Content
## Question Mapping

- "How do I list all printouts?" -> GET /almaws/v1/task-lists/printouts
- "Show me printouts filtered by a specific printer" -> GET /almaws/v1/task-lists/printouts?printer_id={id}
- "Get details for a specific printout" -> GET /almaws/v1/task-lists/printouts/{printout_id}
- "How do I mark printouts as printed or change their status?" -> POST /almaws/v1/task-lists/printouts?op={operation}
- "How do I perform an action on a specific printout?" -> POST /almaws/v1/task-lists/printouts/{printout_id}?op={operation}
- "How do I create a new printout?" -> POST /almaws/v1/task-lists/printouts/create
- "What resources are waiting to be picked up at a circulation desk?" -> GET /almaws/v1/task-lists/requested-resources?library={lib}&circ_desk={desk}
- "Show requested resources sorted by title instead of call number" -> GET /almaws/v1/task-lists/requested-resources?library={lib}&circ_desk={desk}&order_by=title
- "How do I bulk-process requested resources at a desk?" -> POST /almaws/v1/task-lists/requested-resources?op={operation}
- "List all active resource sharing lending requests" -> GET /almaws/v1/task-lists/rs/lending-requests
- "Show lending requests from a specific partner library" -> GET /almaws/v1/task-lists/rs/lending-requests?partner={code}
- "Filter lending requests by status and format" -> GET /almaws/v1/task-lists/rs/lending-requests?status={status}&requested_format={format}
- "How do I batch-update lending requests?" -> POST /almaws/v1/task-lists/rs/lending-requests?op={operation}
- "Is the Alma API reachable?" -> GET /almaws/v1/task-lists/test
- "How do I page through a large list of printouts?" -> GET /almaws/v1/task-lists/printouts?limit={n}&offset={n}

## Response Tips

- **Printouts** (GET/POST /printouts): Results are paginated via `limit`/`offset` -- check `total_record_count` in the response to know if more pages exist. Individual printout GETs return a single object, not a list wrapper.
- **Requested Resources** (GET/POST /requested-resources): `library` and `circ_desk` are required for reads -- omitting them returns 400. Results support `order_by` (call_number, title) and `direction` (asc/desc) for sorting.
- **Lending Requests** (GET/POST /rs/lending-requests): All filters are optional; an unfiltered call returns all lending requests. Watch for empty result sets when combining narrow filters.
- **Test endpoints** (GET/POST /test): Return simple health/connectivity confirmation -- no meaningful payload to parse.
- **Errors**: All endpoints return 400 (bad request -- check parameter values) or 500 (server error -- retry after a delay). Error responses typically contain an `errorList` array with `errorCode` and `errorMessage` fields.

## Anomaly Flags

- **400 errors with vague messages**: Ex Libris APIs sometimes return 400 for permission issues rather than 401/403 -- surface this when the API key might lack the required role.
- **Empty result sets on filtered queries**: Flag when a filtered printout or lending request query returns zero results but an unfiltered call returns data -- the filter value may be misspelled or the enum may have changed.
- **Pagination exhaustion**: Alert when `offset + limit >= total_record_count` so the caller knows they have retrieved all pages.
- **Missing `op` parameter on POST calls**: POST to /printouts and /printouts/{printout_id} require `op` -- surface a clear message if the caller forgets it, since the 400 error from Alma can be cryptic.
- **500 errors on batch operations**: Batch POSTs to /requested-resources or /lending-requests may partially succeed before a 500 -- flag that some records may have been modified even though the call returned an error.
- **Deprecated or renamed filter values**: If a previously working `status` or `letter` value starts returning 400, flag that Ex Libris may have updated the allowed enum values in a recent release.

## Playbook

### 1. Review and Reprint Failed Printouts

1. List printouts filtered to failed status: `GET /almaws/v1/task-lists/printouts?status=FAILED&limit=50`
2. Review each failed printout's details: `GET /almaws/v1/task-lists/printouts/{printout_id}`
3. Identify the printer or letter type causing failures
4. Re-trigger the printout: `POST /almaws/v1/task-lists/printouts/{printout_id}?op=reprint`
5. Verify the status changed by fetching the printout again

### 2. Process Hold Shelf Pickups at a Circulation Desk

1. Retrieve requested resources for the desk: `GET /almaws/v1/task-lists/requested-resources?library=MAIN&circ_desk=DEFAULT&order_by=call_number&direction=asc`
2. Page through results if needed by incrementing `offset` by `limit` until all items are retrieved
3. Identify items ready for the shelf (check reported/printed flags)
4. Batch-process the list: `POST /almaws/v1/task-lists/requested-resources?library=MAIN&circ_desk=DEFAULT&op=mark_reported`
5. Confirm processing by re-fetching the list with `reported=true`

### 3. Monitor and Fulfill Resource Sharing Lending Requests

1. List open lending requests: `GET /almaws/v1/task-lists/rs/lending-requests?status=OPEN`
2. Filter by partner if prioritizing a specific institution: add `&partner={partner_code}`
3. Review requested vs. supplied format to identify mismatches
4. Process fulfilled requests in batch: `POST /almaws/v1/task-lists/rs/lending-requests?op=mark_shipped&status=OPEN&partner={partner_code}`
5. Verify completion by re-listing with `status=SHIPPED`

### 4. Generate and Verify New Printouts

1. Test API connectivity: `GET /almaws/v1/task-lists/test`
2. Create a new printout batch: `POST /almaws/v1/task-lists/printouts/create`
3. List recent printouts to find the new batch: `GET /almaws/v1/task-lists/printouts?status=PENDING&limit=10`
4. Confirm each printout generated correctly: `GET /almaws/v1/task-lists/printouts/{printout_id}` for each result
5. If any are stuck, re-trigger: `POST /almaws/v1/task-lists/printouts/{printout_id}?op=reprint`

### 5. Audit Printout Activity by Staff Member

1. List all printouts by a specific user: `GET /almaws/v1/task-lists/printouts?printed_by={username}&limit=50`
2. Page through all results using `offset` increments
3. Cross-reference with specific letter types if needed: add `&letter={letter_type}`
4. Export or log the full list for audit records
5. Flag any printouts with unexpected status values for follow-up


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
