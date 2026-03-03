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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationMachineRuns -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationMachineRuns/{softwareUpdateConfigurationMachineRunId} | Get a single software update configuration machine run by Id. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationMachineRuns | Return list of software update configuration machine runs |

## Enhanced Skill Content
## Question Mapping

- "What happened during a specific update run?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationMachineRuns/{softwareUpdateConfigurationMachineRunId}
- "Show me the details of machine run {id}" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationMachineRuns/{softwareUpdateConfigurationMachineRunId}
- "Did the update succeed on machine {id}?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationMachineRuns/{softwareUpdateConfigurationMachineRunId}
- "List all update runs for my automation account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurationMachineRuns
- "Which machines were patched recently?" -> GET /...softwareUpdateConfigurationMachineRuns?$filter=properties/startTime ge 2024-01-01T00:00:00Z
- "Show me failed update runs" -> GET /...softwareUpdateConfigurationMachineRuns?$filter=properties/status eq 'Failed'
- "Get the first 10 update machine runs" -> GET /...softwareUpdateConfigurationMachineRuns?$top=10
- "Skip the first 5 runs and show the next page" -> GET /...softwareUpdateConfigurationMachineRuns?$skip=5&$top=10
- "Which machines are part of a specific update configuration?" -> GET /...softwareUpdateConfigurationMachineRuns?$filter=properties/softwareUpdateConfiguration/name eq '{configName}'
- "Were any machines rebooted during the last patch cycle?" -> GET /...softwareUpdateConfigurationMachineRuns?$filter=properties/startTime ge '{cycleStart}'
- "How long did the update take on machine {id}?" -> GET /...softwareUpdateConfigurationMachineRuns/{softwareUpdateConfigurationMachineRunId} (check startTime/endTime in response)
- "What updates were installed on a particular machine run?" -> GET /...softwareUpdateConfigurationMachineRuns/{softwareUpdateConfigurationMachineRunId}
- "Show me all runs sorted by most recent" -> GET /...softwareUpdateConfigurationMachineRuns?$filter=properties/startTime desc

## Response Tips

- **Single machine run (by ID):** Response wraps properties under a `properties` object containing `targetComputer`, `status`, `startTime`, `endTime`, `osType`, `softwareUpdateConfiguration`, `correlationId`, and `error`. Always check `properties.status` for the outcome (`Succeeded`, `Failed`, `InProgress`).
- **List of machine runs:** Response includes a `value` array of run objects and a `nextLink` field for pagination. If `nextLink` is present, follow it to retrieve subsequent pages. Use `$top` and `$skip` for manual paging. OData `$filter` follows Azure conventions -- string comparisons require single quotes.

## Anomaly Flags

- **Failed runs:** Proactively surface any machine run where `properties.status` is `Failed` or `properties.error` is non-null -- these indicate patching failures that may need intervention.
- **Long-running updates:** Flag runs where `endTime - startTime` exceeds a reasonable threshold (e.g., 2+ hours) or where `endTime` is null (still in progress / stuck).
- **Pagination truncation:** If `nextLink` is present in list responses, warn the user that results are truncated and offer to fetch the next page.
- **Empty result sets:** If `value` array is empty after filtering, surface this explicitly -- the filter may be too restrictive or the automation account may have no runs.
- **API version deprecation:** This spec uses `2017-05-15-preview` -- a preview API version. Flag that this may be deprecated or replaced by a GA version, and suggest checking for newer API versions.
- **Throttling (429):** If a 429 response is returned, surface the `Retry-After` header value and pause before retrying.

## Playbook

### 1. Audit All Failed Patch Runs for an Automation Account

1. Call `GET /...softwareUpdateConfigurationMachineRuns?$filter=properties/status eq 'Failed'` to list all failed runs.
2. If `nextLink` is present, follow it to collect all pages.
3. For each failed run, extract `properties.targetComputer`, `properties.error`, and `properties.softwareUpdateConfiguration.name`.
4. Group failures by target computer to identify machines that consistently fail patching.
5. For deeper details on a specific failure, call `GET /...softwareUpdateConfigurationMachineRuns/{id}` with the run's ID.

### 2. Check Patch Compliance for a Recent Update Window

1. Determine the update window start and end times.
2. Call `GET /...softwareUpdateConfigurationMachineRuns?$filter=properties/startTime ge '{windowStart}' and properties/startTime le '{windowEnd}'`.
3. Page through all results using `nextLink` if needed.
4. Tally runs by `properties.status` (Succeeded vs Failed vs InProgress).
5. Report compliance percentage and list any machines still showing `InProgress` or `Failed`.

### 3. Investigate a Specific Machine's Update History

1. Call `GET /...softwareUpdateConfigurationMachineRuns?$filter=properties/targetComputer eq '{machineName}'` to list all runs for that machine.
2. Sort results by `properties.startTime` to see chronological history.
3. For any run that looks anomalous (failed, long duration), call `GET /...softwareUpdateConfigurationMachineRuns/{id}` for full details.
4. Check `properties.error` for root cause information.

### 4. Page Through Large Result Sets

1. Call `GET /...softwareUpdateConfigurationMachineRuns?$top=50` to get the first 50 results.
2. Check the response for a `nextLink` field.
3. If `nextLink` exists, issue a GET to that exact URL (it includes continuation tokens).
4. Repeat until `nextLink` is absent, indicating the last page.
5. Alternatively, use `$skip` to manually offset: `$skip=50&$top=50` for page 2, `$skip=100&$top=50` for page 3, etc.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
