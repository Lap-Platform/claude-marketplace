---
name: analytics-api
description: "Analytics API skill. Use when working with Analytics for rate_limit, user_rate_limit. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Analytics API
API version: v1_beta.0.1

## Auth
OAuth2

## Base URL
https://api.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /rate_limit/ -- verify access

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### rate_limit
| Method | Path | Description |
|--------|------|-------------|
| GET | /rate_limit/ | This method retrieves the call limit and utilization data for an application. The data is retrieved for all RESTful APIs and the legacy Trading API.  <br><br>The response from <b>getRateLimits</b> includes a list of the applicable resources and the "call limit", or quota, that is set for each resource. In addition to quota information, the response also includes the number of remaining calls available before the limit is reached, the time remaining before the quota resets, the number of calls made to the specific resource, and the length of the "time window" to which the quota applies.  <br><br>By default, this method returns utilization data for all RESTful API and the legacy Trading API resources. Use the <b>api_name</b> and <b>api_context</b> query parameters to filter the response to only the desired APIs.  <br><br>For more on call limits, see <a href="https://developer.ebay.com/support/app-check " target="_blank">Application Growth Check</a>. |

### user_rate_limit
| Method | Path | Description |
|--------|------|-------------|
| GET | /user_rate_limit/ | This method retrieves the call limit and utilization data for an application user. The call-limit data is returned for all RESTful APIs and the legacy Trading API that limit calls on a per-user basis.  <br><br>The response from <b>getUserRateLimits</b> includes a list of the applicable resources and the "call limit", or quota, that is set for each resource. In addition to quota information, the response also includes the number of remaining calls available before the limit is reached, the time remaining before the quota resets, the number of calls made to the specific resource, and the length of the "time window" to which the quota applies.  <br><br>By default, this method returns utilization data for all RESTful APIs resources and the legacy Trading API calls that limit request access by user. Use the <b>api_name</b> and <b>api_context</b> query parameters to filter the response to only the desired APIs.  <br><br>For more on call limits, see <a href="https://developer.ebay.com/support/app-check " target="_blank">Application Growth Check</a>. |

## Enhanced Skill Content
## Question Mapping

- "What are my current API rate limits?" -> GET /rate_limit/
- "How many calls can I make to the Browse API?" -> GET /rate_limit/ (with api_name filter)
- "What are the rate limits for a specific API context?" -> GET /rate_limit/ (with api_context filter)
- "What is my personal usage against rate limits?" -> GET /user_rate_limit/
- "Am I close to hitting my rate limit on any API?" -> GET /user_rate_limit/
- "What are the user-level limits for the Inventory API?" -> GET /user_rate_limit/ (with api_name filter)
- "Are there any rate limits defined for this API context?" -> GET /rate_limit/ (check for 204 No Content)
- "How do app-level limits differ from my user-level limits?" -> GET /rate_limit/ then GET /user_rate_limit/ (compare both)
- "Which APIs have the tightest rate limits?" -> GET /rate_limit/ (parse and sort rateLimits array)
- "Has my user rate limit been reduced or throttled?" -> GET /user_rate_limit/ (compare against GET /rate_limit/)
- "Do any APIs have no rate limit configured?" -> GET /rate_limit/ (look for 204 responses across api_name values)
- "What rate limits apply in the production context?" -> GET /rate_limit/ (with api_context=production)

## Response Tips

- **rate_limit**: Returns `rateLimits` as an array of maps -- each entry represents a limit tier for the queried API. A 204 means no limits are configured for the given filters; do not treat this as an error.
- **user_rate_limit**: Same structure as rate_limit but scoped to the authenticated user's consumption. Compare values against rate_limit responses to calculate remaining headroom.
- **Errors**: A 500 indicates a server-side issue on eBay's end -- retry with exponential backoff. No 4xx errors are documented, so auth failures surface through the OAuth2 layer, not these endpoints.

## Anomaly Flags

- **Approaching limits**: When user_rate_limit values are within 10-20% of the corresponding rate_limit ceiling, proactively warn the user.
- **204 No Content**: If rate_limit returns 204 for an API the user is actively calling, flag that no limits are defined -- this may indicate a misconfigured api_name or api_context parameter.
- **Discrepancy between app and user limits**: If user_rate_limit returns tighter limits than rate_limit, surface this as the user may be individually throttled.
- **Repeated 500 errors**: If either endpoint returns 500 on consecutive calls, flag potential eBay platform instability and suggest checking eBay's status page.
- **Empty rateLimits array on 200**: A 200 with an empty array (vs 204) is ambiguous -- surface this for the user to investigate.

## Playbook

### Check Overall Rate Limit Health

1. Call `GET /rate_limit/` with no filters to retrieve all app-level limits
2. Call `GET /user_rate_limit/` with no filters to retrieve user-level consumption
3. Compare each entry in user_rate_limit against the matching rate_limit entry
4. Flag any API where usage exceeds 80% of the allowed limit

### Investigate Limits for a Specific API

1. Call `GET /rate_limit/?api_name={name}` to get app-level limits for the target API
2. If 204, inform the user no limits are configured for that API name
3. Call `GET /user_rate_limit/?api_name={name}` to see user-specific consumption
4. Present both side by side with remaining capacity calculated

### Monitor Rate Limits Across Contexts

1. Call `GET /rate_limit/?api_context=production` for production limits
2. Call `GET /rate_limit/?api_context=sandbox` for sandbox limits
3. Compare the two to identify environment-specific differences
4. Repeat with `GET /user_rate_limit/` for both contexts to see actual usage per environment


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
