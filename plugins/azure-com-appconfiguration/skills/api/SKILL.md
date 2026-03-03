---
name: appconfigurationmanagementclient
description: "AppConfigurationManagementClient API skill. Use when working with AppConfigurationManagementClient for subscriptions, providers. Covers 17 endpoints."
version: 1.0.0
generator: lapsh
---

# AppConfigurationManagementClient
API version: 2019-11-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.AppConfiguration/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.AppConfiguration/checkNameAvailability -- create first checkNameAvailability

## Endpoints

17 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.AppConfiguration/configurationStores | Lists the configuration stores for a given subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores | Lists the configuration stores for a given resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName} | Gets the properties of the specified configuration store. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName} | Creates a configuration store with the specified parameters. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName} | Deletes a configuration store. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName} | Updates a configuration store with the specified parameters. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.AppConfiguration/checkNameAvailability | Checks whether the configuration store name is available for use. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/ListKeys | Lists the access key for the specified configuration store. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/RegenerateKey | Regenerates an access key for the specified configuration store. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/listKeyValue | Lists a configuration store key-value. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/privateEndpointConnections | Lists all private endpoint connections for a configuration store. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/privateEndpointConnections/{privateEndpointConnectionName} | Gets the specified private endpoint connection associated with the configuration store. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/privateEndpointConnections/{privateEndpointConnectionName} | Update the state of the specified private endpoint connection associated with the configuration store. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/privateEndpointConnections/{privateEndpointConnectionName} | Deletes a private endpoint connection. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/privateLinkResources | Gets the private link resources that need to be created for a configuration store. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/privateLinkResources/{groupName} | Gets a private link resource that need to be created for a configuration store. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.AppConfiguration/operations | Lists the operations available from this provider. |

## Enhanced Skill Content
## Question Mapping

- "List all my App Configuration stores?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.AppConfiguration/configurationStores
- "What config stores exist in a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores
- "Get details for a specific configuration store?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}
- "Create a new App Configuration store?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}
- "Update an existing configuration store's settings?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}
- "Delete a configuration store?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}
- "Is this configuration store name available?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.AppConfiguration/checkNameAvailability
- "List access keys for a config store?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/ListKeys
- "Rotate or regenerate an access key?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/RegenerateKey
- "Retrieve a specific key-value from a store?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/listKeyValue
- "List private endpoint connections for a store?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/privateEndpointConnections
- "Approve or reject a private endpoint connection?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/privateEndpointConnections/{privateEndpointConnectionName}
- "Remove a private endpoint connection?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/privateEndpointConnections/{privateEndpointConnectionName}
- "What private link resources are available for my store?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.AppConfiguration/configurationStores/{configStoreName}/privateLinkResources
- "What operations does the App Configuration resource provider support?" -> GET /providers/Microsoft.AppConfiguration/operations

## Response Tips

- **Store listings** (GET .../configurationStores): Returns a paginated array with `nextLink`; follow `$skipToken` from `nextLink` query param until absent to retrieve all stores.
- **Store CRUD** (PUT/PATCH): 200 means completed synchronously, 201 means the resource was created; PATCH may also return 201 if the update triggers recreation -- check `provisioningState` in the response body.
- **Async deletes** (DELETE): 200 = done, 202 = accepted for async deletion (poll the `Location` or `Azure-AsyncOperation` header), 204 = resource already gone (idempotent, not an error).
- **Key listings** (ListKeys): Paginated with `$skipToken`; each key object contains `id`, `name`, `value`, `connectionString`, `readOnly`, and timestamps.
- **Private endpoint connections**: The `privateLinkServiceConnectionState` nested object holds `status` (Pending/Approved/Rejected/Disconnected), `description`, and `actionsRequired`.
- **Error responses**: All endpoints return an `error` object with `code` and `message` fields on failure; common codes include `ResourceNotFound`, `NameNotAvailable`, and `ConflictError`.

## Anomaly Flags

- **Provisioning stuck**: If a store's `provisioningState` is not `Succeeded` after creation or update, surface this -- it may be `Creating`, `Updating`, `Deleting`, or `Failed`.
- **202 on delete without completion**: When DELETE returns 202, flag that the operation is async and the caller should poll until completion before assuming the resource is gone.
- **Name unavailability**: If `checkNameAvailability` returns `nameAvailable: false`, surface the `reason` field (e.g., `AlreadyExists` vs `Invalid`) and the `message` explaining why.
- **Soft-delete conflict**: Creating a store may fail if a soft-deleted store with the same name exists; flag `ConflictError` responses and suggest purging the deleted resource.
- **Private endpoint pending approval**: When listing private endpoint connections, flag any with `status: Pending` -- these require explicit approval via PUT before they become functional.
- **Key regeneration impact**: After `RegenerateKey`, flag that all clients using the old key value will lose access immediately; recommend rotating one key at a time.
- **Pagination truncation**: If a list response includes `nextLink` but the caller did not follow it, warn that results are incomplete.

## Playbook

### 1. Provision a New Configuration Store

1. Call POST `.../checkNameAvailability` with `{ "name": "<desired-name>", "type": "Microsoft.AppConfiguration/configurationStores" }` to verify the name is free.
2. If `nameAvailable` is `true`, call PUT `.../configurationStores/{configStoreName}` with `configStoreCreationParameters` including `location`, `sku` (e.g., `{ "name": "Standard" }`), and optional `tags`.
3. Check the response: 201 means created, 200 means it already existed and was updated.
4. Verify `provisioningState` is `Succeeded`; if not, poll the GET endpoint until it resolves.
5. Call POST `.../ListKeys` to retrieve access keys and connection strings for application use.

### 2. Rotate Access Keys Without Downtime

1. Call POST `.../ListKeys` to list all current access keys (typically a primary and secondary pair, each with read-write and read-only variants).
2. Update all application configurations to use the secondary key's connection string.
3. Call POST `.../RegenerateKey` with `{ "id": "<primary-key-id>" }` to regenerate the primary key.
4. Verify the new primary key by calling `.../ListKeys` again.
5. Optionally update applications back to the new primary key, keeping secondary as fallback.

### 3. Set Up Private Endpoint Access

1. Call GET `.../privateLinkResources` to discover available group IDs (typically `configurationStores`).
2. Create a private endpoint in your VNet via the Networking resource provider, targeting the App Configuration store's resource ID and the group ID from step 1.
3. Call GET `.../privateEndpointConnections` to find the new connection in `Pending` status.
4. Call PUT `.../privateEndpointConnections/{name}` with `privateLinkServiceConnectionState.status` set to `Approved` and a `description`.
5. Verify the connection status changes to `Approved` by calling GET on the specific connection.

### 4. Clean Up a Configuration Store and Its Private Endpoints

1. Call GET `.../privateEndpointConnections` to list all connections.
2. For each connection, call DELETE `.../privateEndpointConnections/{name}` and handle 202 (async) by polling until 200 or 204.
3. Once all private endpoints are removed, call DELETE `.../configurationStores/{configStoreName}`.
4. If 202 is returned, poll the store's GET endpoint until it returns 404, confirming deletion.

### 5. Audit Configuration Stores Across a Subscription

1. Call GET `.../configurationStores` (subscription-level) to list all stores; follow `$skipToken` pagination until all results are collected.
2. For each store, note `provisioningState`, `sku`, `creationDate`, `endpoint`, and `encryption` settings.
3. For each store, call GET `.../privateEndpointConnections` to check network isolation status.
4. Flag any stores with `provisioningState` != `Succeeded`, stores on the Free SKU in production, or stores without private endpoints in regulated environments.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
