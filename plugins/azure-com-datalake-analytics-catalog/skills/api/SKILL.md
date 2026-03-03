---
name: datalakeanalyticscatalogmanagementclient
description: "DataLakeAnalyticsCatalogManagementClient API skill. Use when working with DataLakeAnalyticsCatalogManagementClient for catalog. Covers 45 endpoints."
version: 1.0.0
generator: lapsh
---

# DataLakeAnalyticsCatalogManagementClient
API version: 2016-11-01

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /catalog/usql/acl -- verify access
3. POST /catalog/usql/databases/{databaseName}/credentials/{credentialName} -- create first credentials

## Endpoints

45 endpoints across 1 groups. See references/api-spec.lap for full details.

### catalog
| Method | Path | Description |
|--------|------|-------------|
| PUT | /catalog/usql/databases/{databaseName}/secrets/{secretName} | Creates the specified secret for use with external data sources in the specified database. This is deprecated and will be removed in the next release. Please use CreateCredential instead. |
| GET | /catalog/usql/databases/{databaseName}/secrets/{secretName} | Gets the specified secret in the specified database. This is deprecated and will be removed in the next release. Please use GetCredential instead. |
| PATCH | /catalog/usql/databases/{databaseName}/secrets/{secretName} | Modifies the specified secret for use with external data sources in the specified database. This is deprecated and will be removed in the next release. Please use UpdateCredential instead. |
| DELETE | /catalog/usql/databases/{databaseName}/secrets/{secretName} | Deletes the specified secret in the specified database. This is deprecated and will be removed in the next release. Please use DeleteCredential instead. |
| DELETE | /catalog/usql/databases/{databaseName}/secrets | Deletes all secrets in the specified database. This is deprecated and will be removed in the next release. In the future, please only drop individual credentials using DeleteCredential |
| PUT | /catalog/usql/databases/{databaseName}/credentials/{credentialName} | Creates the specified credential for use with external data sources in the specified database. |
| GET | /catalog/usql/databases/{databaseName}/credentials/{credentialName} | Retrieves the specified credential from the Data Lake Analytics catalog. |
| PATCH | /catalog/usql/databases/{databaseName}/credentials/{credentialName} | Modifies the specified credential for use with external data sources in the specified database |
| POST | /catalog/usql/databases/{databaseName}/credentials/{credentialName} | Deletes the specified credential in the specified database |
| GET | /catalog/usql/databases/{databaseName}/credentials | Retrieves the list of credentials from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/externaldatasources/{externalDataSourceName} | Retrieves the specified external data source from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/externaldatasources | Retrieves the list of external data sources from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/procedures/{procedureName} | Retrieves the specified procedure from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/procedures | Retrieves the list of procedures from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName} | Retrieves the specified table from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}/tablefragments | Retrieves the list of table fragments from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables | Retrieves the list of tables from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/statistics | Retrieves the list of all table statistics within the specified schema from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tabletypes/{tableTypeName} | Retrieves the specified table type from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tabletypes | Retrieves the list of table types from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/packages/{packageName} | Retrieves the specified package from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/packages | Retrieves the list of packages from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/views/{viewName} | Retrieves the specified view from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/views | Retrieves the list of views from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}/statistics/{statisticsName} | Retrieves the specified table statistics from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}/statistics | Retrieves the list of table statistics from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}/partitions/{partitionName}/previewrows | Retrieves a preview set of rows in given partition. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}/partitions/{partitionName} | Retrieves the specified table partition from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}/previewrows | Retrieves a preview set of rows in given table. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}/partitions | Retrieves the list of table partitions from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/types | Retrieves the list of types within the specified database and schema from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tablevaluedfunctions/{tableValuedFunctionName} | Retrieves the specified table valued function from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tablevaluedfunctions | Retrieves the list of table valued functions from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/assemblies/{assemblyName} | Retrieves the specified assembly from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/assemblies | Retrieves the list of assemblies from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas/{schemaName} | Retrieves the specified schema from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/schemas | Retrieves the list of schemas from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/statistics | Retrieves the list of all statistics in a database from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/tables | Retrieves the list of all tables in a database from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/tablevaluedfunctions | Retrieves the list of all table valued functions in a database from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/views | Retrieves the list of all views in a database from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName}/acl | Retrieves the list of access control list (ACL) entries for the database from the Data Lake Analytics catalog. |
| GET | /catalog/usql/acl | Retrieves the list of access control list (ACL) entries for the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases/{databaseName} | Retrieves the specified database from the Data Lake Analytics catalog. |
| GET | /catalog/usql/databases | Retrieves the list of databases from the Data Lake Analytics catalog. |

## Enhanced Skill Content
## Question Mapping

