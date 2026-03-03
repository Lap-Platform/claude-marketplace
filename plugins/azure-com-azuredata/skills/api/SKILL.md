---
name: azuredatamanagementclient
description: "AzureDataManagementClient API skill. Use when working with AzureDataManagementClient for providers, subscriptions. Covers 11 endpoints."
version: 1.0.0
generator: lapsh
---

# AzureDataManagementClient
API version: 2017-03-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.AzureData/operations -- verify access

## Endpoints

11 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.AzureData/operations | Lists all of the available SQL Server Registration API operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName} | Gets a SQL Server registration. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName} | Creates or updates a SQL Server registration. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName} | Deletes a SQL Server registration. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName} | Updates SQL Server Registration tags. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations | Gets all SQL Server registrations in a resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.AzureData/sqlServerRegistrations | Gets all SQL Server registrations in a subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName}/sqlServers/{sqlServerName} | Gets a SQL Server. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName}/sqlServers/{sqlServerName} | Creates or updates a SQL Server. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName}/sqlServers/{sqlServerName} | Deletes a SQL Server. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName}/sqlServers | Gets all SQL Servers in a SQL Server Registration. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available in the AzureData provider?" -> GET /providers/Microsoft.AzureData/operations
- "Get details of a specific SQL Server registration?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName}
- "How do I register a new SQL Server?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName}
- "How do I remove a SQL Server registration?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName}
- "Update properties on an existing SQL Server registration?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName}
- "List all SQL Server registrations in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations
- "List all SQL Server registrations across my entire subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AzureData/sqlServerRegistrations
- "Get details of a specific SQL Server instance within a registration?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName}/sqlServers/{sqlServerName}
- "Add a SQL Server instance to an existing registration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName}/sqlServers/{sqlServerName}
- "Remove a SQL Server instance from a registration?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName}/sqlServers/{sqlServerName}
- "List all SQL Server instances under a registration?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName}/sqlServers
- "How do I see expanded details for SQL Server instances?" -> GET .../sqlServers/{sqlServerName} or .../sqlServers with `$expand` parameter
- "What SQL Servers exist across all my resource groups?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AzureData/sqlServerRegistrations (then enumerate sqlServers per registration)

## Response Tips

- **Operations (providers)**: Returns a list of available operations with `name`, `display`, and `isDataAction` fields; no pagination expected.
- **Registration CRUD (GET/PUT/PATCH)**: 200 returns the full registration resource with `id`, `name`, `type`, `location`, `tags`, and `properties`; PUT may return 201 for newly created resources.
- **Registration DELETE**: 200 means deleted successfully; 204 means the resource did not exist (already deleted) -- both are success states; do not treat 204 as an error.
- **List endpoints**: Responses include a `value` array and may include a `nextLink` property for pagination; always check `nextLink` and follow it until null.
- **SQL Server resources**: Use `$expand` query parameter to include additional nested details in GET responses; omitting it returns a compact representation.
- **Error responses**: Azure ARM errors follow `{ "error": { "code": "...", "message": "..." } }` structure; watch for `ResourceNotFound`, `ResourceGroupNotFound`, and `AuthorizationFailed`.

## Anomaly Flags

- **201 on PUT**: Surface when a PUT returns 201 instead of 200 -- this means a new resource was created rather than an existing one updated. Confirm the user intended to create, not update.
- **204 on DELETE**: Flag when DELETE returns 204 -- the resource was already absent. The caller may have a stale reference or a naming mismatch.
- **Missing nextLink traversal**: If a list response contains `nextLink` but the caller stops after the first page, warn that results are incomplete.
- **api-version mismatch**: This spec targets `2017-03-01-preview` (a preview version). Surface a warning that preview APIs may change or be deprecated without notice.
- **Empty SQL Server lists**: When a registration returns zero sqlServers, proactively note it -- the registration may be orphaned or misconfigured.
- **Authorization errors**: If any call returns 403, surface immediately -- the OAuth token may lack the `Microsoft.AzureData/*` RBAC permissions.
- **$expand ignored**: If the user requests expanded details but the response appears compact, flag that the `$expand` value may be unsupported or misspelled.

## Playbook

### 1. Register and Populate a New SQL Server Registration

1. Call PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureData/sqlServerRegistrations/{sqlServerRegistrationName}` with `parameters` containing `location` and optional `tags`.
2. Confirm a 200 (updated existing) or 201 (created new) response.
3. For each SQL Server instance to add, call PUT `.../sqlServerRegistrations/{sqlServerRegistrationName}/sqlServers/{sqlServerName}` with `parameters` specifying the server connection details.
4. Verify by calling GET `.../sqlServerRegistrations/{sqlServerRegistrationName}/sqlServers` and confirming all instances appear.

### 2. Audit All SQL Server Registrations Across a Subscription

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.AzureData/sqlServerRegistrations` to list all registrations.
2. Follow any `nextLink` values until all pages are retrieved.
3. For each registration, call GET `.../sqlServerRegistrations/{name}/sqlServers?$expand=full` to retrieve detailed SQL Server instance info.
4. Aggregate results and flag any registrations with zero SQL Servers as potentially orphaned.

### 3. Decommission a SQL Server Registration

1. Call GET `.../sqlServerRegistrations/{sqlServerRegistrationName}/sqlServers` to list all child SQL Server instances.
2. For each SQL Server instance, call DELETE `.../sqlServers/{sqlServerName}` and confirm 200 or 204.
3. Once all child servers are removed, call DELETE `.../sqlServerRegistrations/{sqlServerRegistrationName}`.
4. Verify removal by calling GET on the registration -- expect a 404 `ResourceNotFound` error.

### 4. Update Tags on a SQL Server Registration

1. Call GET `.../sqlServerRegistrations/{sqlServerRegistrationName}` to retrieve current properties and tags.
2. Call PATCH `.../sqlServerRegistrations/{sqlServerRegistrationName}` with `parameters` containing only the updated `tags` map.
3. Confirm the 200 response includes the merged tag set.
4. Note: PATCH performs a merge update -- existing tags not included in the request are preserved.

### 5. Discover Available API Operations

1. Call GET `/providers/Microsoft.AzureData/operations` to list all supported operations.
2. Review the returned operation names to understand available RBAC action strings (useful for role assignments).
3. Use these operation names when constructing custom Azure RBAC roles that need fine-grained access to AzureData resources.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
