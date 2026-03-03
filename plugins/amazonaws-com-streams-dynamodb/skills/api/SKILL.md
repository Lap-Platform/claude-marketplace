---
name: amazon-dynamodb-streams
description: "Amazon DynamoDB Streams API skill. Use when working with Amazon DynamoDB Streams for root. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon DynamoDB Streams
API version: 2012-08-10

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Returns information about a stream, including the current status of the stream, its Amazon Resource Name (ARN), the composition of its shards, and its corresponding DynamoDB table.  You can call DescribeStream at a maximum rate of 10 times per second.  Each shard in the stream has a SequenceNumberRange associated with it. If the SequenceNumberRange has a StartingSequenceNumber but no EndingSequenceNumber, then the shard is still open (able to receive more stream records). If both StartingSequenceNumber and EndingSequenceNumber are present, then that shard is closed and can no longer receive more data. |
| POST | / | Retrieves the stream records from a given shard. Specify a shard iterator using the ShardIterator parameter. The shard iterator specifies the position in the shard from which you want to start reading stream records sequentially. If there are no stream records available in the portion of the shard that the iterator points to, GetRecords returns an empty list. Note that it might take multiple calls to get to a portion of the shard that contains stream records.   GetRecords can retrieve a maximum of 1 MB of data or 1000 stream records, whichever comes first. |
| POST | / | Returns a shard iterator. A shard iterator provides information about how to retrieve the stream records from within a shard. Use the shard iterator in a subsequent GetRecords request to read the stream records from the shard.  A shard iterator expires 15 minutes after it is returned to the requester. |
| POST | / | Returns an array of stream ARNs associated with the current account and endpoint. If the TableName parameter is present, then ListStreams will return only the streams ARNs for that table.  You can call ListStreams at a maximum rate of 5 times per second. |

## Enhanced Skill Content
## Question Mapping

- "What streams exist for my DynamoDB table?" -> POST / (ListStreams with TableName)
- "Show me all DynamoDB streams in my account" -> POST / (ListStreams without TableName)
- "What are the details of this stream?" -> POST / (DescribeStream with StreamArn)
- "What shards does my stream have?" -> POST / (DescribeStream, read Shards array)
- "How do I start reading records from a shard?" -> POST / (GetShardIterator with ShardIteratorType)
- "Get the latest changes from a shard" -> POST / (GetShardIterator with ShardIteratorType=LATEST, then GetRecords)
- "Read all records from the beginning of a shard" -> POST / (GetShardIterator with ShardIteratorType=TRIM_HORIZON, then GetRecords)
- "Get the next batch of records after my last read" -> POST / (GetRecords with NextShardIterator from previous call)
- "Resume reading from a specific sequence number" -> POST / (GetShardIterator with ShardIteratorType=AFTER_SEQUENCE_NUMBER + SequenceNumber)
- "Is my stream enabled and active?" -> POST / (DescribeStream, check StreamStatus field)
- "What view type is configured on my stream?" -> POST / (DescribeStream, read StreamViewType)
- "Are there more streams I haven't listed yet?" -> POST / (ListStreams, check LastEvaluatedStreamArn presence)
- "Are there more shards I haven't seen?" -> POST / (DescribeStream, check LastEvaluatedShardId presence)
- "When was this stream created?" -> POST / (DescribeStream, read CreationRequestDateTime)

## Response Tips

- **ListStreams**: Paginated via `LastEvaluatedStreamArn` -- if present, pass it as `ExclusiveStartStreamArn` in the next call to get more results.
- **DescribeStream**: Shard list may be paginated via `LastEvaluatedShardId` -- if present, pass it as `ExclusiveStartShardId` to continue. `StreamStatus` values are ENABLING, ENABLED, DISABLING, DISABLED.
- **GetShardIterator**: Returns a single opaque `ShardIterator` string that expires after 15 minutes of inactivity. Treat it as a cursor, not a stable reference.
- **GetRecords**: `Records` may be empty even when the shard is active (no new changes yet). Always use `NextShardIterator` for the next poll unless it is null (shard is closed).

## Anomaly Flags

- **Shard iterator expiration**: Surface a warning if GetRecords returns an `ExpiredIteratorException` -- the agent should automatically re-obtain the iterator via GetShardIterator.
- **Empty Records with non-null NextShardIterator**: Normal, but if it persists across many polls, flag that the shard may have low throughput or the table is idle.
- **Null NextShardIterator**: The shard has been closed (parent shard split/merged). Agent should surface this and suggest reading child shards from DescribeStream.
- **StreamStatus not ENABLED**: If DescribeStream returns DISABLING or DISABLED, warn the user that records may stop flowing.
- **Pagination truncation**: If ListStreams or DescribeStream returns a continuation token, proactively note that results are incomplete and offer to fetch the next page.
- **Throttling (400 LimitExceededException)**: DynamoDB Streams has low read limits per shard. Surface backoff guidance (wait 1s+) when this occurs.
- **StreamViewType mismatch**: If the user expects full item images but StreamViewType is KEYS_ONLY or OLD_IMAGE, flag that the stream won't include the data they need.

## Playbook

### 1. Tail a Stream for Real-Time Changes

1. Call **ListStreams** with `TableName` to find the stream ARN for your table.
2. Call **DescribeStream** with the `StreamArn` to get the list of shards.
3. For each open shard, call **GetShardIterator** with `ShardIteratorType=LATEST` to start from now.
4. Poll **GetRecords** using the returned `ShardIterator`.
5. Use `NextShardIterator` from each response for subsequent polls. If null, the shard closed -- re-check DescribeStream for child shards.

### 2. Replay All Historical Records from a Stream

1. Call **DescribeStream** to list all shards (paginate with `ExclusiveStartShardId` if needed).
2. Identify root shards (those without `ParentShardId`).
3. For each root shard, call **GetShardIterator** with `ShardIteratorType=TRIM_HORIZON`.
4. Poll **GetRecords** until `NextShardIterator` is null (shard exhausted).
5. Follow the shard lineage: when a shard closes, read its child shards in order.

### 3. Resume Processing from a Known Position

1. Store the last successfully processed `SequenceNumber` from a previous GetRecords call.
2. Call **GetShardIterator** with `ShardIteratorType=AFTER_SEQUENCE_NUMBER` and the stored `SequenceNumber`.
3. Continue polling **GetRecords** with the new iterator.
4. If the shard has closed and the sequence number is no longer valid, re-discover shards via DescribeStream and locate the successor shard.

### 4. Discover and Inventory All Streams

1. Call **ListStreams** without `TableName` to get all streams in the account.
2. If `LastEvaluatedStreamArn` is present, pass it as `ExclusiveStartStreamArn` and repeat.
3. For each stream, call **DescribeStream** to get status, view type, shard count, and table association.
4. Build an inventory grouping streams by `TableName` and `StreamStatus`.

### 5. Handle Shard Splits and Merges

1. Call **DescribeStream** and examine each shard's `ParentShardId` and `SequenceNumberRange`.
2. A shard with `EndingSequenceNumber` set is closed -- identify its children by finding shards whose `ParentShardId` matches.
3. Finish reading the parent shard (GetRecords until `NextShardIterator` is null).
4. Begin reading each child shard with `ShardIteratorType=TRIM_HORIZON` to pick up where the parent left off.
5. Maintain a shard graph to avoid re-processing or missing records during topology changes.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
