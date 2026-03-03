---
name: gallerymanagementclient
description: "GalleryManagementClient API skill. Use when working with GalleryManagementClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# GalleryManagementClient
API version: 2015-04-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Gallery.Admin/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Gallery.Admin/operations | Gets the available gallery admin operations. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available in the Gallery Management API?" -> GET /providers/Microsoft.Gallery.Admin/operations
- "List all supported admin operations for Azure Gallery" -> GET /providers/Microsoft.Gallery.Admin/operations
- "What can I do with the Gallery Admin provider?" -> GET /providers/Microsoft.Gallery.Admin/operations
- "Show me the resource provider operations for Gallery" -> GET /providers/Microsoft.Gallery.Admin/operations
- "What permissions or actions exist for Microsoft.Gallery.Admin?" -> GET /providers/Microsoft.Gallery.Admin/operations
- "Which RBAC operations does the Gallery Admin provider expose?" -> GET /providers/Microsoft.Gallery.Admin/operations
- "How do I discover available API actions before making calls?" -> GET /providers/Microsoft.Gallery.Admin/operations
- "What operations can I assign in role definitions for Gallery?" -> GET /providers/Microsoft.Gallery.Admin/operations
- "List the display names and descriptions of Gallery admin actions" -> GET /providers/Microsoft.Gallery.Admin/operations
- "Are there any write or delete operations available for Gallery Admin?" -> GET /providers/Microsoft.Gallery.Admin/operations

## Response Tips

- **Operations listing**: Response contains a `value` array of operation objects, each with `name` (e.g., `Microsoft.Gallery.Admin/artifacts/read`), `display.provider`, `display.resource`, `display.operation`, and `display.description`. Check for a `nextLink` property for pagination, though this single-resource endpoint rarely paginates.

## Anomaly Flags

- **Empty operations list**: If `value` returns an empty array, the Gallery Admin resource provider may not be registered in the subscription -- surface a suggestion to run `az provider register --namespace Microsoft.Gallery.Admin`.
- **401/403 responses**: OAuth2 token may lack sufficient scope or the caller may not have Reader role on the subscription. Flag with remediation steps.
- **404 response**: The resource provider namespace may have changed or been deprecated in newer API versions (this spec targets 2015-04-01). Surface a warning that this is a legacy API version.
- **Deprecated API version**: 2015-04-01 is dated. Proactively note when newer api-versions are available for Azure Gallery management.
- **Throttling (429)**: Azure ARM applies per-subscription rate limits. Surface `Retry-After` header value and recommend exponential backoff.

## Playbook

### 1. Discover Available Gallery Admin Operations

1. Authenticate with Azure AD to obtain an OAuth2 bearer token with `https://management.azure.com/.default` scope
2. Call `GET /providers/Microsoft.Gallery.Admin/operations?api-version=2015-04-01`
3. Parse the `value` array from the response
4. Each entry's `name` field gives the fully qualified operation ID (used in RBAC role definitions)
5. Use `display.operation` and `display.description` for human-readable summaries

### 2. Build a Custom RBAC Role for Gallery Admin

1. Call `GET /providers/Microsoft.Gallery.Admin/operations` to retrieve all available actions
2. Filter the returned operations by type (read, write, delete) based on the `name` suffix
3. Select the subset of operations needed for the custom role
4. Use the operation `name` values as `actions` in an Azure role definition
5. Create the custom role via the Azure RBAC API with the selected permissions

### 3. Audit Permissions Against Available Operations

1. Call `GET /providers/Microsoft.Gallery.Admin/operations` to get the full operation list
2. Retrieve current role assignments for the target principal via Azure RBAC APIs
3. Compare assigned permissions against the full operations list
4. Flag any overly broad wildcards (e.g., `Microsoft.Gallery.Admin/*`) as potential security concerns
5. Report any missing operations that the principal needs but lacks


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
