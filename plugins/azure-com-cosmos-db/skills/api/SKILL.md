---
name: cosmos-db
description: "Cosmos DB API skill. Use when working with Cosmos DB for subscriptions, providers. Covers 101 endpoints."
version: 1.0.0
generator: lapsh
---

# Cosmos DB
API version: 2019-08-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.DocumentDB/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/failoverPriorityChange -- create first failoverPriorityChange

## Endpoints

101 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName} | Retrieves the properties of an existing Azure Cosmos DB database account. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName} | Updates the properties of an existing Azure Cosmos DB database account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName} | Creates or updates an Azure Cosmos DB database account. The "Update" method is preferred when performing updates on an account. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName} | Deletes an existing Azure Cosmos DB database account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/failoverPriorityChange | Changes the failover priority for the Azure Cosmos DB database account. A failover priority of 0 indicates a write region. The maximum value for a failover priority = (total number of regions - 1). Failover priority values must be unique for each of the regions in which the database account exists. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.DocumentDB/databaseAccounts | Lists all the Azure Cosmos DB database accounts available under the subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts | Lists all the Azure Cosmos DB database accounts available under the given resource group. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/listKeys | Lists the access keys for the specified Azure Cosmos DB database account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/listConnectionStrings | Lists the connection strings for the specified Azure Cosmos DB database account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/offlineRegion | Offline the specified region for the specified Azure Cosmos DB database account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/onlineRegion | Online the specified region for the specified Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/readonlykeys | Lists the read-only access keys for the specified Azure Cosmos DB database account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/readonlykeys | Lists the read-only access keys for the specified Azure Cosmos DB database account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/regenerateKey | Regenerates an access key for the specified Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/metrics | Retrieves the metrics determined by the given filter for the given database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/databases/{databaseRid}/metrics | Retrieves the metrics determined by the given filter for the given database account and database. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/databases/{databaseRid}/collections/{collectionRid}/metrics | Retrieves the metrics determined by the given filter for the given database account and collection. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/region/{region}/databases/{databaseRid}/collections/{collectionRid}/metrics | Retrieves the metrics determined by the given filter for the given database account, collection and region. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/region/{region}/metrics | Retrieves the metrics determined by the given filter for the given database account and region. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sourceRegion/{sourceRegion}/targetRegion/{targetRegion}/percentile/metrics | Retrieves the metrics determined by the given filter for the given account, source and target region. This url is only for PBS and Replication Latency data |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/targetRegion/{targetRegion}/percentile/metrics | Retrieves the metrics determined by the given filter for the given account target region. This url is only for PBS and Replication Latency data |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/percentile/metrics | Retrieves the metrics determined by the given filter for the given database account. This url is only for PBS and Replication Latency data |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/region/{region}/databases/{databaseRid}/collections/{collectionRid}/partitions/metrics | Retrieves the metrics determined by the given filter for the given collection and region, split by partition. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/databases/{databaseRid}/collections/{collectionRid}/partitions/metrics | Retrieves the metrics determined by the given filter for the given collection, split by partition. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/databases/{databaseRid}/collections/{collectionRid}/partitionKeyRangeId/{partitionKeyRangeId}/metrics | Retrieves the metrics determined by the given filter for the given partition key range id. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/region/{region}/databases/{databaseRid}/collections/{collectionRid}/partitionKeyRangeId/{partitionKeyRangeId}/metrics | Retrieves the metrics determined by the given filter for the given partition key range id and region. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/usages | Retrieves the usages (most recent data) for the given database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/databases/{databaseRid}/usages | Retrieves the usages (most recent data) for the given database. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/databases/{databaseRid}/collections/{collectionRid}/usages | Retrieves the usages (most recent storage data) for the given collection. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/databases/{databaseRid}/collections/{collectionRid}/partitions/usages | Retrieves the usages (most recent storage data) for the given collection, split by partition. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/databases/{databaseRid}/metricDefinitions | Retrieves metric definitions for the given database. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/databases/{databaseRid}/collections/{collectionRid}/metricDefinitions | Retrieves metric definitions for the given collection. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/metricDefinitions | Retrieves metric definitions for the given database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases | Lists the SQL databases under an existing Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName} | Gets the SQL database under an existing Azure Cosmos DB database account with the provided name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName} | Create or update an Azure Cosmos DB SQL database |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName} | Deletes an existing Azure Cosmos DB SQL database. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/throughputSettings/default | Gets the RUs per second of the SQL database under an existing Azure Cosmos DB database account with the provided name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/throughputSettings/default | Update RUs per second of an Azure Cosmos DB SQL database |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers | Lists the SQL container under an existing Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName} | Gets the SQL container under an existing Azure Cosmos DB database account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName} | Create or update an Azure Cosmos DB SQL container |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName} | Deletes an existing Azure Cosmos DB SQL container. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/throughputSettings/default | Gets the RUs per second of the SQL container under an existing Azure Cosmos DB database account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/throughputSettings/default | Update RUs per second of an Azure Cosmos DB SQL container |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/storedProcedures | Lists the SQL storedProcedure under an existing Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/storedProcedures/{storedProcedureName} | Gets the SQL storedProcedure under an existing Azure Cosmos DB database account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/storedProcedures/{storedProcedureName} | Create or update an Azure Cosmos DB SQL storedProcedure |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/storedProcedures/{storedProcedureName} | Deletes an existing Azure Cosmos DB SQL storedProcedure. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/userDefinedFunctions | Lists the SQL userDefinedFunction under an existing Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/userDefinedFunctions/{userDefinedFunctionName} | Gets the SQL userDefinedFunction under an existing Azure Cosmos DB database account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/userDefinedFunctions/{userDefinedFunctionName} | Create or update an Azure Cosmos DB SQL userDefinedFunction |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/userDefinedFunctions/{userDefinedFunctionName} | Deletes an existing Azure Cosmos DB SQL userDefinedFunction. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/triggers | Lists the SQL trigger under an existing Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/triggers/{triggerName} | Gets the SQL trigger under an existing Azure Cosmos DB database account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/triggers/{triggerName} | Create or update an Azure Cosmos DB SQL trigger |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}/containers/{containerName}/triggers/{triggerName} | Deletes an existing Azure Cosmos DB SQL trigger. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/mongodbDatabases | Lists the MongoDB databases under an existing Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/mongodbDatabases/{databaseName} | Gets the MongoDB databases under an existing Azure Cosmos DB database account with the provided name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/mongodbDatabases/{databaseName} | Create or updates Azure Cosmos DB MongoDB database |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/mongodbDatabases/{databaseName} | Deletes an existing Azure Cosmos DB MongoDB database. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/mongodbDatabases/{databaseName}/throughputSettings/default | Gets the RUs per second of the MongoDB database under an existing Azure Cosmos DB database account with the provided name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/mongodbDatabases/{databaseName}/throughputSettings/default | Update RUs per second of the an Azure Cosmos DB MongoDB database |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/mongodbDatabases/{databaseName}/collections | Lists the MongoDB collection under an existing Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/mongodbDatabases/{databaseName}/collections/{collectionName} | Gets the MongoDB collection under an existing Azure Cosmos DB database account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/mongodbDatabases/{databaseName}/collections/{collectionName} | Create or update an Azure Cosmos DB MongoDB Collection |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/mongodbDatabases/{databaseName}/collections/{collectionName} | Deletes an existing Azure Cosmos DB MongoDB Collection. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/mongodbDatabases/{databaseName}/collections/{collectionName}/throughputSettings/default | Gets the RUs per second of the MongoDB collection under an existing Azure Cosmos DB database account with the provided name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/mongodbDatabases/{databaseName}/collections/{collectionName}/throughputSettings/default | Update the RUs per second of an Azure Cosmos DB MongoDB collection |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/tables | Lists the Tables under an existing Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/tables/{tableName} | Gets the Tables under an existing Azure Cosmos DB database account with the provided name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/tables/{tableName} | Create or update an Azure Cosmos DB Table |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/tables/{tableName} | Deletes an existing Azure Cosmos DB Table. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/tables/{tableName}/throughputSettings/default | Gets the RUs per second of the Table under an existing Azure Cosmos DB database account with the provided name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/tables/{tableName}/throughputSettings/default | Update RUs per second of an Azure Cosmos DB Table |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/cassandraKeyspaces | Lists the Cassandra keyspaces under an existing Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/cassandraKeyspaces/{keyspaceName} | Gets the Cassandra keyspaces under an existing Azure Cosmos DB database account with the provided name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/cassandraKeyspaces/{keyspaceName} | Create or update an Azure Cosmos DB Cassandra keyspace |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/cassandraKeyspaces/{keyspaceName} | Deletes an existing Azure Cosmos DB Cassandra keyspace. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/cassandraKeyspaces/{keyspaceName}/throughputSettings/default | Gets the RUs per second of the Cassandra Keyspace under an existing Azure Cosmos DB database account with the provided name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/cassandraKeyspaces/{keyspaceName}/throughputSettings/default | Update RUs per second of an Azure Cosmos DB Cassandra Keyspace |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/cassandraKeyspaces/{keyspaceName}/tables | Lists the Cassandra table under an existing Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/cassandraKeyspaces/{keyspaceName}/tables/{tableName} | Gets the Cassandra table under an existing Azure Cosmos DB database account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/cassandraKeyspaces/{keyspaceName}/tables/{tableName} | Create or update an Azure Cosmos DB Cassandra Table |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/cassandraKeyspaces/{keyspaceName}/tables/{tableName} | Deletes an existing Azure Cosmos DB Cassandra table. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/cassandraKeyspaces/{keyspaceName}/tables/{tableName}/throughputSettings/default | Gets the RUs per second of the Cassandra table under an existing Azure Cosmos DB database account with the provided name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/cassandraKeyspaces/{keyspaceName}/tables/{tableName}/throughputSettings/default | Update RUs per second of an Azure Cosmos DB Cassandra table |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/gremlinDatabases | Lists the Gremlin databases under an existing Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/gremlinDatabases/{databaseName} | Gets the Gremlin databases under an existing Azure Cosmos DB database account with the provided name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/gremlinDatabases/{databaseName} | Create or update an Azure Cosmos DB Gremlin database |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/gremlinDatabases/{databaseName} | Deletes an existing Azure Cosmos DB Gremlin database. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/gremlinDatabases/{databaseName}/throughputSettings/default | Gets the RUs per second of the Gremlin database under an existing Azure Cosmos DB database account with the provided name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/gremlinDatabases/{databaseName}/throughputSettings/default | Update RUs per second of an Azure Cosmos DB Gremlin database |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/gremlinDatabases/{databaseName}/graphs | Lists the Gremlin graph under an existing Azure Cosmos DB database account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/gremlinDatabases/{databaseName}/graphs/{graphName} | Gets the Gremlin graph under an existing Azure Cosmos DB database account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/gremlinDatabases/{databaseName}/graphs/{graphName} | Create or update an Azure Cosmos DB Gremlin graph |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/gremlinDatabases/{databaseName}/graphs/{graphName} | Deletes an existing Azure Cosmos DB Gremlin graph. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/gremlinDatabases/{databaseName}/graphs/{graphName}/throughputSettings/default | Gets the Gremlin graph throughput under an existing Azure Cosmos DB database account with the provided name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/gremlinDatabases/{databaseName}/graphs/{graphName}/throughputSettings/default | Update RUs per second of an Azure Cosmos DB Gremlin graph |

