---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 3 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs/{sourceControlSyncJobId} | Creates the sync job for a source control. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs/{sourceControlSyncJobId} | Retrieve the source control sync job identified by job id. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs | Retrieve a list of source control sync jobs. |

## Enhanced Skill Content


## Question Mapping

- "How do I trigger a source control sync job?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs/{sourceControlSyncJobId}
- "How do I create a new sync job for my automation source control?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs/{sourceControlSyncJobId}
- "What is the status of my source control sync job?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs/{sourceControlSyncJobId}
- "Did my sync job succeed or fail?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs/{sourceControlSyncJobId}
- "List all sync jobs for a source control connection" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs
- "Show me recent sync job history for my automation account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs
- "How do I filter sync jobs by status?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs (use $filter param)
- "How do I re-run a failed sync job?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs/{sourceControlSyncJobId} (create a new job with a new GUID)
- "What sync job ID should I use when creating a job?" -> PUT ...sourceControlSyncJobs/{sourceControlSyncJobId} (generate a new GUID client-side)
- "How do I check if source control is syncing right now?" -> GET ...sourceControlSyncJobs (list jobs, check for `InProgress` status)
- "Can I cancel an in-progress sync job?" -> No cancel endpoint exists in this API; monitor via GET until completion
- "How do I sync a specific source control by name?" -> PUT ...sourceControls/{sourceControlName}/sourceControlSyncJobs/{sourceControlSyncJobId}

## Response Tips

- **Create (PUT) sync jobs**: Returns 201 on success; the response body contains the job ID and initial provisioning state -- do not assume sync is complete on 201.
- **Get single sync job**: Returns 200 with current job status (`Completed`, `Failed`, `InProgress`); check `properties.syncType` and `properties.exception` for failure details.
- **List sync jobs**: Returns 200 with a paginated array; look for `nextLink` to retrieve additional pages. Use `$filter` for OData-style filtering (e.g., by status or creation time).

## Anomaly Flags

- **Sync job stuck in `InProgress`**: Surface if a job has been in progress for longer than expected (no timeout endpoint exists; the agent should poll and alert).
- **Repeated `Failed` status**: Flag when multiple consecutive sync jobs fail for the same source control -- likely a configuration or credential issue.
- **`properties.exception` present**: Proactively surface the exception message from a failed sync job rather than requiring the user to drill in.
- **API version `2017-05-15-preview`**: This is a preview API version; flag that behavior may change and recommend checking for GA availability.
- **Missing `nextLink` awareness**: If listing returns a large number of jobs, ensure pagination is followed -- incomplete results may hide failures.

## Playbook

### 1. Trigger and Monitor a Source Control Sync

1. Generate a new GUID to use as `sourceControlSyncJobId`.
2. PUT to `.../sourceControls/{sourceControlName}/sourceControlSyncJobs/{newGuid}` with required `parameters` body (typically `commitId` to sync to).
3. Confirm 201 response and note the returned job ID.
4. Poll GET `.../sourceControlSyncJobs/{jobId}` every 15-30 seconds.
5. Check `properties.provisioningState` -- stop polling when status is `Completed` or `Failed`.
6. If `Failed`, read `properties.exception` for the root cause.

### 2. Audit Recent Sync Activity

1. GET `.../sourceControls/{sourceControlName}/sourceControlSyncJobs` to list all jobs.
2. Follow `nextLink` if present to retrieve the full history.
3. Optionally use `$filter` to narrow by date range or status.
4. For each job of interest, GET the individual job endpoint to see full details including exception messages.
5. Summarize results: count of succeeded, failed, and in-progress jobs.

### 3. Diagnose a Failed Sync Job

1. GET `.../sourceControlSyncJobs/{sourceControlSyncJobId}` for the failed job.
2. Read `properties.provisioningState` to confirm `Failed`.
3. Extract `properties.exception` for the error message.
4. Common causes: expired credentials on the source control connection, branch deleted or renamed, merge conflicts in runbooks.
5. Fix the underlying issue, then trigger a new sync (Playbook 1) with a fresh GUID.

### 4. List and Filter Sync Jobs by Status

1. GET `.../sourceControlSyncJobs` with `$filter=properties/provisioningState eq 'Failed'` to find all failed jobs.
2. Follow `nextLink` for complete results.
3. For each failed job, GET individual details to collect exception messages.
4. Use this to build a failure report or trigger automated remediation.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
