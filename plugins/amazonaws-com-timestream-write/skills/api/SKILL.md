---
name: amazon-timestream-write
description: "Amazon Timestream Write API skill. Use when working with Amazon Timestream Write for root. Covers 19 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Timestream Write
API version: 2018-11-01

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

19 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Creates a new Timestream batch load task. A batch load task processes data from a CSV source in an S3 location and writes to a Timestream table. A mapping from source to target is defined in a batch load task. Errors and events are written to a report at an S3 location. For the report, if the KMS key is not specified, the report will be encrypted with an S3 managed key when SSE_S3 is the option. Otherwise an error is thrown. For more information, see Amazon Web Services managed keys. Service quotas apply. For details, see code sample. |
| POST | / | Creates a new Timestream database. If the KMS key is not specified, the database will be encrypted with a Timestream managed KMS key located in your account. For more information, see Amazon Web Services managed keys. Service quotas apply. For details, see code sample. |
| POST | / | Adds a new table to an existing database in your account. In an Amazon Web Services account, table names must be at least unique within each Region if they are in the same database. You might have identical table names in the same Region if the tables are in separate databases. While creating the table, you must specify the table name, database name, and the retention properties. Service quotas apply. See code sample for details. |
| POST | / | Deletes a given Timestream database. This is an irreversible operation. After a database is deleted, the time-series data from its tables cannot be recovered.   All tables in the database must be deleted first, or a ValidationException error will be thrown.  Due to the nature of distributed retries, the operation can return either success or a ResourceNotFoundException. Clients should consider them equivalent.  See code sample for details. |
| POST | / | Deletes a given Timestream table. This is an irreversible operation. After a Timestream database table is deleted, the time-series data stored in the table cannot be recovered.   Due to the nature of distributed retries, the operation can return either success or a ResourceNotFoundException. Clients should consider them equivalent.  See code sample for details. |
| POST | / | Returns information about the batch load task, including configurations, mappings, progress, and other details. Service quotas apply. See code sample for details. |
| POST | / | Returns information about the database, including the database name, time that the database was created, and the total number of tables found within the database. Service quotas apply. See code sample for details. |
| POST | / | Returns a list of available endpoints to make Timestream API calls against. This API operation is available through both the Write and Query APIs. Because the Timestream SDKs are designed to transparently work with the service’s architecture, including the management and mapping of the service endpoints, we don't recommend that you use this API operation unless:   You are using VPC endpoints (Amazon Web Services PrivateLink) with Timestream    Your application uses a programming language that does not yet have SDK support   You require better control over the client-side implementation   For detailed information on how and when to use and implement DescribeEndpoints, see The Endpoint Discovery Pattern. |
| POST | / | Returns information about the table, including the table name, database name, retention duration of the memory store and the magnetic store. Service quotas apply. See code sample for details. |
| POST | / | Provides a list of batch load tasks, along with the name, status, when the task is resumable until, and other details. See code sample for details. |
| POST | / | Returns a list of your Timestream databases. Service quotas apply. See code sample for details. |
| POST | / | Provides a list of tables, along with the name, status, and retention properties of each table. See code sample for details. |
| POST | / | Lists all tags on a Timestream resource. |
| POST | / |  |
| POST | / | Associates a set of tags with a Timestream resource. You can then activate these user-defined tags so that they appear on the Billing and Cost Management console for cost allocation tracking. |
| POST | / | Removes the association of tags from a Timestream resource. |
| POST | / | Modifies the KMS key for an existing database. While updating the database, you must specify the database name and the identifier of the new KMS key to be used (KmsKeyId). If there are any concurrent UpdateDatabase requests, first writer wins.  See code sample for details. |
| POST | / | Modifies the retention duration of the memory store and magnetic store for your Timestream table. Note that the change in retention duration takes effect immediately. For example, if the retention period of the memory store was initially set to 2 hours and then changed to 24 hours, the memory store will be capable of holding 24 hours of data, but will be populated with 24 hours of data 22 hours after this change was made. Timestream does not retrieve data from the magnetic store to populate the memory store.  See code sample for details. |
| POST | / | Enables you to write your time-series data into Timestream. You can specify a single data point or a batch of data points to be inserted into the system. Timestream offers you a flexible schema that auto detects the column names and data types for your Timestream tables based on the dimension names and data types of the data points you specify when invoking writes into the database.  Timestream supports eventual consistency read semantics. This means that when you query data immediately after writing a batch of data into Timestream, the query results might not reflect the results of a recently completed write operation. The results may also include some stale data. If you repeat the query request after a short time, the results should return the latest data. Service quotas apply.  See code sample for details.  Upserts  You can use the Version parameter in a WriteRecords request to update data points. Timestream tracks a version number with each record. Version defaults to 1 when it's not specified for the record in the request. Timestream updates an existing record’s measure value along with its Version when it receives a write request with a higher Version number for that record. When it receives an update request where the measure value is the same as that of the existing record, Timestream still updates Version, if it is greater than the existing value of Version. You can update a data point as many times as desired, as long as the value of Version continuously increases.   For example, suppose you write a new record without indicating Version in the request. Timestream stores this record, and set Version to 1. Now, suppose you try to update this record with a WriteRecords request of the same record with a different measure value but, like before, do not provide Version. In this case, Timestream will reject this update with a RejectedRecordsException since the updated record’s version is not greater than the existing value of Version.  However, if you were to resend the update request with Version set to 2, Timestream would then succeed in updating the record’s value, and the Version would be set to 2. Next, suppose you sent a WriteRecords request with this same record and an identical measure value, but with Version set to 3. In this case, Timestream would only update Version to 3. Any further updates would need to send a version number greater than 3, or the update requests would receive a RejectedRecordsException. |