### providers
| Method | Path | Description |
|--------|------|-------------|
| HEAD | /providers/Microsoft.DocumentDB/databaseAccountNames/{accountName} | Checks that the Azure Cosmos DB account name already exists. A valid account name may contain only lowercase letters, numbers, and the '-' character, and must be between 3 and 50 characters. |
| GET | /providers/Microsoft.DocumentDB/operations | Lists all of the available Cosmos DB Resource Provider operations. |

## Enhanced Skill Content
## Question Mapping

- "How do I get details about my Cosmos DB account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}
- "How do I create a new Cosmos DB account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}
- "How do I delete a Cosmos DB account?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}
- "How do I list all Cosmos DB accounts in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DocumentDB/databaseAccounts
- "How do I get connection strings for my Cosmos DB account?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/listConnectionStrings
- "How do I retrieve the access keys for my account?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/listKeys
- "How do I rotate or regenerate an account key?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/regenerateKey
- "How do I check if a Cosmos DB account name is available?" -> HEAD /providers/Microsoft.DocumentDB/databaseAccountNames/{accountName}
- "How do I create a SQL database inside my Cosmos DB account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/sqlDatabases/{databaseName}
- "How do I scale throughput on a SQL container?" -> PUT .../sqlDatabases/{databaseName}/containers/{containerName}/throughputSettings/default
- "How do I get performance metrics for a specific collection?" -> GET .../databaseAccounts/{accountName}/databases/{databaseRid}/collections/{collectionRid}/metrics
- "How do I trigger a failover priority change for disaster recovery?" -> POST .../databaseAccounts/{accountName}/failoverPriorityChange
- "How do I take a region offline for maintenance?" -> POST .../databaseAccounts/{accountName}/offlineRegion
- "How do I list stored procedures in a SQL container?" -> GET .../sqlDatabases/{databaseName}/containers/{containerName}/storedProcedures
- "How do I create a Cassandra keyspace?" -> PUT .../databaseAccounts/{accountName}/cassandraKeyspaces/{keyspaceName}

