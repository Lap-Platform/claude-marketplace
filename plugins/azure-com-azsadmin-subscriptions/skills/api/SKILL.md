---
name: subscriptionclient
description: "SubscriptionClient API skill. Use when working with SubscriptionClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionClient
API version: 2015-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions | Get the list of subscriptions. |
| GET | /subscriptions/{subscriptionId} | Gets details about particular subscription. |
| PUT | /subscriptions/{subscriptionId} | Create or updates a subscription. |
| DELETE | /subscriptions/{subscriptionId} | Delete the specified subscription. |

## Enhanced Skill Content
## Question Mapping

- "What subscriptions do I have?" -> GET /subscriptions
- "List all my Azure subscriptions" -> GET /subscriptions
- "Show me subscription details for a specific ID" -> GET /subscriptions/{subscriptionId}
- "Get info about subscription abc-123" -> GET /subscriptions/{subscriptionId}
- "Is my subscription still active?" -> GET /subscriptions/{subscriptionId}
- "Create a new subscription" -> PUT /subscriptions/{subscriptionId}
- "Update an existing subscription's configuration" -> PUT /subscriptions/{subscriptionId}
- "Register a subscription with a specific ID" -> PUT /subscriptions/{subscriptionId}
- "Cancel a subscription" -> DELETE /subscriptions/{subscriptionId}
- "Remove subscription abc-123" -> DELETE /subscriptions/{subscriptionId}
- "How many subscriptions are in my tenant?" -> GET /subscriptions (count the results)
- "Does subscription xyz exist?" -> GET /subscriptions/{subscriptionId} (check for 404)
- "Replace a subscription definition entirely" -> PUT /subscriptions/{subscriptionId}
- "Clean up unused subscriptions" -> GET /subscriptions then DELETE /subscriptions/{subscriptionId} for each target

## Response Tips

- **GET /subscriptions**: Returns a list; expect a `value` array with pagination via `nextLink`. Always follow `nextLink` until exhausted to get all results.
- **GET /subscriptions/{subscriptionId}**: Returns a single subscription object. Key fields: `subscriptionId`, `displayName`, `state` (Enabled/Disabled/Warned/Deleted/PastDue).
- **PUT /subscriptions/{subscriptionId}**: 201 means created, 200 means updated in place. The response body contains the final subscription state -- always read it back rather than assuming your input was applied unchanged.
- **DELETE /subscriptions/{subscriptionId}**: 200 means deleted, 204 means it was already gone (idempotent). Treat both as success.
- **All endpoints**: Errors follow Azure's standard `error.code` / `error.message` structure. Always include `api-version=2015-11-01` as a query parameter.

## Anomaly Flags

- **Subscription state drift**: If GET returns `state: Warned`, `PastDue`, or `Disabled`, surface this immediately -- the subscription may lose access to resources.
- **Throttling (429)**: Azure management APIs enforce rate limits per tenant. If you receive 429, surface the `Retry-After` header value and pause before retrying.
- **Stale API version**: This spec uses `2015-11-01`. If Azure returns warnings about deprecated API versions or suggests a newer version in response headers, flag it.
- **Unexpected 404 on known subscription**: If a subscription that previously existed returns 404, it may have been deleted externally or moved to a different tenant -- flag for investigation.
- **201 on an update**: If PUT returns 201 when you expected to update an existing subscription, it was actually created fresh -- the original may have been deleted. Surface this discrepancy.
- **Long-running operation**: If any response includes a `Location` or `Azure-AsyncOperation` header, the operation is async. Surface the polling URL so the user can track completion.

## Playbook

### 1. Audit All Subscriptions in a Tenant

1. Call `GET /subscriptions?api-version=2015-11-01`
2. Iterate through the `value` array in the response
3. If `nextLink` is present, follow it and repeat until no more pages
4. For each subscription, note the `subscriptionId`, `displayName`, and `state`
5. Flag any subscriptions with `state` other than `Enabled`

### 2. Create or Update a Subscription

1. Define the subscription body with required fields in `subscriptionDefinition`
2. Call `PUT /subscriptions/{subscriptionId}?api-version=2015-11-01` with the body
3. Check the status code: 201 = new, 200 = updated
4. Read the response body to confirm the final applied state
5. Call `GET /subscriptions/{subscriptionId}` to verify the subscription is live

### 3. Safely Delete a Subscription

1. Call `GET /subscriptions/{subscriptionId}?api-version=2015-11-01` to confirm it exists and review its current state
2. Verify you have the correct subscription (check `displayName`)
3. Call `DELETE /subscriptions/{subscriptionId}?api-version=2015-11-01`
4. Accept both 200 and 204 as success
5. Optionally call `GET /subscriptions/{subscriptionId}` to confirm it returns 404

### 4. Check if a Specific Subscription Exists

1. Call `GET /subscriptions/{subscriptionId}?api-version=2015-11-01`
2. If 200: subscription exists -- inspect the `state` field
3. If 404: subscription does not exist or is not accessible in this tenant
4. If 403: subscription may exist but you lack permissions -- surface this to the user

### 5. Bulk Cleanup of Disabled Subscriptions

1. Call `GET /subscriptions?api-version=2015-11-01` and paginate through all results
2. Filter for subscriptions where `state` is `Disabled` or `Deleted`
3. Present the filtered list to the user for confirmation before proceeding
4. For each confirmed subscription, call `DELETE /subscriptions/{subscriptionId}?api-version=2015-11-01`
5. Log the result of each deletion (200 = removed, 204 = already gone, other = investigate)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
