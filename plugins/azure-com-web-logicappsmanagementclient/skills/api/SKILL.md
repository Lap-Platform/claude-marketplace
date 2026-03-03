---
name: logicappsmanagementclient
description: "LogicAppsManagementClient API skill. Use when working with LogicAppsManagementClient for subscriptions. Covers 26 endpoints."
version: 1.0.0
generator: lapsh
---

# LogicAppsManagementClient
API version: 2016-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/connectionGateways -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/customApis/{apiName}/move -- create first move

## Endpoints

26 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/connectionGateways | Lists all of the connection gateways |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connectionGateways | Lists all of the connection gateways |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connectionGateways/{connectionGatewayName} | Gets a specific gateway |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connectionGateways/{connectionGatewayName} | Replaces a specific gateway |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connectionGateways/{connectionGatewayName} | Updates a specific gateway |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connectionGateways/{connectionGatewayName} | Deletes a specific gateway |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/connectionGatewayInstallations | Gets a list of installed gateways that the user is an admin of |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/connectionGatewayInstallations/{gatewayId} | Gets an installed gateway that the user is an admin of |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/customApis | List of custom APIs |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/customApis | List of custom APIs |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/customApis/{apiName} | Get a custom API |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/customApis/{apiName} | Replaces an existing custom API |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/customApis/{apiName} | Update an existing custom API |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/customApis/{apiName} | Delete a custom API |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/customApis/{apiName}/move | Moves the custom API |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/listWsdlInterfaces | Lists WSDL interfaces |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/extractApiDefinitionFromWsdl | Returns API definition from WSDL |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/managedApis | Lists managed APIs |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/managedApis/{apiName} | Gets managed API |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connections | Get all connections |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connections/{connectionName} | Get a connection |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connections/{connectionName} | Replace an existing connection |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connections/{connectionName} | Update an existing connection |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connections/{connectionName} | Delete an existing connection |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connections/{connectionName}/listConsentLinks | Lists consent links for a connection |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connections/{connectionName}/confirmConsentCode | Confirms the consent code for a connection |

## Enhanced Skill Content
## Question Mapping

- "What connection gateways exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/connectionGateways
- "List connection gateways in a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connectionGateways
- "Get details of a specific connection gateway?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connectionGateways/{connectionGatewayName}
- "Create or replace a connection gateway?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connectionGateways/{connectionGatewayName}
- "Update properties on an existing connection gateway?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connectionGateways/{connectionGatewayName}
- "Delete a connection gateway I no longer need?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connectionGateways/{connectionGatewayName}
- "What gateway installations are available in a region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/connectionGatewayInstallations
- "List all custom APIs across my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/customApis
- "Move a custom API to a different resource group?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/customApis/{apiName}/move
- "What managed (built-in) connectors are available in a region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/managedApis
- "List all connections in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connections
- "Generate consent links for an OAuth connection?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connections/{connectionName}/listConsentLinks
- "Confirm an OAuth consent code to activate a connection?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/connections/{connectionName}/confirmConsentCode
- "Extract an API definition from a WSDL?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/extractApiDefinitionFromWsdl
- "List WSDL interfaces for a service definition?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Web/locations/{location}/listWsdlInterfaces

## Response Tips

- **List endpoints** (gateways, custom APIs, connections): Return a `value` array of resource objects; check for `nextLink` property to handle pagination via `skiptoken`.
- **Custom APIs listing**: Supports `$top` for page size and `skiptoken` for continuation; always drain `nextLink` for complete results.
- **Connections listing**: Supports `$top` and `$filter` (OData); filter by connector type or status to reduce payload.
- **PUT (create/replace)**: Returns 200 if the resource already existed (updated) or 201 if newly created; check status code to distinguish.
- **DELETE**: Returns 200 on successful deletion or 204 if the resource was already gone; both are success cases, do not treat 204 as an error.
- **WSDL operations** (listWsdlInterfaces, extractApiDefinitionFromWsdl): Return structured definitions; the response body contains the converted OpenAPI/Swagger schema or interface list.
- **Consent link flow**: `listConsentLinks` returns URLs the user must visit in a browser; `confirmConsentCode` finalizes the OAuth handshake -- the response indicates whether the connection is now active.

