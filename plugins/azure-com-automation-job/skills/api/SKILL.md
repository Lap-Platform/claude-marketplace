---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# AutomationManagement
API version: 2017-05-15-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobs/{jobName}/output -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobs/{jobName}/suspend -- create first suspend

## Endpoints

10 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobs/{jobName}/output | Retrieve the job output identified by job name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobs/{jobName}/runbookContent | Retrieve the runbook content of the job identified by job name. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobs/{jobName}/suspend | Suspend the job identified by job name. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobs/{jobName}/stop | Stop the job identified by jobName. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobs/{jobName} | Retrieve the job identified by job name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobs/{jobName} | Create a job of the runbook. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobs | Retrieve a list of jobs. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobs/{jobName}/resume | Resume the job identified by jobName. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobs/{jobName}/streams/{jobStreamId} | Retrieve the job stream identified by job stream id. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobs/{jobName}/streams | Retrieve a list of jobs streams identified by job name. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all jobs in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobs
- "How do I filter jobs by status?" -> GET /...automationAccounts/{automationAccountName}/jobs with `$filter` parameter
- "How do I get details for a specific job?" -> GET /...automationAccounts/{automationAccountName}/jobs/{jobName}
- "How do I create or start a new automation job?" -> PUT /...automationAccounts/{automationAccountName}/jobs/{jobName}
- "How do I stop a running job?" -> POST /...automationAccounts/{automationAccountName}/jobs/{jobName}/stop
- "How do I suspend a job temporarily?" -> POST /...automationAccounts/{automationAccountName}/jobs/{jobName}/suspend
- "How do I resume a suspended job?" -> POST /...automationAccounts/{automationAccountName}/jobs/{jobName}/resume
- "How do I get the output of a completed job?" -> GET /...automationAccounts/{automationAccountName}/jobs/{jobName}/output
- "How do I see the runbook content associated with a job?" -> GET /...automationAccounts/{automationAccountName}/jobs/{jobName}/runbookContent
- "How do I list all streams for a job?" -> GET /...automationAccounts/{automationAccountName}/jobs/{jobName}/streams
- "How do I get a specific job stream by ID?" -> GET /...automationAccounts/{automationAccountName}/jobs/{jobName}/streams/{jobStreamId}
- "How do I filter job streams (e.g., only errors)?" -> GET /...automationAccounts/{automationAccountName}/jobs/{jobName}/streams with `$filter` parameter
- "How do I check if a job finished successfully?" -> GET /...automationAccounts/{automationAccountName}/jobs/{jobName} (inspect `status` and `provisioningState`)
- "How do I re-run a failed job?" -> PUT /...automationAccounts/{automationAccountName}/jobs/{jobName} (create a new job referencing the same runbook)

## Response Tips

- **Job listings** (GET .../jobs): Results are paginated via `nextLink`; follow it until absent to retrieve all jobs. Use `$filter` with OData syntax (e.g., `status eq 'Running'`).
- **Job details** (GET .../jobs/{jobName}): Key fields are `properties.status` (New, Activating, Running, Completed, Failed, Stopped, Suspended), `properties.provisioningState`, and `properties.startTime`/`endTime`.
- **Job creation** (PUT .../jobs/{jobName}): Returns 201 on success. The `parameters` body must include `properties.runbook.name` at minimum. The job name you supply becomes the resource ID.
- **Job actions** (stop/suspend/resume): Return 200 with empty or minimal body on success. A non-200 response indicates the job was not in a valid state for that transition.
- **Job output** (GET .../output): Returns raw text output, not JSON. Handle the response as plain text.
- **Job streams** (GET .../streams): Each stream entry has a `streamType` (Output, Error, Warning, Verbose, Progress). Filter with `$filter=properties/streamType eq 'Error'` to isolate failures.

## Anomaly Flags

- **Job stuck in Activating**: If a job stays in `Activating` status for more than a few minutes, surface this -- it may indicate a worker shortage or configuration issue.
- **Repeated Failed status**: When listing jobs, flag if a high proportion have `Failed` status, suggesting a systemic runbook or credential problem.
- **Empty job output**: If GET .../output returns empty for a `Completed` job, warn the user -- the runbook may not produce output or may be writing to streams only.
- **Error streams present**: After job completion, proactively check streams with `$filter=properties/streamType eq 'Error'` and surface any error stream entries.
- **Throttling (429)**: Azure Resource Manager enforces rate limits. If you receive 429 responses, surface the `Retry-After` header value and pause before retrying.
- **Deprecated API version**: This spec uses `2017-05-15-preview`. Flag that newer stable API versions may be available and preview versions can be retired without notice.
- **Suspend on non-running job**: Attempting to suspend a job that is not `Running` returns an error. Flag the current job state before attempting lifecycle actions.

## Playbook

### 1. Run a Runbook and Collect Output

1. Create a new job: PUT .../jobs/{jobName} with `parameters` body containing `properties.runbook.name` set to the target runbook.
2. Poll job status: GET .../jobs/{jobName} and check `properties.status` until it reaches `Completed`, `Failed`, or `Stopped`.
3. Retrieve output: GET .../jobs/{jobName}/output to get the raw text result.
4. Check for errors: GET .../jobs/{jobName}/streams?$filter=properties/streamType eq 'Error' to catch any error streams.

### 2. Diagnose a Failed Job

1. Get job details: GET .../jobs/{jobName} and note the `status`, `exception`, and `startTime`/`endTime` fields.
2. List all streams: GET .../jobs/{jobName}/streams to see the full execution trace.
3. Filter to errors: GET .../jobs/{jobName}/streams?$filter=properties/streamType eq 'Error' for targeted diagnostics.
4. Inspect specific stream: GET .../jobs/{jobName}/streams/{jobStreamId} using the ID from step 3 for full error details.
5. Review runbook content: GET .../jobs/{jobName}/runbookContent to verify the script that was executed.

### 3. Suspend, Inspect, and Resume a Long-Running Job

1. Confirm job is running: GET .../jobs/{jobName} and verify `properties.status` is `Running`.
2. Suspend the job: POST .../jobs/{jobName}/suspend.
3. Inspect progress: GET .../jobs/{jobName}/streams to review output and progress streams so far.
4. Resume the job: POST .../jobs/{jobName}/resume when ready to continue execution.

### 4. Audit All Jobs by Status

1. List all jobs: GET .../jobs to retrieve the full job list (follow `nextLink` for pagination).
2. Filter by status: GET .../jobs?$filter=status eq 'Failed' to find all failed jobs.
3. For each failed job, retrieve streams: GET .../jobs/{jobName}/streams?$filter=properties/streamType eq 'Error'.
4. Compile a summary of failure patterns across jobs for remediation.

### 5. Emergency Stop All Running Jobs

1. List running jobs: GET .../jobs?$filter=status eq 'Running'.
2. For each running job, issue a stop: POST .../jobs/{jobName}/stop.
3. Verify each job transitioned: GET .../jobs/{jobName} and confirm `properties.status` is `Stopped`.
4. Review streams for any jobs that did not stop cleanly: GET .../jobs/{jobName}/streams.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
