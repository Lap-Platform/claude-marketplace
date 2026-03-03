---
name: kustomanagementclient
description: "KustoManagementClient API skill. Use when working with KustoManagementClient for subscriptions, providers. Covers 34 endpoints."
version: 1.0.0
generator: lapsh
---

# KustoManagementClient
API version: 2019-09-07

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Kusto/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/stop -- create first stop

## Endpoints

34 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName} | Gets a Kusto cluster. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName} | Create or update a Kusto cluster. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName} | Update a Kusto cluster. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName} | Deletes a Kusto cluster. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/stop | Stops a Kusto cluster. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/start | Starts a Kusto cluster. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/listFollowerDatabases | Returns a list of databases that are owned by this cluster and were followed by another cluster. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/detachFollowerDatabases | Detaches all followers of a database owned by this cluster. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters | Lists all Kusto clusters within a resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Kusto/clusters | Lists all Kusto clusters within a subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Kusto/skus | Lists eligible SKUs for Kusto resource provider. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Kusto/locations/{location}/checkNameAvailability | Checks that the cluster name is valid and is not already in use. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/checkNameAvailability | Checks that the database name is valid and is not already in use. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/skus | Returns the SKUs available for the provided resource. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases | Returns the list of databases of the given Kusto cluster. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName} | Returns a database. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName} | Creates or updates a database. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName} | Updates a database. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName} | Deletes the database with the given name. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName}/listPrincipals | Returns a list of database principals of the given Kusto cluster and database. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName}/addPrincipals | Add Database principals permissions. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/attachedDatabaseConfigurations | Returns the list of attached database configurations of the given Kusto cluster. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/attachedDatabaseConfigurations/{attachedDatabaseConfigurationName} | Returns an attached database configuration. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/attachedDatabaseConfigurations/{attachedDatabaseConfigurationName} | Creates or updates an attached database configuration. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/attachedDatabaseConfigurations/{attachedDatabaseConfigurationName} | Deletes the attached database configuration with the given name. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName}/removePrincipals | Remove Database principals permissions. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName}/dataConnections | Returns the list of data connections of the given Kusto database. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName}/dataConnectionValidation | Checks that the data connection parameters are valid. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName}/checkNameAvailability | Checks that the data connection name is valid and is not already in use. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName}/dataConnections/{dataConnectionName} | Returns a data connection. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName}/dataConnections/{dataConnectionName} | Creates or updates a data connection. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName}/dataConnections/{dataConnectionName} | Updates a data connection. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName}/dataConnections/{dataConnectionName} | Deletes the data connection with the given name. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Kusto/operations | Lists available operations for the Microsoft.Kusto provider. |

## Enhanced Skill Content
## Question Mapping

- "How do I get details about my Kusto cluster?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}
- "How do I create a new Azure Data Explorer cluster?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}
- "How do I update an existing Kusto cluster configuration?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}
- "How do I delete a Kusto cluster?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}
- "How do I stop a running cluster to save costs?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/stop
- "How do I restart a stopped cluster?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/start
- "How do I list all clusters in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Kusto/clusters
- "How do I check if a cluster name is available before creating one?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Kusto/locations/{location}/checkNameAvailability
- "How do I list databases in a cluster?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases
- "How do I add a principal (user/group) to a database?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName}/addPrincipals
- "How do I set up a data connection (Event Hub, IoT Hub) for ingestion?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName}/dataConnections/{dataConnectionName}
- "How do I validate a data connection before creating it?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/databases/{databaseName}/dataConnectionValidation
- "How do I see which databases are following my cluster?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/listFollowerDatabases
- "How do I attach a follower database from another cluster?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/attachedDatabaseConfigurations/{attachedDatabaseConfigurationName}
- "What SKUs (VM sizes) are available for my cluster?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}/skus

## Response Tips

- **Cluster operations (GET/PUT/PATCH):** Response contains a `properties` object with `state`, `provisioningState`, `uri`, and `dataIngestionUri`. Check `provisioningState` for async operation progress -- values include `Running`, `Creating`, `Deleting`, `Succeeded`, `Failed`.
- **Long-running operations (POST stop/start, PUT/PATCH/DELETE returning 202):** A 202 means the operation is accepted but not complete. Poll the `Azure-AsyncOperation` or `Location` header URL until the operation reaches a terminal state.
- **List endpoints (clusters, databases, data connections):** Results are returned in a `value` array. There is no cursor-based pagination for most Kusto list endpoints; all items are returned in a single response.
- **Name availability checks:** Response includes `nameAvailable` (boolean), `name`, and `message`. Always check `nameAvailable` before attempting a create.
- **SKU listings:** Returns a `value` array of SKU objects. Subscription-level SKUs differ from cluster-level SKUs (cluster-level shows what the specific cluster can scale to).
- **Database principals (list/add/remove):** Returns a `value` array of principal objects with `role`, `name`, `type`, and `fqn` (fully qualified name).
- **Error responses:** Azure returns `{ "error": { "code": "...", "message": "..." } }` with standard codes like `ResourceNotFound`, `ResourceGroupNotFound`, `BadRequest`.