## Response Tips

- **Account operations**: GET returns full resource properties; PUT/PATCH return the updated resource on 200; DELETE returns 202 (accepted, async) or 204 (already gone) with no body.
- **Resource creation (PUT)**: Returns 200 if the resource already exists and was updated, or 202 if provisioning is async -- poll the `Azure-AsyncOperation` header URL for completion.
- **List endpoints**: Responses wrap items in a `value` array at the top level; there is no next-page token since ARM resources are not paginated by default at this scope.
- **Metrics and usages**: Require a `$filter` query parameter (OData syntax, e.g., time grain and time range); responses contain a `value` array of metric objects with `name`, `unit`, `metricValues`.
- **Throughput settings**: GET returns a `resource.throughput` integer (RU/s); PUT accepts an `updateThroughputParameters` body with the new RU/s value.
- **Key operations (listKeys, regenerateKey)**: POST returns `primaryMasterKey`, `secondaryMasterKey`, `primaryReadonlyMasterKey`, `secondaryReadonlyMasterKey` -- treat these as secrets.
- **Name availability (HEAD)**: 200 means the name is taken; 404 means available -- the inverse of what you might expect.

## Anomaly Flags

- **202 Accepted on mutations**: Surface that the operation is async. Extract and present the `Azure-AsyncOperation` or `Location` header so the user can poll for completion status.
- **204 on DELETE**: Flag that the resource was already deleted or did not exist -- this is idempotent but may indicate a stale reference in automation.
- **HEAD name check returning 200**: Proactively warn that the desired account name is already taken before the user attempts a PUT.
- **Throughput values near limits**: When reading throughput settings, flag if the value is at the minimum (400 RU/s) or at common tier boundaries (e.g., 10,000+ RU/s) that may affect billing.
- **Region offline/online operations**: These are disruptive -- surface a confirmation prompt before executing offlineRegion or onlineRegion calls, and note the async 202 response.
- **Key regeneration**: Warn that regenerating a key immediately invalidates the old key -- all clients using that key will lose access until updated.
- **$filter missing on metrics endpoints**: These endpoints require a `$filter` parameter; surface a clear error if the user omits it rather than sending a request that will fail.
- **api-version mismatch**: This spec targets `2019-08-01`. Flag if the user attempts features from a newer API version that won't be available.

