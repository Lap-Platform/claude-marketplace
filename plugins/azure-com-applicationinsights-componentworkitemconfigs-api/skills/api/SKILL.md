---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# ApplicationInsightsManagementClient
API version: 2015-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs -- create first WorkItemConfigs

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs | Gets the list work item configurations that exist for the application |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs | Create a work item configuration for an Application Insights component. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/DefaultWorkItemConfig | Gets default work item configurations that exist for the application |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs/{workItemConfigId} | Delete a work item configuration of an Application Insights component. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs/{workItemConfigId} | Gets specified work item configuration for an Application Insights component. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs/{workItemConfigId} | Update a work item configuration for an Application Insights component. |

## Enhanced Skill Content


## Question Mapping

- "What work item configurations exist for my Application Insights component?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs
- "How do I create a new work item integration for my App Insights resource?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs
- "What is the default work item configuration for my component?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/DefaultWorkItemConfig
- "How do I remove a specific work item configuration?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs/{workItemConfigId}
- "How do I get details for a specific work item config by ID?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs/{workItemConfigId}
- "How do I update an existing work item configuration?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs/{workItemConfigId}
- "Which connector is set as the default for creating work items from alerts?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/DefaultWorkItemConfig
- "How do I link Application Insights to Azure DevOps or ITSM?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs
- "How do I change the connector settings for an existing work item integration?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs/{workItemConfigId}
- "How do I disconnect a work item connector from my App Insights component?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs/{workItemConfigId}
- "Can I list all work item configs and then delete a specific one?" -> GET WorkItemConfigs (list) then DELETE WorkItemConfigs/{workItemConfigId}
- "How do I verify my work item integration is correctly configured?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/WorkItemConfigs/{workItemConfigId}

## Response Tips

- **List endpoints (GET WorkItemConfigs):** Returns an array of configuration objects; iterate over the list to extract individual `workItemConfigId` values for further operations.
- **Single resource endpoints (GET/PATCH/DELETE by ID):** Return the full configuration object on success (200); a 404 indicates the `workItemConfigId` is invalid or already deleted.
- **Create endpoint (POST):** The response includes the newly assigned `workItemConfigId`; capture this for subsequent GET/PATCH/DELETE calls.
- **Default config (GET DefaultWorkItemConfig):** May return an empty or null body if no default has been set; treat this as "no default configured" rather than an error.
- **All endpoints:** Errors follow standard Azure error format with `error.code` and `error.message` fields; check for 401 (token expired) and 403 (insufficient RBAC role).

## Anomaly Flags

- **OAuth token expiry:** Surface 401 responses immediately and prompt for token refresh before retrying.
- **Missing default config:** If GET DefaultWorkItemConfig returns empty, alert the user that no default connector is set and work item creation from alerts may not function.
- **Orphaned configs:** When listing returns configs that reference connectors or projects that no longer exist (stale `ConnectorId` or broken URLs in properties), flag for cleanup.
- **Throttling (429):** Azure Resource Manager enforces rate limits; surface `Retry-After` header values and pause before retrying.
- **API version deprecation:** This spec uses `2015-05-01`; if Azure returns warnings or `x-ms-deprecation` headers, surface them as the API version may be sunset.
- **Permission errors (403):** Flag when the caller lacks the Contributor or Owner role on the Application Insights resource, since all write operations require it.

## Playbook

### 1. Set Up a New Work Item Integration

1. Identify your `subscriptionId`, `resourceGroupName`, and Application Insights `resourceName`.
2. POST to `/WorkItemConfigs` with `WorkItemConfigurationProperties` containing connector type, project URI, and field mappings.
3. Capture the returned `workItemConfigId` from the response.
4. GET the config by ID to verify it was created correctly.
5. GET `/DefaultWorkItemConfig` to check whether this new config was set as default.

### 2. Audit and Clean Up Existing Configurations

1. GET `/WorkItemConfigs` to list all configurations for the component.
2. For each config, GET by `workItemConfigId` to inspect connector details.
3. Identify stale or unused configs (broken connector URLs, deprecated projects).
4. DELETE each unwanted config by `workItemConfigId`.
5. Re-list configs to confirm only active integrations remain.

### 3. Update a Connector's Field Mappings

1. GET `/WorkItemConfigs/{workItemConfigId}` to retrieve the current configuration.
2. Modify the `WorkItemConfigurationProperties` map with updated field mappings or connector settings.
3. PATCH `/WorkItemConfigs/{workItemConfigId}` with the updated properties.
4. GET the same config again to verify changes were applied.

### 4. Migrate Default Work Item Config

1. GET `/DefaultWorkItemConfig` to identify the current default connector.
2. POST `/WorkItemConfigs` to create a new configuration with the desired connector target.
3. PATCH the new config or set it as default through the properties map.
4. DELETE the old default config by its `workItemConfigId` if it is no longer needed.
5. GET `/DefaultWorkItemConfig` again to confirm the new default is active.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
