---
name: visual-studio-resource-provider-client
description: "Visual Studio Resource Provider Client API skill. Use when working with Visual Studio Resource Provider Client for providers, subscriptions. Covers 15 endpoints."
version: 1.0.0
generator: lapsh
---

# Visual Studio Resource Provider Client
API version: 2017-11-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/microsoft.visualstudio/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/microsoft.visualstudio/checkNameAvailability -- create first checkNameAvailability

## Endpoints

15 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/microsoft.visualstudio/operations | Operations_List |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /subscriptions/{subscriptionId}/providers/microsoft.visualstudio/checkNameAvailability | Accounts_CheckNameAvailability |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account | Accounts_ListByResourceGroup |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{accountResourceName}/extension | Extensions_ListByAccount |
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{accountResourceName}/extension/{extensionResourceName} | Extensions_Create |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{accountResourceName}/extension/{extensionResourceName} | Extensions_Delete |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{accountResourceName}/extension/{extensionResourceName} | Extensions_Get |
| PATCH | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{accountResourceName}/extension/{extensionResourceName} | Extensions_Update |
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{resourceName} | Accounts_CreateOrUpdate |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{resourceName} | Accounts_Delete |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{resourceName} | Accounts_Get |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project | Projects_ListByAccountResource |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName} | Projects_Create |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName} | Projects_Get |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName} | Projects_Update |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for the Visual Studio resource provider?" -> GET /providers/microsoft.visualstudio/operations
- "Is this Visual Studio account name available?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.visualstudio/checkNameAvailability
- "List all Visual Studio accounts in my resource group?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account
- "Get details for a specific Visual Studio account?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{resourceName}
- "How do I create or update a Visual Studio account?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{resourceName}
- "How do I delete a Visual Studio account?" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{resourceName}
- "What extensions are installed on my Visual Studio account?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{accountResourceName}/extension
- "How do I install an extension on a Visual Studio account?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{accountResourceName}/extension/{extensionResourceName}
- "How do I get details for a specific extension?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{accountResourceName}/extension/{extensionResourceName}
- "How do I update an existing extension's configuration?" -> PATCH /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{accountResourceName}/extension/{extensionResourceName}
- "How do I remove an extension from a Visual Studio account?" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{accountResourceName}/extension/{extensionResourceName}
- "List all projects under a Visual Studio account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project
- "How do I create a new project in my Visual Studio account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName}
- "How do I get details for a specific project?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName}
- "How do I update an existing project's properties?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName}

## Response Tips

- **Operations (providers):** Returns a flat list of available operations; no pagination. Use to discover supported actions before scripting.
- **Accounts & Extensions:** 200 means success; 404 on GET/PUT for accounts and GET for extensions means the resource does not exist. Check the `error.code` and `error.message` fields in error responses for actionable detail.
- **Projects (PUT):** Returns 200 for immediate completion or 202 for long-running creation. On 202, check the `Location` or `Azure-AsyncOperation` header to poll for completion status.
- **Name Availability:** The 200 response body contains a boolean `nameAvailable` field and a `message` explaining why a name is unavailable -- always check both.
- **List endpoints:** Account and project list responses return arrays; extension lists are scoped to a single account. No server-side pagination is documented, so expect the full set in one response.

## Anomaly Flags

- **202 Accepted on project creation:** The operation is running asynchronously. Surface this immediately so the agent can poll for completion rather than assuming success.
- **404 on account or project GET:** The resource was deleted or never existed. Flag when this appears mid-workflow (e.g., after a PUT that returned 200) as it may indicate a race condition or propagation delay.
- **404 on account PUT:** Unlike most Azure PUT-creates, this endpoint can return 404, suggesting the resource group or subscription is invalid. Surface with a suggestion to verify the parent resources.
- **Missing api-version parameter:** Every endpoint requires `api-version`. If omitted, Azure returns a generic 400. Flag this as the likely root cause for any unexpected 400 errors.
- **Extension GET returning 404 vs list returning empty:** A 404 on a specific extension means it was never installed or was removed. An empty list means no extensions at all. Distinguish these for the user.
- **Deprecated API version (2017-11-01-preview):** This is a preview API version from 2017. Proactively warn that newer stable versions may be available and behavior may change without notice.

## Playbook

### 1. Set Up a New Visual Studio Account with Extensions

1. Call POST `/subscriptions/{subscriptionId}/providers/microsoft.visualstudio/checkNameAvailability` with the desired account name to verify availability.
2. If `nameAvailable` is true, call PUT `/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{resourceName}` with the account configuration body.
3. Confirm creation by calling GET on the same account path and verifying the returned properties.
4. Install required extensions by calling PUT `.../account/{accountResourceName}/extension/{extensionResourceName}` for each extension, passing the extension configuration body.
5. Verify installed extensions by calling GET `.../account/{accountResourceName}/extension` and confirming all expected extensions appear.

### 2. Create and Monitor a Project

1. Call PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName}` with the project body. Optionally set `validating` parameter to validate without creating.
2. If response is 200, the project is ready immediately.
3. If response is 202, extract the async operation URL from response headers and poll until the operation completes.
4. Confirm project details by calling GET on the project path.

### 3. Audit and Clean Up Extensions

1. List all extensions by calling GET `.../account/{accountResourceName}/extension`.
2. For each extension, call GET `.../extension/{extensionResourceName}` to inspect its configuration and status.
3. For unwanted extensions, call DELETE `.../extension/{extensionResourceName}`.
4. For extensions needing configuration changes, call PATCH `.../extension/{extensionResourceName}` with the updated body.

### 4. Decommission a Visual Studio Account

1. List all projects under the account by calling GET `.../account/{rootResourceName}/project` and note any active projects.
2. List all extensions by calling GET `.../account/{accountResourceName}/extension`.
3. Remove each extension by calling DELETE on each extension resource.
4. Delete the account by calling DELETE `/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{resourceName}`.
5. Verify deletion by calling GET on the account path and confirming a 404 response.

### 5. Discover Available Operations and Validate Access

1. Call GET `/providers/microsoft.visualstudio/operations` to list all supported operations.
2. Verify your subscription has access by calling GET `.../account` against a known resource group.
3. If the account list returns successfully, your OAuth token and subscription are valid for this provider.
4. If you receive a 403 or 401, check that your OAuth2 token has the required Azure RBAC role assignments for the Visual Studio resource provider.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
