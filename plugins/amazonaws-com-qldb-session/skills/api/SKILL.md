---
name: amazon-qldb-session
description: "Amazon QLDB Session API skill. Use when working with Amazon QLDB Session for root. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Amazon QLDB Session
API version: 2019-07-11

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Sends a command to an Amazon QLDB ledger.  Instead of interacting directly with this API, we recommend using the QLDB driver or the QLDB shell to execute data transactions on a ledger.   If you are working with an AWS SDK, use the QLDB driver. The driver provides a high-level abstraction layer above this QLDB Session data plane and manages SendCommand API calls for you. For information and a list of supported programming languages, see Getting started with the driver in the Amazon QLDB Developer Guide.   If you are working with the AWS Command Line Interface (AWS CLI), use the QLDB shell. The shell is a command line interface that uses the QLDB driver to interact with a ledger. For information, see Accessing Amazon QLDB using the QLDB shell. |

## Enhanced Skill Content
## Question Mapping

- "How do I connect to a QLDB ledger?" -> POST / (with StartSession)
- "How do I start a new transaction?" -> POST / (with StartTransaction)
- "How do I run a PartiQL query against my ledger?" -> POST / (with ExecuteStatement)
- "How do I commit a transaction?" -> POST / (with CommitTransaction)
- "How do I roll back a transaction?" -> POST / (with AbortTransaction)
- "How do I end my QLDB session?" -> POST / (with EndSession)
- "How do I paginate through large query results?" -> POST / (with FetchPage)
- "How do I check how many read/write IOs a query consumed?" -> POST / (with ExecuteStatement or CommitTransaction, inspect ConsumedIOs)
- "How do I measure query processing time?" -> POST / (inspect TimingInformation in any result)
- "How do I get a commit digest for verification?" -> POST / (with CommitTransaction, inspect CommitDigest)
- "How do I execute a statement and fetch all pages of results?" -> POST / (ExecuteStatement, then repeated FetchPage with NextPageToken)
- "How do I insert a document into a QLDB table?" -> POST / (StartTransaction + ExecuteStatement with INSERT PartiQL + CommitTransaction)
- "How do I read the current state of a document?" -> POST / (StartTransaction + ExecuteStatement with SELECT PartiQL + CommitTransaction)

## Response Tips

- **Session operations** (StartSession/EndSession): Return a SessionToken on start; include it in all subsequent requests. EndSession returns only timing info.
- **Transaction lifecycle** (StartTransaction/CommitTransaction/AbortTransaction): StartTransaction returns a TransactionId required for ExecuteStatement and CommitTransaction. CommitTransaction includes a CommitDigest (bytes) and ConsumedIOs.
- **Query results** (ExecuteStatement/FetchPage): Results come in Pages containing Values (array of ValueHolder). If NextPageToken is present, more pages remain -- call FetchPage with that token. ConsumedIOs accumulate across pages.
- **Timing** (all operations): Every result includes an optional TimingInformation block with ProcessingTimeMilliseconds (int64); use it for performance monitoring.
- **Errors**: This is a single-endpoint multiplexed API -- errors arrive as standard AWS error responses (check `__type` and `message` fields); common ones include `BadRequestException`, `InvalidSessionException`, `OccConflictException`, and `LimitExceededException`.

## Anomaly Flags

- **OCC conflict detected**: Surface `OccConflictException` immediately -- the transaction must be retried from StartTransaction, not just re-committed.
- **Invalid session**: Flag `InvalidSessionException` -- the session expired or was invalidated; a new StartSession is required before any further operations.
- **High IO consumption**: Alert when ConsumedIOs (ReadIOs or WriteIOs) exceeds expected thresholds, as this affects cost directly.
- **Slow processing time**: Flag when ProcessingTimeMilliseconds exceeds a reasonable baseline (e.g., >1000ms), which may indicate table scan queries or ledger contention.
- **Missing NextPageToken assumption**: Warn if a FetchPage call returns no Values and no NextPageToken -- this may indicate the result set was empty or the token expired.
- **Rate limiting**: Surface `LimitExceededException` and recommend exponential backoff before retrying.
- **Session token reuse after EndSession**: Flag any attempt to use a SessionToken after EndSession has been called -- it will fail.

## Playbook

### 1. Execute a Single Query (Read)

1. Call POST / with `StartSession: { LedgerName: "my-ledger" }` to get a SessionToken.
2. Call POST / with `SessionToken`, `StartTransaction: {}` to get a TransactionId.
3. Call POST / with `SessionToken`, `ExecuteStatement: { TransactionId, Statement: "SELECT * FROM MyTable WHERE id = ?", Parameters: [...] }`.
4. If `FirstPage.NextPageToken` exists, call POST / with `SessionToken`, `FetchPage: { TransactionId, NextPageToken }` repeatedly until no NextPageToken remains.
5. Call POST / with `SessionToken`, `CommitTransaction: { TransactionId, CommitDigest }` to finalize.
6. Call POST / with `SessionToken`, `EndSession: {}` to clean up.

### 2. Insert a Document

1. Start a session and transaction (steps 1-2 above).
2. Call POST / with `ExecuteStatement: { TransactionId, Statement: "INSERT INTO MyTable ?", Parameters: [{ IonBinary: <ion-encoded-document> }] }`.
3. Inspect the returned document ID from `FirstPage.Values`.
4. Commit the transaction with the computed CommitDigest.
5. End the session.

### 3. Retry on OCC Conflict

1. Execute a read-modify-write workflow (start session, start transaction, execute SELECT, execute UPDATE, commit).
2. If CommitTransaction returns `OccConflictException`, do NOT re-commit.
3. Start a new transaction (reuse the same SessionToken).
4. Re-execute the full read-modify-write sequence with the new TransactionId.
5. Commit again. Repeat up to a maximum retry count (typically 3-4 attempts).

### 4. Paginate Through Large Results

1. Start a session and transaction.
2. Execute a broad query (e.g., `SELECT * FROM MyTable`).
3. Collect `FirstPage.Values` and note `FirstPage.NextPageToken`.
4. Loop: call FetchPage with the NextPageToken, accumulate Values, and track cumulative ConsumedIOs.
5. Stop when FetchPage returns no NextPageToken.
6. Commit or abort the transaction, then end the session.

### 5. Monitor Query Performance

1. After each ExecuteStatement or FetchPage call, extract `TimingInformation.ProcessingTimeMilliseconds`.
2. After CommitTransaction, extract both `TimingInformation` and `ConsumedIOs`.
3. Sum ReadIOs and WriteIOs across all operations in the transaction for total cost attribution.
4. Log or alert if processing time or IO counts exceed established baselines.
5. Use this data to identify candidates for query optimization (e.g., adding indexes or narrowing WHERE clauses).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
