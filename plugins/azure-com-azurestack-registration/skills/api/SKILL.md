---
name: azure-stack-azure-bridge-client
description: "Azure Stack Azure Bridge Client API skill. Use when working with Azure Stack Azure Bridge Client for subscriptions. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# Azure Stack Azure Bridge Client
API version: 2017-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/getactivationkey -- create first getactivationkey

## Endpoints

8 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations | Returns a list of all registrations. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.AzureStack/registrations | Returns a list of all registrations under current subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName} | Returns the properties of an Azure Stack registration. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName} | Delete the requested Azure Stack registration. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName} | Create or update an Azure Stack registration. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName} | Patch an Azure Stack registration. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/getactivationkey | Returns Azure Stack Activation Key. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/enableRemoteManagement | Enables remote management for device under the Azure Stack registration. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all Azure Stack registrations in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations
- "Show me all Azure Stack registrations across my entire subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AzureStack/registrations
- "Get details for a specific Azure Stack registration" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}
- "How do I register a new Azure Stack environment?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}
- "How do I update an existing Azure Stack registration?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}
- "How do I remove an Azure Stack registration?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}
- "How do I get the activation key for my Azure Stack registration?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/getactivationkey
- "How do I enable remote management on my Azure Stack?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/enableRemoteManagement
- "Does a specific Azure Stack registration exist in my resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}
- "How do I rotate or refresh the registration token for Azure Stack?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}
- "How do I migrate an Azure Stack registration to a different resource group?" -> PUT (create new) + DELETE (remove old)
- "What registrations exist and which resource groups are they in?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AzureStack/registrations
- "How do I set up Azure Stack from scratch including activation?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName} then POST .../getactivationkey

## Response Tips

- **List endpoints (GET .../registrations):** Response is an Azure ARM list with `value` array and optional `nextLink` for pagination. Iterate `nextLink` until null to retrieve all results.
- **Single resource (GET .../registrations/{name}):** Returns a standard ARM resource object with `id`, `name`, `type`, `location`, and `properties`. A 404 means the registration does not exist.
- **Create/Update (PUT, PATCH):** PUT returns 200 (updated) or 201 (created). PATCH returns 200 only. Both require a `token` map in the request body. Check `properties.provisioningState` for async operation status.
- **Delete (DELETE):** Returns 200 (deleted) or 204 (already gone). Both are success -- do not treat 204 as an error.
- **Action endpoints (POST .../getactivationkey, .../enableRemoteManagement):** Return 200 with operation-specific payloads. The activation key response contains the key string needed for on-premises setup.

## Anomaly Flags

- **204 on DELETE:** Registration was already removed or never existed. Surface this so the user knows the resource was not found rather than assuming a successful deletion of an existing resource.
- **Missing nextLink awareness:** If listing registrations returns a `nextLink` but the caller stops after the first page, flag that results are incomplete.
- **Token expiry:** The `token` map required by PUT/PATCH may contain time-bound credentials. Flag if a create or update fails with 401/403 as the token may have expired.
- **Provisioning state stuck:** After PUT/PATCH, if `properties.provisioningState` is not `Succeeded` after a reasonable interval, surface the stalled state.
- **API version mismatch:** This spec targets `2017-06-01`. If Azure returns errors about unsupported API versions, flag that a newer `api-version` query parameter may be required.
- **Rate limiting (429):** Azure ARM enforces throttling. Surface `Retry-After` header value and pause before retrying.

## Playbook

### 1. Register a New Azure Stack Environment

1. Confirm the target subscription ID and resource group name (create the resource group first if needed).
2. PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}` with the required `token` map in the body.
3. Check the response: 201 means created, 200 means an existing registration was updated.
4. Verify `properties.provisioningState` equals `Succeeded`.
5. POST `.../getactivationkey` to retrieve the activation key for on-premises configuration.

### 2. Retrieve the Activation Key for On-Premises Setup

1. GET the registration to confirm it exists and is in a healthy state.
2. POST `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/getactivationkey`.
3. Extract the activation key from the response body.
4. Use this key in the on-premises Azure Stack setup wizard.

### 3. Enable Remote Management

1. GET the registration to confirm it exists and note its current properties.
2. POST `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/enableRemoteManagement`.
3. Verify a 200 response confirming remote management is enabled.
4. Test remote connectivity to the Azure Stack environment.

### 4. Audit All Registrations Across a Subscription

1. GET `/subscriptions/{subscriptionId}/providers/Microsoft.AzureStack/registrations` to list all registrations subscription-wide.
2. Follow `nextLink` pagination until all results are collected.
3. For each registration, note the resource group, location, and provisioning state.
4. Flag any registrations with non-`Succeeded` provisioning states for investigation.

### 5. Decommission an Azure Stack Registration

1. GET the specific registration to confirm its name and properties.
2. Record any dependent resources or configurations that reference this registration.
3. DELETE `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}`.
4. Confirm 200 (deleted) or 204 (already removed).
5. Verify removal by attempting a GET on the same path -- expect 404.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
