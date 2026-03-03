---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 5 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies | Lists all the Global Policy definitions of the Api Management service. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId} | Gets the entity state (Etag) version of the Global policy definition in the Api Management service. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId} | Get the Global policy definition of the Api Management service. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId} | Creates or updates the global policy configuration of the Api Management service. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId} | Deletes the global policy configuration of the Api Management Service. |

## Enhanced Skill Content
## Question Mapping

- "What policies are configured on my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies
- "List all global policies for service {serviceName}." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies
- "Does a specific policy exist on my APIM instance?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "Check if the global policy is set before I try to update it." -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "Show me the details of policy {policyId}." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "Get the XML content of the global policy on my API Management service." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "Create a new policy on my APIM service." -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "Update the global policy with new rate-limit rules." -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "Replace the existing policy XML with a new configuration." -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "Remove the global policy from my API Management service." -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "Delete policy {policyId} and confirm it is gone." -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "How do I set up a rate-limiting policy on my APIM instance?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}
- "I want to back up my current policy before making changes." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policies/{policyId}

## Response Tips

- **List policies (GET .../policies):** Returns a `value` array of policy contract objects; the collection is typically small (global scope), so pagination via `nextLink` is rare but should be followed if present.
- **Check existence (HEAD .../policies/{policyId}):** 200 means the policy exists; a 404 (or non-200) means it does not -- no response body is returned, only headers including `ETag`.
- **Get policy (GET .../policies/{policyId}):** The response `properties.value` contains the raw policy XML; `properties.format` indicates `xml` or `xml-link` -- always check format before parsing.
- **Create/Update (PUT .../policies/{policyId}):** 201 indicates creation, 200 indicates update of an existing policy; include `If-Match: *` header to force overwrite or use the `ETag` from a prior GET to enable optimistic concurrency.
- **Delete (DELETE .../policies/{policyId}):** 200 confirms deletion, 204 means the resource was already absent; both are success states -- do not treat 204 as an error.

## Anomaly Flags

- **ETag mismatch on PUT:** If an update returns 412 Precondition Failed, surface that someone else modified the policy since the last read -- recommend re-fetching before retrying.
- **404 on GET or DELETE:** The policy or the APIM service itself may not exist -- confirm the `serviceName`, `resourceGroupName`, and `subscriptionId` are correct before retrying.
- **Malformed policy XML in PUT body:** Azure returns 400 with a detailed error message when policy XML is invalid -- surface the `error.message` field verbatim, as it usually pinpoints the exact XML element.
- **Throttling (429):** Azure Resource Manager enforces per-subscription rate limits; if `Retry-After` header appears, surface the wait duration and pause before retrying.
- **Deprecated api-version:** If the response includes `x-ms-deprecation` headers or the error suggests using a newer version, flag that `2019-01-01` may need upgrading.
- **Missing authorization scope:** A 403 suggests the OAuth2 token lacks the required RBAC role (e.g., API Management Service Contributor) -- surface the specific permission needed.

## Playbook

### 1. Inspect the Current Global Policy

1. Call GET `.../policies` to list all policy contracts on the service.
2. Identify the target policy ID from the response (typically `policy` for global scope).
3. Call GET `.../policies/{policyId}` to retrieve the full policy XML.
4. Read `properties.value` for the raw XML content and `properties.format` for the encoding.

### 2. Safely Update a Policy with Concurrency Control

1. Call GET `.../policies/{policyId}` and capture the `ETag` header from the response.
2. Prepare the updated policy XML in the request body under `properties.value`.
3. Call PUT `.../policies/{policyId}` with the `If-Match` header set to the captured ETag.
4. If 200/201, the update succeeded. If 412, re-fetch the policy (step 1) and reapply changes.

### 3. Back Up, Modify, and Restore a Policy

1. Call GET `.../policies/{policyId}` and save the full response body (including XML) as a backup.
2. Modify the policy XML as needed (e.g., add a `<rate-limit>` element).
3. Call PUT `.../policies/{policyId}` with the modified XML.
4. Verify by calling GET `.../policies/{policyId}` again and comparing to the intended change.
5. If the change caused issues, call PUT with the original saved XML to restore.

### 4. Delete a Policy After Confirming It Exists

1. Call HEAD `.../policies/{policyId}` to confirm the policy exists (expect 200).
2. Optionally call GET to retrieve and log the policy content before deletion.
3. Call DELETE `.../policies/{policyId}`.
4. Confirm deletion by calling HEAD again -- expect a non-200 response.

### 5. Audit All Policies Across Multiple Services

1. For each APIM service in scope, call GET `.../policies` to list policies.
2. For each policy returned, call GET `.../policies/{policyId}` to retrieve the full XML.
3. Parse the XML to check for specific elements (e.g., `<ip-filter>`, `<rate-limit>`, `<cors>`).
4. Compile a summary of which services have which policy types configured.
5. Flag any services with no global policy set (empty `value` array in step 1).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
