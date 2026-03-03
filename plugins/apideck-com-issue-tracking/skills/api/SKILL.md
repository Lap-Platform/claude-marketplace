---
name: issue-tracking-api
description: "Issue Tracking API skill. Use when working with Issue Tracking for issue-tracking. Covers 15 endpoints."
version: 1.0.0
generator: lapsh
---

# Issue Tracking API
API version: 10.24.0

## Auth
ApiKey Authorization in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /issue-tracking/collections -- verify access
3. POST /issue-tracking/collections/{collection_id}/tickets -- create first tickets

## Endpoints

15 endpoints across 1 groups. See references/api-spec.lap for full details.

### issue-tracking
| Method | Path | Description |
|--------|------|-------------|
| GET | /issue-tracking/collections | List Collections |
| GET | /issue-tracking/collections/{collection_id} | Get Collection |
| GET | /issue-tracking/collections/{collection_id}/tickets | List Tickets |
| POST | /issue-tracking/collections/{collection_id}/tickets | Create Ticket |
| GET | /issue-tracking/collections/{collection_id}/tickets/{ticket_id} | Get Ticket |
| PATCH | /issue-tracking/collections/{collection_id}/tickets/{ticket_id} | Update Ticket |
| DELETE | /issue-tracking/collections/{collection_id}/tickets/{ticket_id} | Delete Ticket |
| GET | /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments | List Comments |
| POST | /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments | Create Comment |
| GET | /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments/{id} | Get Comment |
| PATCH | /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments/{id} | Update Comment |
| DELETE | /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments/{id} | Delete Comment |
| GET | /issue-tracking/collections/{collection_id}/users | List Users |
| GET | /issue-tracking/collections/{collection_id}/users/{id} | Get user |
| GET | /issue-tracking/collections/{collection_id}/tags | List Tags |

## Enhanced Skill Content
## Question Mapping

- "What collections or projects are available?" -> GET /issue-tracking/collections
- "Show me the details of a specific collection" -> GET /issue-tracking/collections/{collection_id}
- "List all tickets in a project" -> GET /issue-tracking/collections/{collection_id}/tickets
- "Create a new ticket in a collection" -> POST /issue-tracking/collections/{collection_id}/tickets
- "Get the details of a specific ticket" -> GET /issue-tracking/collections/{collection_id}/tickets/{ticket_id}
- "Update the priority or status of a ticket" -> PATCH /issue-tracking/collections/{collection_id}/tickets/{ticket_id}
- "Delete a ticket" -> DELETE /issue-tracking/collections/{collection_id}/tickets/{ticket_id}
- "Show all comments on a ticket" -> GET /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments
- "Add a comment to a ticket" -> POST /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments
- "Edit an existing comment on a ticket" -> PATCH /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments/{id}
- "Delete a comment from a ticket" -> DELETE /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments/{id}
- "Who are the users in this collection?" -> GET /issue-tracking/collections/{collection_id}/users
- "Get a user's profile and email" -> GET /issue-tracking/collections/{collection_id}/users/{id}
- "What tags are available in a collection?" -> GET /issue-tracking/collections/{collection_id}/tags
- "Find all urgent tickets assigned to someone" -> GET /issue-tracking/collections/{collection_id}/tickets (use `filter` and check `priority`/`assignees` in response)

## Response Tips

- **List endpoints** (collections, tickets, comments, users, tags): All return cursor-based pagination in `meta.cursors` and `links`. Use `links.next` to page forward; `null` means last page. `meta.items_on_page` tells you how many items were returned vs the `limit` requested.
- **Single-resource endpoints** (get collection, ticket, user, comment): Data lives in `data` as a flat map. Nullable fields (marked `?`) may be absent or null -- always check before accessing nested properties like `assignees` or `tags`.
- **Write endpoints** (POST, PATCH, DELETE): Return only `data.id` on success -- not the full object. To confirm changes, follow up with a GET on the same resource.
- **All endpoints**: The envelope always includes `status_code`, `status`, `service`, `resource`, and `operation`. Use `service` to identify which downstream connector handled the request when debugging multi-service setups.
- **Error responses**: Codes 400 (bad request), 401 (auth), 402 (payment/plan limit), 404 (not found), 422 (validation). The error body follows the same envelope pattern -- check `status` and `message` fields for details.

