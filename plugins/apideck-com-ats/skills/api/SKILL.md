---
name: ats-api
description: "ATS API skill. Use when working with ATS for ats. Covers 12 endpoints."
version: 1.0.0
generator: lapsh
---

# ATS API
API version: 10.24.0

## Auth
ApiKey Authorization in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /ats/jobs -- verify access
3. POST /ats/applicants -- create first applicants

## Endpoints

12 endpoints across 1 groups. See references/api-spec.lap for full details.

### ats
| Method | Path | Description |
|--------|------|-------------|
| GET | /ats/jobs | List Jobs |
| GET | /ats/jobs/{id} | Get Job |
| GET | /ats/applicants | List Applicants |
| POST | /ats/applicants | Create Applicant |
| GET | /ats/applicants/{id} | Get Applicant |
| PATCH | /ats/applicants/{id} | Update Applicant |
| DELETE | /ats/applicants/{id} | Delete Applicant |
| GET | /ats/applications | List Applications |
| POST | /ats/applications | Create Application |
| GET | /ats/applications/{id} | Get Application |
| PATCH | /ats/applications/{id} | Update Application |
| DELETE | /ats/applications/{id} | Delete Application |

## Enhanced Skill Content
## Question Mapping

- "What jobs are currently open?" -> GET /ats/jobs
- "Show me details for a specific job posting" -> GET /ats/jobs/{id}
- "List all applicants in the system" -> GET /ats/applicants
- "Find applicants with a specific filter" -> GET /ats/applicants (with filter param)
- "Get full profile for an applicant" -> GET /ats/applicants/{id}
- "Add a new candidate to the ATS" -> POST /ats/applicants
- "Update an applicant's contact information or stage" -> PATCH /ats/applicants/{id}
- "Remove an applicant from the system" -> DELETE /ats/applicants/{id}
- "List all applications across jobs" -> GET /ats/applications
- "Submit an applicant to a job" -> POST /ats/applications
- "Check the status of a specific application" -> GET /ats/applications/{id}
- "Move an application to a different stage or status" -> PATCH /ats/applications/{id}
- "Withdraw or delete an application" -> DELETE /ats/applications/{id}
- "How many applicants applied this page and is there a next page?" -> GET /ats/applicants (inspect meta.cursors and meta.items_on_page)
- "What is the salary range for a job?" -> GET /ats/jobs/{id} (inspect data.salary)

## Response Tips

- **List endpoints** (jobs, applicants, applications): Results are in `data` (array). Paginate using `meta.cursors.next` as the `cursor` param; stop when `links.next` is null. Default page size is 20.
- **Detail endpoints** (by ID): Single object in `data` (map). Many fields are nullable (`?`); always check before accessing nested properties like `department.name` or `stage.name`.
- **Write endpoints** (POST/PATCH/DELETE): Return only `data.id` on success. Use the returned ID to fetch the full record if you need confirmation of written fields.
- **Errors**: All endpoints share the same error codes -- 400 (bad request), 401 (unauthorized), 402 (payment required), 404 (not found), 422 (unprocessable entity). Parse the response body for `status` and `service` to identify which downstream connector failed.

## Anomaly Flags

- **402 Payment Required**: Surface immediately -- indicates the Apideck plan or connected service lacks access to this endpoint. User action required.
- **Cursor loop detection**: If `meta.cursors.next` returns a value already seen, flag infinite pagination to the user.
- **Empty `data` on list calls**: Distinguish between "no results matching filter" vs. misconfigured `x-apideck-service-id`. Check that headers are set correctly.
- **`deleted: true` on applicants**: Proactively warn when a fetched applicant is soft-deleted, since writes against deleted records may behave unexpectedly.
- **`confidential: true` on jobs or applicants**: Flag to the user that this record has restricted visibility and actions may be audited.
- **Missing `x-apideck-consumer-id` or `x-apideck-app-id`**: These common fields are required by Apideck's unified API layer. Surface auth misconfiguration early rather than letting it cascade to a 401.
- **`_raw` field present**: When `raw=true` is passed, responses include the upstream provider's raw payload. Flag if it contains unexpected nulls or schema drift compared to the unified response.

## Playbook

### 1. Submit a New Candidate to a Job

1. `POST /ats/applicants` with at minimum `first_name`, `last_name`, and one entry in `emails` (email is required within the map).
2. Capture the returned `data.id` (this is the applicant ID).
3. `POST /ats/applications` with `applicant_id` set to the new ID and `job_id` set to the target job.
4. Optionally set `status` to `"open"` and provide a `stage` map if the initial pipeline stage is known.
5. Confirm by calling `GET /ats/applications/{id}` with the returned application ID.

### 2. Review All Applicants for a Job

1. `GET /ats/jobs` to list jobs. Identify the target `job_id`.
2. `GET /ats/applications` and page through all results using `cursor`.
3. Filter the returned applications client-side where `job_id` matches the target.
4. For each matching application, call `GET /ats/applicants/{applicant_id}` to retrieve full candidate details.
5. Compile the results into a summary with name, email, stage, and status.

### 3. Advance an Applicant Through the Pipeline

1. `GET /ats/applications/{id}` to confirm current `status` and `stage`.
2. `PATCH /ats/applications/{id}` with updated `stage` (provide both `id` and `name` of the new stage) and keep `applicant_id` and `job_id` unchanged (they are required on PATCH).
3. Optionally update `status` to `"hired"` or `"rejected"` if this is a terminal move.
4. Verify the change with `GET /ats/applications/{id}`.

### 4. Update Applicant Contact Details

1. `GET /ats/applicants/{id}` to fetch the current record.
2. `PATCH /ats/applicants/{id}` with only the changed fields (e.g., updated `emails`, `phone_numbers`, or `addresses` arrays).
3. Include the full array for nested collections -- partial array updates are not supported; send the complete list with modifications.
4. Confirm the update with `GET /ats/applicants/{id}`.

### 5. Paginate Through Large Result Sets

1. Call the list endpoint (e.g., `GET /ats/applicants`) with `limit=20` (or desired page size).
2. Read `meta.cursors.next` from the response.
3. If `next` is not null, repeat the call with `cursor` set to that value.
4. Continue until `meta.cursors.next` is null or `links.next` is null.
5. Aggregate `data` arrays from each page into a single collection.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
