---
name: updateadminclient
description: "UpdateAdminClient API skill. Use when working with UpdateAdminClient for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# UpdateAdminClient
API version: 2016-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/ -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/ | Get the list of update locations. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation} | Get an update location based on name. |

## Enhanced Skill Content


## Question Mapping

- "What update locations are available in my resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/
- "List all update locations for a specific subscription?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/
- "Get details about a specific update location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}
- "What is the status of update location X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}
- "Which regions have update infrastructure configured?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/
- "Show me the update location properties for a given location name?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}
- "Are there any update locations in resource group Y?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/
- "What update services are running at location Z?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}
- "How do I verify my Azure Stack update infrastructure is registered?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/
- "Get the current state of a specific update location before applying updates?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}
- "List all update admin locations, then drill into one for details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/ then GET .../{updateLocation}

## Response Tips

- **List endpoint (updateLocations/)**: Returns a `value` array of location objects. Check for `nextLink` property for pagination -- if present, follow it for additional results.
- **Detail endpoint (updateLocations/{updateLocation})**: Returns a single resource object with `id`, `name`, `type`, `location`, and `properties`. The `properties` block contains the operational state and configuration details.
- **Errors**: 4xx responses follow Azure error format with `error.code` and `error.message`. A 404 means the update location name is wrong or the resource provider is not registered on the subscription.

## Anomaly Flags

- **Missing update locations**: If the list endpoint returns an empty `value` array, the Update Admin resource provider may not be registered -- surface this to the user and suggest running `az provider register --namespace Microsoft.Update.Admin`.
- **Stale API version**: This spec uses `2016-05-01`. If responses include `x-ms-deprecation` headers or unknown properties, flag that a newer API version may be available.
- **Throttling**: Watch for `429 Too Many Requests` or `Retry-After` headers. Azure ARM has per-subscription rate limits -- surface remaining quota from `x-ms-ratelimit-remaining-subscription-reads` headers.
- **Unexpected location state**: If a location's `properties` indicate a degraded, offline, or error state, proactively alert the user before they attempt update operations against it.
- **Authorization failures**: A `403 Forbidden` likely means the caller lacks the Update Admin reader/contributor role -- suggest checking RBAC assignments.

## Playbook

### 1. Discover Update Infrastructure

1. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/` to list all locations.
2. Review the `value` array for available locations and their names.
3. If the array is empty, verify the resource provider is registered on the subscription.
4. Note each location's `name` for use in detail queries.

### 2. Inspect a Specific Update Location

1. Identify the target location name from the list call or from known infrastructure.
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}`.
3. Examine `properties` for current state, configuration, and any reported issues.
4. Use this information to decide whether to proceed with update operations.

### 3. Pre-Update Health Check

1. List all update locations to confirm infrastructure is visible.
2. For each location, fetch the detail endpoint to check operational state.
3. Flag any location reporting errors or degraded status.
4. Only proceed with update application if all target locations report healthy state.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
