---
name: deploymentadminclient
description: "DeploymentAdminClient API skill. Use when working with DeploymentAdminClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# DeploymentAdminClient
API version: 2019-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Deployment.Admin/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Deployment.Admin/operations | Returns the list of supported REST operations. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available in the Deployment Admin API?" -> GET /providers/Microsoft.Deployment.Admin/operations
- "List all supported operations for Microsoft.Deployment.Admin" -> GET /providers/Microsoft.Deployment.Admin/operations
- "What can I do with the Azure Deployment Admin resource provider?" -> GET /providers/Microsoft.Deployment.Admin/operations
- "Which CRUD actions does the Deployment Admin provider expose?" -> GET /providers/Microsoft.Deployment.Admin/operations
- "What permissions or actions exist under Microsoft.Deployment.Admin?" -> GET /providers/Microsoft.Deployment.Admin/operations
- "Show me the available ARM operations for deployment administration" -> GET /providers/Microsoft.Deployment.Admin/operations
- "What API version should I use for Deployment Admin operations?" -> GET /providers/Microsoft.Deployment.Admin/operations (check api-version param)
- "Are there any write operations available in the Deployment Admin provider?" -> GET /providers/Microsoft.Deployment.Admin/operations (filter results for write actions)
- "How do I discover what resources the Deployment Admin provider manages?" -> GET /providers/Microsoft.Deployment.Admin/operations
- "What display names are associated with Deployment Admin operations?" -> GET /providers/Microsoft.Deployment.Admin/operations (inspect display property in response)
- "Is there a delete or remove capability in the Deployment Admin API?" -> GET /providers/Microsoft.Deployment.Admin/operations (scan for DELETE actions)
- "What role-based access control actions map to this provider?" -> GET /providers/Microsoft.Deployment.Admin/operations (check operation names for RBAC mapping)

## Response Tips

- **Operations list**: Returns an array under `value[]`; each entry has `name` (resource provider action string like `Microsoft.Deployment.Admin/*/read`), `display` (nested object with `provider`, `resource`, `operation`, `description`), and optionally `isDataAction`. Always pass `api-version=2019-01-01` or the call will 400.

## Anomaly Flags

- **Missing api-version parameter**: The endpoint requires `api-version` as a query parameter. Omitting it returns a 400 error -- surface this immediately if the user forgets it.
- **Empty operations list**: If `value[]` comes back empty, flag that the resource provider may not be registered in the current subscription. Suggest running `az provider register --namespace Microsoft.Deployment.Admin`.
- **Unexpected 404**: Indicates the Deployment Admin resource provider is not available in the target Azure Stack environment. Surface this with a note that this API is Azure Stack Hub-specific, not public Azure.
- **Authentication scope mismatch**: OAuth2 tokens scoped to `https://management.azure.com` are required. If a 401 is returned, flag that the token audience may be wrong (common when switching between Azure public and Azure Stack endpoints).
- **API version drift**: The spec pins `2019-01-01`. If Azure returns an error suggesting a newer version, surface the mismatch and recommend checking for updated specs.

## Playbook

### 1. Discover All Available Operations

1. Authenticate and obtain an OAuth2 bearer token scoped to `https://management.azure.com`
2. Call `GET /providers/Microsoft.Deployment.Admin/operations?api-version=2019-01-01`
3. Parse the `value[]` array from the response
4. Each entry's `name` field contains the full operation identifier (e.g., `Microsoft.Deployment.Admin/locations/read`)
5. Use the `display.description` field to understand what each operation does

### 2. Check for Write or Destructive Operations

1. Retrieve the full operations list (see Playbook 1)
2. Filter results where `name` contains `/write` or `/delete`
3. Cross-reference with `isDataAction` to distinguish control-plane vs data-plane actions
4. Use this filtered list to understand what modifications the API allows before assigning RBAC roles

### 3. Validate Resource Provider Registration

1. Call `GET /providers/Microsoft.Deployment.Admin/operations?api-version=2019-01-01`
2. If the response is 404 or the `value[]` array is empty, the provider may be unregistered
3. Register it: `POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/register?api-version=2019-01-01`
4. Wait 30-60 seconds, then retry the operations call to confirm registration succeeded

### 4. Audit RBAC Permissions Against Available Operations

1. Retrieve all operations (see Playbook 1)
2. Extract each `name` field to get the full list of action strings
3. Compare against role definitions assigned to target users/service principals using `GET /providers/Microsoft.Authorization/roleDefinitions`
4. Identify any gaps where operations exist but the principal lacks the matching action permission
5. Surface unmatched operations as potential access issues


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
