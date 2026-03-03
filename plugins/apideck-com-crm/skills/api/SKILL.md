---
name: crm-api
description: "CRM API skill. Use when working with CRM for crm. Covers 50 endpoints."
version: 1.0.0
generator: lapsh
---

# CRM API
API version: 10.24.0

## Auth
ApiKey Authorization in header | ApiKey x-apideck-app-id in header | ApiKey x-apideck-consumer-id in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /crm/companies -- verify access
3. POST /crm/companies -- create first companies

## Endpoints

50 endpoints across 1 groups. See references/api-spec.lap for full details.

### crm
| Method | Path | Description |
|--------|------|-------------|
| GET | /crm/companies | List companies |
| POST | /crm/companies | Create company |
| GET | /crm/companies/{id} | Get company |
| PATCH | /crm/companies/{id} | Update company |
| DELETE | /crm/companies/{id} | Delete company |
| GET | /crm/contacts | List contacts |
| POST | /crm/contacts | Create contact |
| GET | /crm/contacts/{id} | Get contact |
| PATCH | /crm/contacts/{id} | Update contact |
| DELETE | /crm/contacts/{id} | Delete contact |
| GET | /crm/opportunities | List opportunities |
| POST | /crm/opportunities | Create opportunity |
| GET | /crm/opportunities/{id} | Get opportunity |
| PATCH | /crm/opportunities/{id} | Update opportunity |
| DELETE | /crm/opportunities/{id} | Delete opportunity |
| GET | /crm/leads | List leads |
| POST | /crm/leads | Create lead |
| GET | /crm/leads/{id} | Get lead |
| PATCH | /crm/leads/{id} | Update lead |
| DELETE | /crm/leads/{id} | Delete lead |
| GET | /crm/pipelines | List pipelines |
| POST | /crm/pipelines | Create pipeline |
| GET | /crm/pipelines/{id} | Get pipeline |
| PATCH | /crm/pipelines/{id} | Update pipeline |
| DELETE | /crm/pipelines/{id} | Delete pipeline |
| GET | /crm/notes | List notes |
| POST | /crm/notes | Create note |
| GET | /crm/notes/{id} | Get note |
| PATCH | /crm/notes/{id} | Update note |
| DELETE | /crm/notes/{id} | Delete note |
| GET | /crm/users | List users |
| POST | /crm/users | Create user |
| GET | /crm/users/{id} | Get user |
| PATCH | /crm/users/{id} | Update user |
| DELETE | /crm/users/{id} | Delete user |
| GET | /crm/activities | List activities |
| POST | /crm/activities | Create activity |
| GET | /crm/activities/{id} | Get activity |
| PATCH | /crm/activities/{id} | Update activity |
| DELETE | /crm/activities/{id} | Delete activity |
| GET | /crm/custom-object-schemas | List custom object schemas |
| POST | /crm/custom-object-schemas | Create custom object schema |
| GET | /crm/custom-object-schemas/{id} | Get custom object schema |
| PATCH | /crm/custom-object-schemas/{id} | Update custom object schema |
| DELETE | /crm/custom-object-schemas/{id} | Delete custom object schema |
| GET | /crm/custom-objects/{object_id} | List custom objects |
| POST | /crm/custom-objects/{object_id} | Create custom object |
| GET | /crm/custom-objects/{object_id}/{id} | Get custom object |
| PATCH | /crm/custom-objects/{object_id}/{id} | Update custom object |
| DELETE | /crm/custom-objects/{object_id}/{id} | Delete custom object |

## Enhanced Skill Content
## Question Mapping

- "Show me all companies in the CRM?" -> GET /crm/companies
- "Create a new company called Acme Corp?" -> POST /crm/companies
- "What are the details for company {id}?" -> GET /crm/companies/{id}
- "Update the name or industry of a company?" -> PATCH /crm/companies/{id}
- "Delete a company from the CRM?" -> DELETE /crm/companies/{id}
- "List all contacts, filtered by status?" -> GET /crm/contacts
- "Add a new contact and link them to a company?" -> POST /crm/contacts
- "What opportunities are in the pipeline right now?" -> GET /crm/opportunities
- "Create a deal worth $50k in USD?" -> POST /crm/opportunities
- "Move an opportunity to a different pipeline stage?" -> PATCH /crm/opportunities/{id}
- "Show me all leads and their sources?" -> GET /crm/leads
- "Log a call activity for a contact?" -> POST /crm/activities
- "What notes are attached to this opportunity?" -> GET /crm/notes
- "List all sales pipelines and their stages?" -> GET /crm/pipelines
- "Define a custom object schema with specific fields?" -> POST /crm/custom-object-schemas

## Response Tips

