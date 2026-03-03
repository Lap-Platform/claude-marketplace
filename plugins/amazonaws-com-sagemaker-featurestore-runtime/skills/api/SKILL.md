---
name: amazon-sagemaker-feature-store-runtime
description: "Amazon SageMaker Feature Store Runtime API skill. Use when working with Amazon SageMaker Feature Store Runtime for BatchGetRecord, FeatureGroup. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon SageMaker Feature Store Runtime
API version: 2020-07-01

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /FeatureGroup/{FeatureGroupName} -- verify access
3. POST /BatchGetRecord -- create first BatchGetRecord

## Endpoints

4 endpoints across 2 groups. See references/api-spec.lap for full details.

### BatchGetRecord
| Method | Path | Description |
|--------|------|-------------|
| POST | /BatchGetRecord | Retrieves a batch of Records from a FeatureGroup. |

### FeatureGroup
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /FeatureGroup/{FeatureGroupName} | Deletes a Record from a FeatureGroup in the OnlineStore. Feature Store supports both SoftDelete and HardDelete. For SoftDelete (default), feature columns are set to null and the record is no longer retrievable by GetRecord or BatchGetRecord. For HardDelete, the complete Record is removed from the OnlineStore. In both cases, Feature Store appends the deleted record marker to the OfflineStore. The deleted record marker is a record with the same RecordIdentifer as the original, but with is_deleted value set to True, EventTime set to the delete input EventTime, and other feature values set to null. Note that the EventTime specified in DeleteRecord should be set later than the EventTime of the existing record in the OnlineStore for that RecordIdentifer. If it is not, the deletion does not occur:   For SoftDelete, the existing (not deleted) record remains in the OnlineStore, though the delete record marker is still written to the OfflineStore.    HardDelete returns EventTime: 400 ValidationException to indicate that the delete operation failed. No delete record marker is written to the OfflineStore.   When a record is deleted from the OnlineStore, the deleted record marker is appended to the OfflineStore. If you have the Iceberg table format enabled for your OfflineStore, you can remove all history of a record from the OfflineStore using Amazon Athena or Apache Spark. For information on how to hard delete a record from the OfflineStore with the Iceberg table format enabled, see Delete records from the offline store. |
| GET | /FeatureGroup/{FeatureGroupName} | Use for OnlineStore serving from a FeatureStore. Only the latest records stored in the OnlineStore can be retrieved. If no Record with RecordIdentifierValue is found, then an empty result is returned. |
| PUT | /FeatureGroup/{FeatureGroupName} | The PutRecord API is used to ingest a list of Records into your feature group.  If a new record’s EventTime is greater, the new record is written to both the OnlineStore and OfflineStore. Otherwise, the record is a historic record and it is written only to the OfflineStore.  You can specify the ingestion to be applied to the OnlineStore, OfflineStore, or both by using the TargetStores request parameter.  You can set the ingested record to expire at a given time to live (TTL) duration after the record’s event time, ExpiresAt = EventTime + TtlDuration, by specifying the TtlDuration parameter. A record level TtlDuration is set when specifying the TtlDuration parameter using the PutRecord API call. If the input TtlDuration is null or unspecified, TtlDuration is set to the default feature group level TtlDuration. A record level TtlDuration supersedes the group level TtlDuration. |

## Enhanced Skill Content
## Question Mapping

- "How do I get a single record from a feature group?" -> GET /FeatureGroup/{FeatureGroupName}
- "How do I fetch multiple records across feature groups in one call?" -> POST /BatchGetRecord
- "How do I write a record to a feature group?" -> PUT /FeatureGroup/{FeatureGroupName}
- "How do I delete a record from a feature group?" -> DELETE /FeatureGroup/{FeatureGroupName}
- "Can I retrieve only specific features instead of the full record?" -> GET /FeatureGroup/{FeatureGroupName} (use FeatureName filter)
- "How do I check when a record expires?" -> GET /FeatureGroup/{FeatureGroupName} (use ExpirationTimeResponse)
- "How do I set a TTL on a record?" -> PUT /FeatureGroup/{FeatureGroupName} (use TtlDuration)
- "How do I delete a record from only the online or offline store?" -> DELETE /FeatureGroup/{FeatureGroupName} (use TargetStores + DeletionMode)
- "What happens if some records fail in a batch get?" -> POST /BatchGetRecord (check Errors and UnprocessedIdentifiers)
- "How do I soft-delete vs hard-delete a record?" -> DELETE /FeatureGroup/{FeatureGroupName} (use DeletionMode)
- "How do I write a record to only the online store?" -> PUT /FeatureGroup/{FeatureGroupName} (use TargetStores)
- "How do I look up a record by its identifier value?" -> GET /FeatureGroup/{FeatureGroupName} (RecordIdentifierValueAsString is required)
- "How do I batch-retrieve records and also get expiration times?" -> POST /BatchGetRecord (use ExpirationTimeResponse)

