---
name: amazon-qldb
description: "Amazon QLDB API skill. Use when working with Amazon QLDB for ledgers, journal-s3-exports, tags. Covers 20 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon QLDB
API version: 2019-01-02

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /journal-s3-exports -- verify access
3. POST /ledgers -- create first ledgers

## Endpoints

20 endpoints across 3 groups. See references/api-spec.lap for full details.

### ledgers
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /ledgers/{name}/journal-kinesis-streams/{streamId} | Ends a given Amazon QLDB journal stream. Before a stream can be canceled, its current status must be ACTIVE. You can't restart a stream after you cancel it. Canceled QLDB stream resources are subject to a 7-day retention period, so they are automatically deleted after this limit expires. |
| POST | /ledgers | Creates a new ledger in your Amazon Web Services account in the current Region. |
| DELETE | /ledgers/{name} | Deletes a ledger and all of its contents. This action is irreversible. If deletion protection is enabled, you must first disable it before you can delete the ledger. You can disable it by calling the UpdateLedger operation to set this parameter to false. |
| GET | /ledgers/{name}/journal-kinesis-streams/{streamId} | Returns detailed information about a given Amazon QLDB journal stream. The output includes the Amazon Resource Name (ARN), stream name, current status, creation time, and the parameters of the original stream creation request. This action does not return any expired journal streams. For more information, see Expiration for terminal streams in the Amazon QLDB Developer Guide. |
| GET | /ledgers/{name}/journal-s3-exports/{exportId} | Returns information about a journal export job, including the ledger name, export ID, creation time, current status, and the parameters of the original export creation request. This action does not return any expired export jobs. For more information, see Export job expiration in the Amazon QLDB Developer Guide. If the export job with the given ExportId doesn't exist, then throws ResourceNotFoundException. If the ledger with the given Name doesn't exist, then throws ResourceNotFoundException. |
| GET | /ledgers/{name} | Returns information about a ledger, including its state, permissions mode, encryption at rest settings, and when it was created. |
| POST | /ledgers/{name}/journal-s3-exports | Exports journal contents within a date and time range from a ledger into a specified Amazon Simple Storage Service (Amazon S3) bucket. A journal export job can write the data objects in either the text or binary representation of Amazon Ion format, or in JSON Lines text format. If the ledger with the given Name doesn't exist, then throws ResourceNotFoundException. If the ledger with the given Name is in CREATING status, then throws ResourcePreconditionNotMetException. You can initiate up to two concurrent journal export requests for each ledger. Beyond this limit, journal export requests throw LimitExceededException. |
| POST | /ledgers/{name}/block | Returns a block object at a specified address in a journal. Also returns a proof of the specified block for verification if DigestTipAddress is provided. For information about the data contents in a block, see Journal contents in the Amazon QLDB Developer Guide. If the specified ledger doesn't exist or is in DELETING status, then throws ResourceNotFoundException. If the specified ledger is in CREATING status, then throws ResourcePreconditionNotMetException. If no block exists with the specified address, then throws InvalidParameterException. |
| POST | /ledgers/{name}/digest | Returns the digest of a ledger at the latest committed block in the journal. The response includes a 256-bit hash value and a block address. |
| POST | /ledgers/{name}/revision | Returns a revision data object for a specified document ID and block address. Also returns a proof of the specified revision for verification if DigestTipAddress is provided. |
| GET | /ledgers/{name}/journal-kinesis-streams | Returns all Amazon QLDB journal streams for a given ledger. This action does not return any expired journal streams. For more information, see Expiration for terminal streams in the Amazon QLDB Developer Guide. This action returns a maximum of MaxResults items. It is paginated so that you can retrieve all the items by calling ListJournalKinesisStreamsForLedger multiple times. |
| GET | /ledgers/{name}/journal-s3-exports | Returns all journal export jobs for a specified ledger. This action returns a maximum of MaxResults items, and is paginated so that you can retrieve all the items by calling ListJournalS3ExportsForLedger multiple times. This action does not return any expired export jobs. For more information, see Export job expiration in the Amazon QLDB Developer Guide. |
| GET | /ledgers | Returns all ledgers that are associated with the current Amazon Web Services account and Region. This action returns a maximum of MaxResults items and is paginated so that you can retrieve all the items by calling ListLedgers multiple times. |
| POST | /ledgers/{name}/journal-kinesis-streams | Creates a journal stream for a given Amazon QLDB ledger. The stream captures every document revision that is committed to the ledger's journal and delivers the data to a specified Amazon Kinesis Data Streams resource. |
| PATCH | /ledgers/{name} | Updates properties on a ledger. |
| PATCH | /ledgers/{name}/permissions-mode | Updates the permissions mode of a ledger.  Before you switch to the STANDARD permissions mode, you must first create all required IAM policies and table tags to avoid disruption to your users. To learn more, see Migrating to the standard permissions mode in the Amazon QLDB Developer Guide. |

