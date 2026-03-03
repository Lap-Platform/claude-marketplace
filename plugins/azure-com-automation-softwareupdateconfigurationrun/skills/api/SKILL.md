---
name: update-management-api
description: "Update Management API skill. Use when working with Update Management for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Update Management API
API version: 2017-05-15-preview

## Auth
OAuth2

## Base URL
https://management.azure.com/

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns/{softwareUpdateConfigurationRunId} | Get a single software update configuration Run by Id. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns | Return list of software update configuration runs |

## Enhanced Skill Content
## Question Mapping

- "What update runs exist for my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns
- "Show me details of a specific update run" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns/{softwareUpdateConfigurationRunId}
- "Did my last patch deployment succeed?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns
- "List failed update runs" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns
- "How many machines were patched in a specific run?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns/{softwareUpdateConfigurationRunId}
- "Filter update runs by a specific configuration name" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns
- "Get the most recent update run only" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns
- "Skip the first 10 results and show the next page" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns
- "What was the start and end time of update run X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns/{softwareUpdateConfigurationRunId}
- "Show me update runs from the last 24 hours" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns
- "Which OS type was targeted in this update run?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns/{softwareUpdateConfigurationRunId}
- "Are there any in-progress update runs right now?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationRuns

## Response Tips

- **Single run (by ID):** Response contains a `properties` object with `softwareUpdateConfiguration`, `status`, `startTime`, `endTime`, `computerCount`, and `failedCount` -- check `properties.status` for overall outcome before inspecting nested machine details.
- **List runs:** Returns a `value` array; use `$top` to limit page size, `$skip` to offset into results, and check for a `nextLink` property to determine if more pages exist. `$filter` accepts OData expressions (e.g., filtering by `properties/startTime` or `properties/status`).
- **Errors:** Azure Resource Manager returns `error.code` and `error.message` in the response body; common codes include `ResourceNotFound` (404 equivalent), `AuthorizationFailed`, and `InvalidFilterExpression` for bad `$filter` syntax.

## Anomaly Flags

- **Failed runs detected:** When listing runs, proactively flag any entries where `properties.status` is `Failed` or where `properties.failedCount > 0`, as these indicate machines that were not successfully patched.
- **Stale or long-running updates:** Flag runs where `properties.status` is still `InProgress` but `properties.startTime` is more than 4 hours ago -- these may be stuck.
- **High failure ratio:** If `failedCount` approaches or exceeds `computerCount`, surface this as a critical issue -- the update configuration may be misconfigured.
- **API version deprecation:** This spec uses `2017-05-15-preview` -- a preview API version. Flag that newer stable versions may be available and this version could be retired without notice.
- **Pagination truncation:** If responses include a `nextLink` but the user only inspects the first page, warn that results are incomplete.
- **Empty result sets with filters:** If a `$filter` query returns zero results, suggest verifying filter syntax and time ranges before assuming no runs exist.

## Playbook

### 1. Audit all failed update runs

1. Call GET on the runs list endpoint with `$filter=properties/status eq 'Failed'` to retrieve only failed runs.
2. For each failed run in the `value` array, note the `softwareUpdateConfigurationRunId` and `properties.failedCount`.
3. Call GET on the single run endpoint with each run ID to inspect detailed failure information.
4. Check `properties.softwareUpdateConfiguration` to identify which configuration caused failures.
5. Compile a summary of affected machines and failure reasons for remediation.

### 2. Monitor a currently running update deployment

1. Call GET on the runs list endpoint with `$filter=properties/status eq 'InProgress'` and `$top=1` to find the active run.
2. Extract the `softwareUpdateConfigurationRunId` from the response.
3. Periodically call GET on the single run endpoint using that ID.
4. Compare `properties.computerCount` and `properties.failedCount` to track progress.
5. Once `properties.status` changes from `InProgress` to `Succeeded` or `Failed`, report the final outcome.

### 3. Retrieve a paginated history of all update runs

1. Call GET on the runs list endpoint with `$top=50` and no `$skip` to get the first page.
2. Process the `value` array and record relevant run details.
3. If the response contains a `nextLink` property, increment `$skip` by 50 and repeat.
4. Continue until no `nextLink` is returned or the `value` array is empty.
5. Aggregate results to build a complete update history report.

### 4. Investigate a specific update run by ID

1. Obtain the `softwareUpdateConfigurationRunId` (from a list query, alert, or Azure portal).
2. Call GET on the single run endpoint with that ID.
3. Check `properties.status` for overall result (`Succeeded`, `Failed`, `InProgress`).
4. Inspect `properties.startTime` and `properties.endTime` to calculate duration.
5. Review `properties.softwareUpdateConfiguration` for the targeted OS, included/excluded patches, and reboot settings.

### 5. Compare recent runs of a specific update configuration

1. Call GET on the runs list endpoint with `$filter=properties/softwareUpdateConfiguration/name eq '<config-name>'` and `$top=10`.
2. For each run in the response, extract `status`, `startTime`, `computerCount`, and `failedCount`.
3. Sort by `startTime` to establish a timeline.
4. Compare `failedCount` across runs to identify trends (improving, worsening, or stable).
5. If failures are increasing, call GET on the most recent failed run ID to inspect root cause details.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
