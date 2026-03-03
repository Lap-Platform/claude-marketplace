---
name: subscriptionsmanagementclient
description: "SubscriptionsManagementClient API skill. Use when working with SubscriptionsManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionsManagementClient
API version: 2015-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants | Lists all the directory tenants under the current subscription and given resource group name. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant} | Get a directory tenant by name. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant} | Delete a directory tenant under a resource group. |
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant} | Create or updates a directory tenant. |

## Enhanced Skill Content
## Question Mapping

- "What directory tenants are configured for this subscription?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants
- "List all tenants in resource group {resourceGroupName}." -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants
- "Get details for tenant {tenant}." -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant}
- "Does tenant {tenant} exist in this subscription?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant}
- "Remove directory tenant {tenant}." -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant}
- "Delete a tenant that is no longer needed." -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant}
- "Register a new directory tenant." -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant}
- "Update the configuration of tenant {tenant}." -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant}
- "Add an Azure AD tenant to the subscription admin." -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant}
- "Replace the tenant definition for {tenant} with new settings." -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant}
- "How many directory tenants are associated with resource group {resourceGroupName}?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants
- "Verify a tenant exists before deleting it." -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant} then DELETE

## Response Tips

- **List (GET collection):** Response is typically a JSON object with a `value` array of tenant objects; check for a `nextLink` property for pagination and follow it until absent.
- **Get single (GET by tenant):** Returns the full tenant resource object on 200; a 404 means the tenant does not exist in that resource group.
- **Delete:** 200 means the tenant was deleted; 204 means it was already absent (idempotent) -- both are success states, do not treat 204 as an error.
- **Put (create/update):** 200 indicates an existing tenant was updated; 201 indicates a new tenant was created -- inspect the status code to distinguish upsert behavior.

## Anomaly Flags

- **DELETE returning 200 vs 204:** Surface which code was returned so the user knows whether the tenant actually existed before the call.
- **PUT returning 201 on expected update:** If the caller intended to update an existing tenant but receives 201, flag that a new resource was created unexpectedly -- the tenant name may have been misspelled.
- **Missing `nextLink` awareness:** If the list endpoint returns a `nextLink` and the agent stops at the first page, warn the user that results are incomplete.
- **OAuth2 token expiry:** If any call returns 401, proactively surface that the OAuth2 token may have expired and suggest re-authentication before retrying.
- **Throttling (429):** Azure ARM APIs enforce rate limits; if a 429 is received, surface the `Retry-After` header value and pause before retrying.
- **Deprecated API version:** The spec uses version `2015-11-01`; flag if Azure returns a warning header indicating a newer API version is available.

## Playbook

### 1. Register a New Directory Tenant

1. Confirm the target `subscriptionId` and `resourceGroupName`.
2. Prepare the `tenantDefinition` map with required properties (e.g., tenant domain, directory ID).
3. Call PUT `/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant}` with the definition in the request body.
4. Check the response: 201 confirms creation, 200 means a tenant with that name already existed and was updated.
5. Call GET on the same tenant path to verify the stored configuration matches intent.

### 2. Audit All Directory Tenants in a Resource Group

1. Call GET `/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants`.
2. Collect the `value` array from the response.
3. If a `nextLink` is present, follow it repeatedly until no more pages remain.
4. For each tenant, inspect properties for compliance (e.g., expected domains, valid configurations).
5. Report any tenants that are unrecognized or misconfigured.

### 3. Safely Remove a Directory Tenant

1. Call GET `/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant}` to confirm the tenant exists and review its properties.
2. Verify this is the correct tenant to remove (check domain, directory ID).
3. Call DELETE on the same path.
4. If 200 is returned, the tenant was deleted. If 204, it was already gone.
5. Call GET on the tenant path again to confirm it returns 404 (no longer exists).

### 4. Update an Existing Tenant Configuration

1. Call GET `/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant}` to retrieve the current definition.
2. Modify the desired fields in the tenant definition map.
3. Call PUT with the full updated `tenantDefinition` in the request body.
4. Confirm 200 is returned (update, not 201 which would indicate accidental creation under a different name).
5. Call GET to verify the update took effect.

### 5. Verify Tenant Existence Before Acting

1. Call GET `/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/directoryTenants/{tenant}`.
2. If 200, the tenant exists -- proceed with the intended operation (update, delete, or reference).
3. If 404, the tenant does not exist -- decide whether to create it (PUT) or abort.
4. This check prevents accidental creation via PUT when the intent was to update only.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
