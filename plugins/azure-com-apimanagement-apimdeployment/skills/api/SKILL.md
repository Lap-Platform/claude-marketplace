---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for providers, subscriptions. Covers 13 endpoints."
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
2. GET /providers/Microsoft.ApiManagement/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore -- create first restore

## Endpoints

13 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.ApiManagement/operations | Lists all of the available REST API operations of the Microsoft.ApiManagement provider. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/skus | Gets available SKUs for API Management service |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore | Restores a backup of an API Management service created using the ApiManagementService_Backup operation on the current service. This is a long running operation and could take several minutes to complete. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup | Creates a backup of the API Management service to the given Azure Storage Account. This is long running operation and could take several minutes to complete. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName} | Creates or updates an API Management service. This is long running operation and could take several minutes to complete. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName} | Updates an existing API Management service. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName} | Gets an API Management service resource description. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName} | Deletes an existing API Management service. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service | List all API Management services within a resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.ApiManagement/service | Lists all API Management services within an Azure subscription. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/getssotoken | Gets the Single-Sign-On token for the API Management Service which is valid for 5 Minutes. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.ApiManagement/checkNameAvailability | Checks availability and correctness of a name for an API Management service. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/applynetworkconfigurationupdates | Updates the Microsoft.ApiManagement resource running in the Virtual network to pick the updated network settings. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for the API Management provider?" -> GET /providers/Microsoft.ApiManagement/operations
- "What SKUs can I use for my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/skus
- "How do I restore an API Management service from a backup?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore
- "How do I back up my API Management instance?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup
- "How do I create a new API Management service?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}
- "How do I update properties on an existing API Management service?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}
- "How do I get details about a specific API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}
- "How do I delete an API Management service?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}
- "What API Management services exist in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service
- "List all API Management services in my subscription." -> GET /subscriptions/{subscriptionId}/providers/Microsoft.ApiManagement/service
- "How do I get an SSO token for my API Management service?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/getssotoken
- "Is this API Management service name available?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.ApiManagement/checkNameAvailability
- "How do I apply network configuration updates to my service?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/applynetworkconfigurationupdates
- "How do I migrate my API Management service to a different SKU tier?" -> PATCH .../{serviceName} (update the sku property)
- "How do I set up disaster recovery for API Management?" -> POST .../backup then POST .../restore on a secondary instance

## Response Tips

- **Operations (providers):** Returns a flat list of available ARM operations; use for RBAC scoping and permission audits.
- **Service CRUD (GET/PUT/PATCH/DELETE):** 200 means the operation completed synchronously; 201 means resource created; 202 means a long-running operation was accepted -- check the `Location` or `Azure-AsyncOperation` header to poll for completion.
- **List endpoints (service by resource group or subscription):** Responses are paginated via `nextLink`; keep fetching until `nextLink` is null.
- **Backup/Restore:** 202 is the expected success code for large instances; the response body contains operation status metadata, not the service itself.
- **Delete:** 204 means the resource was already gone (idempotent); 200 means it was deleted now; 202 means deletion is in progress.
- **Check Name Availability:** Returns a simple object with `nameAvailable` (boolean) and `reason`/`message` if unavailable.
- **SSO Token:** Returns a short-lived redirect URL; treat it as sensitive and do not log it.

## Anomaly Flags

- **202 without async headers:** If a long-running operation returns 202 but no `Azure-AsyncOperation` or `Location` header, surface this immediately -- polling will be impossible.
- **Repeated 429 (Too Many Requests):** Azure ARM has subscription-level throttling; surface the `Retry-After` header value and recommend backing off before retrying.
- **Backup/Restore failures:** If restore returns a non-200/202 status, flag that data loss may be at risk and recommend verifying the backup blob exists in the storage account.
- **Service stuck in transitional state:** If GET on a service shows `provisioningState` as anything other than `Succeeded` (e.g., `Updating`, `Failed`, `Stopped`), flag this proactively with the current state.
- **Name unavailability with reason `AlreadyExists`:** When checking name availability, surface whether the conflict is within the same subscription or global, and suggest alternative naming conventions.
- **Deprecated API version:** If any response includes a `Sunset` or `Deprecation` header, flag the timeline and recommend migrating to a newer api-version.
- **SKU tier mismatch:** If the user attempts operations only available on Premium tier (e.g., multi-region, VNet) on a Developer or Basic SKU, surface the incompatibility before the call fails.

## Playbook

### 1. Provision a New API Management Service

1. Check name availability: `POST /subscriptions/{subscriptionId}/providers/Microsoft.ApiManagement/checkNameAvailability` with the desired service name.
2. If available, create the service: `PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}` with SKU, location, and publisher details in the request body.
3. Poll the `Azure-AsyncOperation` URL from the 202 response until `provisioningState` is `Succeeded` (can take 30-60 minutes for non-Developer SKUs).
4. Verify the service: `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}` to confirm configuration.

### 2. Backup and Restore for Disaster Recovery

1. Back up the source service: `POST .../service/{serviceName}/backup` with a request body specifying the storage account, container name, and backup blob name.
2. Wait for the 202 async operation to complete by polling the operation URL.
3. Provision or identify the target service in the recovery region (see Playbook 1).
4. Restore to the target: `POST .../service/{targetServiceName}/restore` with the same storage account and blob details.
5. Poll until restore completes, then validate by fetching the service details with GET.

### 3. Scale or Change SKU Tier

1. Get current service details: `GET .../service/{serviceName}` to review the current SKU and capacity.
2. Check available SKUs: `GET .../service/{serviceName}/skus` to see which tiers and unit counts are valid.
3. Update the service: `PATCH .../service/{serviceName}` with the new `sku` object (name and capacity).
4. Monitor the 202 async operation -- tier changes can take significant time especially when moving to/from Consumption tier.

### 4. Audit All API Management Services Across a Subscription

1. List all services: `GET /subscriptions/{subscriptionId}/providers/Microsoft.ApiManagement/service`.
2. Follow `nextLink` pagination until all services are collected.
3. For each service, inspect `provisioningState`, `sku.name`, and `createdAtUtc` to build an inventory.
4. Optionally retrieve SSO tokens for portal access: `POST .../service/{serviceName}/getssotoken` for each service requiring direct management.

### 5. Apply Network Configuration Updates After VNet Changes

1. Verify the service is on a VNet-capable SKU (Developer or Premium) by checking `GET .../service/{serviceName}`.
2. If the VNet or subnet has been modified externally, trigger a network refresh: `POST .../service/{serviceName}/applynetworkconfigurationupdates`.
3. Poll the 202 async operation until the service re-establishes connectivity.
4. Confirm the updated configuration with `GET .../service/{serviceName}` and inspect the `virtualNetworkConfiguration` property.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
