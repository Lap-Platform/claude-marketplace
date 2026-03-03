---
name: keyvaultmanagementclient
description: "KeyVaultManagementClient API skill. Use when working with KeyVaultManagementClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# KeyVaultManagementClient
API version: 2017-02-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.KeyVault.Admin/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.KeyVault.Admin/operations | Get the list of support rest operations. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available in Key Vault Admin?" -> GET /providers/Microsoft.KeyVault.Admin/operations
- "List all supported Key Vault management operations" -> GET /providers/Microsoft.KeyVault.Admin/operations
- "What actions can I perform with the Key Vault Admin provider?" -> GET /providers/Microsoft.KeyVault.Admin/operations
- "Show me the resource provider operations for Key Vault" -> GET /providers/Microsoft.KeyVault.Admin/operations
- "Which RBAC permissions exist for Key Vault Admin?" -> GET /providers/Microsoft.KeyVault.Admin/operations
- "What API version does Key Vault Admin support?" -> GET /providers/Microsoft.KeyVault.Admin/operations (use api-version=2017-02-01-preview)
- "Can I see the display names for Key Vault Admin operations?" -> GET /providers/Microsoft.KeyVault.Admin/operations
- "What write operations does Key Vault Admin expose?" -> GET /providers/Microsoft.KeyVault.Admin/operations (filter results client-side for write actions)
- "List read-only operations for Key Vault management" -> GET /providers/Microsoft.KeyVault.Admin/operations (filter results client-side for read actions)
- "What operations are available for building custom Azure roles around Key Vault?" -> GET /providers/Microsoft.KeyVault.Admin/operations
- "How do I check if a specific Key Vault action is supported?" -> GET /providers/Microsoft.KeyVault.Admin/operations (then search results for the action string)

## Response Tips

- **Operations list**: Response is a JSON object with a `value` array of operation objects. Each operation typically contains `name` (e.g., `Microsoft.KeyVault.Admin/vaults/read`), `display` (with `provider`, `resource`, `operation`, `description` fields), and `isDataAction`. Check for a `nextLink` property for pagination -- if present, follow it to retrieve additional pages.

## Anomaly Flags

- **Missing api-version parameter**: The `api-version` query parameter is required on every request. Omitting it returns a 400 error -- surface this immediately if a user forgets it.
- **Outdated API version**: This spec uses `2017-02-01-preview` (a preview version). Flag if the user is building production workloads against a preview API and suggest checking for GA versions.
- **Empty operations list**: If `value` comes back as an empty array, the resource provider may not be registered in the subscription -- surface a suggestion to run `az provider register --namespace Microsoft.KeyVault.Admin`.
- **401/403 responses**: OAuth2 token may lack sufficient scope. Surface that the caller needs at least Reader role or `Microsoft.KeyVault.Admin/operations/read` permission.
- **429 throttling**: Azure ARM APIs enforce rate limits per subscription. If a 429 is returned, surface the `Retry-After` header value and pause before retrying.

## Playbook

### 1. List All Key Vault Admin Operations

1. Authenticate and obtain an OAuth2 bearer token with Azure Resource Manager scope (`https://management.azure.com/.default`).
2. Send `GET /providers/Microsoft.KeyVault.Admin/operations?api-version=2017-02-01-preview`.
3. Parse the `value` array from the response.
4. If `nextLink` is present, send a GET to that URL and append results.
5. Each entry's `name` field is the operation identifier (e.g., `Microsoft.KeyVault.Admin/vaults/write`).

### 2. Build a Custom RBAC Role Using Available Operations

1. Call `GET /providers/Microsoft.KeyVault.Admin/operations?api-version=2017-02-01-preview` to retrieve all operations.
2. Filter results to select only the `name` values relevant to the desired role (e.g., read-only operations where `name` ends in `/read`).
3. Use the filtered operation names as `actions` in a custom role definition payload.
4. Submit the role definition via `PUT /subscriptions/{sub}/providers/Microsoft.Authorization/roleDefinitions/{roleId}`.

### 3. Verify a Specific Permission Exists

1. Call `GET /providers/Microsoft.KeyVault.Admin/operations?api-version=2017-02-01-preview`.
2. Search the `value` array for an entry whose `name` matches the target action string (e.g., `Microsoft.KeyVault.Admin/vaults/secrets/read`).
3. If found, confirm the operation is supported and note its `display.description` for documentation.
4. If not found, the action may belong to a different provider namespace (e.g., `Microsoft.KeyVault` instead of `Microsoft.KeyVault.Admin`) -- retry with that provider.

### 4. Audit Data Actions vs. Control Plane Actions

1. Retrieve all operations via `GET /providers/Microsoft.KeyVault.Admin/operations?api-version=2017-02-01-preview`.
2. Separate results into two groups based on the `isDataAction` boolean field.
3. Data actions (`isDataAction: true`) operate on vault contents (keys, secrets, certificates).
4. Control plane actions (`isDataAction: false`) manage vault resources themselves.
5. Use this separation to design least-privilege access policies.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