## Enhanced Skill Content
## Question Mapping

- "How do I write time-series records to Timestream?" -> POST / (WriteRecords: DatabaseName, TableName, Records)
- "How do I create a new Timestream database?" -> POST / (CreateDatabase: DatabaseName)
- "How do I create a table with custom retention settings?" -> POST / (CreateTable: DatabaseName, TableName, RetentionProperties)
- "How do I bulk-load data from S3 into Timestream?" -> POST / (CreateBatchLoadTask: DataSourceConfiguration, TargetDatabaseName, TargetTableName)
- "What is the status of my batch load job?" -> POST / (DescribeBatchLoadTask: TaskId)
- "How do I list all my Timestream databases?" -> POST / (ListDatabases: optional NextToken, MaxResults)
- "How do I list tables in a specific database?" -> POST / (ListTables: DatabaseName)
- "How do I check a table's retention policy and schema?" -> POST / (DescribeTable: DatabaseName, TableName)
- "How do I change the retention period on an existing table?" -> POST / (UpdateTable: DatabaseName, TableName, RetentionProperties)
- "How do I rotate the KMS key on a database?" -> POST / (UpdateDatabase: DatabaseName, KmsKeyId)
- "How do I delete a database or table?" -> POST / (DeleteDatabase: DatabaseName) or POST / (DeleteTable: DatabaseName, TableName)
- "How do I tag and untag Timestream resources?" -> POST / (TagResource: ResourceARN, Tags) and POST / (UntagResource: ResourceARN, TagKeys)
- "How do I resume a failed batch load task?" -> POST / (ResumeBatchLoadTask: TaskId)
- "How do I discover the correct Timestream ingest endpoint?" -> POST / (DescribeEndpoints)
- "How do I list all batch load tasks filtered by status?" -> POST / (ListBatchLoadTasks: TaskStatus)

## Response Tips

- **Write operations** (CreateDatabase, CreateTable, UpdateDatabase, UpdateTable): Return the full resource object; check nested `RetentionProperties` and `MagneticStoreWriteProperties` to confirm your settings took effect.
- **List operations** (ListDatabases, ListTables, ListBatchLoadTasks): Paginated via `NextToken`; keep calling with the returned `NextToken` until it is null. Respect `MaxResults` to control page size.
- **WriteRecords**: Returns `RecordsIngested` with `Total`, `MemoryStore`, and `MagneticStore` counts; compare `Total` against your submitted record count to detect partial failures.
- **DescribeBatchLoadTask**: The `ProgressReport` block contains granular counters (`RecordsProcessed`, `ParseFailures`, `RecordIngestionFailures`, `FileFailures`); check these rather than relying solely on `TaskStatus`.
- **Delete operations** (DeleteDatabase, DeleteTable): Return no body on success; a non-error response confirms deletion.
- **DescribeEndpoints**: Returns an array of `Endpoint` objects; cache the result and use the returned endpoint for all subsequent Timestream calls.

## Anomaly Flags

