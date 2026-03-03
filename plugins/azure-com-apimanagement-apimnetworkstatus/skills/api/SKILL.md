---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 2 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/networkstatus -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/networkstatus | Gets the Connectivity Status to the external resources on which the Api Management service depends from inside the Cloud Service. This also returns the DNS Servers as visible to the CloudService. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/locations/{locationName}/networkstatus | Gets the Connectivity Status to the external resources on which the Api Management service depends from inside the Cloud Service. This also returns the DNS Servers as visible to the CloudService. |

## Enhanced Skill Content
## Question Mapping

- "What is the network status of my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/networkstatus
- "Is my APIM instance healthy across all locations?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/networkstatus
- "What is the network connectivity status in a specific region?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/locations/{locationName}/networkstatus
- "Can my API Management service reach its dependencies?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/networkstatus
- "Why is my APIM instance having connectivity issues in East US?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/locations/{locationName}/networkstatus
- "Show me network dependency status for all regions of my APIM service." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/networkstatus
- "Is the SQL dependency reachable from my APIM in westeurope?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/locations/{locationName}/networkstatus
- "Are there any failed connectivity checks for my API Management instance?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/networkstatus
- "Check network status for APIM in a multi-region deployment." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/networkstatus
- "What external dependencies does my APIM service connect to?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/locations/{locationName}/networkstatus
- "Troubleshoot APIM network isolation issues in a specific location." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/locations/{locationName}/networkstatus
- "Compare network health across all APIM deployment locations." -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/networkstatus

## Response Tips

- **Network status (all locations):** Returns an array of per-location status objects, each containing `connectivityStatus` entries for dependencies (SQL, Storage, AAD, etc.) -- iterate the array to cover multi-region deployments.
- **Network status (single location):** Returns a flat object with `connectivityStatus` array -- each entry has `name`, `status` (success/failure), `lastUpdated`, and `error` fields; check `status` != "success" to find problems.
- **Errors:** 4xx responses typically indicate invalid subscription/resource names or missing permissions; 401 means the OAuth2 token is expired or lacks the `Microsoft.ApiManagement/service/read` permission.

## Anomaly Flags

- **Connectivity failure detected:** Surface immediately when any `connectivityStatus` entry has `status` other than "success" -- this indicates the APIM instance cannot reach a critical dependency.
- **Stale status data:** Flag when `lastUpdated` timestamps are older than 1 hour, as this may indicate the monitoring probe itself is unhealthy.
- **Partial region outage:** When the all-locations endpoint returns mixed results (some locations healthy, others not), highlight the affected regions explicitly.
- **Authentication dependency failure:** Specifically call out when AAD/identity-related connectivity checks fail, as this can cascade to all API authentication.
- **DNS resolution failures:** Flag DNS-related connectivity issues separately, as they often indicate VNET misconfiguration in internal-mode deployments.

## Playbook

### 1. Diagnose APIM connectivity issues

1. Call GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/networkstatus` to get status across all locations.
2. Scan each location's `connectivityStatus` array for entries where `status` != "success".
3. For any failing location, call GET `.../locations/{locationName}/networkstatus` to get detailed per-dependency status.
4. Check the `error` field on failed entries to identify root cause (DNS, firewall, NSG rules).
5. Cross-reference `lastUpdated` to determine if the failure is ongoing or resolved.

### 2. Validate multi-region APIM health

1. Call the all-locations network status endpoint.
2. Extract the list of locations from the response array.
3. Verify each location has all expected dependencies reporting "success".
4. Compare dependency lists across locations to ensure consistency (e.g., all regions can reach SQL and Storage).
5. Report any location that is degraded relative to others.

### 3. Pre-deployment network readiness check

1. Before deploying API changes, call the all-locations network status endpoint.
2. Confirm all `connectivityStatus` entries show "success" across every region.
3. If any dependency is failing, abort the deployment and investigate using the per-location endpoint.
4. Verify `lastUpdated` timestamps are recent (within the last 15 minutes) to ensure data is fresh.

### 4. Monitor APIM after VNET configuration change

1. Apply the VNET or NSG change to the APIM subnet.
2. Wait 2-5 minutes for connectivity probes to refresh.
3. Call the location-specific network status endpoint for the affected region.
4. Verify all dependencies still report "success" -- pay special attention to SQL, Storage, and Azure AD.
5. If failures appear, check NSG rules and service endpoint configurations for the APIM subnet.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
