---
name: returns-management
description: "Returns Management API skill. Use when working with Returns Management for returns, feeds. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Returns Management

## Auth
ApiKey WM_SEC.ACCESS_TOKEN in header

## Base URL
https://marketplace.walmartapis.com

## Setup
1. Set your API key in the appropriate header
2. GET /v3/returns -- verify access
3. POST /v3/returns/{returnOrderId}/refund -- create first refund

## Endpoints

3 endpoints across 2 groups. See references/api-spec.lap for full details.

### returns
| Method | Path | Description |
|--------|------|-------------|
| POST | /v3/returns/{returnOrderId}/refund | Issue refund |
| GET | /v3/returns | Returns |

### feeds
| Method | Path | Description |
|--------|------|-------------|
| POST | /v3/feeds | Return Item Overrides |

## Enhanced Skill Content
## Question Mapping

- "How do I issue a refund for a return?" -> POST /v3/returns/{returnOrderId}/refund
- "How do I refund a specific line item on a return order?" -> POST /v3/returns/{returnOrderId}/refund
- "Can I partially refund a return by specifying quantity?" -> POST /v3/returns/{returnOrderId}/refund
- "How do I list all returns?" -> GET /v3/returns
- "How do I look up a return by order ID?" -> GET /v3/returns (use `returnOrderId` or `customerOrderId` filter)
- "How do I find returns with a specific status?" -> GET /v3/returns (use `status` filter)
- "How do I get returns created within a date range?" -> GET /v3/returns (use `returnCreationStartDate` + `returnCreationEndDate`)
- "How do I find recently modified returns?" -> GET /v3/returns (use `returnLastModifiedStartDate` + `returnLastModifiedEndDate`)
- "How do I check if a return has a replacement?" -> GET /v3/returns (use `replacementInfo` filter)
- "How do I paginate through all returns?" -> GET /v3/returns (use `nextCursor` from response `meta`)
- "How do I submit a returns override feed?" -> POST /v3/feeds (with `feedType=RETURNS_OVERRIDES`)
- "How do I bulk update return overrides?" -> POST /v3/feeds
- "How do I filter returns by type?" -> GET /v3/returns (use `returnType` filter)
- "How do I refund multiple line items at once?" -> POST /v3/returns/{returnOrderId}/refund (pass multiple entries in `refundLines` array)

## Response Tips

- **Returns listing** (`GET /v3/returns`): Response is cursor-paginated -- use `meta.nextCursor` to fetch the next page; `meta.totalCount` gives the full result count; default `limit` is 10. `returnOrders` is an array of maps with nested line-item detail.
- **Refund** (`POST /v3/returns/{returnOrderId}/refund`): Response mirrors back the `returnOrderId`, `customerOrderId`, and processed `refundLines` -- compare against your request to confirm all lines were accepted.
- **Feeds** (`POST /v3/feeds`): Returns only a `feedId` string -- you must poll the Walmart Feed Status API separately to track processing progress; a 200 means accepted, not completed.

## Anomaly Flags

- **Missing `nextCursor`**: When `meta.nextCursor` is absent or empty but `meta.totalCount` exceeds the returned count, pagination may have silently stopped -- surface this mismatch.
- **Partial refund acceptance**: If the refund response contains fewer `refundLines` entries than submitted, flag that some lines may have been rejected silently.
- **Feed accepted but no status endpoint**: After `POST /v3/feeds` returns a `feedId`, remind the user this API has no feed-status endpoint -- they need the separate Feeds API to check processing outcome.
- **Auth header requirements**: All three endpoints require `WM_SEC.ACCESS_TOKEN`, `WM_QOS.CORRELATION_ID`, and `WM_SVC.NAME` -- flag immediately if any are missing before making a call.
- **Date filter without both bounds**: Using `returnCreationStartDate` without `returnCreationEndDate` (or vice versa) may return unexpected results -- warn when only one bound is set.
- **Unusual HTTP status codes**: Surface 429 (rate limit), 401/403 (token expired or invalid), and 409 (conflict, e.g., duplicate refund attempt) with actionable next steps.

## Playbook

### 1. Issue a Full Refund on a Return Order

1. Call `GET /v3/returns` with `returnOrderId` or `customerOrderId` to retrieve the return and its line items.
2. Extract each line's `returnOrderLineNumber` and full quantity from the response.
3. Build the `refundLines` array with all lines and their original quantities.
4. Call `POST /v3/returns/{returnOrderId}/refund` with the complete `refundLines` payload.
5. Verify the response `refundLines` matches your request to confirm all lines were refunded.

### 2. Search and Filter Returns by Date and Status

1. Call `GET /v3/returns` with `status` set to the desired value (e.g., `INITIATED`, `COMPLETED`).
2. Add `returnCreationStartDate` and `returnCreationEndDate` to narrow the time window.
3. Set `limit` to control page size (default is 10).
4. Read `meta.nextCursor` from the response and pass it in subsequent requests to paginate through all matching results.
5. Repeat until `nextCursor` is absent or empty.

### 3. Bulk Override Returns via Feed

1. Prepare the returns override payload file in the format required by Walmart's feed specification.
2. Call `POST /v3/feeds` with `feedType=RETURNS_OVERRIDES` and the payload in the request body.
3. Capture the `feedId` from the response.
4. Use the Walmart Feeds API (`GET /v3/feeds/{feedId}`) to poll for processing status until the feed reaches a terminal state.
5. Review any error details in the feed status response for lines that failed processing.

### 4. Reconcile Refunds Against Customer Orders

1. Call `GET /v3/returns` with `customerOrderId` to retrieve all returns associated with a specific customer order.
2. For each return in `returnOrders`, note the `returnOrderId` and line-item details.
3. Cross-reference against your internal order system to identify any returns not yet refunded.
4. For each unrefunded return, call `POST /v3/returns/{returnOrderId}/refund` with the appropriate `refundLines`.
5. Log each refund response for audit trail and flag any mismatches between requested and confirmed lines.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
