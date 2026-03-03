---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 5 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration -- create first exportconfiguration

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration | Gets a list of Continuous Export configuration of an Application Insights component. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration | Create a Continuous Export configuration of an Application Insights component. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId} | Delete a Continuous Export configuration of an Application Insights component. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId} | Get the Continuous Export configuration for this export id. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId} | Update the Continuous Export configuration for this export id. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all continuous export configurations for my Application Insights resource?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration
- "How do I create a new continuous export for Application Insights?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration
- "How do I delete a specific export configuration?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId}
- "How do I get details of a specific export configuration by ID?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId}
- "How do I update an existing continuous export configuration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId}
- "What export configurations exist in my resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration
- "How do I change the storage account for an existing export?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId}
- "How do I stop exporting telemetry data from Application Insights?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId}
- "How do I set up telemetry export to blob storage?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration
- "How do I check if a continuous export is running or disabled?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId}
- "How do I replace the full configuration of an export?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId}
- "How do I find the exportId I need to manage a specific export?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration
- "How do I export requests and exceptions to a storage container?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration

## Response Tips

- **List/Get endpoints**: Responses return export configuration objects with fields like `ExportId`, `StorageAccountUrl`, `ContainerName`, `RecordTypes`, `IsEnabled`, and `LastSuccessTime` -- always check `IsEnabled` and `LastSuccessTime` to confirm active data flow.
- **Create (POST)**: Returns an array of created export configurations; the `ExportId` in the response is required for all subsequent GET, PUT, and DELETE calls on that export.
- **Update (PUT)**: Returns the full updated configuration; compare against your request to confirm all properties were applied since partial updates are not supported (PUT replaces the full config).
- **Delete**: Returns 200 on success with no meaningful body; a 404 means the exportId was already removed or never existed.
- **Errors**: Azure ARM returns structured error objects with `code` and `message` fields; common codes include `ResourceNotFound`, `InvalidSubscriptionId`, and `AuthorizationFailed`.

## Anomaly Flags

- **IsEnabled is false**: Surface when a retrieved export shows `IsEnabled: false` -- the export exists but is not actively sending data, which may indicate a misconfiguration or storage issue.
- **LastSuccessTime is stale**: If `LastSuccessTime` is more than a few hours old, flag that the export pipeline may be broken or the destination storage is unreachable.
- **404 on GET by exportId**: The export was deleted externally or the ID is wrong -- prompt the user to re-list all exports to discover current IDs.
- **AuthorizationFailed (403)**: The OAuth2 token lacks the `Microsoft.Insights/components/exportconfiguration/write` or `/delete` permission -- surface the required RBAC role (Contributor or Application Insights Component Contributor).
- **Multiple exports on one resource**: If listing returns several export configs, flag this since each export duplicates telemetry to a separate destination, which increases storage costs.
- **api-version mismatch**: This spec uses `2015-05-01`; if Azure returns deprecation warnings or unexpected fields, flag that a newer API version may be available.

## Playbook

### 1. Set Up a New Continuous Export to Blob Storage

1. Identify your `subscriptionId`, `resourceGroupName`, and Application Insights `resourceName`.
2. Prepare `ExportProperties` with the destination storage account SAS URL, container name, and record types (e.g., `Requests`, `Exceptions`, `CustomEvents`).
3. Call POST `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration` with the `ExportProperties` body.
4. Note the `ExportId` from the response for future management.
5. Verify by calling GET on the specific `exportId` and confirm `IsEnabled` is `true`.

### 2. Audit and Review All Active Exports

1. Call GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration` to list all exports.
2. For each returned configuration, check the `IsEnabled` and `LastSuccessTime` fields.
3. Flag any export where `IsEnabled` is `false` or `LastSuccessTime` is stale.
4. Note the `StorageAccountUrl` and `ContainerName` for each to confirm data destinations are correct and intended.

### 3. Update an Export's Destination or Record Types

1. Call GET on the specific export using its `exportId` to retrieve the current configuration.
2. Modify the `ExportProperties` map with the new storage account SAS URL, container, or record types.
3. Call PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId}` with the full updated properties.
4. Verify the response reflects your changes, paying attention to `StorageAccountUrl` and `RecordTypes`.

### 4. Decommission a Continuous Export

1. Call GET on the list endpoint to find the `ExportId` of the export to remove.
2. Confirm the export details by calling GET with the specific `exportId`.
3. Call DELETE `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/exportconfiguration/{exportId}`.
4. Verify removal by re-listing all exports and confirming the deleted ID no longer appears.

### 5. Troubleshoot a Broken Export Pipeline

1. Call GET on the specific `exportId` and inspect `IsEnabled` and `LastSuccessTime`.
2. If `IsEnabled` is `false`, call PUT with the same configuration but ensure the storage SAS URL is valid and not expired.
3. If `LastSuccessTime` is stale but `IsEnabled` is `true`, verify the destination storage account is accessible and the container exists.
4. If the export cannot be repaired, DELETE it and create a fresh export via POST with corrected properties.
5. Monitor `LastSuccessTime` on the new export after a few minutes to confirm data flow resumes.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
