---
name: cosmos-db
description: "Cosmos DB API skill. Use when working with Cosmos DB for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Cosmos DB
API version: 2019-08-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections | List all private endpoint connections on a Cosmos DB account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName} | Gets a private endpoint connection. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName} | Approve or reject a private endpoint connection with a given name. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName} | Deletes a private endpoint connection with a given name. |

## Enhanced Skill Content
## Question Mapping

- "What private endpoint connections exist for my Cosmos DB account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections
- "Show me details of a specific private endpoint connection" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName}
- "How do I create a private endpoint connection for Cosmos DB?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName}
- "Update the approval status of a private endpoint connection" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName}
- "How do I approve a pending private endpoint connection?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName}
- "Reject a private endpoint connection request" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName}
- "Remove a private endpoint connection from my Cosmos DB account" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName}
- "Is my Cosmos DB account using private endpoints?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections
- "What is the provisioning state of a private endpoint connection?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName}
- "How do I lock down my Cosmos DB to only allow private network access?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName}
- "List all pending private endpoint approval requests" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections
- "Delete a rejected private endpoint connection" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName}

## Response Tips

- **List endpoints (GET collection):** Returns a `value` array of connection objects; check for empty arrays meaning no private endpoints are configured. No pagination in this API version.
- **Get single connection (GET by name):** Returns the full connection resource including `properties.privateLinkServiceConnectionState` with `status` (Approved/Pending/Rejected/Disconnected) and `actionsRequired` fields.
- **Create/Update (PUT):** Returns 200 for synchronous completion or 202 for async; on 202 check the `Azure-AsyncOperation` header URL to poll for provisioning status.
- **Delete (DELETE):** Returns 202 for async deletion in progress or 204 if the resource was already gone; poll the async operation header on 202.

## Anomaly Flags

- **202 Accepted without completion:** PUT and DELETE operations may return 202, indicating a long-running operation. Surface the `Azure-AsyncOperation` or `Location` header and remind the user to poll for final status.
- **Preview API version:** This spec uses `2019-08-01-preview`. Flag that this is a preview version and behavior may change. Recommend checking for GA versions.
- **Connection state mismatch:** If a GET returns `privateLinkServiceConnectionState.status` as "Disconnected" or `actionsRequired` is non-empty, surface this as it may indicate a broken or stale connection.
- **204 on DELETE:** A 204 means the resource did not exist. Surface this so the user knows the connection was already removed rather than assuming the delete succeeded on an existing resource.
- **Missing required parameters:** All endpoints require `subscriptionId`, `resourceGroupName`, and `accountName` in the path. Flag early if any are missing rather than hitting a 404.

## Playbook

### 1. Audit Private Endpoint Connections for a Cosmos DB Account

1. Call GET on the private endpoint connections collection for the target account.
2. Review the returned `value` array for all connections.
3. For each connection, check `properties.privateLinkServiceConnectionState.status` to identify Approved, Pending, or Rejected connections.
4. Flag any connections with `actionsRequired` set to a non-empty value.

### 2. Approve a Pending Private Endpoint Connection

1. Call GET on the connections collection to list all connections and find the one with status "Pending".
2. Note the `privateEndpointConnectionName` from the pending connection.
3. Call PUT with a `parameters` body setting `privateLinkServiceConnectionState.status` to "Approved" and an optional description.
4. If the response is 202, poll the `Azure-AsyncOperation` URL until provisioning completes.
5. Call GET on the specific connection to verify the status is now "Approved".

### 3. Reject and Clean Up an Unwanted Private Endpoint Connection

1. Call GET on the specific connection by name to confirm it exists and check its current state.
2. Call PUT with `privateLinkServiceConnectionState.status` set to "Rejected" and a reason in the description.
3. Wait for the operation to complete (poll on 202).
4. Call DELETE to remove the rejected connection entirely.
5. If DELETE returns 202, poll until the operation finishes. A 204 confirms removal.

### 4. Set Up a New Private Endpoint Connection

1. Call PUT with the desired `privateEndpointConnectionName` and a `parameters` body containing the private endpoint resource ID and connection state.
2. If the response is 202, extract the `Azure-AsyncOperation` header and poll for completion.
3. Call GET on the new connection to verify `provisioningState` is "Succeeded" and the connection status is as expected.
4. Call GET on the collection to confirm the new connection appears in the list.

### 5. Remove All Private Endpoint Connections

1. Call GET on the connections collection to retrieve all connections.
2. For each connection in the `value` array, call DELETE using the connection's name.
3. Track each DELETE response: 202 means deletion is in progress, 204 means already removed.
4. For any 202 responses, poll the async operation URLs until all deletions complete.
5. Call GET on the collection again to confirm the list is empty.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
