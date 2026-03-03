---
name: visual-studio-projects-resource-provider-client
description: "Visual Studio Projects Resource Provider Client API skill. Use when working with Visual Studio Projects Resource Provider Client for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Visual Studio Projects Resource Provider Client
API version: 2018-08-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project | Projects_ListByAccountResource |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName} | Projects_CreateOrUpdate |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName} | Projects_Get |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName} | Projects_Update |

## Enhanced Skill Content


## Question Mapping

- "What projects exist in my Visual Studio account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project
- "How do I list all projects under a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project
- "How do I create a new Visual Studio project?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName}
- "Can I validate a project configuration before creating it?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName} (with `validating` parameter)
- "How do I get details for a specific project?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName}
- "Does a particular project exist in my account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName}
- "How do I update an existing project's properties?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName}
- "How do I rename or modify a Visual Studio project?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName}
- "How do I replace an entire project resource definition?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName}
- "What api-version should I use for Visual Studio project operations?" -> All endpoints require `api-version: 2018-08-01-preview`
- "How do I check if a project was successfully created or is still provisioning?" -> PUT returns 200 (complete) or 202 (accepted, async provisioning)
- "How do I move a project between resource groups?" -> Requires delete + recreate workflow using GET then PUT in new resource group

## Response Tips

- **List projects (GET collection):** Returns an array of project resources; always pass `api-version` as a query parameter or the call will fail.
- **Create project (PUT):** A 200 means the resource was created or already exists synchronously; a 202 means provisioning is asynchronous -- check the `Location` or `Azure-AsyncOperation` header to poll for completion.
- **Get project (GET single):** Returns the full resource object on 200; a 404 means the project does not exist under that account -- verify `resourceName` and `rootResourceName` spelling.
- **Update project (PATCH):** Returns 200 with the merged resource; only include fields you want to change in the body, unchanged fields are preserved.

## Anomaly Flags

- **202 on PUT without polling:** If a create returns 202, the agent should proactively surface the async operation URL and remind the user to poll for completion status.
- **404 on GET single project:** Surface immediately -- the project name or account name may be misspelled, or the project may have been deleted.
- **Preview API version:** `2018-08-01-preview` is a preview version; flag that behavior may change and the endpoint could be deprecated without standard lifecycle guarantees.
- **Missing api-version parameter:** All four endpoints require `api-version` -- omitting it produces an opaque error; the agent should always auto-include it.
- **Validation mode ignored:** If the user sets `validating` on PUT but still gets a 200 with a created resource, the parameter may not have taken effect -- surface this discrepancy.

## Playbook

### 1. Create a New Visual Studio Project

1. Confirm the subscription ID, resource group name, and Visual Studio account name (`rootResourceName`).
2. Choose a `resourceName` for the new project.
3. Call PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.visualstudio/account/{rootResourceName}/project/{resourceName}` with the project definition in the request body and `api-version=2018-08-01-preview`.
4. If the response is 200, the project is ready.
5. If the response is 202, extract the async operation URL from response headers and poll until provisioning completes.

### 2. Validate Before Creating

1. Build the project body as you would for creation.
2. Call PUT with the same path and body, but add the `validating` query parameter.
3. Inspect the response for validation errors or confirmation.
4. If validation passes, re-issue the PUT without the `validating` parameter to perform the actual creation.

### 3. List and Inspect Projects

1. Call GET on the collection endpoint to retrieve all projects under the account.
2. Iterate the response array and identify the project of interest.
3. Call GET on the single-project endpoint with the specific `resourceName` to retrieve full details.
4. If 404 is returned, verify the project name and account name are correct.

### 4. Update Project Properties

1. Call GET on the specific project to retrieve its current state.
2. Identify the fields that need to change.
3. Call PATCH with a body containing only the changed fields and `api-version=2018-08-01-preview`.
4. Verify the 200 response contains the expected merged resource.

### 5. Audit All Projects in a Resource Group

1. Call GET on the collection endpoint to list all projects.
2. For each project in the response, call GET on the individual project endpoint to retrieve full metadata.
3. Compare properties across projects (versioning, tags, provisioning state).
4. Flag any projects still in a provisioning or failed state for follow-up.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
