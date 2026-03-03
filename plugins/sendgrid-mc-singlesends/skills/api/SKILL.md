---
name: twilio-sendgrid-marketing-campaigns-single-sends-api
description: "Twilio SendGrid Marketing Campaigns Single Sends API skill. Use when working with Twilio SendGrid Marketing Campaigns Single Sends for marketing. Covers 11 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio SendGrid Marketing Campaigns Single Sends API
API version: 1.0.0

## Auth
Bearer bearer

## Base URL
https://api.sendgrid.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v3/marketing/singlesends -- verify access
3. POST /v3/marketing/singlesends -- create first singlesends

## Endpoints

11 endpoints across 1 groups. See references/api-spec.lap for full details.

### marketing
| Method | Path | Description |
|--------|------|-------------|
| POST | /v3/marketing/singlesends | Create Single Send |
| GET | /v3/marketing/singlesends | Get All Single Sends |
| DELETE | /v3/marketing/singlesends | Bulk Delete Single Sends |
| POST | /v3/marketing/singlesends/{id} | Duplicate Single Send |
| PATCH | /v3/marketing/singlesends/{id} | Update Single Send |
| GET | /v3/marketing/singlesends/{id} | Get Single Send by ID |
| DELETE | /v3/marketing/singlesends/{id} | Delete Single Send by ID |
| PUT | /v3/marketing/singlesends/{id}/schedule | Schedule Single Send |
| DELETE | /v3/marketing/singlesends/{id}/schedule | Delete Single Send Schedule |
| GET | /v3/marketing/singlesends/categories | Get All Categories |
| POST | /v3/marketing/singlesends/search | Get Single Sends Search |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new single send email campaign?" -> POST /v3/marketing/singlesends
- "Show me all my single send campaigns" -> GET /v3/marketing/singlesends
- "Get details for a specific single send" -> GET /v3/marketing/singlesends/{id}
- "How do I update an existing single send?" -> PATCH /v3/marketing/singlesends/{id}
- "How do I duplicate or copy a single send?" -> POST /v3/marketing/singlesends/{id}
- "Delete a single send campaign" -> DELETE /v3/marketing/singlesends/{id}
- "Delete multiple single sends at once" -> DELETE /v3/marketing/singlesends
- "Schedule a single send for a specific date and time" -> PUT /v3/marketing/singlesends/{id}/schedule
- "Cancel a scheduled single send" -> DELETE /v3/marketing/singlesends/{id}/schedule
- "What categories are available for single sends?" -> GET /v3/marketing/singlesends/categories
- "Search for single sends by name or status" -> POST /v3/marketing/singlesends/search
- "Find all draft single sends" -> POST /v3/marketing/singlesends/search (with `status: ["draft"]`)
- "How do I send a campaign to a specific contact list?" -> POST /v3/marketing/singlesends (set `send_to.list_ids`)
- "How do I send to a segment instead of a list?" -> POST /v3/marketing/singlesends (set `send_to.segment_ids`)
- "How do I send to all contacts?" -> POST /v3/marketing/singlesends (set `send_to.all: true`)

## Response Tips

- **List/Search endpoints** (`GET /singlesends`, `POST /search`): Results are in `result` array; paginate using `_metadata.next` as `page_token`. `_metadata.count` gives total items.
- **Create/Update endpoints** (`POST`, `PATCH`): Return the full single send object. Check `warnings` array for non-fatal issues (e.g., missing plain content). `status` field reflects lifecycle state (draft, scheduled, triggered).
- **Schedule endpoints** (`PUT/DELETE .../schedule`): Return only `send_at` and `status` -- not the full object. After unscheduling, status reverts so the send can be re-edited.
- **Delete endpoints** (`DELETE`): Return 204 with no body on success. Bulk delete accepts `ids` as query param array.
- **Error responses**: 400 indicates validation failures (check response body for field-level errors). 404 means the single send ID does not exist or was already deleted. 500 is a server-side issue -- retry with backoff.

## Anomaly Flags

- **`warnings` array is non-empty**: Surface any warnings returned on create/update -- these often indicate missing plain content, invalid sender configuration, or suppression group issues that will block sending.
- **`send_at` in the past**: Flag if a create or schedule request sets `send_at` to a datetime that has already passed -- the API may reject or immediately trigger the send.
- **`send_to` missing or empty**: Alert if a single send has no lists, segments, or `all` flag set -- it cannot be sent without recipients.
- **`status` unexpected transitions**: Flag if a single send shows `triggered` status when the user expected `scheduled`, or vice versa.
- **Bulk delete with no `ids`**: Warn before calling `DELETE /singlesends` without specifying IDs -- behavior may be unexpected.
- **500 errors on any endpoint**: These indicate SendGrid server issues. Surface immediately and suggest retrying after a short delay.
- **Pagination exhaustion**: If `_metadata.next` is null/absent, all results have been fetched. Flag if the agent is looping unnecessarily.

## Playbook

### 1. Create and Schedule a Single Send Campaign

1. Call `POST /v3/marketing/singlesends` with `name`, `email_config` (subject, html_content, sender_id), and `send_to` (list_ids or segment_ids).
2. Check the response for `warnings` -- resolve any issues (e.g., missing suppression group).
3. Note the returned `id`.
4. Call `PUT /v3/marketing/singlesends/{id}/schedule` with the desired `send_at` datetime (ISO 8601, future).
5. Confirm the response shows `status: "scheduled"`.

### 2. Search, Review, and Update Campaigns

1. Call `POST /v3/marketing/singlesends/search` with filters (e.g., `status: ["draft"]`, `name: "newsletter"`).
2. Page through results using `_metadata.next` as `page_token` if `count` exceeds `page_size`.
3. Pick a single send and call `GET /v3/marketing/singlesends/{id}` to review full details.
4. Call `PATCH /v3/marketing/singlesends/{id}` with updated fields (e.g., new subject line or html_content).
5. Verify `updated_at` has changed and check `warnings`.

### 3. Cancel and Reschedule a Scheduled Send

1. Call `GET /v3/marketing/singlesends/{id}` to confirm current `status` is `"scheduled"` and note the current `send_at`.
2. Call `DELETE /v3/marketing/singlesends/{id}/schedule` to unschedule. Confirm status is no longer `"scheduled"`.
3. Optionally update the send with `PATCH /v3/marketing/singlesends/{id}` if content changes are needed.
4. Call `PUT /v3/marketing/singlesends/{id}/schedule` with the new `send_at` datetime.
5. Confirm the response shows the new schedule and `status: "scheduled"`.

### 4. Duplicate a Campaign and Send to a Different Audience

1. Call `POST /v3/marketing/singlesends/{id}` to duplicate an existing send. Optionally pass a new `name`.
2. Note the new `id` in the response.
3. Call `PATCH /v3/marketing/singlesends/{new_id}` to update `send_to` with different `list_ids` or `segment_ids`.
4. Adjust `email_config` fields if needed (e.g., different subject line for A/B variant).
5. Schedule with `PUT /v3/marketing/singlesends/{new_id}/schedule`.

### 5. Clean Up Old Campaigns in Bulk

1. Call `POST /v3/marketing/singlesends/search` with `status: ["triggered"]` to find completed sends.
2. Collect the `id` values of campaigns to delete.
3. Call `DELETE /v3/marketing/singlesends` with the `ids` array to bulk-remove them.
4. Confirm 204 response. If any return 404, they were already deleted.
5. Verify cleanup by calling `GET /v3/marketing/singlesends` to check remaining campaigns.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
