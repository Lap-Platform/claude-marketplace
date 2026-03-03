---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 18 endpoints."
version: 1.0.0
generator: lapsh
---

# AutomationManagement
API version: 2018-06-30

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/content -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/publish -- create first publish

## Endpoints

18 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/content | Retrieve the content of runbook draft identified by runbook name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/content | Replaces the runbook draft content. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft | Retrieve the runbook draft identified by runbook name. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/publish | Publish runbook draft. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/undoEdit | Undo draft edit to last known published state identified by runbook name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/content | Retrieve the content of runbook identified by runbook name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName} | Retrieve the runbook identified by runbook name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName} | Create the runbook identified by runbook name. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName} | Update the runbook identified by runbook name. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName} | Delete the runbook by name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks | Retrieve a list of runbooks. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/testJob/streams/{jobStreamId} | Retrieve a test job stream of the test job identified by runbook name and stream id. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/testJob/streams | Retrieve a list of test job streams identified by runbook name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/testJob | Create a test job of the runbook. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/testJob | Retrieve the test job for the specified runbook. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/testJob/resume | Resume the test job. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/testJob/stop | Stop the test job. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/testJob/suspend | Suspend the test job. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all runbooks in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks
- "What is the content of a published runbook?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/content
- "How do I read the draft version of a runbook?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/content
- "How do I update a runbook's draft content?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/content
- "How do I create a new runbook?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}
- "How do I publish a draft runbook to production?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/publish
- "How do I discard draft changes and revert?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/undoEdit
- "How do I run a test job against a draft runbook?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/testJob
- "How do I check the status of a test job?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/testJob
- "How do I view output streams from a test job?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/testJob/streams
- "How do I stop a running test job?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/testJob/stop
- "How do I delete a runbook I no longer need?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}
- "How do I update runbook properties without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}
- "How do I get metadata for a specific runbook?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}
- "How do I resume a suspended test job?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/runbooks/{runbookName}/draft/testJob/resume

## Response Tips

- **Runbook listing** (GET .../runbooks): Returns a paged array with `value` and `nextLink`; follow `nextLink` until null to retrieve all results.
- **Runbook CRUD** (GET/PUT/PATCH/DELETE .../runbooks/{name}): Returns the full runbook resource object with `properties`, `id`, `name`, `type`, and `location`; 201 on create, 200 on update, 204 on delete-already-gone.
- **Draft content** (GET/PUT .../draft/content): Returns raw runbook script text (not JSON); PUT returns 202 when accepted for async processing.
- **Publish** (POST .../publish): Returns 202 Accepted with a `Location` header for polling the long-running operation; no response body.
- **Test jobs** (PUT/GET .../draft/testJob): PUT returns 201 with job metadata including `status`, `creationTime`, and `parameters`; poll GET until `status` reaches a terminal state (Completed, Failed, Stopped).
- **Test job streams** (GET .../testJob/streams): Returns an array of stream records; use `$filter` to narrow by stream type (e.g., `Output`, `Error`); individual stream content requires the `{jobStreamId}` sub-resource.
- **Errors**: All endpoints return `ErrorResponse` with `code` and `message` on 4xx/5xx; watch for `ResourceNotFound` (404), `OperationNotAllowed` (409 on publish conflicts), and `AuthorizationFailed` (403).

## Anomaly Flags

- **202 without polling**: If `publish` or `draft/content PUT` returns 202, surface the `Location` header and remind the user to poll for completion -- the operation is not yet done.
- **204 on delete**: A 204 means the runbook was already absent; flag this as a no-op so the user does not assume a deletion occurred.
- **Test job stuck in non-terminal state**: If a test job GET returns `Running` or `Suspended` for an extended period, proactively suggest using the stop or resume endpoints.
- **Missing draft**: If GET .../draft returns 404 while the published runbook exists, flag that the runbook has no pending draft -- edits must go through draft/content PUT first.
- **$filter ignored**: If test job streams return unfiltered results despite a `$filter` parameter, warn that the filter syntax may be malformed (OData format required).
- **OAuth2 token expiry**: Surface token refresh reminders when requests start returning 401, since Azure tokens expire after ~60 minutes.
- **API version mismatch**: This spec targets `2018-06-30`; flag if a newer api-version is available or if responses contain `deprecated` annotations.

## Playbook

### 1. Edit and Publish a Runbook Draft

1. Retrieve the current draft content: GET `.../runbooks/{runbookName}/draft/content`
2. Modify the script locally as needed.
3. Upload the updated draft: PUT `.../runbooks/{runbookName}/draft/content` with the new script body.
4. If PUT returns 202, poll the `Location` URL until the operation completes.
5. Publish the draft to production: POST `.../runbooks/{runbookName}/publish`.
6. Poll the `Location` header from the 202 response until the publish operation finishes.
7. Verify the published content: GET `.../runbooks/{runbookName}/content`.

### 2. Test a Draft Runbook Before Publishing

1. Upload or confirm draft content: PUT `.../runbooks/{runbookName}/draft/content`.
2. Create a test job: PUT `.../runbooks/{runbookName}/draft/testJob` with required parameters.
3. Poll test job status: GET `.../runbooks/{runbookName}/draft/testJob` until `status` is terminal (Completed, Failed, Stopped).
4. Retrieve output streams: GET `.../runbooks/{runbookName}/draft/testJob/streams` (optionally filter with `$filter=properties/streamType eq 'Output'`).
5. Inspect individual stream details: GET `.../runbooks/{runbookName}/draft/testJob/streams/{jobStreamId}`.
6. If the test passes, publish: POST `.../runbooks/{runbookName}/publish`.
7. If the test fails, fix the draft (step 1) and re-run.

### 3. Create a New Runbook from Scratch

1. Create the runbook resource: PUT `.../runbooks/{runbookName}` with `parameters` including `runbookType` (e.g., PowerShell, Python2, Graph), `location`, and `properties`.
2. Confirm creation via the 201 response and inspect the returned resource object.
3. Upload draft content: PUT `.../runbooks/{runbookName}/draft/content` with the script body.
4. Test the draft (see Playbook 2).
5. Publish when ready: POST `.../runbooks/{runbookName}/publish`.

### 4. Roll Back a Draft Edit

1. Check the current draft: GET `.../runbooks/{runbookName}/draft` to review pending changes.
2. If the draft should be discarded, undo the edit: POST `.../runbooks/{runbookName}/draft/undoEdit`.
3. Verify the draft is reverted: GET `.../runbooks/{runbookName}/draft/content` to confirm it matches the last published version.

### 5. Manage a Stuck or Long-Running Test Job

1. Check current test job status: GET `.../runbooks/{runbookName}/draft/testJob`.
2. If status is `Suspended`, resume it: POST `.../runbooks/{runbookName}/draft/testJob/resume`.
3. If status is `Running` and appears stuck, stop it: POST `.../runbooks/{runbookName}/draft/testJob/stop`.
4. Review streams for error output: GET `.../runbooks/{runbookName}/draft/testJob/streams` with `$filter=properties/streamType eq 'Error'`.
5. Fix the draft content and create a new test job if needed.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
