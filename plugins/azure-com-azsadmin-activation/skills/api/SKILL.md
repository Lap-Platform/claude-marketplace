---
name: azurebridgeadminclient
description: "AzureBridgeAdminClient API skill. Use when working with AzureBridgeAdminClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# AzureBridgeAdminClient
API version: 2016-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations | Returns the list of activations. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName} | Returns activation name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName} | Create a new activation. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName} | Delete an activation. |

## Enhanced Skill Content
## Question Mapping

- "What activations exist in my resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations
- "List all Azure Bridge activations for subscription X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations
- "Get details for a specific activation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}
- "What is the status of activation Y?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}
- "Create a new Azure Bridge activation?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}
- "Update an existing activation's configuration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}
- "Register a new Azure Bridge activation in my resource group?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}
- "Remove an activation from my resource group?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}
- "Delete activation Y and confirm it is gone?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName} then GET the same resource
- "How many activations do I have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations
- "Does activation X already exist before I create it?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}
- "Replace an activation's configuration entirely?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AzureBridge.Admin/activations/{activationName}

## Response Tips

- **List activations (GET collection):** Response is a JSON object with a `value` array; check for `nextLink` property for pagination across large sets.
- **Get single activation (GET by name):** Returns the full activation resource object including `properties`, `id`, `name`, `type`, and `location` fields.
- **Create/Update activation (PUT):** Returns 200 with the created or updated resource; the `activation` body parameter is a map -- include all required properties. No 201 distinction, so check the response body to confirm state.
- **Delete activation (DELETE):** Returns 200 on successful deletion or 204 if the resource was already absent -- both indicate a safe terminal state. A 404 may occur if the resource never existed.

## Anomaly Flags

- **DELETE returning 204 vs 200:** Surface this distinction -- 204 means the activation was already gone (idempotent delete), which may indicate a race condition or prior cleanup.
- **PUT with incomplete activation map:** The `activation` parameter is required as a map; flag any request missing this body or sending an empty object.
- **API version pinned to 2016-01-01:** This is a legacy API version. Flag if the user expects newer Azure Stack Hub features that may require a more recent api-version query parameter.
- **OAuth2 token expiry:** Surface proactively when tokens are near expiration; Azure AD tokens typically last 60-90 minutes.
- **Missing resource group or subscription:** Flag early if path parameters are empty or malformed -- Azure Resource Manager returns opaque 400 errors for these.
- **Throttling (429 responses):** Azure ARM applies per-subscription rate limits; surface `Retry-After` header values when encountered.

## Playbook

### 1. Register a New Azure Bridge Activation

1. Confirm the target subscription ID and resource group name are correct
2. GET the activations list to verify the desired activation name is not already taken
3. PUT to `/activations/{activationName}` with the `activation` map containing required properties (display name, Azure Stack registration resource ID)
4. Verify the 200 response and inspect the returned resource's `properties.provisioningState`

### 2. Audit All Activations in a Resource Group

1. GET the activations collection for the target resource group
2. If `nextLink` is present in the response, follow it to retrieve subsequent pages
3. For each activation, note the `properties.provisioningState` and `properties.displayName`
4. Flag any activations with unexpected states (e.g., `Failed`, `Deleting`)

### 3. Safely Remove an Activation

1. GET the specific activation by name to confirm it exists and capture its current state
2. DELETE the activation by name
3. If response is 200, deletion succeeded; if 204, it was already absent
4. GET the activation again to confirm a 404, verifying full removal

### 4. Update an Existing Activation

1. GET the current activation by name to retrieve its full resource body
2. Modify the desired fields in the `activation` map (PUT is a full replace, not a patch)
3. PUT the updated activation body back to the same endpoint
4. Compare the response resource against your intended changes to confirm the update applied

### 5. Verify Connectivity and Permissions

1. GET the activations list with your OAuth2 token to confirm basic read access
2. If you receive 401, re-authenticate and obtain a fresh token scoped to the subscription
3. If you receive 403, verify your Azure RBAC role includes `Microsoft.AzureBridge.Admin/activations/read`
4. Attempt a GET on a known activation name to confirm resource-level access


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
