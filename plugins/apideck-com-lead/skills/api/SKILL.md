---
name: lead-api
description: "Lead API skill. Use when working with Lead for lead. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Lead API
API version: 10.24.0

## Auth
ApiKey Authorization in header | ApiKey x-apideck-app-id in header | ApiKey x-apideck-consumer-id in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /lead/leads -- verify access
3. POST /lead/leads -- create first leads

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### lead
| Method | Path | Description |
|--------|------|-------------|
| GET | /lead/leads | List leads |
| POST | /lead/leads | Create lead |
| GET | /lead/leads/{id} | Get lead |
| PATCH | /lead/leads/{id} | Update lead |
| DELETE | /lead/leads/{id} | Delete lead |

## Enhanced Skill Content
## Question Mapping

- "Show me all my leads" -> GET /lead/leads
- "How many leads do I have?" -> GET /lead/leads (check `meta.items_on_page` and paginate)
- "Find a specific lead by ID" -> GET /lead/leads/{id}
- "Create a new lead with a name and company" -> POST /lead/leads
- "Update a lead's status or monetary amount" -> PATCH /lead/leads/{id}
- "Delete a lead I no longer need" -> DELETE /lead/leads/{id}
- "Get the next page of leads" -> GET /lead/leads (pass `cursor` from previous `meta.cursors.next`)
- "List leads sorted by a specific field" -> GET /lead/leads (use `sort` parameter)
- "Filter leads by status or owner" -> GET /lead/leads (use `filter` parameter)
- "Add contact details like phone and email to an existing lead" -> PATCH /lead/leads/{id} (include `phone_numbers` and `emails` arrays)
- "Create a lead with a full mailing address" -> POST /lead/leads (include `addresses` array)
- "What service is connected for leads?" -> GET /lead/leads (check `service` field in response)
- "Get only specific fields for a lead" -> GET /lead/leads/{id} (use `fields` parameter)
- "Get the raw downstream response from the connector" -> GET /lead/leads/{id} (set `raw=true`, check `_raw`)

## Response Tips

- **List endpoint (GET /lead/leads):** Data lives in `data[]`. Paginate via `meta.cursors.next` passed as `cursor` on the next request. `links.next` gives the full URL. `items_on_page` tells you how many came back (default limit is 20).
- **Single lead (GET /lead/leads/{id}):** Data is in `data` (single object, not array). Many fields are nullable -- always null-check `company_name`, `owner_id`, `monetary_amount`, `emails`, etc.
- **Create/Update/Delete (POST, PATCH, DELETE):** Response `data` only contains `{id}` -- you must follow up with a GET to confirm full state. Success codes: 201 for create, 200 for update/delete.
- **Errors:** 400 = bad request (malformed body), 401 = missing/invalid auth headers, 402 = payment required (plan limit), 404 = lead not found, 422 = validation failure (check response body for field-level errors).

## Anomaly Flags

- **402 Payment Required:** Surface immediately -- indicates the user's Apideck plan has hit a limit. No retry will help; requires plan upgrade.
- **Repeated 401 errors:** Likely misconfigured headers. Verify all three auth headers (`Authorization`, `x-apideck-app-id`, `x-apideck-consumer-id`) are present and correct.
- **Empty `data[]` with 200 status:** Not an error, but surface when the user expects results -- suggest checking filters or confirming the connected service has data.
- **`_raw` field present unexpectedly:** Only appears when `raw=true`. If it shows up without being requested, flag as unusual connector behavior.
- **Null `cursors.next` on a full page:** When `items_on_page` equals the limit but `cursors.next` is null, pagination has ended -- surface this to avoid infinite loops.
- **422 on PATCH with valid-looking data:** Often means `row_version` conflict or connector-specific validation. Surface the full error body for diagnosis.
- **`service` field changes between calls:** Indicates the Apideck Vault routing switched connectors mid-session. Flag this -- it can cause inconsistent data.

## Playbook

### 1. Import a Batch of Leads

1. Prepare lead data with at minimum a `name` for each entry.
2. For each lead, call POST /lead/leads with `name` and any additional fields (`company_name`, `emails`, `phone_numbers`, `addresses`).
3. Capture the returned `id` from each 201 response.
4. After all creates, call GET /lead/leads to verify the count matches expectations.
5. If any call returns 422, log the failed record and its error body, then retry with corrected data.

### 2. Paginate Through All Leads

1. Call GET /lead/leads with desired `limit` (max varies by connector, default 20).
2. Read `data[]` for the current page of leads.
3. Check `meta.cursors.next` -- if non-null, call GET /lead/leads with `cursor` set to that value.
4. Repeat until `meta.cursors.next` is null.
5. Accumulate results client-side or process each page as a stream.

### 3. Update a Lead's Contact Information

1. Call GET /lead/leads/{id} to fetch the current lead and confirm it exists.
2. Review existing `phone_numbers`, `emails`, and `addresses` arrays.
3. Call PATCH /lead/leads/{id} with the updated arrays (include existing entries you want to keep, omit ones to remove).
4. Confirm the response returns 200 with the lead's `id`.
5. Optionally call GET /lead/leads/{id} again to verify the changes persisted.

### 4. Clean Up Stale Leads

1. Call GET /lead/leads with a `filter` to narrow by status (e.g., lost or inactive leads).
2. Paginate through all matching results using the cursor pattern.
3. For each lead to remove, call DELETE /lead/leads/{id}.
4. Confirm each delete returns 200 with the lead's `id`.
5. After cleanup, call GET /lead/leads to verify the remaining count is correct.

### 5. Connect via a Specific Service Integration

1. Set the `x-apideck-service-id` header to the target connector (e.g., `salesforce`, `hubspot`).
2. Call GET /lead/leads to confirm data flows from the correct service -- check the `service` field in the response.
3. Proceed with create, update, or delete operations using the same `x-apideck-service-id` header on every call.
4. If the service returns unexpected errors, try without `x-apideck-service-id` to let Apideck auto-select and compare behavior.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
