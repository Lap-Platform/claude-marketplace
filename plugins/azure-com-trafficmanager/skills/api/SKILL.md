---
name: trafficmanagermanagementclient
description: "TrafficManagerManagementClient API skill. Use when working with TrafficManagerManagementClient for subscriptions, providers. Covers 16 endpoints."
version: 1.0.0
generator: lapsh
---

# TrafficManagerManagementClient
API version: 2018-04-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Network/trafficManagerGeographicHierarchies/default -- verify access
3. POST /providers/Microsoft.Network/checkTrafficManagerNameAvailability -- create first checkTrafficManagerNameAvailability

## Endpoints

16 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/{endpointType}/{endpointName} | Update a Traffic Manager endpoint. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/{endpointType}/{endpointName} | Gets a Traffic Manager endpoint. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/{endpointType}/{endpointName} | Create or update a Traffic Manager endpoint. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/{endpointType}/{endpointName} | Deletes a Traffic Manager endpoint. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles | Lists all Traffic Manager profiles within a resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficmanagerprofiles | Lists all Traffic Manager profiles within a subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName} | Gets a Traffic Manager profile. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName} | Create or update a Traffic Manager profile. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName} | Deletes a Traffic Manager profile. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName} | Update a Traffic Manager profile. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/heatMaps/{heatMapType} | Gets latest heatmap for Traffic Manager profile. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys/default | Get the subscription-level key used for Real User Metrics collection. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys/default | Create or update a subscription-level key used for Real User Metrics collection. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys/default | Delete a subscription-level key used for Real User Metrics collection. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| POST | /providers/Microsoft.Network/checkTrafficManagerNameAvailability | Checks the availability of a Traffic Manager Relative DNS name. |
| GET | /providers/Microsoft.Network/trafficManagerGeographicHierarchies/default | Gets the default Geographic Hierarchy used by the Geographic traffic routing method. |

## Enhanced Skill Content
## Question Mapping

- "Is this Traffic Manager profile name available?" -> POST /providers/Microsoft.Network/checkTrafficManagerNameAvailability
- "List all Traffic Manager profiles in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficmanagerprofiles
- "List Traffic Manager profiles in a specific resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles
- "Get details of a specific Traffic Manager profile" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}
- "Create a new Traffic Manager profile" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}
- "Update an existing Traffic Manager profile" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}
- "Delete a Traffic Manager profile" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}
- "Add an endpoint to a Traffic Manager profile" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/{endpointType}/{endpointName}
- "Get a specific endpoint from a Traffic Manager profile" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/{endpointType}/{endpointName}
- "Remove an endpoint from a Traffic Manager profile" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/{endpointType}/{endpointName}
- "Update endpoint properties like weight or priority" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/{endpointType}/{endpointName}
- "View the heat map for a Traffic Manager profile" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/heatMaps/{heatMapType}
- "Get the geographic hierarchy for geographic routing" -> GET /providers/Microsoft.Network/trafficManagerGeographicHierarchies/default
- "Check if Real User Metrics are enabled" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys/default
- "Enable Real User Metrics collection" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys/default

## Response Tips

- **Profile & endpoint CRUD (200):** Response body contains the full resource object with `properties.endpointStatus`, `properties.monitorConfig`, and `properties.trafficRoutingMethod` -- always check `properties.profileStatus` for enabled/disabled state.
- **Create operations (201):** A 201 indicates the resource was newly created; a 200 on the same PUT means it was updated in place -- branch your logic accordingly.
- **Delete operations (200 vs 204):** 200 means the resource was found and deleted; 204 means it was already gone -- treat both as success, do not retry on 204.
- **List endpoints:** Profiles list returns a flat array in `value`; there is no server-side pagination for Traffic Manager -- expect the full set in one response.
- **Heat maps:** Response includes `properties.endpoints[]` and `properties.trafficFlows[]` with latitude/longitude data; use `topLeft` and `botRight` query params to scope the geographic bounding box.
- **Name availability check:** Returns `nameAvailable` (boolean) and `reason`/`message` when unavailable -- always read `reason` for actionable detail.
- **User Metrics keys:** GET returns the key in `properties.key`; a 200 with no key means the feature is not enabled yet.