## Anomaly Flags

- **402 Payment Required**: Surface immediately -- indicates the connected service plan does not support this operation or the account has hit a plan limit. User action required.
- **422 Unprocessable Entity on writes**: Flag the specific validation failures. Common causes: missing required `id` field on ticket creation, invalid `priority` value (must be one of `low`, `normal`, `high`, `urgent`), or malformed date-time strings.
- **Empty `assignees` or `tags` arrays**: When creating/updating tickets, warn if these are omitted -- some downstream services require at least one assignee.
- **Cursor pagination exhaustion**: If `meta.cursors.next` is null but `items_on_page` equals the `limit`, there may be exactly one more page. Flag when total results seem truncated.
- **Stale `x-apideck-service-id`**: If the user switches connected services mid-workflow, warn that collection and ticket IDs may no longer be valid across services.
- **`_raw` field present**: Only returned when `raw=True` is passed. If unexpectedly large, flag potential performance impact on response parsing.
- **401 after previously successful calls**: The API key or consumer connection may have been revoked. Prompt the user to re-check their Apideck connection settings.

## Playbook

### 1. Create and assign a new ticket

1. GET /issue-tracking/collections to find the target collection's `id`
2. GET /issue-tracking/collections/{collection_id}/users to find the assignee's `id`
3. GET /issue-tracking/collections/{collection_id}/tags to find relevant tag IDs
4. POST /issue-tracking/collections/{collection_id}/tickets with `subject`, `description`, `priority`, `assignees: [{id: "..."}]`, and `tags: [{id: "..."}]`
5. Capture the returned `data.id` as the new ticket ID
6. GET /issue-tracking/collections/{collection_id}/tickets/{ticket_id} to verify the ticket was created correctly

### 2. Triage and update ticket priority

1. GET /issue-tracking/collections/{collection_id}/tickets with `sort` to list tickets by creation date
2. For each ticket needing triage, GET /issue-tracking/collections/{collection_id}/tickets/{ticket_id} to review full details
3. PATCH /issue-tracking/collections/{collection_id}/tickets/{ticket_id} with updated `priority` (one of `low`, `normal`, `high`, `urgent`) and optionally `status`
4. POST /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments with a `body` explaining the triage decision

### 3. Review and respond to ticket comments

1. GET /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments to list all comments (paginate with `cursor` if needed)
2. GET /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments/{id} for full detail on a specific comment
3. POST /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments with `body` containing the response
4. Optionally PATCH the ticket's `status` to reflect progress (e.g., change to "in_progress" or "waiting_on_customer")

### 4. Bulk export tickets from a collection

1. GET /issue-tracking/collections/{collection_id}/tickets with `limit=20` (or max supported)
2. Collect all tickets from `data` array
3. Check `links.next` -- if not null, GET the next page using the `cursor` from `meta.cursors.next`
4. Repeat until `links.next` is null
5. For each ticket, optionally GET /issue-tracking/collections/{collection_id}/tickets/{ticket_id}/comments to include comment history

### 5. Clean up resolved tickets

1. GET /issue-tracking/collections/{collection_id}/tickets with `filter` to find tickets with `status` of "done" or "closed"
2. For each resolved ticket, GET /issue-tracking/collections/{collection_id}/tickets/{ticket_id} to confirm `completed_at` is set
3. Archive or DELETE /issue-tracking/collections/{collection_id}/tickets/{ticket_id} as appropriate
4. Confirm deletion by checking the returned `data.id` matches the deleted ticket


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
