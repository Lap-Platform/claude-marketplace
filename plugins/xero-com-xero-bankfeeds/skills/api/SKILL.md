---
name: xero-bank-feeds-api
description: "Xero Bank Feeds API skill. Use when working with Xero Bank Feeds for FeedConnections, Statements. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# Xero Bank Feeds API
API version: 11.1.0

## Auth
OAuth2

## Base URL
https://api.xero.com/bankfeeds.xro/1.0

## Setup
1. Configure auth: OAuth2
2. GET /FeedConnections -- verify access
3. POST /FeedConnections -- create first FeedConnections

## Endpoints

7 endpoints across 2 groups. See references/api-spec.lap for full details.

### FeedConnections
| Method | Path | Description |
|--------|------|-------------|
| GET | /FeedConnections | Searches for feed connections |
| POST | /FeedConnections | Create one or more new feed connection |
| GET | /FeedConnections/{id} | Retrieve single feed connection based on a unique id provided |
| POST | /FeedConnections/DeleteRequests | Delete an existing feed connection |

### Statements
| Method | Path | Description |
|--------|------|-------------|
| GET | /Statements | Retrieve all statements |
| POST | /Statements | Creates one or more new statements |
| GET | /Statements/{statementId} | Retrieve single statement based on unique id provided |

## Enhanced Skill Content
## Question Mapping

- "How do I list all bank feed connections?" -> GET /FeedConnections
- "How do I create a new bank feed connection?" -> POST /FeedConnections
- "How do I get details for a specific feed connection?" -> GET /FeedConnections/{id}
- "How do I delete a bank feed connection?" -> POST /FeedConnections/DeleteRequests
- "How do I disconnect a bank account from Xero?" -> POST /FeedConnections/DeleteRequests
- "How do I list all bank statements?" -> GET /Statements
- "How do I push bank statement data into Xero?" -> POST /Statements
- "How do I get a specific statement by ID?" -> GET /Statements/{statementId}
- "How do I paginate through all feed connections?" -> GET /FeedConnections (use page & pageSize params)
- "How do I check the status of a feed connection?" -> GET /FeedConnections/{id} (inspect status field)
- "How do I submit statement lines with balances for a date range?" -> POST /Statements
- "How do I find which feed connection a statement belongs to?" -> GET /Statements/{statementId} (check feedConnectionId)
- "How do I ensure my POST request is not processed twice?" -> POST /FeedConnections or POST /Statements (use Idempotency-Key header)
- "How do I check for errors on a submitted statement?" -> GET /Statements/{statementId} (inspect errors array)

## Response Tips

- **FeedConnections (list/create/delete)**: All return 202 with a `pagination` object and `items` array. Check `pagination.pageCount` to determine if more pages exist. Each item includes a `status` field and an optional `error` map when something went wrong.
- **FeedConnections (single)**: Returns 200 with a flat object (no wrapper). The `error` field is only present when `status` indicates a problem.
- **Statements (list)**: Returns 200 with `pagination` + `items`. Use `page` and `pageSize` query params to iterate. Note the custom headers `Xero-Application-Id` and `Xero-User-Id` which have default values.
- **Statements (create)**: Returns 202 (accepted, not completed). Check returned items for per-statement `errors` arrays -- a 202 does not guarantee all statements succeeded.
- **Statements (single)**: Returns 200 with full detail including `statementLines` array and `errors` array. A 404 means the statementId is invalid or inaccessible.

## Anomaly Flags

- **202 with errors in items**: POST endpoints return 202 even when individual items fail. Always inspect each item's `error` or `errors` field -- do not treat 202 as blanket success.
- **Feed connection status changes**: Surface when a feed connection's `status` is anything other than active (e.g., suspended, error). This may silently block statement submission.
- **409 Conflict on statement POST**: Indicates a duplicate statement for the same feed connection and date range. Surface as a likely idempotency issue.
- **413 Payload Too Large**: Statement POST has a size limit. Flag when submitting large batches of statement lines and suggest splitting into smaller payloads.
- **422 Unprocessable Entity**: Indicates validation failure on statement data (e.g., balance mismatch, invalid dates). Surface the detail field for actionable guidance.
- **Missing Idempotency-Key**: Warn when making POST requests without the `Idempotency-Key` header, as retries could create duplicates.
- **Pagination exhaustion**: When `page >= pageCount`, flag that all results have been retrieved to prevent unnecessary requests.

## Playbook

### 1. Set Up a New Bank Feed Connection

1. Call `POST /FeedConnections` with an `Idempotency-Key` header and an `items` array containing the account details (`accountToken`, `accountNumber`, `accountName`, `currency`, `country`).
2. Check the 202 response -- inspect each item in `items` for an `error` field.
3. Note the returned `id` (UUID) for each successfully created connection.
4. Verify by calling `GET /FeedConnections/{id}` and confirming `status` is active.

### 2. Submit Bank Statements for a Feed Connection

1. Call `GET /FeedConnections` to find the target connection's `id`.
2. Build the statement payload: set `feedConnectionId` to the connection ID, define `startDate`/`endDate`, provide `startBalance` and `endBalance` with `amount` and `creditDebitIndicator`, and populate `statementLines` with transaction details.
3. Call `POST /Statements` with the `Idempotency-Key` header and the statement in the `items` array.
4. Inspect the 202 response. Check each item's `errors` array for line-level or statement-level failures.
5. Optionally call `GET /Statements/{statementId}` to confirm final status.

### 3. Remove a Bank Feed Connection

1. Call `GET /FeedConnections` to identify the connection to remove. Note its `id`.
2. Call `POST /FeedConnections/DeleteRequests` with an `items` array containing the connection(s) to delete (by `id`).
3. Check the 202 response for per-item errors.
4. Verify removal by calling `GET /FeedConnections` and confirming the connection is no longer listed or its status has changed.

### 4. Audit All Statements for a Period

1. Call `GET /Statements` with `page=1` and a suitable `pageSize`.
2. Loop through pages while `page < pageCount`, incrementing `page` each iteration.
3. For each statement in `items`, check the `status` field and `errors` array.
4. For any statement with errors, call `GET /Statements/{statementId}` to retrieve full detail including `statementLines`.
5. Compile a report of failed or problematic statements with their error details.

### 5. Retry a Failed Statement Submission

1. Call `GET /Statements/{statementId}` to review the `errors` array and identify the failure reason.
2. Fix the issue in the statement data (e.g., correct balance mismatch, fix date range, reduce payload size).
3. Generate a new `Idempotency-Key` (do not reuse the original key if you changed the payload).
4. Call `POST /Statements` with the corrected statement.
5. Verify success by checking the response `items` for errors and confirming via `GET /Statements/{statementId}`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