### journal-s3-exports
| Method | Path | Description |
|--------|------|-------------|
| GET | /journal-s3-exports | Returns all journal export jobs for all ledgers that are associated with the current Amazon Web Services account and Region. This action returns a maximum of MaxResults items, and is paginated so that you can retrieve all the items by calling ListJournalS3Exports multiple times. This action does not return any expired export jobs. For more information, see Export job expiration in the Amazon QLDB Developer Guide. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{resourceArn} | Returns all tags for a specified Amazon QLDB resource. |
| POST | /tags/{resourceArn} | Adds one or more tags to a specified Amazon QLDB resource. A resource can have up to 50 tags. If you try to create more than 50 tags for a resource, your request fails and returns an error. |
| DELETE | /tags/{resourceArn} | Removes one or more tags from a specified Amazon QLDB resource. You can specify up to 50 tag keys to remove. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new QLDB ledger?" -> POST /ledgers
- "How do I delete a ledger?" -> DELETE /ledgers/{name}
- "What ledgers exist in my account?" -> GET /ledgers
- "What is the current state of my ledger?" -> GET /ledgers/{name}
- "How do I enable or disable deletion protection on a ledger?" -> PATCH /ledgers/{name}
- "How do I change the permissions mode of a ledger?" -> PATCH /ledgers/{name}/permissions-mode
- "How do I export journal blocks to S3?" -> POST /ledgers/{name}/journal-s3-exports
- "What is the status of my S3 export?" -> GET /ledgers/{name}/journal-s3-exports/{exportId}
- "How do I list all journal exports across all ledgers?" -> GET /journal-s3-exports
- "How do I stream journal data to Kinesis?" -> POST /ledgers/{name}/journal-kinesis-streams
- "How do I check if a Kinesis stream is active?" -> GET /ledgers/{name}/journal-kinesis-streams/{streamId}
- "How do I stop streaming to Kinesis?" -> DELETE /ledgers/{name}/journal-kinesis-streams/{streamId}
- "How do I get the current digest of a ledger for verification?" -> POST /ledgers/{name}/digest
- "How do I verify a specific document revision is intact?" -> POST /ledgers/{name}/revision
- "How do I get a specific block and its proof for cryptographic verification?" -> POST /ledgers/{name}/block

## Response Tips

- **Ledger operations**: State field transitions through `CREATING` -> `ACTIVE` -> `DELETING`; poll GET /ledgers/{name} until desired state is reached.
- **List endpoints** (GET /ledgers, GET /journal-s3-exports, GET /journal-kinesis-streams): Paginated via `NextToken` and `max_results`; loop until `NextToken` is null or absent.
- **Export/stream descriptions**: Contain nested configuration objects (S3EncryptionConfiguration, KinesisConfiguration); always destructure one level deeper to get actionable fields.
- **Verification endpoints** (block, revision, digest): Return `ValueHolder` objects with `IonText` strings that must be parsed as Amazon Ion format, not plain JSON.
- **Tag operations**: POST returns no body on success; DELETE requires `tagKeys` as a query string array, not a body field.

