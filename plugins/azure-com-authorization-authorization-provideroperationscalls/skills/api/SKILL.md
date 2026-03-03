---
name: authorizationmanagementclient
description: "AuthorizationManagementClient API skill. Use when working with AuthorizationManagementClient for providers. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# AuthorizationManagementClient
API version: 2018-01-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Authorization/providerOperations -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Authorization/providerOperations/{resourceProviderNamespace} | Gets provider operations metadata for the specified resource provider. |
| GET | /providers/Microsoft.Authorization/providerOperations | Gets provider operations metadata for all resource providers. |

## Enhanced Skill Content
## Question Mapping

- "What operations does a specific Azure resource provider support?" -> GET /providers/Microsoft.Authorization/providerOperations/{resourceProviderNamespace}
- "List all available provider operations in Azure" -> GET /providers/Microsoft.Authorization/providerOperations
- "What permissions are available for Microsoft.Compute?" -> GET /providers/Microsoft.Authorization/providerOperations/Microsoft.Compute
- "Show me the full operation details for a provider namespace" -> GET /providers/Microsoft.Authorization/providerOperations/{resourceProviderNamespace} (with $expand=resourceTypes)
- "What RBAC operations exist across all Azure providers?" -> GET /providers/Microsoft.Authorization/providerOperations
- "Which actions can I assign in a custom role for Microsoft.Storage?" -> GET /providers/Microsoft.Authorization/providerOperations/Microsoft.Storage
- "Get expanded operation metadata for all providers" -> GET /providers/Microsoft.Authorization/providerOperations (with $expand)
- "What data actions does Microsoft.KeyVault expose?" -> GET /providers/Microsoft.Authorization/providerOperations/Microsoft.KeyVault
- "How do I discover which permissions to grant for a custom RBAC role?" -> GET /providers/Microsoft.Authorization/providerOperations then GET /providers/Microsoft.Authorization/providerOperations/{resourceProviderNamespace}
- "List operations without expanding nested resource types" -> GET /providers/Microsoft.Authorization/providerOperations (omit $expand)
- "What is the full permission tree for Microsoft.Network?" -> GET /providers/Microsoft.Authorization/providerOperations/Microsoft.Network (with $expand=resourceTypes)
- "Compare operations between two resource providers" -> GET /providers/Microsoft.Authorization/providerOperations/{resourceProviderNamespace} (call twice with different namespaces)

## Response Tips

- **Single provider operations**: Response contains a `name`, `displayName`, and nested `resourceTypes` array -- each resource type lists its own `operations` with `name`, `displayName`, `description`, and `isDataAction` fields. Use `$expand=resourceTypes` to populate the nested tree.
- **All provider operations**: Returns a `value` array of provider operation objects. No pagination on this endpoint -- the full list is returned in one call. Each entry follows the same nested structure as the single-provider response.
- **Errors**: Expect `CloudError` responses with `error.code` and `error.message`. Common codes: `AuthorizationFailed` (403), `InvalidResourceNamespace` (404 for unknown providers), `AuthenticationFailed` (401 for bad/expired OAuth token).

## Anomaly Flags

- **Unknown namespace**: If querying a specific provider returns 404, surface that the resource provider namespace may be misspelled or not registered in the subscription.
- **Empty resourceTypes**: If `$expand` is omitted or the response returns empty `resourceTypes` arrays, warn the user that operation details are collapsed -- suggest re-querying with `$expand=resourceTypes`.
- **Auth failures**: Surface 401/403 errors immediately -- the OAuth2 token may be expired, or the caller may lack `Microsoft.Authorization/providerOperations/read` permission.
- **API version mismatch**: This spec uses `2018-01-01-preview`. If Azure returns `InvalidApiVersionParameter`, flag that a newer api-version may be required and suggest checking current Azure docs.
- **Throttling**: Azure Management API enforces per-subscription rate limits. If 429 responses appear, surface the `Retry-After` header value and pause before retrying.

## Playbook

### 1. Discover All Permissions for a Custom RBAC Role

1. Call GET `/providers/Microsoft.Authorization/providerOperations` to retrieve the full list of resource providers.
2. Identify the target provider namespace(s) from the `value` array (e.g., `Microsoft.Compute`).
3. Call GET `/providers/Microsoft.Authorization/providerOperations/Microsoft.Compute` with `$expand=resourceTypes`.
4. Iterate through `resourceTypes` and their `operations` to find the specific action strings (e.g., `Microsoft.Compute/virtualMachines/read`).
5. Use these action strings in your custom role definition's `Actions` or `DataActions` array.

### 2. Audit Data Actions for a Specific Provider

1. Call GET `/providers/Microsoft.Authorization/providerOperations/{namespace}` with `$expand=resourceTypes`.
2. Flatten all operations across all `resourceTypes` in the response.
3. Filter for entries where `isDataAction` is `true`.
4. Review these data actions -- they represent operations on data within the resource (e.g., blob reads) rather than management plane operations.

### 3. Compare Permissions Between Two Providers

1. Call GET `/providers/Microsoft.Authorization/providerOperations/Microsoft.Storage` with `$expand=resourceTypes`.
2. Call GET `/providers/Microsoft.Authorization/providerOperations/Microsoft.KeyVault` with `$expand=resourceTypes`.
3. Extract and flatten the operation names from both responses.
4. Compare the two lists to understand the permission surface of each provider and identify any overlapping patterns.

### 4. Validate a Role Definition's Actions

1. Parse the existing role definition to extract all `Actions` and `DataActions` strings.
2. For each unique provider namespace in those strings, call GET `/providers/Microsoft.Authorization/providerOperations/{namespace}` with `$expand=resourceTypes`.
3. Build a set of all valid operation names from the responses.
4. Cross-reference the role's action strings against the valid set -- flag any that do not match (indicating typos, deprecated actions, or removed operations).


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
