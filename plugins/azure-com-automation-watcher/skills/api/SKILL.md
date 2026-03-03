---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# AutomationManagement
API version: 2015-10-31

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName}/start -- create first start

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName} | Create the watcher identified by watcher name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName} | Retrieve the watcher identified by watcher name. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName} | Update the watcher identified by watcher name. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName} | Delete the watcher by name. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName}/start | Resume the watcher identified by watcher name. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName}/stop | Resume the watcher identified by watcher name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers | Retrieve a list of watchers. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new watcher in my automation account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName}
- "What are the details of a specific watcher?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName}
- "How do I update properties on an existing watcher without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName}
- "How do I delete a watcher I no longer need?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName}
- "How do I activate or turn on a watcher?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName}/start
- "How do I stop a running watcher?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName}/stop
- "Can I list all watchers in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers
- "How do I filter watchers by a specific property?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers (use `$filter` query param)
- "How do I replace a watcher's configuration entirely?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName}
- "Is a specific watcher currently running or stopped?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers/{watcherName} (check `status` in response)
- "How do I restart a watcher that has been stopped?" -> POST .../watchers/{watcherName}/start (stop first if running, then start)
- "What watchers exist across a resource group's automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/watchers

## Response Tips

- **Single watcher responses (GET/PUT/PATCH):** Response body is the full watcher resource object including `properties.status`, `properties.executionFrequencyInSeconds`, and `properties.scriptRunOn`; check `properties.status` for current state.
- **PUT create vs update:** 201 means a new watcher was created; 200 means an existing watcher was updated in place.
- **List watchers (GET collection):** Response contains a `value` array of watcher objects; use OData `$filter` for server-side filtering; check for `nextLink` property for pagination if the account has many watchers.
- **DELETE/start/stop (action endpoints):** 200 confirms success; no response body is typical for DELETE; start/stop are idempotent-safe but may error if the watcher is in an unexpected state.
- **Error responses:** Azure ARM errors follow `{ "error": { "code": "...", "message": "..." } }` structure; common codes include `ResourceNotFound`, `ResourceGroupNotFound`, and `AuthorizationFailed`.

## Anomaly Flags

- **OAuth2 token expiry:** Surface when the bearer token is near expiration or when a 401 is returned mid-workflow -- prompt for token refresh before retrying.
- **201 vs 200 on PUT:** Flag when a PUT returns 201 unexpectedly, as this means a new resource was created rather than updating an existing one (possible naming mismatch).
- **Watcher stuck in transitional state:** If a GET after start/stop still shows the previous status, surface that the watcher may be in a provisioning state and suggest polling.
- **$filter ignored or unsupported fields:** If a filtered list returns unfiltered results, flag that the filter expression may be malformed or targeting a non-filterable property.
- **API version drift:** This spec targets `2015-10-31`; surface a warning if Azure documentation or error messages reference a newer api-version, as behavior may differ.
- **Throttling (429 responses):** Azure ARM enforces subscription-level rate limits; surface `Retry-After` header values proactively if any request returns 429.

## Playbook

### 1. Create and Start a New Watcher

1. Build the watcher parameters object with required properties (`scriptName`, `scriptRunOn`, `executionFrequencyInSeconds`, etc.).
2. Call PUT `.../watchers/{watcherName}` with the parameters body.
3. Confirm the response is 201 (created) or 200 (updated).
4. Call POST `.../watchers/{watcherName}/start` to activate the watcher.
5. Call GET `.../watchers/{watcherName}` to verify `properties.status` is `Running`.

### 2. Pause, Modify, and Resume a Watcher

1. Call POST `.../watchers/{watcherName}/stop` to pause execution.
2. Call GET `.../watchers/{watcherName}` to confirm status is no longer `Running`.
3. Call PATCH `.../watchers/{watcherName}` with only the properties to update (e.g., changed frequency or script parameters).
4. Verify the 200 response contains the updated values.
5. Call POST `.../watchers/{watcherName}/start` to resume with the new configuration.

### 3. Audit All Watchers in an Automation Account

1. Call GET `.../watchers` (no filter) to retrieve the full list.
2. If `nextLink` is present in the response, follow it to get additional pages.
3. For each watcher, inspect `properties.status` to identify stopped or errored watchers.
4. Optionally call GET on individual watchers for full detail including last run information.
5. Compile results into a status summary (running count, stopped count, error count).

### 4. Clean Up Unused Watchers

1. Call GET `.../watchers` to list all watchers.
2. Identify candidates for removal (stopped watchers, watchers with old configurations).
3. For each candidate, call POST `.../watchers/{watcherName}/stop` if status is `Running`.
4. Call DELETE `.../watchers/{watcherName}` to remove the watcher.
5. Confirm 200 response for each deletion.
6. Re-list watchers to verify cleanup is complete.

### 5. Replace a Watcher Configuration (Full Reset)

1. Call GET `.../watchers/{watcherName}` to capture the current configuration for reference.
2. Call POST `.../watchers/{watcherName}/stop` to halt execution.
3. Call PUT `.../watchers/{watcherName}` with the complete new configuration in the parameters body.
4. Confirm 200 response (existing resource updated, not 201 which would indicate a name mismatch).
5. Call POST `.../watchers/{watcherName}/start` to activate with the new configuration.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
