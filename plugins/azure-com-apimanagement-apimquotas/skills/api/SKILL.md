---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# ApiManagementClient
API version: 2019-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey} -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey} | Lists a collection of current quota counter periods associated with the counter-key configured in the policy on the specified service instance. The api does not support paging yet. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey} | Updates all the quota counter values specified with the existing quota counter key to a value in the specified service instance. This should be used for reset of the quota counter values. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey}/periods/{quotaPeriodKey} | Gets the value of the quota counter associated with the counter-key in the policy for the specific period in service instance. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey}/periods/{quotaPeriodKey} | Updates an existing quota counter value in the specified service instance. |

## Enhanced Skill Content


## Question Mapping

- "What are the current quota counter values for a specific key?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey}
- "How do I check quota usage for my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey}
- "How do I update or reset a quota counter?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey}
- "How do I modify quota limits for all periods at once?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey}
- "What is the quota usage for a specific billing period?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey}/periods/{quotaPeriodKey}
- "How do I view quota consumption for a particular time window?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey}/periods/{quotaPeriodKey}
- "How do I adjust the quota counter for a single period?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey}/periods/{quotaPeriodKey}
- "How do I reset quota usage for a specific period?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey}/periods/{quotaPeriodKey}
- "How do I check if a quota is close to its limit?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey} then inspect counter values vs limits
- "How do I audit quota changes over time?" -> GET period-level endpoint repeatedly across period keys to compare values
- "What quota counter keys are available for my service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/quotas/{quotaCounterKey} (enumerate known keys)
- "How do I bulk-update quotas across multiple periods?" -> PATCH the top-level quota counter endpoint (applies to all periods)

## Response Tips

- **GET quota counters**: Returns a collection with `value` array containing counter objects; each has `counterKey`, `periodKey`, `periodStartTime`, `periodEndTime`, and `value` (with `callsCount` and `kbTransferred` nested inside).
- **GET quota period**: Returns a single period object with the same nested `value` structure; check `periodStartTime`/`periodEndTime` to confirm you are inspecting the correct window.
- **PATCH endpoints**: Return 204 No Content on success with no response body; any non-204 indicates failure. Check for `error.code` and `error.message` in error responses.
- **Error responses**: Follow Azure standard format with `error` object containing `code` (string) and `message`; common codes include `ResourceNotFound`, `ValidationError`, and `Unauthorized`.

## Anomaly Flags

- **Quota near threshold**: Surface a warning when `callsCount` exceeds 80% of the configured quota limit for any counter.
- **204 vs non-204 on PATCH**: If a PATCH returns anything other than 204, flag it immediately as the update likely failed silently.
- **Period boundary drift**: Alert if `periodStartTime` or `periodEndTime` do not align with expected billing cycle boundaries.
- **Stale counter values**: Flag when `callsCount` reads as zero in an active period, which may indicate a misconfigured counter key or recent reset.
- **Auth token expiry**: Since this uses OAuth2, proactively warn when the token is nearing expiration before issuing PATCH calls that could fail mid-operation.
- **API version deprecation**: This spec targets `2019-01-01`; flag if Azure returns headers indicating a newer required API version or deprecation notices.

## Playbook

### 1. Check Current Quota Usage

1. Identify the `subscriptionId`, `resourceGroupName`, `serviceName`, and `quotaCounterKey`.
2. GET the quota counter endpoint to retrieve all period summaries.
3. Inspect each item in the `value` array for `callsCount` and `kbTransferred`.
4. Compare against known limits to determine remaining capacity.

### 2. Reset a Quota Counter for All Periods

1. GET the quota counter to confirm current values and note the counter structure.
2. PATCH the quota counter endpoint with `parameters` setting `callsCount` and `kbTransferred` to desired values (typically 0).
3. Confirm a 204 response.
4. GET the quota counter again to verify the reset took effect.

### 3. Adjust Quota for a Specific Billing Period

1. GET the period-level endpoint using the target `quotaPeriodKey` to see current values.
2. PATCH the period-level endpoint with updated `callsCount` or `kbTransferred` values in `parameters`.
3. Confirm 204 No Content response.
4. GET the period-level endpoint again to verify the changes persisted.

### 4. Monitor Quota Approaching Limits

1. GET the quota counter endpoint on a scheduled interval.
2. For each period in the response, calculate usage percentage: `callsCount / quotaLimit * 100`.
3. If any period exceeds 80%, trigger an alert or notification.
4. Optionally PATCH the counter to increase limits if auto-scaling is desired.
5. Log the usage trend for capacity planning.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