## Anomaly Flags

- **204 on DELETE**: The resource was already absent. Surface this so the caller knows the delete was a no-op rather than a true removal.
- **Missing `nextLink` with full `$top` results**: If the result count equals `$top` but no `nextLink` is returned, warn that results may be truncated or the service omitted pagination metadata.
- **OAuth consent not confirmed**: If `listConsentLinks` succeeds but `confirmConsentCode` is never called or returns an error, flag that the connection will remain in a disconnected/unauthenticated state.
- **Gateway installation not found**: A 200 with an empty list from `connectionGatewayInstallations` means no on-premises gateways are registered in that region -- surface this since it blocks hybrid connectivity.
- **Stale api-version**: This spec pins `2016-06-01`. If Azure returns errors about unsupported API versions or deprecation headers (`Sunset`, `Deprecation`), alert the user to upgrade.
- **Throttling (429)**: Azure ARM endpoints enforce rate limits per subscription. Surface `Retry-After` header values and back off automatically.
- **Resource group mismatch on move**: If a custom API move returns an error, flag that the target resource group may not exist or the caller lacks permissions on it.

## Playbook

### 1. Set Up a New Custom API Connector

1. List available managed APIs in your target region to check if a built-in connector already exists: GET `.../locations/{location}/managedApis`
2. If no built-in connector fits, create the custom API: PUT `.../customApis/{apiName}` with the `customApi` body containing the Swagger/OpenAPI definition, backend service URL, and authentication settings.
3. Verify the custom API was created: GET `.../customApis/{apiName}` and confirm the response contains your configuration.
4. Create a connection that uses the custom API: PUT `.../connections/{connectionName}` referencing the custom API resource ID.
5. If the connection requires OAuth consent, call POST `.../connections/{connectionName}/listConsentLinks`, have the user visit the returned URL, then finalize with POST `.../connections/{connectionName}/confirmConsentCode`.

### 2. Register and Configure an On-Premises Data Gateway

1. List gateway installations in the target region: GET `.../locations/{location}/connectionGatewayInstallations` to find the `gatewayId` of the on-premises agent.
2. Create the gateway resource in your resource group: PUT `.../connectionGateways/{connectionGatewayName}` with the body referencing the `gatewayId` from step 1.
3. Verify registration: GET `.../connectionGateways/{connectionGatewayName}` and confirm the status is healthy.
4. Create a connection that routes through the gateway: PUT `.../connections/{connectionName}` with the gateway reference in the connection body.

### 3. Migrate a Custom API to a Different Resource Group

1. Get the current custom API details: GET `.../customApis/{apiName}` to capture the full configuration.
2. Move the custom API: POST `.../customApis/{apiName}/move` with `customApiReference` specifying the target resource group ID.
3. Verify the API is now listed in the new resource group: GET `.../resourceGroups/{newResourceGroup}/providers/Microsoft.Web/customApis`.
4. Update any connections or Logic Apps that reference the old resource path.

### 4. Import a SOAP Service as a Custom API

1. List WSDL interfaces: POST `.../locations/{location}/listWsdlInterfaces` with `wsdlDefinition` containing the WSDL URL or inline content. Review the returned interfaces and port types.
2. Extract the API definition: POST `.../locations/{location}/extractApiDefinitionFromWsdl` with the same `wsdlDefinition` plus the selected service and port. The response contains a converted Swagger definition.
3. Create a custom API using the extracted definition: PUT `.../customApis/{apiName}` with the Swagger definition from step 2 embedded in the `customApi` body.
4. Create a connection and authorize as needed (see Playbook 1, steps 4-5).

### 5. Audit and Clean Up Unused Connections

1. List all connections in the resource group: GET `.../connections` with no filter to get the full inventory.
2. For each connection, inspect its properties (status, last used) via GET `.../connections/{connectionName}`.
3. Delete unused or broken connections: DELETE `.../connections/{connectionName}`. Expect 200 (deleted) or 204 (already gone).
4. List remaining connection gateways: GET `.../connectionGateways` at the resource group level.
5. Delete orphaned gateways that no longer have associated connections: DELETE `.../connectionGateways/{connectionGatewayName}`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
