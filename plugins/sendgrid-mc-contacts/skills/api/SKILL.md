---
name: twilio-sendgrid-marketing-campaigns-contacts-api
description: "Twilio SendGrid Marketing Campaigns Contacts API skill. Use when working with Twilio SendGrid Marketing Campaigns Contacts for marketing. Covers 15 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio SendGrid Marketing Campaigns Contacts API
API version: 1.0.0

## Auth
Bearer bearer

## Base URL
https://api.sendgrid.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v3/marketing/contacts -- verify access
3. POST /v3/marketing/contacts/batch -- create first batch

## Endpoints

15 endpoints across 1 groups. See references/api-spec.lap for full details.

### marketing
| Method | Path | Description |
|--------|------|-------------|
| PUT | /v3/marketing/contacts | Add or Update a Contact |
| DELETE | /v3/marketing/contacts | Delete Contacts |
| GET | /v3/marketing/contacts | Get Sample Contacts |
| GET | /v3/marketing/contacts/{id} | Get a Contact by ID |
| POST | /v3/marketing/contacts/batch | Get Batched Contacts by IDs |
| DELETE | /v3/marketing/contacts/{contact_id}/identifiers | Delete a Contact Identifier |
| GET | /v3/marketing/contacts/count | Get Total Contact Count |
| POST | /v3/marketing/contacts/exports | Export Contacts |
| GET | /v3/marketing/contacts/exports | Get All Existing Exports |
| GET | /v3/marketing/contacts/exports/{id} | Export Contacts Status |
| PUT | /v3/marketing/contacts/imports | Import Contacts |
| GET | /v3/marketing/contacts/imports/{id} | Import Contacts Status |
| POST | /v3/marketing/contacts/search | Search Contacts |
| POST | /v3/marketing/contacts/search/emails | Get Contacts by Emails |
| POST | /v3/marketing/contacts/search/identifiers/{identifier_type} | Get Contacts by Identifiers |

## Enhanced Skill Content
## Question Mapping

- "How do I add or update contacts in SendGrid?" -> PUT /v3/marketing/contacts
- "How do I delete specific contacts by ID?" -> DELETE /v3/marketing/contacts
- "How do I delete all my contacts at once?" -> DELETE /v3/marketing/contacts
- "How do I list all my marketing contacts?" -> GET /v3/marketing/contacts
- "How do I look up a single contact by ID?" -> GET /v3/marketing/contacts/{id}
- "How do I fetch multiple contacts by their IDs in one call?" -> POST /v3/marketing/contacts/batch
- "How do I remove a specific email or phone identifier from a contact?" -> DELETE /v3/marketing/contacts/{contact_id}/identifiers
- "How many contacts do I have, and how many are billable?" -> GET /v3/marketing/contacts/count
- "How do I export my contacts to a CSV or JSON file?" -> POST /v3/marketing/contacts/exports
- "How do I check the status of a contact export job?" -> GET /v3/marketing/contacts/exports/{id}
- "How do I bulk import contacts from a file?" -> PUT /v3/marketing/contacts/imports
- "How do I check if my import job finished and see error counts?" -> GET /v3/marketing/contacts/imports/{id}
- "How do I search contacts using a SGQL query?" -> POST /v3/marketing/contacts/search
- "How do I find contacts by their email addresses?" -> POST /v3/marketing/contacts/search/emails
- "How do I look up contacts by phone number ID or external ID?" -> POST /v3/marketing/contacts/search/identifiers/{identifier_type}

## Response Tips

- **Upsert/Delete/Import operations** return `202 Accepted` with a `job_id` -- these are async; poll the corresponding status endpoint to track completion.
- **List and search responses** include `_metadata` with `self`, `prev`, and `next` URIs for cursor-based pagination; follow `next` until it is null.
- **Contact objects** nest `custom_fields` as a flat key-value map and return `list_ids`/`segment_ids` as arrays of UUIDs.
- **Export status** includes `urls` (array of download links) only when `status` is complete; `expires_at` indicates when those links stop working.
- **Import status** nests counts inside `results` (`created_count`, `updated_count`, `errored_count`) and provides `errors_url` for downloading row-level errors.
- **Batch lookup** (`POST /batch`) returns results in the same order as the input `ids` array; missing IDs are omitted, not errored.
- **Count endpoint** separates `contact_count` (total) from `billable_count` with a nested `billable_breakdown` for plan-level insight.
- **Search by email/identifier** returns a map keyed by the input value, so missing keys mean no match was found.