- **List endpoints** (companies, contacts, leads, opportunities, activities, notes, users, pipelines): Paginated via cursor. Next page token is at `meta.cursors.next`; follow `links.next` URL. Default page size is 20, adjustable via `limit`.
- **Single-resource endpoints** (GET by id): Data lives under `data` key. Most fields are nullable (marked `?`). Always check for `null` before accessing nested objects like `addresses`, `phone_numbers`, `emails`.
- **Create endpoints** (POST): Return only `data.id` of the newly created resource with status 201. Fetch the full record with a follow-up GET if you need the complete object.
- **Update/Delete endpoints** (PATCH/DELETE): Return only `data.id` confirming which record was affected. Status 200 on success.
- **Error responses**: All endpoints share error codes 400 (bad request), 401 (unauthorized), 402 (payment required -- likely plan limits), 404 (not found), 422 (validation failure). Parse the response body for `message` details.
- **Raw responses**: Pass `raw=true` as a query param to get the upstream connector's raw response in the `_raw` field.

## Anomaly Flags

- **402 Payment Required**: The downstream CRM connector may enforce plan limits. Surface this immediately -- it means the user's subscription tier does not support this operation.
- **Deleted records appearing in lists**: Watch for `deleted: true` on companies, opportunities, and activities. Flag soft-deleted records so the user does not act on stale data.
- **Null cursors**: If `meta.cursors.next` is `null` but `items_on_page` equals the limit, warn the user -- pagination may have silently ended or the connector may not support it.
- **Missing required fields on PATCH**: PATCH for companies, leads, opportunities, and pipelines re-requires `name`/`title`. Flag if the user tries to update without including it.
- **Currency set to UNKNOWN_CURRENCY**: Surface when any monetary record (company, opportunity, lead) has this value -- it likely indicates missing configuration.
- **Empty `emails` array on user creation/update**: `emails` is required for users. Flag if the array is empty or missing the required `email` field inside each entry.
- **`pass_through` usage**: When the user sends `pass_through` data, warn that it bypasses Apideck's unified model and goes directly to the downstream connector -- behavior is connector-specific and may break portability.

## Playbook

### 1. Full lead-to-deal conversion

1. Create or retrieve the lead: POST /crm/leads with `name`, `company_name`, `emails`, `phone_numbers`
2. Create a contact from the lead data: POST /crm/contacts with `first_name`, `last_name`, `company_name`, `lead_id` set to the lead's id
3. Create a company if one does not exist: POST /crm/companies with `name`
4. Link the contact to the company: PATCH /crm/contacts/{id} setting `company_id`
5. Create the opportunity: POST /crm/opportunities with `title`, `contact_id`, `company_id`, `monetary_amount`, `currency`, `pipeline_id`, `pipeline_stage_id`
6. Delete or update the lead status: PATCH /crm/leads/{id} setting `status` to "converted", or DELETE /crm/leads/{id}

### 2. Pipeline setup with stages

1. List existing pipelines: GET /crm/pipelines to check what already exists
2. Create a new pipeline: POST /crm/pipelines with `name`, `currency`, `win_probability_enabled: true`, and `stages` array containing objects with `name`, `win_probability`, and `display_order`
3. Verify creation: GET /crm/pipelines/{id} to confirm stages were saved correctly
4. Assign opportunities: PATCH /crm/opportunities/{id} setting `pipeline_id` and `pipeline_stage_id` for each deal

### 3. Logging a meeting with attendees

1. Identify the contact: GET /crm/contacts with filter, or GET /crm/contacts/{id}
2. Create the activity: POST /crm/activities with `type: "meeting"`, `title`, `start_datetime`, `end_datetime`, `contact_id`, `company_id`, and `attendees` array (each with `email_address`, `name`, `status`)
3. Add a follow-up note: POST /crm/notes with `title`, `content`, `contact_id`, `activity_id` set to the meeting's id

### 4. Bulk export all contacts with pagination

1. Fetch the first page: GET /crm/contacts with `limit=20`
2. Check `meta.cursors.next` in the response
3. If non-null, fetch the next page: GET /crm/contacts with `cursor` set to the next cursor value
4. Repeat until `meta.cursors.next` is `null`
5. Optionally use the `fields` parameter to limit returned fields and reduce payload size

### 5. Custom object workflow

1. Define the schema: POST /crm/custom-object-schemas with `name`, `description`, and `fields` array (each with `name`, `type`, `required`)
2. Verify schema: GET /crm/custom-object-schemas/{id} to confirm field definitions
3. Create records: POST /crm/custom-objects/{object_id} with `name` and `fields` array (each with `name`, `value`)
4. List records: GET /crm/custom-objects/{object_id} with pagination via `cursor`
5. Update a record: PATCH /crm/custom-objects/{object_id}/{id} with modified `fields`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