- "What databases exist in my Data Lake Analytics account?" -> GET /catalog/usql/databases
- "Show me the schema details for a specific database" -> GET /catalog/usql/databases/{databaseName}/schemas
- "What tables are in a given schema?" -> GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables
- "How do I preview data in a table without running a query?" -> GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}/previewrows
- "How do I create or update a secret in my database?" -> PUT /catalog/usql/databases/{databaseName}/secrets/{secretName}
- "How do I rotate a credential password?" -> PATCH /catalog/usql/databases/{databaseName}/credentials/{credentialName}
- "What stored procedures exist in a schema?" -> GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/procedures
- "How do I delete all secrets in a database at once?" -> DELETE /catalog/usql/databases/{databaseName}/secrets
- "What external data sources are registered in my database?" -> GET /catalog/usql/databases/{databaseName}/externaldatasources
- "How do I check access control lists for a specific database?" -> GET /catalog/usql/databases/{databaseName}/acl
- "What are the global ACL permissions across the catalog?" -> GET /catalog/usql/acl
- "How do I list table partitions and preview a specific partition's rows?" -> GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}/partitions/{partitionName}/previewrows
- "What table-valued functions are available in a schema?" -> GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tablevaluedfunctions
- "How do I delete a credential with cascade?" -> POST /catalog/usql/databases/{databaseName}/credentials/{credentialName}
- "What assemblies are registered in my database?" -> GET /catalog/usql/databases/{databaseName}/assemblies

## Response Tips

- **List endpoints** (databases, tables, schemas, views, etc.): All support OData query parameters (`$filter`, `$top`, `$skip`, `$orderby`, `$count`, `$select`). Use `$top`/`$skip` for pagination and `$count=true` to get total result count alongside data.
- **Single-item GET endpoints**: Return the full catalog object directly. Nested properties may include type info, column definitions, or relationship references depending on the entity type.
- **Secret/Credential mutations** (PUT, PATCH, DELETE): Return 200 on success with no guaranteed body content. Treat any non-200 as a failure and inspect the error response for details.
- **Credential DELETE via POST**: The POST to credentials with `cascade` parameter is the deletion endpoint (not a typical POST create). The `cascade` option controls whether dependent objects are also removed.
- **Preview rows**: Returns tabular data constrained by `maxRows` and `maxColumns` optional parameters. Default limits apply if omitted.
- **Table listings**: Support a `basic` flag that returns a lightweight representation, omitting column metadata and statistics.

## Anomaly Flags

- **Bulk secret deletion**: Flag any call to `DELETE /catalog/usql/databases/{databaseName}/secrets` (no secretName) as it wipes all secrets in the database. Confirm intent before executing.
- **Cascade credential deletion**: When `cascade=true` is passed to the credential POST/delete endpoint, surface a warning that dependent catalog objects will also be removed.
- **Missing api-version**: The `api-version` common field is required on all requests. Flag requests missing it before they fail with an uninformative error.
- **Large unpaginated result sets**: If a list endpoint is called without `$top` or `$skip`, warn that the response may be very large and suggest adding pagination.
- **Preview row limits unset**: When calling preview rows without `maxRows`/`maxColumns`, flag that the default may return more data than expected for wide or large tables.
- **Secret vs. Credential confusion**: These are separate entity types at distinct paths. Surface a clarification if the user conflates them, as operations are not interchangeable.
- **Deprecated API version**: The spec targets version `2016-11-01`. Flag that this is a legacy API version and newer catalog management capabilities may be available through updated endpoints.

## Playbook

### 1. Explore a Database's Full Schema Structure

1. List all databases: `GET /catalog/usql/databases`
2. Get details for the target database: `GET /catalog/usql/databases/{databaseName}`
3. List all schemas: `GET /catalog/usql/databases/{databaseName}/schemas`
4. For each schema, list tables: `GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables?basic=true`
5. Drill into a specific table for column details: `GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}`
6. Check table statistics: `GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}/statistics`

### 2. Preview Table Data Before Writing a U-SQL Query

1. Identify the target table and schema using the listing endpoints above.
2. Check partitions: `GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}/partitions`
3. Preview full table rows: `GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}/previewrows?maxRows=50&maxColumns=20`
4. Alternatively, preview a specific partition: `GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tables/{tableName}/partitions/{partitionName}/previewrows?maxRows=50`

### 3. Manage Database Credentials (Full Lifecycle)

1. List existing credentials: `GET /catalog/usql/databases/{databaseName}/credentials`
2. Create a new credential: `PUT /catalog/usql/databases/{databaseName}/credentials/{credentialName}` with connection parameters in the body.
3. Update a credential (e.g., rotate password): `PATCH /catalog/usql/databases/{databaseName}/credentials/{credentialName}` with updated parameters.
4. Delete a credential: `POST /catalog/usql/databases/{databaseName}/credentials/{credentialName}` with optional `cascade=true` to remove dependent objects.

### 4. Audit Access Control Across the Catalog

1. Check global ACLs: `GET /catalog/usql/acl`
2. List all databases: `GET /catalog/usql/databases`
3. For each database, check database-level ACLs: `GET /catalog/usql/databases/{databaseName}/acl`
4. Cross-reference with credential and secret listings to identify overly permissive access patterns.

### 5. Inventory All Programmability Objects in a Schema

1. Target a schema: `GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}`
2. List procedures: `GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/procedures`
3. List table-valued functions: `GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tablevaluedfunctions`
4. List views: `GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/views`
5. List packages: `GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/packages`
6. List types and table types: `GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/types` and `GET /catalog/usql/databases/{databaseName}/schemas/{schemaName}/tabletypes`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