## Response Tips

- **BatchGetRecord**: Always check all three response arrays -- `Records` for successes, `Errors` for failures, and `UnprocessedIdentifiers` for items that need retry.
- **GET FeatureGroup**: `Record` and `ExpiresAt` are both optional (nullable) -- a 200 with null Record means the identifier exists but has no stored features.
- **PUT/DELETE FeatureGroup**: No response body on success; rely on HTTP status code (200) to confirm the operation completed.
- **General**: All endpoints use AWS SigV4 auth; a 403 typically means incorrect signing, wrong region, or missing IAM permissions on the feature group resource.

## Anomaly Flags

- **Partial batch failures**: If `Errors` or `UnprocessedIdentifiers` are non-empty in a BatchGetRecord response, surface these immediately -- they indicate throttling, missing feature groups, or permission issues on specific identifiers.
- **Null Record on 200**: A successful GET returning `Record: null` may indicate the record was soft-deleted or expired; flag this if the caller expected data.
- **ExpiresAt in the past**: If a GET returns an `ExpiresAt` timestamp that has already passed, the record is stale and may be purged soon -- warn the user.
- **DeletionMode mismatch**: If a DELETE uses `SoftDelete` mode but the caller later expects the record to be fully gone from the offline store, flag the inconsistency.
- **Missing TargetStores on write**: If the user writes to both stores (default) but only needs online serving, flag the unnecessary offline store cost.

## Playbook

### 1. Retrieve a Single Feature Record

1. Identify the feature group name and the record identifier value.
2. Call `GET /FeatureGroup/{FeatureGroupName}` with `RecordIdentifierValueAsString`.
3. Optionally pass `FeatureName` array to retrieve only specific features.
4. Check if `Record` is null (record may not exist or may be expired).
5. If `ExpiresAt` is present, verify it is in the future.

### 2. Batch Retrieve Records Across Feature Groups

1. Build an `Identifiers` array of `BatchGetRecordIdentifier` objects, each specifying a feature group and record identifier.
2. Call `POST /BatchGetRecord` with the identifiers.
3. Process the `Records` array for successful retrievals.
4. Check `Errors` for any failed lookups and log the error codes.
5. Retry any items listed in `UnprocessedIdentifiers` using exponential backoff.

### 3. Write a Record with TTL

1. Construct the `Record` as an array of `FeatureValue` objects (name-value pairs).
2. Call `PUT /FeatureGroup/{FeatureGroupName}` with the record and a `TtlDuration` specifying the expiration window.
3. Optionally set `TargetStores` to write only to `OnlineStore` or `OfflineStore`.
4. Confirm success via 200 status code.

### 4. Soft-Delete Then Hard-Delete a Record

1. Call `DELETE /FeatureGroup/{FeatureGroupName}` with `DeletionMode: "SoftDelete"` and the required `EventTime` timestamp to mark the record as deleted while preserving history in the offline store.
2. Verify the record is no longer returned by `GET`.
3. When ready to permanently remove, call `DELETE` again with `DeletionMode: "HardDelete"` and `TargetStores: ["OfflineStore"]` to purge from the offline store.

### 5. Populate a Feature Group from a Data Pipeline

1. For each row in the source data, map columns to `FeatureValue` objects.
2. Call `PUT /FeatureGroup/{FeatureGroupName}` for each record, setting `TargetStores` to `["OnlineStore", "OfflineStore"]` for dual-write.
3. Set `TtlDuration` if records should auto-expire.
4. After ingestion, verify a sample using `POST /BatchGetRecord` with a subset of identifiers.
5. Check for any entries in `Errors` or `UnprocessedIdentifiers` to catch ingestion gaps.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
