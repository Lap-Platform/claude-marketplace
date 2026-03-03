---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 1 endpoint."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/linkedWorkspace -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/linkedWorkspace | Retrieve the linked workspace for the account id. |

## Enhanced Skill Content
## Question Mapping

- "What workspace is linked to my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/linkedWorkspace
- "How do I find the Log Analytics workspace for an automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/linkedWorkspace
- "Is there a linked workspace on this automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/linkedWorkspace
- "Which workspace does my automation account use?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/linkedWorkspace
- "Get linked workspace details for a specific resource group's automation account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/linkedWorkspace
- "Check if automation account {name} has a workspace link" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/linkedWorkspace
- "Retrieve the workspace ID tied to my automation account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/linkedWorkspace
- "What Log Analytics integration does this automation account have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/linkedWorkspace
- "Show workspace configuration for automation account in resource group X" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/linkedWorkspace
- "Verify the linked workspace for troubleshooting Update Management" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/linkedWorkspace

## Response Tips

- **Linked Workspace (200):** Response contains a workspace `id` property (full ARM resource ID). If no workspace is linked, expect a 404 or an empty/null `id` field. Parse the resource ID to extract the workspace name and resource group if needed.

## Anomaly Flags

- **404 response:** No linked workspace exists for the automation account -- surface this clearly rather than treating it as an error, since many accounts are unlinked.
- **401/403 response:** OAuth2 token may be expired or the caller lacks `Microsoft.Automation/automationAccounts/read` permissions on the target resource.
- **Subscription or resource not found:** If the subscriptionId, resource group, or automation account name is wrong, Azure returns a generic 404. Agent should confirm all three path parameters before retrying.
- **API version mismatch:** This spec uses `2015-10-31`. If the response includes deprecation headers or unexpected schema, flag that a newer API version may be available.
- **Throttling (429):** Azure Resource Manager enforces per-subscription rate limits. Surface `Retry-After` header value if present.

## Playbook

### 1. Check Linked Workspace for an Automation Account

1. Confirm you have the subscription ID, resource group name, and automation account name.
2. Call GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/linkedWorkspace` with a valid OAuth2 bearer token and query param `api-version=2015-10-31`.
3. On 200, read the `id` field from the response to get the full ARM resource ID of the linked workspace.
4. Parse the workspace resource ID to extract the workspace name and its resource group if needed for downstream calls.

### 2. Diagnose Missing Workspace Link

1. Call the linked workspace endpoint for the target automation account.
2. If 404 is returned, confirm the automation account exists by listing accounts in the resource group via the Automation Accounts API.
3. If the account exists but has no linked workspace, advise the user to link one through the Azure portal or via the Operations Management Suite API.

### 3. Validate Update Management Prerequisites

1. Retrieve the linked workspace for the automation account using this endpoint.
2. Confirm the response returns a valid workspace resource ID (required for Update Management, Change Tracking, and Inventory solutions).
3. If no workspace is linked, flag this as a blocking issue -- Update Management will not function without it.
4. Use the workspace resource ID to verify the solution is installed via the Log Analytics Solutions API.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
