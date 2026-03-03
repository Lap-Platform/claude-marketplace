---
name: amazon-augmented-ai-runtime
description: "Amazon Augmented AI Runtime API skill. Use when working with Amazon Augmented AI Runtime for human-loops. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Augmented AI Runtime
API version: 2019-11-07

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /human-loops -- verify access
3. POST /human-loops -- create first human-loops

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### human-loops
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /human-loops/{HumanLoopName} | Deletes the specified human loop for a flow definition. If the human loop was deleted, this operation will return a ResourceNotFoundException. |
| GET | /human-loops/{HumanLoopName} | Returns information about the specified human loop. If the human loop was deleted, this operation will return a ResourceNotFoundException error. |
| GET | /human-loops | Returns information about human loops, given the specified parameters. If a human loop was deleted, it will not be included. |
| POST | /human-loops | Starts a human loop, provided that at least one activation condition is met. |
| POST | /human-loops/stop | Stops the specified human loop. |

## Enhanced Skill Content


## Question Mapping

- "How do I create a new human review loop?" -> POST /human-loops
- "How do I list all human loops for a flow definition?" -> GET /human-loops
- "What is the status of my human loop?" -> GET /human-loops/{HumanLoopName}
- "How do I delete a human loop?" -> DELETE /human-loops/{HumanLoopName}
- "How do I stop a running human loop?" -> POST /human-loops/stop
- "Where can I find the output of a completed human loop?" -> GET /human-loops/{HumanLoopName} (check HumanLoopOutput.OutputS3Uri)
- "Why did my human loop fail?" -> GET /human-loops/{HumanLoopName} (check FailureReason and FailureCode)
- "How do I paginate through all human loops?" -> GET /human-loops (use NextToken from previous response)
- "How do I filter human loops by creation date?" -> GET /human-loops (use CreationTimeAfter/CreationTimeBefore)
- "How do I sort human loops?" -> GET /human-loops (use SortOrder parameter)
- "What ARN was assigned to my new human loop?" -> POST /human-loops (check HumanLoopArn in response)
- "How do I cancel a human loop without deleting it?" -> POST /human-loops/stop
- "How do I clean up old human loops?" -> GET /human-loops (filter by date) then DELETE /human-loops/{HumanLoopName} for each

## Response Tips

- **Single loop detail** (GET /human-loops/{name}): HumanLoopOutput is only present when status is "Completed" -- check HumanLoopStatus before accessing OutputS3Uri.
- **Loop listing** (GET /human-loops): Paginated via NextToken; keep calling with the returned NextToken until it is null. MaxResults caps per-page size.
- **Loop creation** (POST /human-loops): HumanLoopArn may be null in edge cases -- always null-check before storing.
- **Delete/Stop** (DELETE, POST /stop): Empty 200 response indicates success; any non-2xx means the operation failed.

## Anomaly Flags

- **Failed loops**: Surface immediately when HumanLoopStatus is "Failed" -- include FailureReason and FailureCode in the alert.
- **Missing output**: Flag when status is "Completed" but HumanLoopOutput is null or OutputS3Uri is empty.
- **Stale loops**: Warn when loops have been in "InProgress" status for an unusually long time (compare CreationTime to now).
- **Pagination overflow**: Flag if repeated listing calls return the same NextToken, indicating a possible API issue.
- **Throttling**: Surface AWS throttling errors (HTTP 429 or "ThrottlingException") and suggest exponential backoff.
- **Deprecated flow definitions**: Flag if FlowDefinitionArn references a deleted or inactive flow definition (will cause creation failures).

## Playbook

### 1. Create and Monitor a Human Review Loop

1. Call POST /human-loops with HumanLoopName, FlowDefinitionArn, and HumanLoopInput.
2. Store the returned HumanLoopArn for reference.
3. Poll GET /human-loops/{HumanLoopName} periodically.
4. When HumanLoopStatus changes to "Completed", retrieve the output from HumanLoopOutput.OutputS3Uri.
5. If status is "Failed", inspect FailureReason and FailureCode to diagnose.

### 2. List and Filter Human Loops by Date Range

1. Call GET /human-loops with FlowDefinitionArn and set CreationTimeAfter/CreationTimeBefore to your desired range.
2. Optionally set SortOrder to "Ascending" or "Descending".
3. Process the HumanLoopSummaries array from the response.
4. If NextToken is present, repeat the call with NextToken to fetch the next page.
5. Continue until NextToken is null.

### 3. Gracefully Stop and Clean Up a Human Loop

1. Call POST /human-loops/stop with the HumanLoopName to halt processing.
2. Call GET /human-loops/{HumanLoopName} to confirm status changed (no longer "InProgress").
3. If the loop is no longer needed, call DELETE /human-loops/{HumanLoopName} to remove it.
4. Verify deletion by calling GET /human-loops/{HumanLoopName} and confirming a 404 or error response.

### 4. Bulk Cleanup of Old Human Loops

1. Call GET /human-loops with FlowDefinitionArn and CreationTimeBefore set to your cutoff date.
2. Iterate through all pages using NextToken.
3. For each loop in HumanLoopSummaries, call DELETE /human-loops/{HumanLoopName}.
4. Log successes and failures; retry any throttled requests with exponential backoff.
5. Verify cleanup by re-listing with the same filters to confirm an empty result.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
