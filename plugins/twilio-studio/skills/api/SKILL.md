---
name: twilio-studio
description: "Twilio - Studio API skill. Use when working with Twilio - Studio for Flows. Covers 19 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio - Studio
API version: 1.0.0

## Auth
Bearer basic

## Base URL
https://studio.twilio.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v2/Flows -- verify access
3. POST /v2/Flows/{FlowSid}/Executions -- create first Executions

## Endpoints

19 endpoints across 1 groups. See references/api-spec.lap for full details.

### Flows
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/Flows/{FlowSid}/Executions | Retrieve a list of all Executions for the Flow. |
| POST | /v2/Flows/{FlowSid}/Executions | Triggers a new Execution for the Flow |
| GET | /v2/Flows/{FlowSid}/Executions/{Sid} | Retrieve an Execution |
| DELETE | /v2/Flows/{FlowSid}/Executions/{Sid} | Delete the Execution and all Steps relating to it. |
| POST | /v2/Flows/{FlowSid}/Executions/{Sid} | Update the status of an Execution to `ended`. |
| GET | /v2/Flows/{FlowSid}/Executions/{ExecutionSid}/Context | Retrieve the most recent context for an Execution. |
| GET | /v2/Flows/{FlowSid}/Executions/{ExecutionSid}/Steps | Retrieve a list of all Steps for an Execution. |
| GET | /v2/Flows/{FlowSid}/Executions/{ExecutionSid}/Steps/{Sid} | Retrieve a Step. |
| GET | /v2/Flows/{FlowSid}/Executions/{ExecutionSid}/Steps/{StepSid}/Context | Retrieve the context for an Execution Step. |
| POST | /v2/Flows | Create a Flow. |
| GET | /v2/Flows | Retrieve a list of all Flows. |
| POST | /v2/Flows/{Sid} | Update a Flow. |
| GET | /v2/Flows/{Sid} | Retrieve a specific Flow. |
| DELETE | /v2/Flows/{Sid} | Delete a specific Flow. |
| GET | /v2/Flows/{Sid}/Revisions | Retrieve a list of all Flows revisions. |
| GET | /v2/Flows/{Sid}/Revisions/{Revision} | Retrieve a specific Flow revision. |
| POST | /v2/Flows/Validate | Validate flow JSON definition |
| GET | /v2/Flows/{Sid}/TestUsers | Fetch flow test users |
| POST | /v2/Flows/{Sid}/TestUsers | Update flow test users |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my Studio flows?" -> GET /v2/Flows
- "How do I create a new Studio flow?" -> POST /v2/Flows
- "How do I get details about a specific flow?" -> GET /v2/Flows/{Sid}
- "How do I update an existing flow's definition?" -> POST /v2/Flows/{Sid}
- "How do I delete a flow?" -> DELETE /v2/Flows/{Sid}
- "How do I validate a flow definition before publishing?" -> POST /v2/Flows/Validate
- "How do I see the revision history of a flow?" -> GET /v2/Flows/{Sid}/Revisions
- "How do I trigger a flow execution for a phone number?" -> POST /v2/Flows/{FlowSid}/Executions
- "How do I list all executions of a flow within a date range?" -> GET /v2/Flows/{FlowSid}/Executions
- "How do I check the current status of a flow execution?" -> GET /v2/Flows/{FlowSid}/Executions/{Sid}
- "How do I stop a running execution?" -> POST /v2/Flows/{FlowSid}/Executions/{Sid}
- "How do I see what data a flow execution collected?" -> GET /v2/Flows/{FlowSid}/Executions/{ExecutionSid}/Context
- "How do I trace the steps an execution went through?" -> GET /v2/Flows/{FlowSid}/Executions/{ExecutionSid}/Steps
- "How do I see the context/variables at a specific step?" -> GET /v2/Flows/{FlowSid}/Executions/{ExecutionSid}/Steps/{StepSid}/Context
- "How do I manage test users for a flow?" -> GET /v2/Flows/{Sid}/TestUsers + POST /v2/Flows/{Sid}/TestUsers

## Response Tips

