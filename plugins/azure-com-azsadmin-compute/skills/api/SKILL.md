---
name: compute-admin-client
description: "Compute Admin Client API skill. Use when working with Compute Admin Client for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Compute Admin Client
API version: 2015-12-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Compute.Admin/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Compute.Admin/operations | Returns the list of supported REST operations. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available in the Compute Admin API?" -> GET /providers/Microsoft.Compute.Admin/operations
- "List all supported admin operations for compute resources" -> GET /providers/Microsoft.Compute.Admin/operations
- "What can I do with the Azure Compute Admin API?" -> GET /providers/Microsoft.Compute.Admin/operations
- "Show me the available resource provider operations" -> GET /providers/Microsoft.Compute.Admin/operations
- "Which CRUD actions does the Compute Admin provider expose?" -> GET /providers/Microsoft.Compute.Admin/operations
- "What permissions or actions exist under Microsoft.Compute.Admin?" -> GET /providers/Microsoft.Compute.Admin/operations
- "How do I discover which operations are registered for this provider?" -> GET /providers/Microsoft.Compute.Admin/operations
- "Get the operation manifest for Compute Admin" -> GET /providers/Microsoft.Compute.Admin/operations
- "What Azure Resource Manager actions does this provider support?" -> GET /providers/Microsoft.Compute.Admin/operations
- "List operations I can assign in RBAC for Compute Admin" -> GET /providers/Microsoft.Compute.Admin/operations
- "Is there a read operation for compute quotas in the admin API?" -> GET /providers/Microsoft.Compute.Admin/operations (check response for matching operation)
- "What write operations are available for admin compute resources?" -> GET /providers/Microsoft.Compute.Admin/operations (filter response by `isDataAction` or operation name)

## Response Tips

- **Operations listing**: Response is typically an object with a `value` array of operation objects. Each operation includes `name` (e.g., `Microsoft.Compute.Admin/quotas/read`), `display` (localized strings for provider, resource, operation, description), and optionally `isDataAction`. No pagination expected given the small operation set, but check for a `nextLink` field if the pattern follows standard ARM conventions.

## Anomaly Flags

- **Empty operations list**: If `value` is empty or missing, the resource provider may not be registered in the subscription -- surface this with a suggestion to run `az provider register --namespace Microsoft.Compute.Admin`.
- **401/403 responses**: OAuth2 token may lack admin-level scope. Flag that this API targets Azure Stack admin endpoints, not public Azure -- the user may need operator credentials.
- **404 on the provider path**: The `2015-12-01-preview` API version is old and preview-only. Flag that this version may be deprecated or unavailable in newer Azure Stack builds.
- **Preview API version**: Always surface that `2015-12-01-preview` is a preview release -- behavior may change without notice and should not be relied on for production tooling.
- **Unexpected operation names**: If returned operations reference namespaces other than `Microsoft.Compute.Admin`, flag a possible API version mismatch.

## Playbook

### 1. Discover Available Admin Compute Operations

1. Authenticate with OAuth2 using Azure Stack operator credentials.
2. Call `GET /providers/Microsoft.Compute.Admin/operations` with `api-version=2015-12-01-preview`.
3. Parse the `value` array from the response.
4. List each operation's `name` and `display.description` for a human-readable summary.

### 2. Check If a Specific Operation Exists

1. Retrieve all operations via `GET /providers/Microsoft.Compute.Admin/operations`.
2. Filter the `value` array by `name` matching the target action (e.g., `Microsoft.Compute.Admin/quotas/write`).
3. If no match is found, inform the user the action is not supported at this API version.
4. If found, return the operation's `display` block for context on what it does.

### 3. Build an RBAC Role Definition for Compute Admin

1. Call `GET /providers/Microsoft.Compute.Admin/operations` to get the full operation list.
2. Separate operations into `Actions` (where `isDataAction` is false or absent) and `DataActions` (where `isDataAction` is true).
3. Select the subset of operations needed for the custom role.
4. Use the selected operation `name` values as entries in a custom Azure role definition JSON.
5. Apply the role definition via the Azure Stack ARM authorization API.

### 4. Validate Provider Registration and API Availability

1. Attempt `GET /providers/Microsoft.Compute.Admin/operations` with the preview API version.
2. If a 404 is returned, verify the `Microsoft.Compute.Admin` resource provider is registered by calling `GET /subscriptions/{sub}/providers/Microsoft.Compute.Admin`.
3. If unregistered, register it via `POST /subscriptions/{sub}/providers/Microsoft.Compute.Admin/register`.
4. Retry the operations call after registration completes.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
