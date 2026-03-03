---
name: amazon-timestream-query
description: "Amazon Timestream Query API skill. Use when working with Amazon Timestream Query for root. Covers 15 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Timestream Query
API version: 2018-11-01

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

15 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Cancels a query that has been issued. Cancellation is provided only if the query has not completed running before the cancellation request was issued. Because cancellation is an idempotent operation, subsequent cancellation requests will return a CancellationMessage, indicating that the query has already been canceled. See code sample for details. |
| POST | / | Create a scheduled query that will be run on your behalf at the configured schedule. Timestream assumes the execution role provided as part of the ScheduledQueryExecutionRoleArn parameter to run the query. You can use the NotificationConfiguration parameter to configure notification for your scheduled query operations. |
| POST | / | Deletes a given scheduled query. This is an irreversible operation. |
| POST | / | Describes the settings for your account that include the query pricing model and the configured maximum TCUs the service can use for your query workload. You're charged only for the duration of compute units used for your workloads. |
| POST | / | DescribeEndpoints returns a list of available endpoints to make Timestream API calls against. This API is available through both Write and Query. Because the Timestream SDKs are designed to transparently work with the service’s architecture, including the management and mapping of the service endpoints, it is not recommended that you use this API unless:   You are using VPC endpoints (Amazon Web Services PrivateLink) with Timestream     Your application uses a programming language that does not yet have SDK support   You require better control over the client-side implementation   For detailed information on how and when to use and implement DescribeEndpoints, see The Endpoint Discovery Pattern. |
| POST | / | Provides detailed information about a scheduled query. |
| POST | / | You can use this API to run a scheduled query manually. |
| POST | / | Gets a list of all scheduled queries in the caller's Amazon account and Region. ListScheduledQueries is eventually consistent. |
| POST | / | List all tags on a Timestream query resource. |
| POST | / | A synchronous operation that allows you to submit a query with parameters to be stored by Timestream for later running. Timestream only supports using this operation with ValidateOnly set to true. |
| POST | / | Query is a synchronous operation that enables you to run a query against your Amazon Timestream data. Query will time out after 60 seconds. You must update the default timeout in the SDK to support a timeout of 60 seconds. See the code sample for details.  Your query request will fail in the following cases:    If you submit a Query request with the same client token outside of the 5-minute idempotency window.     If you submit a Query request with the same client token, but change other parameters, within the 5-minute idempotency window.     If the size of the row (including the query metadata) exceeds 1 MB, then the query will fail with the following error message:   Query aborted as max page response size has been exceeded by the output result row     If the IAM principal of the query initiator and the result reader are not the same and/or the query initiator and the result reader do not have the same query string in the query requests, the query will fail with an Invalid pagination token error. |
| POST | / | Associate a set of tags with a Timestream resource. You can then activate these user-defined tags so that they appear on the Billing and Cost Management console for cost allocation tracking. |
| POST | / | Removes the association of tags from a Timestream query resource. |
| POST | / | Transitions your account to use TCUs for query pricing and modifies the maximum query compute units that you've configured. If you reduce the value of MaxQueryTCU to a desired configuration, the new value can take up to 24 hours to be effective.  After you've transitioned your account to use TCUs for query pricing, you can't transition to using bytes scanned for query pricing. |
| POST | / | Update a scheduled query. |

## Enhanced Skill Content
## Question Mapping

- "How do I run a Timestream query?" -> POST / (Query: QueryString required, returns Rows + ColumnInfo)
- "How do I cancel a running query?" -> POST / (CancelQuery: QueryId required)
- "How do I create a scheduled query?" -> POST / (CreateScheduledQuery: Name, QueryString, ScheduleConfiguration, NotificationConfiguration, ScheduledQueryExecutionRoleArn, ErrorReportConfiguration required)
- "How do I delete a scheduled query?" -> POST / (DeleteScheduledQuery: ScheduledQueryArn required)
- "How do I get details about a scheduled query?" -> POST / (DescribeScheduledQuery: ScheduledQueryArn required)
- "How do I list all my scheduled queries?" -> POST / (ListScheduledQueries: paginated with MaxResults/NextToken)
- "How do I manually trigger a scheduled query?" -> POST / (ExecuteScheduledQuery: ScheduledQueryArn + InvocationTime required)
- "How do I validate a query without running it?" -> POST / (PrepareQuery: QueryString + ValidateOnly=true)
- "How do I check my account's TCU limits and pricing model?" -> POST / (DescribeAccountSettings: no params required)
- "How do I change the max query TCU or pricing model?" -> POST / (UpdateAccountSettings: MaxQueryTCU and/or QueryPricingModel)
- "How do I pause or resume a scheduled query?" -> POST / (UpdateScheduledQuery: ScheduledQueryArn + State)
- "How do I tag a Timestream resource?" -> POST / (TagResource: ResourceARN + Tags)
- "How do I remove tags from a resource?" -> POST / (UntagResource: ResourceARN + TagKeys)
- "How do I list tags on a resource?" -> POST / (ListTagsForResource: ResourceARN, paginated)
- "How do I discover the correct Timestream endpoint?" -> POST / (DescribeEndpoints: no params, returns Endpoints list)