## Anomaly Flags

- **Job stuck in pending**: If an import or export `status` has not changed after repeated polls (>10 min), surface a warning that the job may be stalled.
- **High error rate on import**: When `errored_count` exceeds 10% of `requested_count`, proactively flag and suggest downloading the `errors_url` for diagnosis.
- **Billable count discrepancy**: If `billable_count` is significantly lower than `contact_count`, alert the user -- contacts may be missing email addresses or duplicated.
- **Export link expiration**: When `expires_at` on an export is within 1 hour, warn the user to download immediately before URLs become invalid.
- **408 on search**: The search endpoint uniquely returns `408 Request Timeout` -- flag this as a query complexity issue and suggest narrowing the SGQL query.
- **Approaching plan limits**: If `contact_count` from the count endpoint is near known plan thresholds (2K, 10K, 50K), surface a billing warning.
- **Empty identifiers after delete**: After deleting an identifier, the contact still exists but may become unreachable -- flag if the last email identifier was removed.

## Playbook

### 1. Bulk Add Contacts to a List

1. Call `GET /v3/marketing/contacts/count` to confirm current contact count and check plan headroom.
2. Call `PUT /v3/marketing/contacts` with the `contacts` array and include `list_ids` to assign them to one or more lists.
3. Capture the `job_id` from the `202` response.
4. Poll `GET /v3/marketing/contacts/imports/{job_id}` until `status` shows complete.
5. Check `results.errored_count` -- if non-zero, download and review the file at `errors_url`.

### 2. Export Contacts for External Analysis

1. Call `POST /v3/marketing/contacts/exports` with `file_type` set to `csv` or `json`. Optionally filter by `list_ids` or `segment_ids`.
2. Capture the export `id` from the `202` response.
3. Poll `GET /v3/marketing/contacts/exports/{id}` until `status` is complete.
4. Download files from the `urls` array before the `expires_at` timestamp.
5. If the export is large, check `contact_count` in the status response to confirm all records were included.

### 3. Find and Update a Contact by Email

1. Call `POST /v3/marketing/contacts/search/emails` with the target email in the `emails` array.
2. Extract the contact object from the `result` map (keyed by email address). If the key is missing, the contact does not exist.
3. Note the contact's `id` and current field values.
4. Call `PUT /v3/marketing/contacts` with the updated fields in the `contacts` array (include the `email` field to match on upsert).
5. Confirm the async job completes by checking the returned `job_id`.

### 4. Clean Up Stale Contacts

1. Call `POST /v3/marketing/contacts/search` with a SGQL query filtering by `updated_at` older than your cutoff date.
2. Collect the `id` values from all pages of results (follow `_metadata.next` for pagination).
3. Call `DELETE /v3/marketing/contacts` with the comma-separated `ids` string (max batch per API limits).
4. Capture the `job_id` and poll until deletion completes.
5. Call `GET /v3/marketing/contacts/count` to verify the updated totals.

### 5. Migrate a Contact's Identifier

1. Call `GET /v3/marketing/contacts/{id}` to review the contact's current identifiers (email, phone_number_id, external_id).
2. Call `PUT /v3/marketing/contacts` with the new identifier value in the contacts array, matching on the existing `email`.
3. Wait for the upsert `job_id` to complete.
4. Call `DELETE /v3/marketing/contacts/{contact_id}/identifiers` with `identifier_type` and `identifier_value` set to the old identifier.
5. Verify by calling `GET /v3/marketing/contacts/{id}` to confirm the old identifier is removed and the new one is present.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