## Anomaly Flags

- **Ledger state is not ACTIVE**: Surface immediately if GET /ledgers/{name} returns State as `CREATING`, `DELETING`, or `DELETED` -- most operations will fail on non-active ledgers.
- **DeletionProtection is false**: Warn when describing a ledger that has deletion protection disabled, as it is vulnerable to accidental deletion.
- **KMS key inaccessible**: If `EncryptionDescription.InaccessibleKmsKeyDateTime` is present, the ledger's KMS key has become inaccessible -- this is a critical issue requiring immediate attention.
- **Kinesis stream in ERROR status**: If a stream's `Status` is `ERROR`, surface the `ErrorCause` field and recommend recreating the stream.
- **Export status not COMPLETED**: Flag S3 exports stuck in `IN_PROGRESS` for an unusually long time or in `CANCELLED`/`FAILED` status.
- **Permissions mode is STANDARD without IAM policies**: If `PermissionsMode` is `STANDARD`, remind the user that fine-grained IAM policies must be configured or access will be denied.

## Playbook

### 1. Create a Ledger and Verify It Is Ready

1. POST /ledgers with `Name`, `PermissionsMode` (use `STANDARD` for production), and optionally `DeletionProtection: true`.
2. Note the returned `Arn` and `State`.
3. Poll GET /ledgers/{name} until `State` equals `ACTIVE`.
4. Optionally tag the ledger with POST /tags/{resourceArn} using the ARN from step 2.

### 2. Export Journal Blocks to S3 for Auditing

1. GET /ledgers/{name} to confirm the ledger is `ACTIVE` and note its ARN.
2. POST /ledgers/{name}/journal-s3-exports with the time range (`InclusiveStartTime`, `ExclusiveEndTime`), `S3ExportConfiguration` (bucket, prefix, encryption), and `RoleArn`.
3. Save the returned `ExportId`.
4. Poll GET /ledgers/{name}/journal-s3-exports/{exportId} until `Status` is `COMPLETED`.
5. Access exported files in the specified S3 bucket and prefix.

### 3. Set Up Real-Time Streaming to Kinesis

1. Confirm the ledger is `ACTIVE` via GET /ledgers/{name}.
2. POST /ledgers/{name}/journal-kinesis-streams with `StreamName`, `RoleArn`, `InclusiveStartTime`, and `KinesisConfiguration` (including the target Kinesis `StreamArn`).
3. Save the returned `StreamId`.
4. Poll GET /ledgers/{name}/journal-kinesis-streams/{streamId} until `Status` is `ACTIVE`.
5. If `Status` becomes `ERROR`, read `ErrorCause`, fix the issue (usually IAM role permissions), delete the stream, and retry from step 2.

### 4. Cryptographically Verify a Document Revision

1. POST /ledgers/{name}/digest to get the current `Digest` and `DigestTipAddress`.
2. POST /ledgers/{name}/revision with the `BlockAddress` of the target revision, the `DocumentId`, and the `DigestTipAddress` from step 1.
3. Parse the returned `Revision.IonText` (Amazon Ion format) to read the document data.
4. Use the returned `Proof` along with the `Digest` to perform local hash-chain verification.

### 5. Clean Up a Ledger and Its Resources

1. GET /ledgers/{name}/journal-kinesis-streams to list all active streams.
2. For each stream, DELETE /ledgers/{name}/journal-kinesis-streams/{streamId}.
3. If `DeletionProtection` is enabled, PATCH /ledgers/{name} with `DeletionProtection: false`.
4. DELETE /ledgers/{name} to initiate ledger deletion.
5. Optionally poll GET /ledgers/{name} to confirm the ledger reaches `DELETED` state (or returns 404).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
