---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 4 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodeConfigurations -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodeConfigurations/{nodeConfigurationName} | Delete the Dsc node configurations by node configuration. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodeConfigurations/{nodeConfigurationName} | Retrieve the Dsc node configurations by node configuration. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodeConfigurations/{nodeConfigurationName} | Create the node configuration identified by node configuration name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodeConfigurations | Retrieve a list of dsc node configurations. |

## Enhanced Skill Content
## Question Mapping

- "What node configurations exist in my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodeConfigurations
- "How do I filter node configurations by name?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodeConfigurations (use $filter)
- "Get details for a specific node configuration" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodeConfigurations/{nodeConfigurationName}
- "How do I create a new node configuration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodeConfigurations/{nodeConfigurationName}
- "How do I update an existing node configuration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodeConfigurations/{nodeConfigurationName}
- "Delete a node configuration from my automation account" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/nodeConfigurations/{nodeConfigurationName}
- "How many node configurations do I have?" -> GET .../nodeConfigurations (use $inlinecount=allpages)
- "Show me the first 10 node configurations" -> GET .../nodeConfigurations (use $top=10)
- "List node configurations skipping the first 5 results" -> GET .../nodeConfigurations (use $skip=5&$top=N)
- "Does a specific node configuration exist before I delete it?" -> GET .../nodeConfigurations/{nodeConfigurationName}, then DELETE if 200
- "Replace a node configuration with a new version" -> PUT .../nodeConfigurations/{nodeConfigurationName} with updated parameters body
- "Remove all node configurations matching a pattern" -> GET .../nodeConfigurations with $filter, then DELETE each result

## Response Tips

- **List endpoint (GET .../nodeConfigurations):** Returns a paged array; check for `nextLink` to retrieve additional pages. Use `$top`/`$skip` for manual pagination or `$inlinecount=allpages` to get total count in the response envelope.
- **Single resource (GET .../nodeConfigurations/{name}):** Returns the full node configuration object. A 404 means the configuration does not exist -- do not retry, verify the name.
- **Create/Update (PUT):** 200 means an existing resource was updated; 201 means a new resource was created. The response body contains the final resource state -- use it to confirm the write succeeded.
- **Delete (DELETE):** 200 confirms deletion. A subsequent GET should return 404. No response body is guaranteed.
- **Errors:** Azure ARM returns structured error objects with `error.code` and `error.message`. Common codes: `ResourceNotFound`, `ResourceGroupNotFound`, `AuthorizationFailed`.

## Anomaly Flags

- **HTTP 429 (Too Many Requests):** Azure ARM throttling hit. Surface the `Retry-After` header value and pause before retrying.
- **HTTP 409 (Conflict):** A concurrent modification occurred on the node configuration. Alert the user and suggest re-fetching before retrying the PUT.
- **201 on PUT when 200 was expected:** The resource was created rather than updated -- the prior version may have been deleted externally. Flag this discrepancy.
- **Empty list with no error:** If GET .../nodeConfigurations returns zero results, confirm the automation account name and resource group are correct before assuming no configurations exist.
- **$filter returning unexpected counts:** If a filtered list returns significantly more or fewer results than expected, surface this so the user can verify the OData filter syntax.
- **Authorization errors (403):** The OAuth2 token may lack the `Microsoft.Automation/automationAccounts/nodeConfigurations/*` permission. Surface the required RBAC role.

## Playbook

### 1. Inventory all node configurations with pagination

1. GET .../nodeConfigurations with `$inlinecount=allpages` and `$top=50`
2. Record `totalCount` from the response envelope
3. Parse the `value` array for configuration names and metadata
4. If `nextLink` is present, follow it to retrieve the next page
5. Repeat until `nextLink` is absent

### 2. Create a new node configuration

1. Confirm the target automation account exists (the account name, resource group, and subscription must all be valid)
2. PUT .../nodeConfigurations/{nodeConfigurationName} with the `parameters` body containing the DSC configuration content
3. Check for 201 (created) in the response
4. GET .../nodeConfigurations/{nodeConfigurationName} to verify the resource matches expectations

### 3. Update and verify an existing node configuration

1. GET .../nodeConfigurations/{nodeConfigurationName} to fetch the current state
2. Modify the desired fields in the parameters body
3. PUT .../nodeConfigurations/{nodeConfigurationName} with the updated parameters
4. Confirm a 200 response (not 201, which would indicate a recreate)
5. GET the resource again to confirm the changes took effect

### 4. Safely delete a node configuration

1. GET .../nodeConfigurations/{nodeConfigurationName} to confirm it exists (expect 200)
2. Record any dependent nodes or assignments referencing this configuration
3. DELETE .../nodeConfigurations/{nodeConfigurationName}
4. Confirm 200 response
5. GET the same resource to verify it returns 404

### 5. Search and filter node configurations

1. GET .../nodeConfigurations with `$filter` set to an OData expression (e.g., `contains(name,'webserver')`)
2. Optionally add `$top=10` to limit results for preview
3. Inspect the `value` array for matches
4. For each match, GET .../nodeConfigurations/{nodeConfigurationName} to retrieve full details if the list response is abbreviated


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
