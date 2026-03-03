---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for providers. Covers 1 endpoint."
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
2. GET /providers/Microsoft.Insights/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Insights/operations | Lists all of the available insights REST API operations. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available in Application Insights?" -> GET /providers/Microsoft.Insights/operations
- "List all supported management operations for Azure Monitor Insights" -> GET /providers/Microsoft.Insights/operations
- "What actions can I perform on Application Insights resources?" -> GET /providers/Microsoft.Insights/operations
- "Which RBAC permissions exist for Microsoft.Insights?" -> GET /providers/Microsoft.Insights/operations
- "Show me the resource provider operations for Insights" -> GET /providers/Microsoft.Insights/operations
- "What write operations does Application Insights support?" -> GET /providers/Microsoft.Insights/operations (filter client-side by operation name containing `/write`)
- "Can I check if a specific operation is supported before calling it?" -> GET /providers/Microsoft.Insights/operations (search result list for target operation)
- "What read-only operations are available for Insights resources?" -> GET /providers/Microsoft.Insights/operations (filter for `/read` operations)
- "List delete operations available on Insights components" -> GET /providers/Microsoft.Insights/operations (filter for `/delete` operations)
- "How do I discover what API actions my Azure role can perform on Insights?" -> GET /providers/Microsoft.Insights/operations (cross-reference with role assignments)
- "What operations require special permissions in Application Insights?" -> GET /providers/Microsoft.Insights/operations (inspect `isDataAction` field)
- "Show all data-plane vs control-plane operations for Insights" -> GET /providers/Microsoft.Insights/operations (group by `isDataAction` boolean)

## Response Tips

- **Operations list**: Response contains a `value` array of operation objects, each with `name` (e.g., `Microsoft.Insights/components/read`), `display` (localized descriptions), and optional `isDataAction` flag. No pagination -- all operations return in a single response. If a `nextLink` field appears, follow it for additional pages (future-proofing).

## Anomaly Flags

- **OAuth2 token expiry**: Surface warnings when the bearer token is within 5 minutes of expiration; Azure tokens typically last 60-90 minutes.
- **Empty operations list**: If `value` is an empty array, flag that the API version may be deprecated or the resource provider is not registered in the subscription.
- **Unexpected HTTP status codes**: Surface `401` (token invalid/expired), `403` (insufficient tenant permissions), and `429` (throttled) immediately with remediation steps.
- **API version drift**: If the response includes operations not documented for `2015-05-01`, flag that a newer API version may be available.
- **Missing display metadata**: If any operation lacks `display.description`, flag it as potentially undocumented or preview-only.

## Playbook

### 1. Discover All Available Insights Operations

1. Authenticate via OAuth2 to obtain a bearer token for the Azure management scope (`https://management.azure.com/.default`).
2. Call `GET /providers/Microsoft.Insights/operations` with header `Authorization: Bearer <token>`.
3. Parse the `value` array from the response.
4. Group operations by resource type (extract from `name` field, e.g., `Microsoft.Insights/components`).
5. Present grouped operations with their `display.operation` and `display.description`.

### 2. Audit RBAC Coverage for a Custom Role

1. Call `GET /providers/Microsoft.Insights/operations` to retrieve the full operations list.
2. Retrieve the target custom role definition via the Azure RBAC API.
3. Compare the role's `actions` and `dataActions` arrays against the operations list.
4. Flag any operations in the role that no longer appear in the provider (stale permissions).
5. Flag any new operations not covered by the role (potential gaps).

### 3. Check if a Specific Operation Exists Before Use

1. Call `GET /providers/Microsoft.Insights/operations`.
2. Search the `value` array for an entry where `name` matches the target operation string (e.g., `Microsoft.Insights/components/write`).
3. If found, confirm the operation is supported and review its `display` metadata.
4. If not found, the operation may require a different API version -- retry with a newer `api-version` parameter.

### 4. Monitor for API Changes Over Time

1. Call `GET /providers/Microsoft.Insights/operations` and store the full response as a baseline snapshot.
2. Schedule periodic re-fetches (daily or weekly).
3. Diff each new response against the baseline: flag added operations (new capabilities), removed operations (breaking changes), and modified display metadata.
4. Alert on removals, as these may indicate deprecated functionality that your application depends on.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
