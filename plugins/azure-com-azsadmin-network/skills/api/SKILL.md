---
name: networkadminmanagementclient
description: "NetworkAdminManagementClient API skill. Use when working with NetworkAdminManagementClient for subscriptions, providers. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# NetworkAdminManagementClient
API version: 2015-06-15

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Network.Admin/operations -- verify access

## Endpoints

5 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminOverview | Get an overview of the state of the network resource provider. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Network.Admin/operations | Returns the list of support REST operations. |
| GET | /providers/Microsoft.Network.Admin/locations | Returns the list of supported locations |
| GET | /providers/Microsoft.Network.Admin/locations/{location}/operationResults | Returns the list of operation results for a location |
| GET | /providers/Microsoft.Network.Admin/locations/{location}/operations | Returns the list of support REST operations. |

## Enhanced Skill Content
## Question Mapping

- "What is the overall network admin status for my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminOverview
- "Show me available Network Admin operations" -> GET /providers/Microsoft.Network.Admin/operations
- "What operations can I perform on the network admin provider?" -> GET /providers/Microsoft.Network.Admin/operations
- "Which locations support Network Admin?" -> GET /providers/Microsoft.Network.Admin/locations
- "List all available regions for network administration" -> GET /providers/Microsoft.Network.Admin/locations
- "What is the result of a recent network operation in eastus?" -> GET /providers/Microsoft.Network.Admin/locations/{location}/operationResults
- "Did my provisioning operation in westeurope succeed?" -> GET /providers/Microsoft.Network.Admin/locations/{location}/operationResults
- "Show running operations in a specific location" -> GET /providers/Microsoft.Network.Admin/locations/{location}/operations
- "Are there any pending network operations in centralus?" -> GET /providers/Microsoft.Network.Admin/locations/{location}/operations
- "Give me a health summary of my network admin environment" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminOverview
- "Check if a long-running deployment finished in northeurope" -> GET /providers/Microsoft.Network.Admin/locations/{location}/operationResults
- "What API actions does the Network Admin resource provider expose?" -> GET /providers/Microsoft.Network.Admin/operations

## Response Tips

- **adminOverview**: Returns a single summary object scoped to the subscription -- look for provisioning state, usage counters, and health indicators at the top level.
- **operations**: Returns a flat list of available ARM operations; each entry includes `name`, `display`, and `isDataAction` -- use `name` for RBAC permission checks.
- **locations**: Returns an array of location objects; filter by `name` to find your target region before calling location-scoped endpoints.
- **operationResults**: May return 200 (completed), 202 (still running), or 404 (expired/unknown) -- always check HTTP status before parsing the body.
- **location operations**: Returns active async operations; entries include a `status` field (Succeeded, Failed, InProgress) -- poll until status is terminal.

## Anomaly Flags

- **202 on operationResults**: Operation is still in progress -- surface this to the user with a polling recommendation and the Retry-After header value if present.
- **Missing or empty adminOverview fields**: May indicate the Network Admin resource provider is not registered on the subscription -- prompt the user to run `az provider register`.
- **Empty locations list**: The Network Admin provider may not be available in the current cloud environment (sovereign clouds) -- flag and suggest verifying provider registration.
- **api-version mismatch**: If the API returns `NoRegisteredProviderFound` or `InvalidApiVersionParameter`, surface that the 2015-06-15 version may be deprecated in the target environment.
- **Throttling (429)**: Azure ARM enforces per-subscription rate limits -- surface the `Retry-After` header and recommend backing off before retrying.
- **Authorization failures (403)**: Likely missing RBAC role -- suggest the user verify they have the Network Admin reader/contributor role on the target scope.

## Playbook

### 1. Check Network Admin Health for a Subscription

1. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminOverview` with your subscription ID.
2. Inspect the response for provisioning state, public IP usage, load balancer counts, and virtual network gateway status.
3. If any counters are near quota limits, flag them for capacity planning.
4. If the call returns 404, register the provider: `az provider register --namespace Microsoft.Network.Admin`.

### 2. Monitor a Long-Running Operation to Completion

1. Call `GET /providers/Microsoft.Network.Admin/locations/{location}/operations` to list active operations in your region.
2. Identify the target operation by name or correlation ID.
3. Call `GET /providers/Microsoft.Network.Admin/locations/{location}/operationResults` with the operation ID.
4. If the response is 202, wait for the duration in the `Retry-After` header, then repeat step 3.
5. When the response is 200, parse the result body for final status (Succeeded or Failed).

### 3. Discover Available Operations for RBAC Planning

1. Call `GET /providers/Microsoft.Network.Admin/operations` with `api-version=2015-06-15`.
2. Collect all entries and group by the resource type prefix in the `name` field.
3. Separate data-plane actions (`isDataAction: true`) from control-plane actions.
4. Use the operation names to build a custom RBAC role definition scoped to your needs.

### 4. Enumerate Supported Locations Before Deployment

1. Call `GET /providers/Microsoft.Network.Admin/locations` to retrieve all supported regions.
2. Filter the list to regions that match your compliance or latency requirements.
3. For each candidate region, call `GET /providers/Microsoft.Network.Admin/locations/{location}/operations` to confirm the region is active and not experiencing issues.
4. Select the target location and proceed with resource provisioning.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
