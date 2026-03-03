---
name: workbookclient
description: "WorkbookClient API skill. Use when working with WorkbookClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# WorkbookClient
API version: 2018-06-17-preview

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

- "What operations are available in Azure Insights?" -> GET /providers/Microsoft.Insights/operations
- "List all supported actions for the Workbook API" -> GET /providers/Microsoft.Insights/operations
- "What can I do with Microsoft.Insights resources?" -> GET /providers/Microsoft.Insights/operations
- "Show me the available resource provider operations" -> GET /providers/Microsoft.Insights/operations
- "Which CRUD operations does the Insights provider support?" -> GET /providers/Microsoft.Insights/operations
- "What permissions do I need for Insights workbooks?" -> GET /providers/Microsoft.Insights/operations
- "List operations to build RBAC role definitions for Insights" -> GET /providers/Microsoft.Insights/operations
- "What write operations exist for workbook resources?" -> GET /providers/Microsoft.Insights/operations
- "Are there any preview operations in Microsoft.Insights?" -> GET /providers/Microsoft.Insights/operations
- "What delete operations can I perform on Insights resources?" -> GET /providers/Microsoft.Insights/operations
- "How do I discover the API surface for Azure Monitor workbooks?" -> GET /providers/Microsoft.Insights/operations
- "Which operations require special permissions in Insights?" -> GET /providers/Microsoft.Insights/operations

## Response Tips

- **Operations list**: Response contains a `value` array of operation objects, each with `name` (e.g., `Microsoft.Insights/workbooks/write`), `display` (localized description with `provider`, `resource`, `operation`, `description` fields), and optional `isDataAction` boolean. Filter by name prefix to narrow to specific resource types like `workbooks` or `components`.

## Anomaly Flags

- **Missing operations**: If the `value` array is empty or significantly smaller than expected (~50+ operations for Insights), the provider may be experiencing issues or the API version may be outdated.
- **401/403 responses**: OAuth2 token may be expired or lack the `user_impersonation` scope required for Azure Management API calls.
- **Deprecated API version**: The spec uses `2018-06-17-preview` -- a preview version from 2018. Surface a warning that a newer stable API version likely exists and the caller should consider upgrading.
- **429 throttling**: Azure Management API enforces per-subscription rate limits. Surface `Retry-After` header value when present.
- **Preview-only operations**: Flag any operations in the response with `isDataAction: true` or names containing `preview`, as these may have limited SLA guarantees.

## Playbook

### 1. Discover Available Workbook Operations

1. Authenticate with Azure AD to obtain an OAuth2 bearer token with `https://management.azure.com/.default` scope.
2. Call `GET /providers/Microsoft.Insights/operations` with `api-version=2018-06-17-preview`.
3. Parse the `value` array from the response.
4. Filter entries where `name` starts with `Microsoft.Insights/workbooks` to isolate workbook-specific operations.
5. Review each operation's `display.operation` field for a human-readable action description.

### 2. Build a Custom RBAC Role for Workbooks

1. Call `GET /providers/Microsoft.Insights/operations` to retrieve the full operations list.
2. Filter to operations matching the desired resource type (e.g., `Microsoft.Insights/workbooks/*`).
3. Separate read operations (`*/read`) from write (`*/write`) and delete (`*/delete`).
4. Use the filtered operation `name` values as `actions` or `dataActions` in an Azure role definition.
5. Validate that no required dependent operations (e.g., `Microsoft.Insights/components/read`) are missing.

### 3. Audit API Surface Changes

1. Call `GET /providers/Microsoft.Insights/operations` and store the full response.
2. Compare the current `value` array against a previously stored baseline.
3. Identify new operations (added since last check) and missing operations (potentially deprecated).
4. Flag any operations where `isDataAction` changed, as this affects RBAC assignments.
5. Update the stored baseline and log changes for review.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
