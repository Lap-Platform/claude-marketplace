---
name: aws-rds-dataservice
description: "AWS RDS DataService API skill. Use when working with AWS RDS DataService for BatchExecute, BeginTransaction, CommitTransaction. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS RDS DataService
API version: 2018-08-01

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST /BatchExecute -- create first BatchExecute

## Endpoints

6 endpoints across 6 groups. See references/api-spec.lap for full details.

### BatchExecute
| Method | Path | Description |
|--------|------|-------------|
| POST | /BatchExecute | Runs a batch SQL statement over an array of data. You can run bulk update and insert operations for multiple records using a DML statement with different parameter sets. Bulk operations can provide a significant performance improvement over individual insert and update operations.  If a call isn't part of a transaction because it doesn't include the transactionID parameter, changes that result from the call are committed automatically. There isn't a fixed upper limit on the number of parameter sets. However, the maximum size of the HTTP request submitted through the Data API is 4 MiB. If the request exceeds this limit, the Data API returns an error and doesn't process the request. This 4-MiB limit includes the size of the HTTP headers and the JSON notation in the request. Thus, the number of parameter sets that you can include depends on a combination of factors, such as the size of the SQL statement and the size of each parameter set. The response size limit is 1 MiB. If the call returns more than 1 MiB of response data, the call is terminated. |

### BeginTransaction
| Method | Path | Description |
|--------|------|-------------|
| POST | /BeginTransaction | Starts a SQL transaction.  A transaction can run for a maximum of 24 hours. A transaction is terminated and rolled back automatically after 24 hours. A transaction times out if no calls use its transaction ID in three minutes. If a transaction times out before it's committed, it's rolled back automatically. DDL statements inside a transaction cause an implicit commit. We recommend that you run each DDL statement in a separate ExecuteStatement call with continueAfterTimeout enabled. |

### CommitTransaction
| Method | Path | Description |
|--------|------|-------------|
| POST | /CommitTransaction | Ends a SQL transaction started with the BeginTransaction operation and commits the changes. |

### ExecuteSql
| Method | Path | Description |
|--------|------|-------------|
| POST | /ExecuteSql | Runs one or more SQL statements.  This operation isn't supported for Aurora PostgreSQL Serverless v2 and provisioned DB clusters, and for Aurora Serverless v1 DB clusters, the operation is deprecated. Use the BatchExecuteStatement or ExecuteStatement operation. |

### Execute
| Method | Path | Description |
|--------|------|-------------|
| POST | /Execute | Runs a SQL statement against a database.  If a call isn't part of a transaction because it doesn't include the transactionID parameter, changes that result from the call are committed automatically. If the binary response data from the database is more than 1 MB, the call is terminated. |

### RollbackTransaction
| Method | Path | Description |
|--------|------|-------------|
| POST | /RollbackTransaction | Performs a rollback of a transaction. Rolling back a transaction cancels its changes. |

## Enhanced Skill Content
## Question Mapping

- "How do I run a SQL query against my Aurora Serverless database?" -> POST /Execute
- "How do I run multiple SQL statements in a single batch?" -> POST /BatchExecute
- "How do I start a database transaction?" -> POST /BeginTransaction
- "How do I commit an open transaction?" -> POST /CommitTransaction
- "How do I roll back a failed transaction?" -> POST /RollbackTransaction
- "How do I execute raw SQL statements using the legacy endpoint?" -> POST /ExecuteSql
- "How do I insert a row and get the auto-generated ID back?" -> POST /Execute (check `generatedFields`)
- "How do I run a parameterized query to avoid SQL injection?" -> POST /Execute with `parameters`
- "How do I run an UPDATE across multiple parameter sets in one call?" -> POST /BatchExecute with `parameterSets`
- "How do I get column names and types alongside query results?" -> POST /Execute with `includeResultMetadata: true`
- "How do I run a long query that might exceed the timeout?" -> POST /Execute with `continueAfterTimeout: true`
- "How do I execute multiple statements inside a transaction?" -> POST /BeginTransaction, then POST /Execute (with `transactionId`), then POST /CommitTransaction
- "How do I get results formatted as JSON instead of field arrays?" -> POST /Execute with `formatRecordsAs: "JSON"`

## Response Tips

