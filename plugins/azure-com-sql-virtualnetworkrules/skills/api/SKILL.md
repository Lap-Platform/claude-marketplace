---
name: sqlmanagementclient
description: "SqlManagementClient API skill. Use when working with SqlManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# SqlManagementClient
API version: 2015-05-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules/{virtualNetworkRuleName} | Gets a virtual network rule. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules/{virtualNetworkRuleName} | Creates or updates an existing virtual network rule. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules/{virtualNetworkRuleName} | Deletes the virtual network rule with the given name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules | Gets a list of virtual network rules in a server. |

## Enhanced Skill Content
## Question Mapping

- "What virtual network rules exist on my SQL server?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules
- "Show me the details of a specific VNet rule." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules/{virtualNetworkRuleName}
- "How do I restrict my SQL server to a specific subnet?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules/{virtualNetworkRuleName}
- "Create a new virtual network rule for my Azure SQL server." -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules/{virtualNetworkRuleName}
- "Update an existing VNet rule to point to a different subnet." -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules/{virtualNetworkRuleName}
- "Remove a virtual network rule from my SQL server." -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules/{virtualNetworkRuleName}
- "Is a specific subnet currently allowed to access my SQL server?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules/{virtualNetworkRuleName}
- "How many VNet rules does my server have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules
- "Delete all virtual network rules from my SQL server." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules then DELETE each
- "Replace a VNet rule so it uses a new virtual network." -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules/{virtualNetworkRuleName} then PUT with new parameters
- "Check if a VNet rule finished provisioning." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules/{virtualNetworkRuleName}
- "Lock down my SQL server to only accept traffic from my VNet." -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules/{virtualNetworkRuleName}

## Response Tips

- **GET (single rule):** Returns 200 with the rule object including `properties.virtualNetworkSubnetId` and `properties.state` (Initializing, InProgress, Ready, Deleting, Unknown). A 404 means the rule name does not exist on that server.
- **GET (list):** Returns 200 with a `value` array of rule objects. Check for a `nextLink` property to paginate through large result sets by issuing GET against that URL.
- **PUT (create/update):** Returns 200 if updated in place, 201 if newly created, or 202 if the operation is accepted but still provisioning asynchronously. On 202, poll using the GET endpoint or the `Azure-AsyncOperation` header URL.
- **DELETE:** Returns 200 if deleted immediately, 202 if deletion is in progress (async), or 204 if the rule was already gone. Treat both 200 and 204 as success.
- **Errors (all endpoints):** Expect a JSON body with `error.code` and `error.message`. Common codes: `ResourceNotFound`, `ResourceGroupNotFound`, `ServerNotFound`, `InvalidParameterValue`.

## Anomaly Flags

- **202 Accepted without completion:** Surface whenever PUT or DELETE returns 202. The operation is async and the agent should recommend polling the resource or the `Azure-AsyncOperation` URL until the state resolves.
- **State stuck in Initializing or InProgress:** If a GET on a rule returns `properties.state` other than `Ready` for an extended period, flag that provisioning may be stalled and suggest checking Azure activity logs.
- **204 on DELETE:** While technically a success (resource already absent), flag this if the user expected the rule to exist, as it may indicate a naming mismatch or prior deletion.
- **Missing api-version parameter:** All endpoints require `api-version=2015-05-01-preview`. Flag if the caller omits it or uses a different version, as behavior may differ or the request will fail.
- **Deprecated API version:** The spec uses `2015-05-01-preview`. Surface a warning that this is a preview-era version and recommend checking for newer stable API versions in Azure documentation.
- **nextLink present in list response:** If the list endpoint returns a `nextLink`, proactively notify the user that additional pages of results exist and offer to fetch them.

## Playbook

### 1. Add a subnet restriction to an Azure SQL server

1. Identify your subscription ID, resource group name, server name, and the target subnet resource ID (format: `/subscriptions/.../virtualNetworks/.../subnets/...`).
2. Choose a rule name (e.g., `allow-app-subnet`).
3. Call PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules/allow-app-subnet` with `api-version=2015-05-01-preview` and body: `{"properties": {"virtualNetworkSubnetId": "<subnet-resource-id>", "ignoreMissingVnetServiceEndpoint": false}}`.
4. If the response is 202, poll with GET on the same URL until `properties.state` is `Ready`.
5. Confirm by listing all rules with GET on `.../virtualNetworkRules` and verifying the new rule appears.

### 2. Audit all VNet rules on a SQL server

1. Call GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/virtualNetworkRules?api-version=2015-05-01-preview`.
2. Iterate through the `value` array. For each rule, note `name`, `properties.virtualNetworkSubnetId`, and `properties.state`.
3. If `nextLink` is present, issue GET against that URL and repeat until no more pages.
4. Flag any rules where `state` is not `Ready` as potentially incomplete.
5. Cross-reference subnet IDs against your known VNets to identify unexpected access paths.

### 3. Migrate a VNet rule to a new subnet

1. Call GET on the existing rule to capture its current configuration.
2. Call PUT on the same rule name with the updated `virtualNetworkSubnetId` pointing to the new subnet.
3. If the response is 202, poll with GET until `properties.state` returns to `Ready`.
4. Verify the change by calling GET and confirming the `virtualNetworkSubnetId` matches the new subnet.

### 4. Remove all VNet rules from a SQL server

1. Call GET `.../virtualNetworkRules` to list all rules. Follow `nextLink` pagination if present.
2. For each rule in the `value` array, call DELETE `.../virtualNetworkRules/{ruleName}`.
3. Handle 202 responses by tracking async deletions. Handle 204 as already-deleted.
4. After all DELETE calls complete, call GET on the list endpoint again to confirm `value` is empty.
5. Note: removing all VNet rules does not by itself open the server to public access -- check the server's firewall rules and "Allow Azure services" setting separately.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
