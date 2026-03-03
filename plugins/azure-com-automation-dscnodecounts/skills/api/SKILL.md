---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 1 endpoint."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodecounts/{countType} -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodecounts/{countType} | Retrieve counts for Dsc Nodes. |

## Enhanced Skill Content
## Question Mapping

- "How many nodes are in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodecounts/{countType}
- "What is the DSC node count by status?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodecounts/status
- "How many nodes are compliant vs non-compliant?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodecounts/status
- "Get node counts grouped by node configuration name" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodecounts/nodeconfiguration
- "Are any DSC nodes in a failed state?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodecounts/status
- "Show me automation node statistics for a specific resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodecounts/{countType}
- "What count types are available for automation nodes?" -> GET .../nodecounts/{countType} (use `status` or `nodeconfiguration` as countType)
- "How many nodes are pending reboot after configuration?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodecounts/status
- "Compare node health across automation accounts" -> GET .../nodecounts/status (call once per account, then compare results)
- "Is my DSC pull server healthy based on node compliance?" -> GET .../nodecounts/status (check ratio of compliant to total nodes)
- "Which node configurations have the most nodes assigned?" -> GET .../nodecounts/nodeconfiguration
- "Get a summary of all managed nodes in my automation account" -> GET .../nodecounts/status

## Response Tips

- **Node counts (GET .../nodecounts/{countType})**: Response contains a `totalCount` and a `value` array with individual count entries. Each entry has a `properties` object with `count` (integer) and grouping metadata. The `countType` path parameter accepts `status` (groups by compliance status) or `nodeconfiguration` (groups by assigned configuration). Empty automation accounts return zero counts, not 404.

## Anomaly Flags

- **Zero total node count**: If `totalCount` is 0, the automation account may have no registered DSC nodes -- surface this as it could indicate a misconfiguration or deregistration event.
- **High non-compliant ratio**: If nodes in `NotCompliant` or `Failed` status exceed 20% of total, flag as a compliance drift warning.
- **Unexpected 404**: A 404 likely means the automation account name, resource group, or subscription ID is incorrect -- prompt the user to verify resource identifiers.
- **Throttling (429)**: Azure ARM APIs enforce per-subscription rate limits. If a 429 is returned, surface the `Retry-After` header value and pause before retrying.
- **Deprecated API version**: The spec uses `2018-01-15`. If Azure returns a warning header about API version deprecation, proactively notify the user to migrate to a newer API version.
- **Authorization errors (401/403)**: The endpoint requires OAuth2 with `Microsoft.Automation/automationAccounts/read` permission. Surface missing role assignments if access is denied.

## Playbook

### 1. Check DSC Node Compliance Health

1. Call `GET .../nodecounts/status` with your subscription, resource group, and automation account name.
2. Parse the `value` array for entries with status names like `Compliant`, `NotCompliant`, `Failed`, `Pending`.
3. Calculate the compliance percentage: `Compliant / totalCount * 100`.
4. If compliance is below your threshold (e.g., 90%), investigate non-compliant nodes individually via the DSC Nodes API.

### 2. Audit Node Distribution Across Configurations

1. Call `GET .../nodecounts/nodeconfiguration` to get counts grouped by node configuration.
2. Review the `value` array to see how many nodes are assigned to each configuration.
3. Identify configurations with zero nodes (potentially orphaned configs to clean up).
4. Identify configurations with unexpectedly high counts (possible misassignment).

### 3. Monitor Automation Account Health Across Resource Groups

1. List all automation accounts in your subscription (via the Automation Accounts list API).
2. For each account, call `GET .../nodecounts/status`.
3. Aggregate `totalCount` and status breakdowns across all accounts.
4. Flag any account where `Failed` or `NotCompliant` nodes exceed your alerting threshold.
5. Use the results to build a dashboard or trigger alerts.

### 4. Troubleshoot Missing Nodes

1. Call `GET .../nodecounts/status` to get current total.
2. Compare `totalCount` against your expected node count (from CMDB or inventory).
3. If counts are lower than expected, check for nodes in `Unresponsive` status.
4. Verify network connectivity and DSC pull server reachability from missing nodes.
5. Re-register missing nodes using the DSC Node registration endpoint.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