- **Partial ingestion**: `RecordsIngested.Total` is less than the number of records submitted in a WriteRecords call -- surface rejected records immediately.
- **Batch load failures climbing**: `ProgressReport.ParseFailures`, `RecordIngestionFailures`, or `FileFailures` are non-zero or increasing -- alert before the job completes so the user can fix source data.
- **Batch load task stuck**: `TaskStatus` remains unchanged across multiple DescribeBatchLoadTask polls, or `ResumableUntil` timestamp is approaching -- warn the user to resume or investigate.
- **Table status not ACTIVE**: `TableStatus` returned from CreateTable or UpdateTable is not `ACTIVE` (e.g., `DELETING`, `RESTORING`) -- flag that the table is not ready for writes.
- **Retention misconfiguration**: `MemoryStoreRetentionPeriodInHours` is very low (< 1) or `MagneticStoreRetentionPeriodInDays` is extremely high (> 73000, i.e., 200 years) -- likely a mistake.
- **MagneticStoreWrites disabled**: Records arriving outside the memory store retention window will be silently rejected if `EnableMagneticStoreWrites` is `false` -- surface this when write errors occur.
- **Missing KmsKeyId on database**: Database created without explicit KMS key uses AWS-managed key; flag if organizational policy requires customer-managed keys.
- **Pagination abandoned**: A list response returned a `NextToken` but the workflow did not continue fetching -- warn that results are incomplete.

## Playbook

### 1. Set up a new Timestream database and table for ingestion

1. Call **DescribeEndpoints** to get the correct ingest endpoint URL; cache it.
2. Call **CreateDatabase** with your chosen `DatabaseName` and optional `KmsKeyId` for encryption.
3. Call **CreateTable** with `DatabaseName`, `TableName`, and `RetentionProperties` (e.g., 24h memory, 365d magnetic).
4. Optionally call **TagResource** with the table's ARN to apply cost-allocation or environment tags.
5. Confirm the table is ready by calling **DescribeTable** and verifying `TableStatus` is `ACTIVE`.

### 2. Ingest time-series data with error handling

1. Build an array of `Record` objects with dimensions, measure name, measure value, and timestamp.
2. Call **WriteRecords** with `DatabaseName`, `TableName`, `Records`, and optionally `CommonAttributes` for shared dimensions.
3. Compare `RecordsIngested.Total` against the submitted count; if fewer, inspect the error response for rejected record details.
4. On throttling errors, implement exponential backoff and retry; consider reducing batch size (max 100 records per call).
5. For late-arriving data, ensure `MagneticStoreWriteProperties.EnableMagneticStoreWrites` is `true` on the target table.

### 3. Bulk-load historical data from S3

1. Upload your CSV/JSON data files to an S3 bucket accessible by the Timestream service role.
2. Call **CreateBatchLoadTask** with `DataSourceConfiguration` (bucket, prefix, format), `ReportConfiguration` (report bucket), `TargetDatabaseName`, and `TargetTableName`.
3. Note the returned `TaskId`.
4. Poll **DescribeBatchLoadTask** with the `TaskId`; monitor `ProgressReport` fields for failures.
5. If the task fails and `ResumableUntil` has not passed, fix the source data issue and call **ResumeBatchLoadTask**.
6. After completion, review the report in the configured S3 report bucket for a full error manifest.

### 4. Modify retention and enable magnetic store writes on an existing table

1. Call **DescribeTable** to inspect current `RetentionProperties` and `MagneticStoreWriteProperties`.
2. Call **UpdateTable** with the new `RetentionProperties` (e.g., increase `MagneticStoreRetentionPeriodInDays` from 365 to 3650).
3. In the same **UpdateTable** call, set `MagneticStoreWriteProperties.EnableMagneticStoreWrites` to `true` and configure `MagneticStoreRejectedDataLocation` with an S3 bucket for rejected records.
4. Verify the update by calling **DescribeTable** again and confirming the returned properties match your intent.

### 5. Audit and manage resource tags

1. Call **ListDatabases** (paginate with `NextToken`) to enumerate all databases.
2. For each database, call **ListTables** with `DatabaseName` to get all tables.
3. For each resource, call **ListTagsForResource** with its ARN to retrieve current tags.
4. Call **TagResource** to add missing tags or **UntagResource** to remove stale ones.
5. Repeat periodically or trigger via automation to enforce tagging compliance.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
