---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 2 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs/{sourceControlSyncJobId}/streams -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs/{sourceControlSyncJobId}/streams | Retrieve a list of sync job streams identified by sync job id. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs/{sourceControlSyncJobId}/streams/{streamId} | Retrieve a sync job stream identified by stream id. |

## Enhanced Skill Content
## Question Mapping

- "List all streams for a source control sync job?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs/{sourceControlSyncJobId}/streams
- "Get details of a specific sync job stream?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/sourceControls/{sourceControlName}/sourceControlSyncJobs/{sourceControlSyncJobId}/streams/{streamId}
- "What output did my source control sync produce?" -> GET .../sourceControlSyncJobs/{sourceControlSyncJobId}/streams
- "Show error streams from a failed sync job?" -> GET .../sourceControlSyncJobs/{sourceControlSyncJobId}/streams with $filter for error type
- "Filter sync job streams by type?" -> GET .../sourceControlSyncJobs/{sourceControlSyncJobId}/streams with $filter parameter
- "Why did my source control sync fail?" -> GET .../sourceControlSyncJobs/{sourceControlSyncJobId}/streams (inspect error/warning streams)
- "Get a specific stream entry by ID?" -> GET .../streams/{streamId}
- "What warnings were emitted during sync?" -> GET .../streams with $filter for warning type
- "Show the full text of a particular sync stream record?" -> GET .../streams/{streamId}
- "List all log output from the last source control sync?" -> GET .../sourceControlSyncJobs/{sourceControlSyncJobId}/streams
- "How many stream records exist for a sync job?" -> GET .../streams (count results in response)
- "Did my automation account sync produce any errors?" -> GET .../streams then inspect stream types

## Response Tips

- **Stream listings** (GET .../streams): Returns a paged array under `value`; check `nextLink` for additional pages. Each entry contains `streamId`, `streamType`, and summary text -- full content requires fetching the individual stream.
- **Stream detail** (GET .../streams/{streamId}): Returns the full stream record including `streamText` with complete output. The `streamType` field indicates whether the entry is Output, Error, or Warning.
- **Errors**: 4xx responses follow Azure error format with `error.code` and `error.message`. A 404 means the sync job ID or stream ID does not exist in the specified automation account.

## Anomaly Flags

- **Error-type streams present**: If any stream in a listing has `streamType` of `Error`, surface this immediately -- the sync job encountered failures.
- **Empty stream list**: A sync job with zero streams may indicate the job never ran or was cancelled before producing output.
- **Truncated stream text**: If `streamText` in a detail response appears cut off, flag that the full output may exceed response limits.
- **Pagination present**: If `nextLink` appears in a list response, warn that results are incomplete and additional pages should be fetched.
- **Mixed stream types**: If a single sync job contains both Error and Output streams, flag partial success -- some operations completed while others failed.

## Playbook

### 1. Diagnose a Failed Source Control Sync

1. List all streams for the failed sync job using GET .../streams
2. Filter or scan results for entries where `streamType` is `Error`
3. For each error stream, fetch the full detail using GET .../streams/{streamId}
4. Read `streamText` to identify the root cause (merge conflicts, auth failures, missing files)

### 2. Audit Full Sync Output

1. Call GET .../streams to retrieve the first page of stream records
2. Check the response for `nextLink`; if present, follow it to get subsequent pages
3. Collect all stream entries and group by `streamType` (Output, Error, Warning)
4. For any stream requiring full text, fetch individual records via GET .../streams/{streamId}

### 3. Monitor Sync Health Across Jobs

1. For each recent sync job ID, call GET .../streams
2. Count entries by `streamType` per job
3. Flag any job with Error streams or with zero streams (possible silent failure)
4. For jobs with warnings, fetch individual warning streams to assess severity

### 4. Retrieve Specific Stream Details

1. Identify the target `streamId` from a previous listing or external reference
2. Call GET .../streams/{streamId} with the full path including subscription, resource group, automation account, source control name, and sync job ID
3. Inspect `streamText` for the complete output content and `streamType` for classification


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