## Response Tips

- **Query results**: Rows are returned with a separate ColumnInfo array describing types; use QueryStatus.ProgressPercentage to track long-running queries. Paginate with NextToken/MaxRows.
- **Scheduled queries**: DescribeScheduledQuery returns deeply nested objects -- check LastRunSummary.RunStatus and RecentlyFailedRuns for health. ListScheduledQueries returns lean summaries; use Describe for full details.
- **Pagination**: ListScheduledQueries, ListTagsForResource, and Query all use NextToken. A missing or null NextToken means you have reached the last page.
- **Account settings**: Both Describe and Update return the same shape (MaxQueryTCU, QueryPricingModel); all fields are optional/nullable, so check for nulls.
- **Endpoints**: DescribeEndpoints returns a list; cache the endpoint and use it for subsequent calls (Timestream requires endpoint discovery).
- **Mutations (Tag/Untag/Delete/Cancel)**: Return empty 200 responses or minimal confirmation; absence of error means success.

## Anomaly Flags

- **Query cost creep**: Surface QueryStatus.CumulativeBytesMetered and CumulativeBytesScanned after each Query call -- alert if values spike unexpectedly compared to prior runs.
- **Scheduled query failures**: When DescribeScheduledQuery shows RecentlyFailedRuns is non-empty or LastRunSummary.RunStatus is not "AUTO_TRIGGER_SUCCESS", surface the FailureReason and ErrorReportLocation immediately.
- **TCU limit proximity**: After DescribeAccountSettings, flag if MaxQueryTCU is set low relative to workload or if QueryPricingModel is unexpected.
- **Stale endpoint**: DescribeEndpoints results should be cached but refreshed periodically; flag if the endpoint call fails or returns an unexpected region.
- **Pagination loops**: If a Query or List call returns the same NextToken repeatedly, flag a potential infinite pagination loop.
- **Missing error report config**: When creating a scheduled query, warn if S3Configuration.ObjectKeyPrefix is empty (reports will land at bucket root) or if EncryptionOption is unset.
- **Idle scheduled queries**: Flag scheduled queries where State is "DISABLED" or where NextInvocationTime is far in the past.

## Playbook

### 1. Run an Ad-Hoc Query and Collect All Results

1. Call POST / (DescribeEndpoints) to get the correct regional endpoint.
2. Call POST / (Query) with your QueryString and optional MaxRows.
3. Read Rows and ColumnInfo from the response; check QueryStatus.ProgressPercentage.
4. If NextToken is present, call Query again with the same QueryString and the returned NextToken.
5. Repeat step 4 until NextToken is null.
6. If the query takes too long, note the QueryId and call POST / (CancelQuery) with that QueryId.

### 2. Set Up a New Scheduled Query with Monitoring

1. Call POST / (PrepareQuery) with ValidateOnly=true to confirm your QueryString is valid and review the returned Columns and Parameters.
2. Call POST / (CreateScheduledQuery) with Name, QueryString, ScheduleConfiguration (cron expression), NotificationConfiguration (SNS topic ARN), execution role ARN, ErrorReportConfiguration (S3 bucket), and TargetConfiguration (Timestream table for results).
3. Note the returned Arn.
4. Call POST / (DescribeScheduledQuery) with the Arn to confirm State is "ENABLED" and review the full configuration.
5. Call POST / (TagResource) to add cost-allocation or environment tags.

### 3. Diagnose a Failing Scheduled Query

1. Call POST / (ListScheduledQueries) to find the target query's Arn.
2. Call POST / (DescribeScheduledQuery) with the Arn.
3. Inspect LastRunSummary.RunStatus and FailureReason.
4. Check RecentlyFailedRuns for patterns (recurring failures, specific invocation times).
5. Review ExecutionStats (DataWrites, BytesMetered, RecordsIngested) to see if partial progress occurred.
6. If an error report exists, retrieve it from the S3 location in ErrorReportLocation.S3ReportLocation.
7. Fix the underlying issue, then call POST / (ExecuteScheduledQuery) with the Arn and an InvocationTime to manually re-trigger.

### 4. Manage Account TCU Settings and Cost Control

1. Call POST / (DescribeAccountSettings) to review current MaxQueryTCU and QueryPricingModel.
2. To change pricing model or adjust TCU cap, call POST / (UpdateAccountSettings) with new values.
3. Verify the change by calling DescribeAccountSettings again and confirming the returned values match.
4. Monitor ongoing query costs by checking QueryStatus.CumulativeBytesMetered in Query responses.

### 5. Tag and Audit Resources

1. Call POST / (ListScheduledQueries) to enumerate all scheduled query ARNs.
2. For each ARN, call POST / (ListTagsForResource) to review existing tags; paginate with NextToken if needed.
3. Call POST / (TagResource) to add missing tags (e.g., environment, team, cost-center).
4. To clean up stale tags, call POST / (UntagResource) with the TagKeys to remove.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
