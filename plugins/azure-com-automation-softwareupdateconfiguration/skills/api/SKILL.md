---
name: update-management-api
description: "Update Management API skill. Use when working with Update Management for subscriptions. Covers 4 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurations -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurations/{softwareUpdateConfigurationName} | Create a new software update configuration with the name given in the URI. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurations/{softwareUpdateConfigurationName} | Get a single software update configuration by name. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurations/{softwareUpdateConfigurationName} | delete a specific software update configuration. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurations | Get all software update configurations for the account. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new software update configuration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurations/{softwareUpdateConfigurationName}
- "How do I update an existing update configuration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurations/{softwareUpdateConfigurationName}
- "What are the details of a specific update configuration?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurations/{softwareUpdateConfigurationName}
- "How do I delete an update configuration?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurations/{softwareUpdateConfigurationName}
- "List all software update configurations for my automation account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/softwareUpdateConfigurations
- "How do I filter update configurations by OS type?" -> GET .../softwareUpdateConfigurations with $filter parameter
- "Does a specific update configuration exist?" -> GET .../softwareUpdateConfigurations/{softwareUpdateConfigurationName} (check for 200 vs error)
- "How do I schedule recurring patch updates?" -> PUT .../softwareUpdateConfigurations/{softwareUpdateConfigurationName} with schedule in parameters
- "How do I remove a configuration that is no longer needed?" -> DELETE .../softwareUpdateConfigurations/{softwareUpdateConfigurationName}
- "How do I replace a configuration with different settings?" -> PUT .../softwareUpdateConfigurations/{softwareUpdateConfigurationName} (PUT replaces the full resource)
- "What update configurations exist in a resource group?" -> GET .../softwareUpdateConfigurations (list all, then inspect)
- "How do I set up update management for Linux VMs?" -> PUT .../softwareUpdateConfigurations/{name} with OS-specific parameters map
- "How do I verify a configuration was created successfully?" -> PUT returns 200 (updated) or 201 (created); follow with GET to confirm

## Response Tips

- **Create/Update (PUT):** 200 means the configuration was updated in place; 201 means a new configuration was created -- check the status code to distinguish between create and update operations. The response body contains the full resource representation.
- **Get (GET single):** 200 returns the full configuration object including schedule, update properties, and provisioning state. Non-existent names return an error, not an empty body.
- **Delete (DELETE):** 200 means the resource was deleted; 204 means it was already gone or the delete was accepted with no content -- both are success cases, treat them identically.
- **List (GET collection):** 200 returns an array of configurations. Use the `$filter` OData parameter to narrow results server-side rather than filtering client-side. Watch for `nextLink` in paginated responses.

## Anomaly Flags

- **201 on PUT when 200 was expected:** The agent should flag when a PUT returns 201 (created) if the caller intended to update an existing configuration -- this indicates the named resource did not previously exist.
- **204 on DELETE:** Surface when a delete returns 204 instead of 200, as it may indicate the resource was already removed by another process or concurrent operation.
- **Empty list results:** If a list call returns zero configurations, flag this proactively -- the automation account may not be set up correctly, or the filter may be too restrictive.
- **OAuth token expiry:** Since this API uses OAuth2, surface warnings when tokens are nearing expiration before making mutating calls (PUT/DELETE) to avoid partial failures.
- **Preview API version:** This uses `2017-05-15-preview` -- flag that this is a preview version and may have breaking changes. Recommend checking for GA versions.
- **$filter syntax errors:** OData filter expressions that return unexpected results or errors should be surfaced with the raw filter string for debugging.

## Playbook

### 1. Create a New Software Update Configuration

1. Determine the target automation account path: subscription ID, resource group, and automation account name.
2. Choose a descriptive `softwareUpdateConfigurationName` (must be unique within the account).
3. Build the `parameters` map with update properties (OS type, included/excluded patches, schedule, target VMs).
4. Call PUT `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.Automation/automationAccounts/{account}/softwareUpdateConfigurations/{name}` with the parameters body.
5. Confirm a 201 response (created). Store the configuration name for future reference.
6. Call GET on the same path to verify the configuration details and provisioning state.

### 2. Audit All Update Configurations in an Account

1. Call GET `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.Automation/automationAccounts/{account}/softwareUpdateConfigurations` with no filter.
2. Iterate through the returned list and record each configuration's name, schedule, and target scope.
3. Optionally re-call with `$filter` to narrow by specific properties (e.g., OS type or provisioning state).
4. For each configuration needing detailed inspection, call GET on the individual resource path.
5. Compile findings and flag any configurations with stale schedules or missing targets.

### 3. Update and Verify a Configuration

1. Call GET on the specific configuration to retrieve its current state.
2. Modify the desired fields in the `parameters` map (e.g., change the schedule window or add VMs to the target scope).
3. Call PUT with the full updated `parameters` body (PUT is a full replace, not a patch).
4. Confirm a 200 response (updated, not 201 which would mean the old one was missing).
5. Call GET again to verify the changes took effect.

### 4. Safely Remove an Update Configuration

1. Call GET on the configuration to confirm it exists and review what it controls.
2. Verify no critical VMs depend solely on this configuration for patching.
3. Call DELETE on the configuration path.
4. Accept either 200 (deleted) or 204 (already absent) as success.
5. Call GET on the same path to confirm it now returns an error (resource not found).

### 5. Filter Configurations by Criteria

1. Identify the OData filter expression for your criteria (e.g., filter by OS type or creation date).
2. Call GET on the list endpoint with `$filter` set to your expression.
3. If the result set is empty, broaden the filter or remove it to list all configurations for comparison.
4. For each matching result, call GET on the individual path if you need full details beyond what the list returns.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
