---
name: updateadminclient
description: "UpdateAdminClient API skill. Use when working with UpdateAdminClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# UpdateAdminClient
API version: 2016-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Update.Admin/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Update.Admin/operations | Get the list of support rest operations. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Update Admin?" -> GET /providers/Microsoft.Update.Admin/operations
- "List all supported actions in the Microsoft Update Admin resource provider" -> GET /providers/Microsoft.Update.Admin/operations
- "Which API operations can I call against Azure Update Admin?" -> GET /providers/Microsoft.Update.Admin/operations
- "What permissions do I need for Update Admin operations?" -> GET /providers/Microsoft.Update.Admin/operations
- "Show me the available CRUD operations for update management" -> GET /providers/Microsoft.Update.Admin/operations
- "What REST actions does the Update Admin provider expose?" -> GET /providers/Microsoft.Update.Admin/operations
- "Can I check if a specific operation exists in Update Admin?" -> GET /providers/Microsoft.Update.Admin/operations
- "What is the latest api-version for Update Admin operations?" -> GET /providers/Microsoft.Update.Admin/operations
- "How do I discover Update Admin capabilities programmatically?" -> GET /providers/Microsoft.Update.Admin/operations
- "List operations to build RBAC role definitions for Update Admin" -> GET /providers/Microsoft.Update.Admin/operations

## Response Tips

- **Operations list**: Response contains a `value` array of operation objects, each with `name` (e.g., `Microsoft.Update.Admin/updates/read`), `display` (localized descriptions), and `isDataAction` flag. Filter by `isDataAction` to separate control-plane from data-plane operations.
- **Errors**: Azure Resource Manager returns `error.code` and `error.message` in a nested `error` object. Common codes: `InvalidApiVersionParameter`, `AuthenticationFailed`, `SubscriptionNotFound`.
- **Pagination**: If the response includes a `nextLink` property, follow it with GET to retrieve additional pages. Absence of `nextLink` means the full result set was returned.

## Anomaly Flags

- **Deprecated API version**: `2016-05-01` is legacy. Surface a warning if Azure returns `x-ms-deprecation` headers or if error messages reference newer required versions.
- **Empty operations list**: A `value` array with zero entries may indicate the resource provider is not registered in the subscription. Proactively suggest running `az provider register --namespace Microsoft.Update.Admin`.
- **Throttling**: Watch for `429 Too Many Requests` with `Retry-After` header. Azure ARM enforces per-subscription read limits (typically 12000/hour). Surface remaining quota from `x-ms-ratelimit-remaining-subscription-reads` response header.
- **Auth failures**: A `401` or `403` with code `AuthorizationFailed` should prompt checking that the OAuth2 token has the correct scope (`https://management.azure.com/.default`) and that the principal has at least Reader role on the subscription.
- **Regional availability**: If the response returns `404` with `ResourceProviderNotFound`, flag that Update Admin may not be available in the target region or subscription type.

## Playbook

### 1. Discover Available Update Admin Operations

1. Authenticate via OAuth2 to obtain a bearer token scoped to `https://management.azure.com/.default`
2. Call `GET /providers/Microsoft.Update.Admin/operations?api-version=2016-05-01`
3. Parse the `value` array from the response
4. For each operation, note the `name` field (e.g., `Microsoft.Update.Admin/updates/read`) for use in RBAC definitions

### 2. Build a Custom RBAC Role for Update Admin

1. Retrieve all operations using `GET /providers/Microsoft.Update.Admin/operations?api-version=2016-05-01`
2. Filter the `value` array to identify the specific `name` values you need (read, write, delete, action)
3. Use the filtered operation names as `Actions` or `DataActions` in an Azure role definition
4. Create the custom role via `PUT /subscriptions/{id}/providers/Microsoft.Authorization/roleDefinitions/{roleId}`

### 3. Verify Resource Provider Registration

1. Call `GET /providers/Microsoft.Update.Admin/operations?api-version=2016-05-01`
2. If the response returns an empty `value` array or a `404`, the provider may not be registered
3. Register the provider: `POST /subscriptions/{id}/providers/Microsoft.Update.Admin/register?api-version=2016-05-01`
4. Re-call the operations endpoint to confirm registration succeeded and operations are now listed

### 4. Handle API Version Migration

1. Call `GET /providers/Microsoft.Update.Admin/operations?api-version=2016-05-01`
2. Inspect response headers for `x-ms-deprecation` or warning indicators
3. If deprecated, query the provider metadata to discover newer supported api-versions
4. Re-issue the operations call with the updated `api-version` parameter
5. Compare old and new operation lists to identify added or removed capabilities


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
