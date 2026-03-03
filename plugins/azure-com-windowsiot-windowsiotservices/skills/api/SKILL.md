---
name: deviceservices
description: "DeviceServices API skill. Use when working with DeviceServices for providers, subscriptions. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# DeviceServices
API version: 2019-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.WindowsIoT/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.WindowsIoT/checkDeviceServiceNameAvailability -- create first checkDeviceServiceNameAvailability

## Endpoints

8 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.WindowsIoT/operations | Lists all of the available Windows IoT Services REST API operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsIoT/deviceServices/{deviceName} | Get the non-security related metadata of a Windows IoT Device Service. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsIoT/deviceServices/{deviceName} | Create or update the metadata of a Windows IoT Device Service. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsIoT/deviceServices/{deviceName} | Updates the metadata of a Windows IoT Device Service. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsIoT/deviceServices/{deviceName} | Delete a Windows IoT Device Service. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsIoT/deviceServices | Get all the IoT hubs in a resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.WindowsIoT/deviceServices | Get all the IoT hubs in a subscription. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.WindowsIoT/checkDeviceServiceNameAvailability | Check if a Windows IoT Device Service name is available. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Windows IoT?" -> GET /providers/Microsoft.WindowsIoT/operations
- "Get details of a specific device service" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsIoT/deviceServices/{deviceName}
- "Create a new Windows IoT device service" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsIoT/deviceServices/{deviceName}
- "Update an existing device service" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsIoT/deviceServices/{deviceName}
- "Replace a device service configuration entirely" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsIoT/deviceServices/{deviceName}
- "Delete a device service" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsIoT/deviceServices/{deviceName}
- "List all device services in a resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.WindowsIoT/deviceServices
- "List all device services in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.WindowsIoT/deviceServices
- "Check if a device service name is available" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.WindowsIoT/checkDeviceServiceNameAvailability
- "How do I provision a new IoT device with conditional creation?" -> PUT .../deviceServices/{deviceName} with If-Match header
- "Can I do a partial update on a device service without replacing it?" -> PATCH .../deviceServices/{deviceName}
- "How do I find device services across all resource groups?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.WindowsIoT/deviceServices
- "Is the name 'my-iot-hub' already taken?" -> POST .../checkDeviceServiceNameAvailability with name in body
- "How do I safely update a device service only if it hasn't changed?" -> PATCH or PUT with If-Match header set to the resource's current ETag

## Response Tips

- **Operations (providers):** Returns a list of available operations; iterate the `value` array for operation names and descriptions.
- **Device GET:** Returns a single device service resource object with `properties`, `location`, `tags`, and `etag` -- cache the `etag` for conditional updates.
- **Device PUT:** 200 means updated in place, 201 means newly created -- check status code to distinguish create vs update.
- **Device PATCH:** Always returns 200; the response body reflects the merged state after partial update.
- **Device DELETE:** 200 means successfully deleted, 204 means the resource was already gone -- both are success; do not treat 204 as an error.
- **List endpoints:** Return a `value` array with optional `nextLink` for pagination -- follow `nextLink` until null to collect all results.
- **Name availability check:** Returns a `nameAvailable` boolean and a `reason`/`message` pair when the name is taken.
- **Errors:** All endpoints may return an error object with `code` and `message` nested under `error` -- always check for this shape on non-2xx responses.

## Anomaly Flags

- **ETag mismatch (412 Precondition Failed):** Surface when a conditional PUT/PATCH fails due to a stale If-Match value -- the resource was modified by another process.
- **204 on DELETE:** Proactively note that the resource did not exist at deletion time; may indicate a race condition or stale reference.
- **Throttling (429):** Azure ARM applies per-subscription rate limits; surface retry-after headers and recommend exponential backoff.
- **Missing nextLink pagination:** If a list response has a large `value` array but no `nextLink`, flag that all results were returned in one page (unusual for large deployments).
- **Subscription/resource group not found (404):** Distinguish between "device service not found" and "resource group not found" by inspecting the error code -- surface the actual missing entity.
- **Long-running operations:** If PUT returns a 201 with an `Azure-AsyncOperation` header, surface that the resource is still provisioning and poll the operation URL.
- **Deprecated API version:** If the response includes a `x-ms-deprecation` or warning header, flag that `api-version=2019-06-01` may be nearing end-of-life.

## Playbook

### 1. Provision a New Device Service

1. Call POST `.../checkDeviceServiceNameAvailability` with the desired name to confirm it is not taken.
2. If `nameAvailable` is true, call PUT `.../deviceServices/{deviceName}` with the full `deviceService` map (location, properties, tags).
3. Check the response: 201 confirms creation; capture the returned `etag` for future updates.
4. Verify by calling GET `.../deviceServices/{deviceName}` to confirm properties match expectations.

### 2. Safe Update with Optimistic Concurrency

1. Call GET `.../deviceServices/{deviceName}` and store the `etag` from the response.
2. Call PATCH `.../deviceServices/{deviceName}` with only the changed fields, passing the stored etag in the `If-Match` header.
3. If 200, the update succeeded -- store the new `etag` from the response for subsequent updates.
4. If 412 (Precondition Failed), re-fetch the resource, merge your changes with the latest state, and retry.

### 3. Inventory All Device Services Across a Subscription

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.WindowsIoT/deviceServices` to list all device services.
2. Collect items from the `value` array.
3. If `nextLink` is present, call GET on that URL and append results.
4. Repeat until `nextLink` is null or absent.
5. Optionally group results by `resourceGroup` extracted from each resource's `id` field.

### 4. Decommission a Device Service

1. Call GET `.../deviceServices/{deviceName}` to confirm the resource exists and capture its current state for audit logging.
2. Call DELETE `.../deviceServices/{deviceName}`.
3. If 200, deletion succeeded. If 204, the resource was already absent.
4. Call GET `.../deviceServices/{deviceName}` to verify -- expect a 404 confirming removal.

### 5. Migrate a Device Service Between Resource Groups

1. Call GET on the source `.../deviceServices/{deviceName}` and save the full resource body.
2. Call DELETE on the source to remove it from the old resource group.
3. Confirm deletion (200 or 204).
4. Call PUT on the target resource group path `.../deviceServices/{deviceName}` with the saved resource body (update `location` or `tags` if needed).
5. Verify the new resource with GET and confirm the returned properties match the original.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
