---
name: fabricadminclient
description: "FabricAdminClient API skill. Use when working with FabricAdminClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# FabricAdminClient
API version: 2016-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Fabric.Admin/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Fabric.Admin/operations | Returns the list of support REST operations. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available in Fabric Admin?" -> GET /providers/Microsoft.Fabric.Admin/operations
- "List all supported Fabric Admin API operations" -> GET /providers/Microsoft.Fabric.Admin/operations
- "What can I do with the Fabric Admin API?" -> GET /providers/Microsoft.Fabric.Admin/operations
- "Show me the resource provider operations for Microsoft Fabric" -> GET /providers/Microsoft.Fabric.Admin/operations
- "What permissions or actions exist for Fabric Admin resources?" -> GET /providers/Microsoft.Fabric.Admin/operations
- "Which RBAC operations does Fabric Admin expose?" -> GET /providers/Microsoft.Fabric.Admin/operations
- "Get the operation manifest for Fabric Admin" -> GET /providers/Microsoft.Fabric.Admin/operations
- "What API version does Fabric Admin support?" -> GET /providers/Microsoft.Fabric.Admin/operations (check api-version param)
- "How do I discover Fabric Admin capabilities programmatically?" -> GET /providers/Microsoft.Fabric.Admin/operations
- "List operations available for role assignment scoping in Fabric" -> GET /providers/Microsoft.Fabric.Admin/operations
- "What actions can I grant in an Azure RBAC role for Fabric Admin?" -> GET /providers/Microsoft.Fabric.Admin/operations
- "Does Fabric Admin support any write or delete operations?" -> GET /providers/Microsoft.Fabric.Admin/operations (filter response for non-read actions)

## Response Tips

- **Operations listing**: Returns an array of operation objects, each with `name` (e.g., `Microsoft.Fabric.Admin/operations/read`), `display` (localized description block with `provider`, `resource`, `operation`, `description`), and optionally `isDataAction`. Paginated via `nextLink` -- follow it until absent. Always pass `api-version=2016-05-01` as a query parameter or the call will 400.

## Anomaly Flags

- **Missing api-version parameter**: The `api-version` query param is required on every call. If omitted, Azure returns a 400 with a misleading error. Always include `api-version=2016-05-01`.
- **Empty operations list**: If the response contains zero operations, the resource provider may not be registered in the subscription. Surface this and suggest running `az provider register --namespace Microsoft.Fabric.Admin`.
- **401/403 responses**: OAuth2 token may be expired or lack sufficient scope. Surface the specific `code` field from the Azure error body (e.g., `AuthorizationFailed`, `InvalidAuthenticationToken`).
- **404 on provider path**: The resource provider namespace is case-sensitive. Flag if the user accidentally uses lowercase or a typo like `Microsoft.fabric.admin`.
- **Deprecation signals**: Watch for `x-ms-deprecation` headers or operations marked with `isDeprecated` in the response body. Surface these immediately since the 2016-05-01 API version is old.
- **Throttling (429)**: Azure ARM applies per-subscription rate limits. If `Retry-After` header appears, surface the wait time and suggest backing off.

## Playbook

### 1. Discover All Fabric Admin Operations

1. Authenticate and obtain an OAuth2 bearer token with scope `https://management.azure.com/.default`
2. Call `GET https://management.azure.com/providers/Microsoft.Fabric.Admin/operations?api-version=2016-05-01`
3. Parse the `value` array from the response
4. If `nextLink` is present, follow it to retrieve additional pages
5. Compile the full list of operation `name` fields for use in RBAC definitions or documentation

### 2. Build a Custom RBAC Role for Fabric Admin

1. Retrieve all operations using the playbook above
2. Filter operations by `isDataAction` to separate control-plane from data-plane actions
3. Select the specific operation `name` values needed for the role (e.g., `Microsoft.Fabric.Admin/*/read`)
4. Use the Azure Role Definitions API (`PUT /subscriptions/{id}/providers/Microsoft.Authorization/roleDefinitions/{roleId}`) to create a custom role with the selected `actions` and `dataActions`
5. Assign the role to users or service principals via the Role Assignments API

### 3. Validate Resource Provider Registration

1. Call `GET https://management.azure.com/providers/Microsoft.Fabric.Admin/operations?api-version=2016-05-01`
2. If the response is 200 with an empty `value` array, or returns 404, the provider may not be registered
3. Check registration: `GET https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Fabric.Admin?api-version=2016-05-01`
4. If `registrationState` is not `Registered`, register it: `POST https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Fabric.Admin/register?api-version=2016-05-01`
5. Poll the registration state until it transitions to `Registered`, then retry the operations call

### 4. Audit Available Actions for Compliance

1. Retrieve all operations using Playbook 1
2. Separate read, write, delete, and action operations by parsing the operation `name` suffix (e.g., `/read`, `/write`, `/delete`, `/action`)
3. Cross-reference against your organization's allowed-actions policy
4. Flag any write or delete operations that are not explicitly approved
5. Document findings and feed into your governance tooling or policy-as-code definitions


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
