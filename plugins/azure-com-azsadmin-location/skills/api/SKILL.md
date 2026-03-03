---
name: subscriptionsmanagementclient
description: "SubscriptionsManagementClient API skill. Use when working with SubscriptionsManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionsManagementClient
API version: 2015-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations | Get a list of all AzureStack location. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location} | Get the specified location. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location} | Updates the specified location. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/operationsStatus/{operationsStatusName} | Get the operation status. |

## Enhanced Skill Content
## Question Mapping

- "What locations are available for my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations
- "List all subscription admin locations" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations
- "Get details for a specific location" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}
- "What properties does location X have?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}
- "Create a new subscription location" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}
- "Update an existing subscription location" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}
- "Register a location for subscription management" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}
- "Check the status of a location operation" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/operationsStatus/{operationsStatusName}
- "Is my location creation still in progress?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/operationsStatus/{operationsStatusName}
- "Did the location update complete successfully?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/operationsStatus/{operationsStatusName}
- "How do I set up a new location and confirm it worked?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location} then GET .../operationsStatus/{operationsStatusName}
- "Which locations are configured under my admin provider?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations

## Response Tips

- **Location list (GET .../locations):** Returns an array of location objects; check for a `nextLink` or `value` wrapper -- Azure ARM APIs typically nest results under `value`.
- **Single location (GET .../locations/{location}):** Returns the full location resource; look for `properties` for config details and `id`/`name`/`type` for ARM resource identity.
- **Create/Update location (PUT):** Returns the created or updated resource on 200; if the response includes a `Location` or `Azure-AsyncOperation` header, the operation is long-running -- extract the operation status URL from the header.
- **Operation status (GET .../operationsStatus):** 200 means complete, 202 means still in progress (poll again), 204 means completed with no body, 404 means the operation was not found or has expired.

## Anomaly Flags

- **202 on operation status:** The operation is still running. Agent should suggest polling at intervals (typically 10-30s) and warn if polling exceeds 5 minutes.
- **404 on operation status:** The operation ID may have expired or never existed. Surface this clearly -- do not silently retry.
- **Missing `Azure-AsyncOperation` header on PUT:** If the PUT returns 200 with no async header, the operation completed synchronously. If it returns 202, the header is expected -- flag if absent.
- **OAuth2 token expiry:** All endpoints require OAuth2. Agent should proactively flag 401 responses and suggest token refresh before retrying.
- **Throttling (429 or `Retry-After` header):** Azure ARM APIs enforce rate limits. Agent should surface any 429 response or `Retry-After` header and pause before retrying.
- **Deprecated API version:** The spec uses version `2015-11-01`. Agent should flag if Azure documentation indicates a newer `api-version` is available and recommend upgrading.

## Playbook

### 1. Discover All Available Locations

1. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations`
2. Parse the `value` array from the response
3. If `nextLink` is present, follow it to retrieve additional pages
4. Extract `name` and `properties` from each location for display

### 2. Create or Update a Location

1. Prepare the location body as a JSON map with required configuration fields
2. Call `PUT /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}` with the body in `newLocation`
3. If the response is 200, the operation completed -- inspect the returned resource
4. If the response includes an `Azure-AsyncOperation` header, extract the operation status name
5. Proceed to poll the operation status (see Playbook 3)

### 3. Poll an Async Operation to Completion

1. Extract `operationsStatusName` from the async operation header or response
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/operationsStatus/{operationsStatusName}`
3. If 202: wait 15-30 seconds and repeat step 2
4. If 200: operation succeeded -- read the response body for final state
5. If 204: operation completed with no additional data
6. If 404: operation not found -- verify the operation ID and location are correct

### 4. Audit Location Configuration

1. List all locations using `GET .../locations`
2. For each location, call `GET .../locations/{location}` to retrieve full details
3. Compare `properties` against expected configuration baselines
4. Flag any locations with unexpected or missing properties

### 5. Verify a Location Update Took Effect

1. Call `PUT .../locations/{location}` with updated configuration
2. If async, poll operation status until 200 or 204 (see Playbook 3)
3. Call `GET .../locations/{location}` to fetch the current state
4. Compare the returned `properties` against the values submitted in the PUT to confirm the update applied


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
