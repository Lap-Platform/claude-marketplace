---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 9 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/agentRegistrationInformation -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/agentRegistrationInformation/regenerateKey -- create first regenerateKey

## Endpoints

9 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/agentRegistrationInformation | Retrieve the automation agent registration information. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/agentRegistrationInformation/regenerateKey | Regenerate a primary or secondary agent registration key |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes/{nodeId} | Delete the dsc node identified by node id. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes/{nodeId} | Retrieve the dsc node identified by node id. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes/{nodeId} | Update the dsc node. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes | Retrieve a list of dsc nodes. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes/{nodeId}/reports | Retrieve the Dsc node report list by node id. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes/{nodeId}/reports/{reportId} | Retrieve the Dsc node report data by node id and report id. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes/{nodeId}/reports/{reportId}/content | Retrieve the Dsc node reports by node id and report id. |

## Enhanced Skill Content
## Question Mapping

- "How do I get the agent registration info for my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/agentRegistrationInformation
- "How do I regenerate a registration key for my automation account?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/agentRegistrationInformation/regenerateKey
- "How do I remove a DSC node from my automation account?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes/{nodeId}
- "How do I get details about a specific DSC node?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes/{nodeId}
- "How do I update a DSC node's configuration?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes/{nodeId}
- "How do I list all DSC nodes in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes
- "How do I filter DSC nodes by status or name?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes (use $filter param)
- "How do I paginate through a large list of DSC nodes?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes (use $skip and $top params)
- "How do I get all reports for a specific DSC node?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes/{nodeId}/reports
- "How do I get a specific DSC node report by ID?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes/{nodeId}/reports/{reportId}
- "How do I download the raw content of a DSC node report?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodes/{nodeId}/reports/{reportId}/content
- "How do I check whether a DSC node's last run was compliant?" -> GET .../nodes/{nodeId}/reports (filter for latest, inspect status)
- "How do I rotate both primary and secondary registration keys?" -> POST .../agentRegistrationInformation/regenerateKey (call twice with keyName "primary" then "secondary")
- "How do I get the total count of DSC nodes without fetching all records?" -> GET .../nodes (use $inlinecount=allpages with $top=0)

## Response Tips

- **Agent Registration Info**: Response contains `keys` (primary/secondary), `endpoint` URL, and `id`. Use the endpoint URL when registering new DSC nodes.
- **Node List**: Supports OData-style pagination via `$skip`/`$top` and filtering via `$filter`. Use `$inlinecount=allpages` to get `totalCount` alongside partial results. Look for `nextLink` in the response for additional pages.
- **Node Details**: Returns node properties including `status` (Compliant/Not Compliant/Pending), `lastSeen`, `nodeConfiguration`, and `registrationTime`. A `null` lastSeen may indicate a node that never checked in.
- **Node Reports**: Each report includes `status`, `startTime`, `endTime`, `type` (Consistency/Initial), and `reportFormatVersion`. Filter by time or status using `$filter`.
- **Report Content**: Returns raw report content (may be large). Response is the full DSC report body, not a JSON wrapper -- handle accordingly.
- **Errors**: All endpoints return standard Azure error responses with `code` and `message` fields nested under an `error` object. Common codes: `ResourceNotFound` (404), `AuthorizationFailed` (403).

## Anomaly Flags

- **Node not checking in**: Surface when a node's `lastSeen` timestamp exceeds 24 hours -- likely indicates connectivity issues or a deregistered machine.
- **Non-compliant nodes**: Proactively flag any node with `status: "Not Compliant"` when listing or retrieving nodes, as this indicates configuration drift.
- **Failed reports**: When fetching reports, flag any with `status: "Failed"` -- these require investigation into the DSC configuration or target machine state.
- **Registration key regeneration**: Warn before regenerating keys that all existing nodes using the old key will fail to check in until re-registered.
- **Large node counts**: If `$inlinecount` returns a total significantly larger than `$top`, alert that pagination is needed and full enumeration may be slow.
- **API version deprecation**: This spec uses `api-version=2018-01-15`. Flag if Azure returns `x-ms-deprecation` headers or if calls begin returning version-related warnings.
- **Throttling**: Watch for `429 Too Many Requests` or `Retry-After` headers. Surface remaining quota from `x-ms-ratelimit-remaining-*` headers when below 20%.

## Playbook

### 1. Register a New DSC Node

1. GET agent registration info to retrieve the registration endpoint URL and primary key
2. On the target machine, configure the Local Configuration Manager (LCM) with the endpoint URL and registration key
3. Run `Update-DscConfiguration` or wait for the LCM refresh cycle
4. GET the node list and confirm the new node appears with `status: "Pending"` or `"Compliant"`
5. If the node does not appear within 15 minutes, check network connectivity and LCM logs on the target

### 2. Investigate a Non-Compliant Node

1. GET the node list with `$filter=properties/status eq 'Not Compliant'` to find non-compliant nodes
2. GET node details for the specific nodeId to review its assigned `nodeConfiguration`
3. GET reports for that node, optionally filtered by `$filter=properties/status eq 'Failed'`
4. GET the report content for the most recent failed report to inspect resource-level errors
5. Fix the DSC configuration or target machine issue, then wait for the next consistency check or trigger one manually

### 3. Rotate Registration Keys Safely

1. GET current agent registration info to note which key (primary/secondary) nodes are using
2. POST regenerateKey with `keyName: "secondary"` to rotate the unused key first
3. Update all nodes to use the new secondary key (via LCM reconfiguration)
4. Confirm all nodes are checking in successfully by listing nodes and verifying `lastSeen` timestamps
5. POST regenerateKey with `keyName: "primary"` to complete the rotation

### 4. Audit Node Compliance Across an Automation Account

1. GET the node list with `$inlinecount=allpages` and `$top=0` to get the total node count
2. Page through all nodes using `$skip` and `$top` (e.g., batches of 100)
3. For each node, check `status` -- collect nodes that are `"Not Compliant"` or `"Pending"`
4. For non-compliant nodes, GET their latest report and report content to build an audit trail
5. Compile results into a compliance summary: total nodes, compliant count, non-compliant count, and nodes not seen in 24+ hours

### 5. Remove a Decommissioned Node

1. GET the node by nodeId to confirm it exists and review its current state
2. Verify the target machine is actually decommissioned or no longer managed
3. DELETE the node by nodeId to remove it from the automation account
4. Confirm removal by attempting to GET the node again -- expect a `ResourceNotFound` error
5. If the machine may come back online, also regenerate the registration key it was using to prevent re-registration


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
