---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# ApplicationInsightsManagementClient
API version: 2019-10-17-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates | Get all Workbook templates defined within a specified resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName} | Get a single workbook template by its resourceName. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName} | Delete a workbook template. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName} | Create a new workbook template. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName} | Updates a workbook template that has already been added. |

## Enhanced Skill Content
## Question Mapping

- "What workbook templates exist in my resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates
- "List all workbook templates for a specific subscription and resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates
- "Get details of a specific workbook template?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName}
- "How do I inspect a workbook template's configuration?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName}
- "Delete a workbook template I no longer need?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName}
- "Remove a workbook template by name?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName}
- "Create a new workbook template?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName}
- "Replace an existing workbook template with a new definition?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName}
- "Update just a few fields on a workbook template without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName}
- "Rename or re-tag a workbook template?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName}
- "Does a specific workbook template exist before I try to create it?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName}
- "How do I clone a workbook template to a new name?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName} + PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName}
- "How do I migrate workbook templates between resource groups?" -> GET (source) + PUT (destination) across resource groups

## Response Tips

- **List (GET collection):** Returns a flat array of workbook template objects; no pagination -- results are scoped to a single resource group so the set is bounded. Check for an empty array rather than null.
- **Get single (GET by resourceName):** Returns the full template object including `properties`, `location`, `tags`, and `id`. A 404 means the template does not exist -- do not retry.
- **Create/Replace (PUT):** 200 means an existing template was updated; 201 means a new one was created. Always check the status code to confirm which occurred. The response body contains the final resource state.
- **Update (PATCH):** Returns 200 with the merged resource. Only fields included in `WorkbookTemplateUpdateParameters` are changed; omitted fields are left untouched.
- **Delete (DELETE):** 200 confirms deletion; 204 means the resource was already gone (idempotent). Do not treat 204 as an error.

## Anomaly Flags

- **Preview API version (2019-10-17-preview):** This is a preview API. Endpoints, request shapes, or behavior may change without notice. Surface a warning when users rely on it for production workflows.
- **HTTP 429 / Throttling:** Azure ARM APIs enforce per-subscription rate limits. If `Retry-After` headers appear, surface them immediately and pause further calls.
- **404 on GET single:** May indicate the resource was deleted externally or the resource name is misspelled. Prompt the user to list all templates to verify.
- **Unexpected 409 Conflict on PUT:** Another process may be modifying the same template. Surface the conflict and suggest re-fetching before retrying.
- **Missing required `workbookTemplateProperties` on PUT:** The API will reject the call. Flag if the user attempts a create/replace without providing template properties.
- **Large response payloads:** Workbook template bodies can contain embedded JSON visualizations. Warn if a response exceeds typical size, as it may indicate overly complex templates that are hard to manage.

## Playbook

### 1. Inventory All Workbook Templates in a Resource Group

1. Call GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates`
2. Parse the response array. Each entry contains `name`, `location`, `tags`, and `properties`.
3. Summarize the list by name and location for the user.
4. If the array is empty, confirm the resource group name and subscription are correct.

### 2. Create a New Workbook Template

1. Call GET on the target `{resourceName}` to check if it already exists.
2. If it exists, ask the user whether to overwrite or choose a different name.
3. Build the `workbookTemplateProperties` payload with required fields (`templateData`, `galleries`, etc.).
4. Call PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName}` with the full body.
5. Confirm success: 201 means created, 200 means replaced. Return the resource `id` to the user.

### 3. Update Tags or Metadata on an Existing Template

1. Call GET on the `{resourceName}` to fetch current state.
2. Construct a `WorkbookTemplateUpdateParameters` object containing only the fields to change (e.g., `tags`).
3. Call PATCH `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName}`.
4. Verify the 200 response reflects the intended changes.

### 4. Clone a Workbook Template to a New Name

1. Call GET on the source `{resourceName}` to retrieve the full template definition.
2. Extract `properties` from the response body.
3. Call PUT with the new `{resourceName}` and the extracted properties as `workbookTemplateProperties`.
4. Confirm 201 (created). Optionally update tags on the clone to distinguish it from the original.

### 5. Safely Delete a Workbook Template

1. Call GET on the `{resourceName}` to confirm it exists and verify it is the correct template.
2. Present the template name, location, and description to the user for confirmation.
3. On confirmation, call DELETE `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooktemplates/{resourceName}`.
4. If 200, deletion succeeded. If 204, the resource was already absent.
5. Optionally call GET on the collection to confirm the template no longer appears.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
