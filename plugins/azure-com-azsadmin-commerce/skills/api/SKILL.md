---
name: commercemanagementclient
description: "CommerceManagementClient API skill. Use when working with CommerceManagementClient for providers, subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# CommerceManagementClient
API version: 2015-06-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Commerce.Admin/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/updateEncryption -- create first updateEncryption

## Endpoints

3 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Commerce.Admin/operations | Returns the list of supported REST operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/subscriberUsageAggregates | Gets a collection of SubscriberUsageAggregates, which are UsageAggregates from users. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/updateEncryption | Update the encryption. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available in the Commerce Admin API?" -> GET /providers/Microsoft.Commerce.Admin/operations
- "How do I list all supported operations?" -> GET /providers/Microsoft.Commerce.Admin/operations
- "What can I do with the Commerce Management API?" -> GET /providers/Microsoft.Commerce.Admin/operations
- "How do I get subscriber usage data for a subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/subscriberUsageAggregates
- "Show me aggregated usage between two dates" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/subscriberUsageAggregates
- "How do I get daily usage breakdown for a subscriber?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/subscriberUsageAggregates (set aggregationGranularity=daily)
- "How do I get hourly usage for a specific subscriber?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/subscriberUsageAggregates (set aggregationGranularity=hourly, subscriberId)
- "How do I page through large usage result sets?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/subscriberUsageAggregates (use continuationToken)
- "How do I filter usage by a specific subscriber ID?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/subscriberUsageAggregates (set subscriberId)
- "How do I update or rotate the encryption key for my subscription?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/updateEncryption
- "How do I re-encrypt commerce data?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/updateEncryption
- "What API version should I use?" -> All endpoints require api-version=2015-06-01-preview
- "How do I authenticate to the Commerce Admin API?" -> OAuth2 bearer token in Authorization header

## Response Tips

- **Operations (providers):** Returns a list of available API operations with display metadata; iterate the value array to discover supported actions and resource types.
- **Usage aggregates (subscriptions):** Returns paginated usage records; check for a continuationToken in the response to fetch the next page -- a missing or null token means you have all results.
- **Update encryption (subscriptions):** Returns 200 on success with no meaningful body; any non-200 status indicates a failure -- check the error object for code and message fields.
- **All endpoints:** Errors follow Azure standard format with a top-level error object containing code and message; always pass api-version as a query parameter.

## Anomaly Flags

- **Pagination not exhausted:** If a continuationToken is present in a usage aggregates response and the caller stops fetching, warn that results are incomplete.
- **Empty usage window:** If reportedStartTime and reportedEndTime span a period but zero records return, flag that the time range may be incorrect or the subscription had no activity.
- **API version mismatch:** If a 400 error mentions api-version, surface that the caller may be using an unsupported version (expected: 2015-06-01-preview).
- **OAuth token expiry:** If a 401 is returned, proactively suggest refreshing the OAuth2 token before retrying.
- **Encryption update on inactive subscription:** If updateEncryption returns an error referencing subscription state, flag that the subscription may be disabled or deleted.
- **Throttling (429):** If any endpoint returns 429 or includes Retry-After headers, surface the wait duration and suggest backing off.

## Playbook

### 1. Discover Available Operations

1. Call `GET /providers/Microsoft.Commerce.Admin/operations?api-version=2015-06-01-preview`.
2. Parse the value array from the response.
3. Review each operation's name and display fields to understand what actions the API supports.

### 2. Pull Full Usage Report for a Date Range

1. Determine the subscription ID, start time, and end time (ISO 8601 format).
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/subscriberUsageAggregates?api-version=2015-06-01-preview&reportedStartTime={start}&reportedEndTime={end}`.
3. Collect records from the response.
4. If a continuationToken is present, repeat the call with `continuationToken={token}` appended until no token is returned.
5. Merge all pages into the final result set.

### 3. Get Hourly Usage for a Specific Subscriber

1. Identify the target subscriberId and the desired time window.
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/subscriberUsageAggregates?api-version=2015-06-01-preview&reportedStartTime={start}&reportedEndTime={end}&aggregationGranularity=hourly&subscriberId={id}`.
3. Page through results using continuationToken if present.
4. Aggregate or display the hourly breakdown as needed.

### 4. Rotate Commerce Encryption Key

1. Confirm the subscription ID and ensure you hold a valid OAuth2 token with write permissions.
2. Call `POST /subscriptions/{subscriptionId}/providers/Microsoft.Commerce.Admin/updateEncryption?api-version=2015-06-01-preview`.
3. Verify a 200 response to confirm success.
4. If an error is returned, check the error code and message -- common issues are insufficient permissions or an inactive subscription.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
