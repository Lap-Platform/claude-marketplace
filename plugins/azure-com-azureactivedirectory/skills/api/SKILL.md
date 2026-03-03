---
name: azureactivedirectory
description: "azureactivedirectory API skill. Use when working with azureactivedirectory for providers. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# azureactivedirectory
API version: 2017-04-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/microsoft.aadiam/operations -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/microsoft.aadiam/operations | Operation to return the list of available operations. |
| GET | /providers/microsoft.aadiam/diagnosticSettings | Gets the active diagnostic settings list for AadIam. |
| GET | /providers/microsoft.aadiam/diagnosticSettings/{name} | Gets the active diagnostic setting for AadIam. |
| PUT | /providers/microsoft.aadiam/diagnosticSettings/{name} | Creates or updates diagnostic settings for AadIam. |
| DELETE | /providers/microsoft.aadiam/diagnosticSettings/{name} | Deletes existing diagnostic setting for AadIam. |
| GET | /providers/microsoft.aadiam/diagnosticSettingsCategories | Lists the diagnostic settings categories for AadIam. |

## Enhanced Skill Content


## Question Mapping

- "What operations are available for Azure AD diagnostic settings?" -> GET /providers/microsoft.aadiam/operations
- "List all diagnostic settings for Azure Active Directory" -> GET /providers/microsoft.aadiam/diagnosticSettings
- "Get the diagnostic setting named 'auditLogs'?" -> GET /providers/microsoft.aadiam/diagnosticSettings/{name}
- "How do I create a new diagnostic setting?" -> PUT /providers/microsoft.aadiam/diagnosticSettings/{name}
- "Update an existing diagnostic setting to send logs to a new workspace" -> PUT /providers/microsoft.aadiam/diagnosticSettings/{name}
- "Delete the diagnostic setting called 'signInLogs'?" -> DELETE /providers/microsoft.aadiam/diagnosticSettings/{name}
- "What log categories can I configure for AAD diagnostics?" -> GET /providers/microsoft.aadiam/diagnosticSettingsCategories
- "Is there a diagnostic setting already configured for audit logs?" -> GET /providers/microsoft.aadiam/diagnosticSettings then filter by name
- "How do I route Azure AD sign-in logs to a storage account?" -> PUT /providers/microsoft.aadiam/diagnosticSettings/{name} with storage account ID in parameters
- "Which diagnostic categories does Azure AD support?" -> GET /providers/microsoft.aadiam/diagnosticSettingsCategories
- "Remove all diagnostic settings?" -> GET /providers/microsoft.aadiam/diagnosticSettings then DELETE each by name
- "How do I verify my diagnostic setting was created?" -> PUT /providers/microsoft.aadiam/diagnosticSettings/{name} then GET /providers/microsoft.aadiam/diagnosticSettings/{name}
- "What API version should I use?" -> All endpoints require `api-version=2017-04-01` as a query parameter

## Response Tips

- **Operations (GET /operations)**: Returns a list of available provider operations with `name`, `display` object, and `isDataAction` flag. No pagination.
- **Diagnostic Settings (GET/PUT)**: Response wraps settings in a `value` array (list) or single resource object (by name). Each setting contains `properties` with `storageAccountId`, `workspaceId`, `eventHubAuthorizationRuleId`, and a `logs` array of category/enabled pairs.
- **DELETE**: Returns 200 on successful deletion, 204 if the resource was already absent. Both are success states -- do not treat 204 as an error.
- **Categories (GET /diagnosticSettingsCategories)**: Returns `value` array of category objects with `categoryType` indicating whether it is a log or metric.
- **Errors**: All endpoints return an `error` object with `code` and `message` on failure. Common codes: `ResourceNotFound` (404), `AuthorizationFailed` (403).

## Anomaly Flags

- **Missing api-version parameter**: All requests require `api-version=2017-04-01` as a query param. Omission returns a `NoRegisteredProviderFound` or `InvalidApiVersionParameter` error.
- **OAuth2 token expiry**: Auth is OAuth2 scoped to `https://management.azure.com`. Surface token refresh failures before they cascade into 401s on every call.
- **DELETE returning 200 vs 204**: Flag when a delete returns 204 (resource already gone) as this may indicate a race condition or stale reference.
- **Empty diagnostic settings list**: If GET returns an empty `value` array, surface this proactively -- it may mean logging is completely unconfigured for the tenant.
- **Deprecated API version**: This spec uses `2017-04-01`. If Azure returns a header like `x-ms-deprecation` or the operations endpoint lists newer versions, flag the upgrade path.
- **Misconfigured log categories**: After a PUT, if the returned `logs` array has categories set to `enabled: false` that the user intended to enable, surface the discrepancy.

## Playbook

### 1. Enable Azure AD Audit Log Forwarding to Log Analytics

1. GET /providers/microsoft.aadiam/diagnosticSettingsCategories to discover available log categories
2. PUT /providers/microsoft.aadiam/diagnosticSettings/{name} with `name` set to a descriptive label (e.g., `auditToWorkspace`) and `parameters` containing `workspaceId` and a `logs` array enabling the `AuditLogs` category
3. GET /providers/microsoft.aadiam/diagnosticSettings/{name} to confirm the setting was created with correct properties

### 2. Audit All Current Diagnostic Configurations

1. GET /providers/microsoft.aadiam/diagnosticSettings to list every configured setting
2. For each setting in the `value` array, inspect `properties.logs` to see which categories are enabled
3. Cross-reference with GET /providers/microsoft.aadiam/diagnosticSettingsCategories to identify any uncovered categories
4. Report gaps where available categories have no enabled diagnostic setting

### 3. Replace a Diagnostic Setting (Change Log Destination)

1. GET /providers/microsoft.aadiam/diagnosticSettings/{name} to retrieve the current configuration
2. Modify the `parameters` body: update `workspaceId`, `storageAccountId`, or `eventHubAuthorizationRuleId` as needed
3. PUT /providers/microsoft.aadiam/diagnosticSettings/{name} with the updated parameters (PUT is a full replace, not a patch)
4. GET /providers/microsoft.aadiam/diagnosticSettings/{name} to verify the change took effect

### 4. Clean Up All Diagnostic Settings

1. GET /providers/microsoft.aadiam/diagnosticSettings to retrieve all settings
2. For each entry in the `value` array, extract its `name`
3. DELETE /providers/microsoft.aadiam/diagnosticSettings/{name} for each setting
4. Expect 200 (deleted) or 204 (already absent) for each call -- both are success
5. GET /providers/microsoft.aadiam/diagnosticSettings to confirm the list is now empty


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
