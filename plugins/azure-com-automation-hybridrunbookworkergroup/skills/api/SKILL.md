---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 4 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/hybridRunbookWorkerGroups -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/hybridRunbookWorkerGroups/{hybridRunbookWorkerGroupName} | Delete a hybrid runbook worker group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/hybridRunbookWorkerGroups/{hybridRunbookWorkerGroupName} | Retrieve a hybrid runbook worker group. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/hybridRunbookWorkerGroups/{hybridRunbookWorkerGroupName} | Update a hybrid runbook worker group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/hybridRunbookWorkerGroups | Retrieve a list of hybrid runbook worker groups. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all hybrid runbook worker groups in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/hybridRunbookWorkerGroups
- "How do I filter hybrid worker groups by a specific property?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/hybridRunbookWorkerGroups (use `$filter` param)
- "How do I get details for a specific hybrid runbook worker group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/hybridRunbookWorkerGroups/{hybridRunbookWorkerGroupName}
- "How do I delete a hybrid runbook worker group?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/hybridRunbookWorkerGroups/{hybridRunbookWorkerGroupName}
- "How do I update or rename a hybrid worker group?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/hybridRunbookWorkerGroups/{hybridRunbookWorkerGroupName}
- "How do I change the credential assigned to a worker group?" -> PATCH .../{hybridRunbookWorkerGroupName} (update `credential` in parameters body)
- "Does a specific hybrid worker group exist in my account?" -> GET .../{hybridRunbookWorkerGroupName} (check for 200 vs 404)
- "How do I remove all hybrid worker groups from an automation account?" -> List with GET then DELETE each one individually
- "How do I audit which worker groups are configured for my automation account?" -> GET .../hybridRunbookWorkerGroups (list all, inspect returned properties)
- "What OData filters can I use when listing worker groups?" -> GET .../hybridRunbookWorkerGroups with `$filter` query parameter
- "How do I verify a worker group was deleted successfully?" -> DELETE returns 200 on success; follow up with GET to confirm 404
- "How do I move a hybrid worker from one group to another?" -> PATCH the target group or use the HybridRunbookWorker sub-resource (outside this spec scope)

## Response Tips

- **List endpoint (GET collection):** Returns a `value` array of worker group objects; check for `nextLink` property for pagination -- keep fetching until `nextLink` is absent.
- **Single resource (GET by name):** Returns the full worker group object with `id`, `name`, `type`, and `properties` nested object containing group configuration.
- **Update (PATCH):** Returns the updated worker group object at 200; compare returned properties against your request body to confirm changes took effect.
- **Delete (DELETE):** Returns 200 with empty or minimal body on success; a 404 means the group was already removed or never existed.
- **Errors (all endpoints):** Azure ARM returns `error.code` and `error.message` in the response body for 4xx/5xx; always parse these for actionable detail rather than relying on status code alone.

## Anomaly Flags

- **404 on GET/DELETE:** Surface immediately -- the worker group name may be misspelled or the resource was deleted out-of-band.
- **429 Too Many Requests:** Azure ARM throttles per-subscription; surface the `Retry-After` header value and pause before retrying.
- **409 Conflict on PATCH:** Another update is in progress; alert the user to retry after a brief wait.
- **Stale api-version:** This spec uses `2015-10-31` -- flag if Azure returns `InvalidApiVersionParameter` suggesting a newer version is required.
- **Empty `value` array on list:** If the user expects worker groups but gets none, surface this as a potential misconfiguration of subscriptionId, resourceGroupName, or automationAccountName.
- **Missing `nextLink` mid-pagination:** If a previous response had `nextLink` but a subsequent one does not, confirm all pages were consumed rather than silently stopping.
- **Long DELETE latency:** If DELETE takes notably longer than usual, surface it -- the group may contain many workers being deregistered.

## Playbook

### 1. Inventory All Hybrid Worker Groups

1. Call GET `.../hybridRunbookWorkerGroups` with no filter.
2. Collect the `value` array from the response.
3. If `nextLink` is present, fetch the next page using that URL.
4. Repeat until no `nextLink` remains.
5. Compile the full list of group names and their properties for review.

### 2. Inspect and Update a Worker Group

1. Call GET `.../hybridRunbookWorkerGroups/{groupName}` to retrieve current configuration.
2. Review the `properties` object (credential, group type).
3. Construct a PATCH body with only the fields you want to change.
4. Call PATCH `.../hybridRunbookWorkerGroups/{groupName}` with the parameters body.
5. Compare the returned object against your intended changes to confirm success.

### 3. Safely Delete a Worker Group

1. Call GET `.../hybridRunbookWorkerGroups/{groupName}` to confirm it exists and inspect its current state.
2. Verify no critical runbooks depend on this group (out-of-band check).
3. Call DELETE `.../hybridRunbookWorkerGroups/{groupName}`.
4. Confirm 200 response.
5. Optionally call GET on the same name to verify a 404, confirming full removal.

### 4. Filter Worker Groups by Criteria

1. Determine your OData filter expression (e.g., `$filter=properties/groupType eq 'User'`).
2. Call GET `.../hybridRunbookWorkerGroups` with the `$filter` query parameter.
3. Parse the `value` array for matching results.
4. Follow `nextLink` if present for additional pages.
5. Use the filtered set for downstream operations (update, delete, reporting).

### 5. Bulk Cleanup of Worker Groups

1. Call GET `.../hybridRunbookWorkerGroups` to list all groups.
2. Identify groups to remove based on naming convention, age, or filter criteria.
3. For each target group, call DELETE `.../hybridRunbookWorkerGroups/{groupName}`.
4. Track 200 (success) vs 404 (already gone) vs other errors per group.
5. Re-run the list call to confirm only intended groups remain.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