- **Execute**: Results come as `records` (array of arrays of `Field` objects, not plain values) -- enable `includeResultMetadata` to map columns by index. `formattedRecords` returns a JSON string when `formatRecordsAs` is set, which is often easier to parse.
- **BatchExecute**: Returns `updateResults` only -- no row data. Each entry corresponds to one parameter set in order. Use this for bulk INSERTs/UPDATEs, not SELECTs.
- **BeginTransaction / CommitTransaction / RollbackTransaction**: Return simple status objects. A missing or empty `transactionId` on begin means the call failed silently -- always validate before proceeding.
- **ExecuteSql (legacy)**: Returns `sqlStatementResults` as a flat list; semicolon-separated statements each produce one result entry. Prefer `/Execute` for new integrations.
- **Errors**: All endpoints return HTTP 200 on success. Failures surface as `BadRequestException`, `ForbiddenException`, `InternalServerErrorException`, `NotFoundException`, or `ServiceUnavailableError` with descriptive messages. Watch for `StatementTimeoutException` on long queries.

## Anomaly Flags

- **`ExecuteSql` usage detected**: This endpoint is deprecated. Flag it and recommend migrating to `POST /Execute` or `POST /BatchExecute`.
- **Transaction left open**: If `BeginTransaction` is called but no `CommitTransaction` or `RollbackTransaction` follows within the workflow, warn the user -- idle transactions auto-expire and can lock rows.
- **Missing `includeResultMetadata`**: When the user runs a SELECT via `/Execute` without this flag, proactively note that column names won't be in the response.
- **Large `parameterSets` in BatchExecute**: If the parameter set count is very high (1000+), warn about potential request size limits and suggest chunking.
- **`continueAfterTimeout` without transaction**: If set outside a transaction, partial results may be non-deterministic. Flag the risk.
- **`transactionStatus` is not "Transaction Committed"**: After `CommitTransaction`, any status other than this indicates a problem -- surface immediately.
- **Empty `generatedFields`**: After an INSERT, if this is empty, the table likely has no auto-increment column. Note this to avoid confusion.

## Playbook

### 1. Run a Simple Query

1. Call `POST /Execute` with `resourceArn`, `secretArn`, `database`, and your SQL in `sql`.
2. Set `includeResultMetadata: true` to get column names.
3. Parse `records` (array of rows, each an array of `Field` objects) using `columnMetadata` for mapping.
4. Alternatively, set `formatRecordsAs: "JSON"` and read `formattedRecords` for a simpler JSON string.

### 2. Execute a Multi-Statement Transaction

1. Call `POST /BeginTransaction` with `resourceArn`, `secretArn`, and `database`. Store the returned `transactionId`.
2. Call `POST /Execute` one or more times, passing the `transactionId` with each request.
3. If all statements succeed, call `POST /CommitTransaction` with the `transactionId`.
4. If any statement fails, call `POST /RollbackTransaction` with the `transactionId`.
5. Verify `transactionStatus` is `"Transaction Committed"` or `"Transaction Rolledback"` respectively.

### 3. Bulk Insert with BatchExecute

1. Prepare your INSERT statement with named placeholders (e.g., `INSERT INTO users (name, email) VALUES (:name, :email)`).
2. Build `parameterSets` -- an array of arrays, each inner array containing `SqlParameter` objects with `name`, `value`, and optionally `typeHint`.
3. Call `POST /BatchExecute` with `resourceArn`, `secretArn`, `database`, `sql`, and `parameterSets`.
4. Check `updateResults` -- each entry's `generatedFields` contains auto-generated values for the corresponding row.

### 4. Migrate from ExecuteSql to Execute

1. Replace `dbClusterOrInstanceArn` with `resourceArn` and `awsSecretStoreArn` with `secretArn`.
2. Replace `sqlStatements` (semicolon-separated) with individual `sql` calls -- one per statement.
3. For multi-statement flows, wrap in a transaction using `BeginTransaction` / `CommitTransaction`.
4. Add `includeResultMetadata: true` to preserve column info that `ExecuteSql` returned by default.
5. Update response parsing: `sqlStatementResults` becomes `records` + `columnMetadata`.

### 5. Handle Long-Running Queries

1. Call `POST /Execute` with `continueAfterTimeout: true` to prevent the Data API from aborting after the default timeout.
2. Wrap the call in a transaction (`BeginTransaction` first) so partial results are consistent.
3. Check `numberOfRecordsUpdated` to confirm the full operation completed.
4. If the response is still truncated or an error occurs, roll back the transaction and retry with a narrower query scope.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