## Anomaly Flags

- **Degraded endpoints:** After fetching a profile, surface any endpoints where `endpointStatus` is `Disabled` or `endpointMonitorStatus` is `Degraded`, `Inactive`, or `Stopped` -- these indicate traffic is not routing as expected.
- **Profile disabled:** Flag when `properties.profileStatus` is `Disabled`, since no traffic routing occurs regardless of endpoint health.
- **Monitor config issues:** Alert if `properties.monitorConfig.intervalInSeconds` is set to 10 (fast probing) without `toleratedNumberOfFailures` tuned accordingly -- this can cause flapping.
- **Endpoint weight imbalance:** When using Weighted routing, flag if any single endpoint carries more than 80% of total weight or if all weights are identical (may indicate unintentional config).
- **204 on delete:** Surface when a delete returns 204 instead of 200 -- the resource was already absent, which may indicate a stale reference or race condition in automation.
- **Heat map empty results:** Flag when `trafficFlows` is empty -- Real User Metrics may not be enabled or insufficient data has been collected.
- **API version drift:** The spec pins `api-version=2018-04-01`; flag if Azure documentation references a newer version with features this client cannot access.

## Playbook

### 1. Create a Traffic Manager Profile with Endpoints

1. Call POST `/providers/Microsoft.Network/checkTrafficManagerNameAvailability` with `{"name": "my-profile", "type": "Microsoft.Network/trafficmanagerprofiles"}` to verify the DNS name is free.
2. Call PUT `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}` with the profile definition including `trafficRoutingMethod`, `dnsConfig`, and `monitorConfig`.
3. For each backend, call PUT `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/externalEndpoints/{endpointName}` (or `azureEndpoints`/`nestedEndpoints` as appropriate) with `target`, `weight`, and `endpointStatus: Enabled`.
4. Call GET on the profile to confirm all endpoints show `endpointMonitorStatus: Online`.

### 2. Failover Testing by Disabling an Endpoint

1. GET the endpoint you want to take offline to capture its current configuration.
2. PATCH the endpoint with `{"properties": {"endpointStatus": "Disabled"}}`.
3. GET the parent profile and verify traffic is redistributed to remaining healthy endpoints.
4. Re-enable by PATCHing the endpoint back to `{"properties": {"endpointStatus": "Enabled"}}`.
5. GET the endpoint again to confirm `endpointMonitorStatus` returns to `Online`.

### 3. Set Up Geographic Routing

1. GET `/providers/Microsoft.Network/trafficManagerGeographicHierarchies/default` to retrieve the full region tree with codes.
2. Create or update the profile via PUT with `trafficRoutingMethod: Geographic`.
3. For each endpoint, PUT with `properties.geoMapping` set to an array of region codes from the hierarchy (e.g., `["US", "CA"]`).
4. Verify by GETting each endpoint and confirming the `geoMapping` array matches expectations.

### 4. Enable and Review Real User Metrics

1. PUT `/subscriptions/{sub}/providers/Microsoft.Network/trafficManagerUserMetricsKeys/default` to generate a RUM key (returns 201).
2. GET the same path to retrieve the key value from `properties.key`.
3. Embed the key in your client-side JavaScript snippet per Azure documentation.
4. After data collection begins, GET `/subscriptions/{sub}/resourceGroups/{rg}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/heatMaps/default` to view latency and traffic origin data.
5. To stop collection and delete data, DELETE the user metrics key endpoint.

### 5. Tear Down a Traffic Manager Profile

1. GET the profile to list all endpoints under it.
2. For each endpoint, call DELETE to remove it (confirms clean removal with 200; 204 means already gone).
3. DELETE the profile itself.
4. Verify by GETting the profile -- expect a 404 confirming full removal.
5. If Real User Metrics were enabled, DELETE the user metrics key to stop data collection.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
