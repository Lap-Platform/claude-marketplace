---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# AutomationManagement
API version: 2018-01-15

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs/{compilationJobName} | Creates the Dsc compilation job of the configuration. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs/{compilationJobName} | Retrieve the Dsc configuration compilation job identified by job id. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs | Retrieve a list of dsc compilation jobs. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs/{jobId}/streams | Retrieve all the job streams for the compilation Job. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs/{jobId}/streams/{jobStreamId} | Retrieve the job stream identified by job stream id. |

## Enhanced Skill Content
## Question Mapping

- "How do I start a DSC compilation job?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs/{compilationJobName}
- "How do I check the status of a compilation job?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs/{compilationJobName}
- "List all compilation jobs in my automation account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs
- "How do I filter compilation jobs by status?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs
- "Show me the output streams for a compilation job" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs/{jobId}/streams
- "How do I read error details from a failed compilation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs/{jobId}/streams/{jobStreamId}
- "Did my DSC configuration compile successfully?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs/{compilationJobName}
- "How do I recompile a DSC configuration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs/{compilationJobName}
- "What compilation jobs ran today?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs
- "How do I get verbose output from a compilation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs/{jobId}/streams
- "Show me a specific log stream entry from a job" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs/{jobId}/streams/{jobStreamId}
- "How do I compile a DSC configuration with parameters?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/compilationjobs/{compilationJobName}
- "Why did my compilation job fail?" -> GET .../compilationjobs/{jobId}/streams then GET .../streams/{jobStreamId} for error streams

## Response Tips

- **Compilation job creation (PUT)**: Returns 201 with a `provisioningState` field -- poll the GET endpoint until state leaves `Processing`; the `parameters` body must include the `configuration.name` referencing an existing DSC configuration.
- **Compilation job details (GET single)**: Check `properties.status` for `Completed`, `Failed`, `Suspended`, or `New`; `properties.exception` contains error text on failure.
- **Compilation job listing (GET list)**: Returns a `value` array with `nextLink` for pagination -- follow `nextLink` until null; use `$filter` with OData syntax (e.g., `properties/status eq 'Failed'`).
- **Job streams (GET list)**: Returns a `value` array of stream records; each has a `streamType` field (`Output`, `Error`, `Warning`, `Verbose`) -- filter client-side or scan for `Error` types first.
- **Job stream detail (GET single)**: Returns full `streamText` and `value` properties with the complete log entry; large outputs may be truncated in the list view so always fetch individual streams for full content.

## Anomaly Flags

- **Stuck compilation jobs**: Surface when a job stays in `Processing` or `New` status for more than 15 minutes -- likely indicates a missing module dependency or resource contention.
- **Repeated failures**: Flag when multiple consecutive compilation jobs for the same configuration return `Failed` status -- suggests a systemic configuration error.
- **Error streams present**: Proactively warn when stream listing contains entries with `streamType: Error`, even if the job status has not yet transitioned to `Failed`.
- **API throttling (429)**: Azure ARM APIs enforce per-subscription rate limits; surface `Retry-After` header values immediately and delay subsequent calls accordingly.
- **Deprecated API version**: This spec uses `2018-01-15` -- flag if Azure returns `x-ms-deprecation` headers or if newer api-version values appear in error responses.
- **Missing configuration reference**: When a PUT returns 400, surface the error body -- it typically means the referenced DSC configuration name does not exist in the automation account.

## Playbook

### 1. Compile a DSC Configuration and Monitor to Completion

1. PUT `/compilationjobs/{compilationJobName}` with `parameters` body containing `configuration.name` set to your DSC configuration name.
2. Note the returned `compilationJobName` and `provisioningState`.
3. Poll GET `/compilationjobs/{compilationJobName}` every 10-15 seconds.
4. When `properties.status` is `Completed`, the node configurations are ready. If `Failed`, proceed to Playbook 3.

### 2. List and Filter Compilation Jobs by Status

1. GET `/compilationjobs` to retrieve all jobs.
2. To filter, append `?$filter=properties/status eq 'Failed'` (or `Completed`, `Suspended`).
3. Follow `nextLink` in each response until it is null to collect all pages.
4. Sort results client-side by `properties.startTime` for chronological ordering.

### 3. Diagnose a Failed Compilation Job

1. GET `/compilationjobs/{compilationJobName}` and confirm `properties.status` is `Failed`.
2. Note the `properties.exception` field for a high-level error summary.
3. GET `/compilationjobs/{jobId}/streams` to list all output streams.
4. Filter for entries where `streamType` is `Error`.
5. GET `/compilationjobs/{jobId}/streams/{jobStreamId}` for each error stream to read the full `streamText` with detailed failure context.

### 4. Recompile After Fixing a Configuration

1. Fix the DSC configuration in the automation account (separate API).
2. PUT `/compilationjobs/{newCompilationJobName}` with a new unique job name and the same `configuration.name`.
3. Monitor via GET `/compilationjobs/{newCompilationJobName}` until status is `Completed`.
4. Compare stream output with the previous failed job to confirm the fix resolved all errors.

### 5. Audit All Compilation Activity for an Automation Account

1. GET `/compilationjobs` with no filter to retrieve the full history.
2. Page through all results using `nextLink`.
3. For each job, record `compilationJobName`, `status`, `startTime`, and `endTime`.
4. For any job with `Failed` status, GET its streams and flag error entries.
5. Aggregate results to identify patterns (recurring failures, slow compilations, frequent recompiles).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