## Anomaly Flags

- **Cluster in `Stopped` state:** Surface when a GET cluster returns `properties.state: "Stopped"` -- most database and data connection operations will fail against a stopped cluster.
- **provisioningState not `Succeeded`:** Flag when any resource shows `provisioningState` of `Failed`, `Deleting`, or `Canceled` -- indicates the resource is in an unhealthy or transitional state.
- **202 without async tracking header:** If a long-running operation returns 202 but no `Azure-AsyncOperation` or `Location` header, the agent cannot poll for completion. Surface this immediately.
- **Follower database inconsistencies:** When `listFollowerDatabases` returns entries that don't match expected attached configurations, flag potential replication issues.
- **Data connection validation failures:** When `dataConnectionValidation` returns errors in the response body (even with 200 status), surface these before the user attempts to create the connection.
- **Deprecated API version:** The spec uses `2019-09-07`. If Azure returns warnings about API version deprecation in response headers (`x-ms-warning`), surface this and suggest upgrading.
- **Throttling (429 responses):** Azure ARM has rate limits per subscription. If a 429 is returned, extract `Retry-After` header and surface the wait time to the user.

## Playbook

### 1. Create a New Kusto Cluster and Database

1. Check name availability: POST `/subscriptions/{subscriptionId}/providers/Microsoft.Kusto/locations/{location}/checkNameAvailability` with `{ "name": "mycluster", "type": "Microsoft.Kusto/clusters" }`.
2. Confirm `nameAvailable` is `true` in the response.
3. Create the cluster: PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Kusto/clusters/{clusterName}` with SKU, location, and desired configuration in `parameters`.
4. Poll the `Azure-AsyncOperation` URL from the 201 response until `provisioningState` is `Succeeded`.
5. Create a database: PUT `.../clusters/{clusterName}/databases/{databaseName}` with `kind` (e.g., `ReadWrite`), `location`, and retention policies in `parameters`.
6. Poll until the database `provisioningState` is `Succeeded`.

### 2. Set Up Data Ingestion from Event Hub

1. List existing data connections: GET `.../databases/{databaseName}/dataConnections` to check for conflicts.
2. Check data connection name availability: POST `.../databases/{databaseName}/checkNameAvailability` with the desired name.
3. Validate the connection: POST `.../databases/{databaseName}/dataConnectionValidation` with Event Hub connection details (resource ID, consumer group, table, mapping, data format).
4. Review validation response for any errors or warnings.
5. Create the data connection: PUT `.../databases/{databaseName}/dataConnections/{dataConnectionName}` with the validated parameters.
6. Poll the 201/202 response until provisioning completes.

### 3. Manage Database Access (Principals)

1. List current principals: POST `.../databases/{databaseName}/listPrincipals` to see who has access.
2. Add new principals: POST `.../databases/{databaseName}/addPrincipals` with `{ "value": [{ "role": "Admin", "name": "user@domain.com", "type": "User", "fqn": "aaduser=..." }] }`.
3. To revoke access: POST `.../databases/{databaseName}/removePrincipals` with the same principal structure.
4. Verify changes by listing principals again.

### 4. Stop and Restart a Cluster (Cost Optimization)

1. Verify cluster state: GET `.../clusters/{clusterName}` and confirm `properties.state` is `Running`.
2. Stop the cluster: POST `.../clusters/{clusterName}/stop`. Expect 202.
3. Poll until the cluster `state` transitions to `Stopped`.
4. When ready to resume: POST `.../clusters/{clusterName}/start`. Expect 202.
5. Poll until `state` returns to `Running` before running any queries or managing databases.

### 5. Configure a Follower (Read-Only) Database

1. On the leader cluster, list follower databases: POST `.../clusters/{leaderClusterName}/listFollowerDatabases` to see current followers.
2. On the follower cluster, create an attached database configuration: PUT `.../clusters/{followerClusterName}/attachedDatabaseConfigurations/{configName}` with the leader cluster resource ID, database name, and default principals modification kind.
3. Poll the 201/202 response until provisioning succeeds.
4. Verify the attachment: GET `.../clusters/{followerClusterName}/attachedDatabaseConfigurations/{configName}`.
5. To detach later: on the leader, POST `.../clusters/{leaderClusterName}/detachFollowerDatabases` with `{ "clusterResourceId": "...", "attachedDatabaseConfigurationName": "..." }`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
