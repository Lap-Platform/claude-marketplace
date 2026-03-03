---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# ApiManagementClient
API version: 2019-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates | Lists a collection of properties defined within a service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName} | Gets the entity state (Etag) version of the email template specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName} | Gets the details of the email template specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName} | Updates an Email Template. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName} | Updates the specific Email Template. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName} | Reset the Email Template to default template provided by the API Management service instance. |

## Enhanced Skill Content
## Question Mapping

- "What email templates are configured for my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates
- "List all notification templates with a specific filter?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates (use $filter)
- "Does a specific template exist in my APIM instance?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName}
- "Get the details of a specific email template?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName}
- "How do I create a new notification template?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName}
- "How do I replace an existing email template?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName}
- "How do I update just one field on a template without replacing the whole thing?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName}
- "How do I delete a custom email template?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName}
- "How do I reset a template back to its default?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName}
- "Can I check if a template was modified before updating it?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName} (check ETag)
- "How do I customize the account confirmation email?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates/{templateName} (templateName = accountClosedDeveloper, confirmSignUpIdentityDefault, etc.)
- "What templates are available to filter by name?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/templates (use $filter=name eq 'value')

## Response Tips

- **List (GET /templates):** Returns a paged collection; check `nextLink` for additional pages and iterate until absent. Each item contains `name`, `subject`, `body`, and `isDefault`.
- **Existence check (HEAD):** Returns 200 with no body if the template exists; use response headers (especially `ETag`) for conditional updates. A 404 means the template does not exist.
- **Single template (GET /templates/{name}):** Response includes `properties.subject`, `properties.body`, `properties.title`, and `properties.isDefault` indicating whether the template has been customized.
- **Create/Replace (PUT):** Returns 201 for new creation, 200 for replacement of an existing template. Always include `If-Match: *` or a specific ETag for safe updates.
- **Partial update (PATCH):** Returns 204 No Content on success -- no response body. Requires `If-Match` header with the current ETag.
- **Delete (DELETE):** Returns 200 or 204 on success. This resets the template to its built-in default rather than truly removing it.

## Anomaly Flags

- **ETag mismatch (412 Precondition Failed):** Another process modified the template since you last read it. Re-fetch and retry.
- **404 on HEAD/GET for a known template name:** The template name may be misspelled or the APIM service instance does not exist. Verify `serviceName` and `templateName` values.
- **isDefault: false on templates you expect to be stock:** Someone has customized a built-in template. Surface this when auditing template configurations.
- **$filter returning empty results:** The OData filter syntax may be malformed. Suggest the user verify the filter expression.
- **Throttling (429 Too Many Requests):** Azure ARM applies rate limits per subscription. Surface `Retry-After` header value and pause before retrying.
- **Long nextLink chains on list calls:** An unusually high number of custom templates may indicate template sprawl worth investigating.
- **201 vs 200 on PUT:** If the caller expected to update an existing template but receives 201, the template did not previously exist -- flag as a potential misconfiguration.

## Playbook

### 1. Audit All Custom Templates

1. Call GET /templates to list all templates (follow `nextLink` for pagination).
2. Filter results where `isDefault` is `false` to identify customized templates.
3. For each customized template, call GET /templates/{templateName} to review `subject` and `body`.
4. Report which templates have been modified from their defaults.

### 2. Safely Update a Template

1. Call HEAD /templates/{templateName} to confirm the template exists and capture the `ETag` header.
2. Call GET /templates/{templateName} to retrieve the current content.
3. Modify the desired fields (`subject`, `body`, etc.) in the response payload.
4. Call PUT /templates/{templateName} with the updated payload and `If-Match: {ETag}` header.
5. Verify the response is 200 (updated) and not 412 (conflict).

### 3. Reset a Template to Default

1. Call GET /templates/{templateName} to confirm the template is currently customized (`isDefault: false`).
2. Call DELETE /templates/{templateName} to remove the customization.
3. Verify response is 200 or 204.
4. Call GET /templates/{templateName} again to confirm `isDefault` is now `true`.

### 4. Bulk Customize Notification Templates

1. Call GET /templates to retrieve all available template names.
2. For each template to customize, call HEAD /templates/{templateName} to get the current `ETag`.
3. Call PUT /templates/{templateName} with the new `subject` and `body` content, including `If-Match: {ETag}`.
4. Check for 200 (replaced) or 201 (created) on each call.
5. After all updates, call GET /templates and verify each customized template shows `isDefault: false`.

### 5. Check Template Existence Before Conditional Logic

1. Call HEAD /templates/{templateName} for the target template.
2. If 200: template exists -- proceed with GET to fetch details or PATCH/PUT to modify.
3. If 404: template does not exist -- proceed with PUT to create it, or surface an error if it was expected to exist.
4. Use the `ETag` from the HEAD response in subsequent write operations to prevent race conditions.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