- **Flows, Executions, Steps, Revisions (list endpoints):** Paginated via `meta` object -- check `meta.next_page_url` (null when on last page). Use `PageSize` (max varies) and `PageToken` for cursor-based paging; `Page` for offset-based.
- **Flow detail/create/update:** Check `valid` (bool) and inspect `errors`/`warnings` arrays before assuming success -- a 200/201 does NOT guarantee the definition is error-free.
- **Execution responses:** The `status` field indicates state (`active`, `ended`, `failed`). The `context` field is freeform (`any`) and holds flow variables set during execution.
- **Step detail:** `transitioned_from` and `transitioned_to` reveal the execution path. `parent_step_sid` is set for nested/sub-flow steps.
- **DELETE endpoints:** Return 204 with no body -- success means empty response.
- **Validate:** Returns only `{valid: bool?}` with no detail on failures; use flow create/update responses for full error diagnostics.

## Anomaly Flags

- **Invalid flow published:** Surface immediately if `valid` is `false` or `errors` array is non-empty after a create/update -- the flow may not execute correctly.
- **Warnings present:** Alert when `warnings` array is populated on flow responses, even if `valid` is `true`.
- **Execution stuck in active:** Flag executions where `status` remains `active` and `date_created` is significantly in the past.
- **Pagination truncation risk:** Warn when `meta.next_page_url` is present but the caller is not paginating -- results are incomplete.
- **Empty context:** Surface when an execution or step context returns `null`/empty, which may indicate the flow ended prematurely or data was not captured.
- **High execution failure rate:** If multiple executions for the same flow show `status: failed`, proactively suggest reviewing flow definition and recent revisions.

## Playbook

### 1. Create and Validate a New Flow

1. Call POST /v2/Flows/Validate with your flow definition to check syntax.
2. If `valid` is `true`, call POST /v2/Flows with the same definition, a `friendly_name`, and `status` set to `draft`.
3. Inspect the response for `errors` and `warnings` arrays.
4. If clean, update the flow via POST /v2/Flows/{Sid} with `status` set to `published`.
5. Optionally add test users via POST /v2/Flows/{Sid}/TestUsers before publishing to production.

### 2. Debug a Failed Execution

1. List recent executions: GET /v2/Flows/{FlowSid}/Executions with `DateCreatedFrom`/`DateCreatedTo` to narrow the window.
2. Identify the failed execution (`status: failed`) and note its `Sid`.
3. Fetch execution context: GET /v2/Flows/{FlowSid}/Executions/{Sid}/Context to see final variable state.
4. List all steps: GET /v2/Flows/{FlowSid}/Executions/{Sid}/Steps.
5. For the last step before failure, fetch step context: GET /v2/Flows/{FlowSid}/Executions/{ExecutionSid}/Steps/{StepSid}/Context.
6. Compare `transitioned_from`/`transitioned_to` to identify where the flow diverged from the expected path.

### 3. Roll Back a Flow to a Previous Revision

1. List revisions: GET /v2/Flows/{Sid}/Revisions, paginating if needed.
2. Fetch the target revision: GET /v2/Flows/{Sid}/Revisions/{Revision} and capture the `definition` field.
3. Update the flow: POST /v2/Flows/{Sid} with the old `definition` and a descriptive `commit_message` (e.g., "Rollback to revision N").
4. Verify the response has `valid: true` and no `errors`.

### 4. Bulk Cleanup of Old Executions

1. List executions: GET /v2/Flows/{FlowSid}/Executions with `DateCreatedTo` set to your cutoff date.
2. Page through all results using `meta.next_page_url`.
3. For each execution with `status: ended`, call DELETE /v2/Flows/{FlowSid}/Executions/{Sid}.
4. Skip any execution still in `active` status to avoid terminating in-progress work.

### 5. Set Up a Flow for Testing Before Go-Live

1. Create the flow as `draft`: POST /v2/Flows with `status: draft`.
2. Add test users: POST /v2/Flows/{Sid}/TestUsers with a list of phone numbers.
3. Trigger a test execution: POST /v2/Flows/{FlowSid}/Executions with a test user's `contact_channel_address`.
4. Monitor execution: GET /v2/Flows/{FlowSid}/Executions/{Sid} until `status` is `ended`.
5. Review step-by-step trace: GET /v2/Flows/{FlowSid}/Executions/{Sid}/Steps to confirm the expected path.
6. When satisfied, publish: POST /v2/Flows/{Sid} with `status: published`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