## Playbook

### 1. Provision a New Cosmos DB SQL Account with a Database and Container

1. Check name availability: `HEAD /providers/Microsoft.DocumentDB/databaseAccountNames/{accountName}` -- expect 404 (available).
2. Create the account: `PUT .../databaseAccounts/{accountName}` with `createUpdateParameters` specifying location, consistency policy, and capabilities.
3. Poll the `Azure-AsyncOperation` URL from the 202 response until status is `Succeeded`.
4. Create a SQL database: `PUT .../sqlDatabases/{databaseName}` with `createUpdateSqlDatabaseParameters` containing the resource `id`.
5. Create a SQL container: `PUT .../sqlDatabases/{databaseName}/containers/{containerName}` with partition key and indexing policy in the parameters.
6. Optionally set throughput: `PUT .../containers/{containerName}/throughputSettings/default` with desired RU/s.

### 2. Rotate Account Keys Without Downtime

1. Retrieve current keys: `POST .../listKeys` to get all four keys.
2. Update all application connection strings to use the secondary key.
3. Regenerate the primary key: `POST .../regenerateKey` with `{"keyKind": "primary"}`.
4. Retrieve the new keys: `POST .../listKeys` again to confirm the new primary key.
5. Update application connection strings back to the new primary key.
6. Optionally regenerate the secondary key using the same process in reverse.

