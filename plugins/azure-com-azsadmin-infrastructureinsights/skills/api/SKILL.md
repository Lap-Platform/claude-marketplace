---
name: infrastructureinsightsmanagementclient
description: "InfrastructureInsightsManagementClient API skill. Use when working with InfrastructureInsightsManagementClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# InfrastructureInsightsManagementClient
API version: 2016-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.InfrastructureInsights.Admin/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.InfrastructureInsights.Admin/operations | Returns a list of support REST operations. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Infrastructure Insights?" -> GET /providers/Microsoft.InfrastructureInsights.Admin/operations
- "List all admin operations for Infrastructure Insights" -> GET /providers/Microsoft.InfrastructureInsights.Admin/operations
- "What can I do with the Infrastructure Insights API?" -> GET /providers/Microsoft.InfrastructureInsights.Admin/operations
- "Show available resource provider operations" -> GET /providers/Microsoft.InfrastructureInsights.Admin/operations
- "What management actions does Infrastructure Insights support?" -> GET /providers/Microsoft.InfrastructureInsights.Admin/operations
- "Which RBAC permissions map to Infrastructure Insights operations?" -> GET /providers/Microsoft.InfrastructureInsights.Admin/operations
- "Get the operation definitions for Infrastructure Insights Admin" -> GET /providers/Microsoft.InfrastructureInsights.Admin/operations
- "What API version should I use for Infrastructure Insights?" -> GET /providers/Microsoft.InfrastructureInsights.Admin/operations (check `api-version` param)
- "Does Infrastructure Insights support any write operations?" -> GET /providers/Microsoft.InfrastructureInsights.Admin/operations (filter results for PUT/POST/DELETE actions)
- "List operations I can assign in Azure RBAC for this provider" -> GET /providers/Microsoft.InfrastructureInsights.Admin/operations
- "What display names do Infrastructure Insights operations use?" -> GET /providers/Microsoft.InfrastructureInsights.Admin/operations (inspect `display` objects)

## Response Tips

- **Operations list**: Response is typically `{ value: [...] }` where each item has `name`, `display` (with `provider`, `resource`, `operation`, `description`), and optionally `isDataAction`. Check for a `nextLink` field for pagination, though this endpoint rarely paginates.

## Anomaly Flags

- **Missing `api-version` parameter**: The request will fail; always include `api-version=2016-05-01` as a query parameter.
- **401/403 responses**: OAuth2 token is missing, expired, or the principal lacks `Microsoft.InfrastructureInsights.Admin/*/read` permissions.
- **Empty `value` array**: May indicate the resource provider is not registered in the subscription or the API version is unsupported.
- **Deprecated API version**: `2016-05-01` is an older version; surface a note if Azure returns deprecation headers (`Sunset` or `x-ms-deprecation`).
- **Throttling (429)**: Azure ARM enforces rate limits; surface `Retry-After` header value when present.

## Playbook

### 1. Discover Available Operations

1. Authenticate with Azure AD to obtain an OAuth2 bearer token with `https://management.azure.com/.default` scope.
2. Call `GET https://management.azure.com/providers/Microsoft.InfrastructureInsights.Admin/operations?api-version=2016-05-01` with the token in the `Authorization` header.
3. Parse the `value` array from the response.
4. Each entry's `name` field (e.g., `Microsoft.InfrastructureInsights.Admin/alerts/read`) represents a single operation.
5. If `nextLink` is present, follow it to retrieve additional pages.

### 2. Audit RBAC Permissions for Infrastructure Insights

1. Retrieve the full operations list using the endpoint above.
2. Separate operations by `isDataAction` (true = data plane, false = management plane).
3. Cross-reference each operation `name` against your custom role definitions to verify coverage.
4. Flag any operations missing from assigned roles that your workload requires.

### 3. Validate API Connectivity and Version Support

1. Send a request to the operations endpoint with `api-version=2016-05-01`.
2. Confirm a `200` response with a non-empty `value` array.
3. Check response headers for `x-ms-request-id` to confirm the request reached ARM.
4. If you receive `400` with an invalid API version error, consult Azure docs for the current supported version and retry.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
