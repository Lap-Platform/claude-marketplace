---
name: azurebridgeadminclient
description: "AzureBridgeAdminClient API skill. Use when working with AzureBridgeAdminClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# AzureBridgeAdminClient
API version: 2016-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.AzureBridge.Admin/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.AzureBridge.Admin/operations | Returns the list of support REST operations. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available in Azure Bridge Admin?" -> GET /providers/Microsoft.AzureBridge.Admin/operations
- "List all supported Azure Bridge Admin operations" -> GET /providers/Microsoft.AzureBridge.Admin/operations
- "What can I do with the Azure Bridge Admin API?" -> GET /providers/Microsoft.AzureBridge.Admin/operations
- "Show me the available resource provider operations" -> GET /providers/Microsoft.AzureBridge.Admin/operations
- "What permissions does Azure Bridge Admin expose?" -> GET /providers/Microsoft.AzureBridge.Admin/operations
- "Which RBAC operations exist for Azure Bridge?" -> GET /providers/Microsoft.AzureBridge.Admin/operations
- "Get the operation manifest for AzureBridge.Admin" -> GET /providers/Microsoft.AzureBridge.Admin/operations
- "What API version does Azure Bridge Admin support?" -> GET /providers/Microsoft.AzureBridge.Admin/operations (check api-version param)
- "List operations filtered by the 2016-01-01 API version" -> GET /providers/Microsoft.AzureBridge.Admin/operations?api-version=2016-01-01
- "Is the Azure Bridge Admin resource provider registered?" -> GET /providers/Microsoft.AzureBridge.Admin/operations (a successful response confirms registration)
- "What display names do Azure Bridge operations use?" -> GET /providers/Microsoft.AzureBridge.Admin/operations (inspect display fields in response)
- "Which Azure Bridge operations are read vs write?" -> GET /providers/Microsoft.AzureBridge.Admin/operations (check operation action types in response)

## Response Tips

- **Operations list**: Response is typically an object with a `value` array; each entry contains `name`, `display` (with `provider`, `resource`, `operation`, `description`), and optionally `isDataAction`. Always iterate `value` -- do not assume the top-level object is the list itself.
- **Pagination**: Check for a `nextLink` field in the response body; if present, follow it to retrieve additional pages.
- **Errors**: Azure ARM returns `error` objects with `code` and `message` fields. Common codes: `AuthorizationFailed` (403), `SubscriptionNotFound` (404), `InvalidApiVersionParameter` (400).
- **api-version is mandatory**: Omitting the `api-version` query parameter results in a 400 error. Always pass `2016-01-01` unless a newer version is documented.

## Anomaly Flags

- **Missing api-version parameter**: Surface immediately if a request omits `api-version` -- the call will fail with 400.
- **Empty operations list**: If `value` is an empty array, the resource provider may not be registered in this Azure Stack environment. Flag this to the user.
- **Authentication failures (401/403)**: Proactively note that OAuth2 tokens must have Azure Stack admin scope; standard Azure public cloud tokens will not work.
- **Unexpected API version errors**: If the server rejects `2016-01-01`, flag that the Azure Stack stamp may be running a different Bridge Admin version.
- **Deprecation signals**: If any operation in the response contains `deprecated` or `preview` in its name or description, surface it as a warning.
- **Rate limiting (429)**: Surface `Retry-After` header value and pause before retrying. Azure ARM typically enforces per-subscription throttling.

## Playbook

### 1. Discover Available Azure Bridge Admin Operations

1. Authenticate with OAuth2 to obtain a bearer token scoped to the Azure Stack admin endpoint
2. Call `GET /providers/Microsoft.AzureBridge.Admin/operations?api-version=2016-01-01`
3. Parse the `value` array from the response
4. For each operation, extract `name` for the programmatic identifier and `display.operation` for the human-readable description
5. If `nextLink` is present, follow it until all pages are retrieved

### 2. Verify Resource Provider Registration

1. Call `GET /providers/Microsoft.AzureBridge.Admin/operations?api-version=2016-01-01`
2. If the response is 200 with a non-empty `value` array, the provider is registered and functional
3. If the response is 404 or returns an empty `value`, the Azure Bridge Admin resource provider is not registered on this stamp
4. Recommend running `Register-AzResourceProvider -ProviderNamespace Microsoft.AzureBridge.Admin` if unregistered

### 3. Audit RBAC-Relevant Operations

1. Retrieve all operations via `GET /providers/Microsoft.AzureBridge.Admin/operations?api-version=2016-01-01`
2. Filter operations by `isDataAction` field: `true` for data-plane, `false` for management-plane
3. Group operations by `display.resource` to understand which resource types are affected
4. Cross-reference with Azure role definitions to ensure custom roles have the correct `actions` or `dataActions` entries

### 4. Troubleshoot API Connectivity

1. Attempt `GET /providers/Microsoft.AzureBridge.Admin/operations?api-version=2016-01-01` with a valid OAuth2 token
2. If 401: token is expired or not scoped to the correct Azure Stack endpoint -- re-authenticate
3. If 403: the identity lacks `Microsoft.AzureBridge.Admin/operations/read` permission -- check role assignments
4. If 400 with `InvalidApiVersionParameter`: confirm the stamp supports `2016-01-01` and adjust if needed
5. If 200 with empty `value`: the resource provider exists but exposes no operations -- verify stamp version and Bridge deployment status


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