### 3. Monitor Performance and Diagnose Throttling

1. Get metric definitions: `GET .../metricDefinitions` to discover available metric names and units.
2. Query account-level metrics: `GET .../metrics?$filter=(name.value eq 'Total Requests') and ...` with a time range filter.
3. Drill into a specific database: `GET .../databases/{databaseRid}/metrics` with the same filter.
4. Drill into a collection: `GET .../databases/{databaseRid}/collections/{collectionRid}/metrics`.
5. Check partition-level metrics: `GET .../collections/{collectionRid}/partitions/metrics` to identify hot partitions.
6. Review usage data: `GET .../usages` at account, database, or collection level to check storage consumption.

### 4. Set Up Multi-Region Failover

1. Get current account configuration: `GET .../databaseAccounts/{accountName}` to review existing regions and failover policies.
2. Update the account to add regions: `PATCH .../databaseAccounts/{accountName}` with updated `locations` array in `updateParameters`.
3. Configure failover priorities: `POST .../failoverPriorityChange` with `failoverParameters` listing regions and their priority ordinals.
4. Verify by re-reading the account: `GET .../databaseAccounts/{accountName}` and confirm the `failoverPolicies` array reflects the new order.
5. Test by taking a region offline: `POST .../offlineRegion` (use with caution in production) and then bring it back with `POST .../onlineRegion`.

### 5. Manage Server-Side Logic (Stored Procedures, Triggers, UDFs)

1. List existing stored procedures: `GET .../containers/{containerName}/storedProcedures`.
2. Create or update a stored procedure: `PUT .../storedProcedures/{storedProcedureName}` with the JavaScript function body in `createUpdateSqlStoredProcedureParameters`.
3. Create a pre-trigger: `PUT .../triggers/{triggerName}` with `triggerType: "Pre"` and `triggerOperation: "All"` in the parameters.
4. Create a UDF for query-time logic: `PUT .../userDefinedFunctions/{udfName}` with the function body.
5. To remove obsolete logic, delete with the corresponding `DELETE .../storedProcedures/{name}`, `.../triggers/{name}`, or `.../userDefinedFunctions/{name}` endpoint -- expect 202 or 204.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
