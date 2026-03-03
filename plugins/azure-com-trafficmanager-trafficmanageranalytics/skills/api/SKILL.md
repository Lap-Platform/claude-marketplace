---
name: trafficmanagermanagementclient
description: "TrafficManagerManagementClient API skill. Use when working with TrafficManagerManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# TrafficManagerManagementClient
API version: 2017-09-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/heatMaps/{heatMapType} | Gets latest heatmap for Traffic Manager profile. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys | Get the subscription-level key used for Real User Metrics collection. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys | Create or update a subscription-level key used for Real User Metrics collection. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys | Delete a subscription-level key used for Real User Metrics collection. |

## Enhanced Skill Content


## Question Mapping

- "How do I get the heat map for a Traffic Manager profile?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/heatMaps/{heatMapType}
- "Can I filter the heat map to a specific geographic region?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/heatMaps/{heatMapType} (use topLeft and botRight params)
- "What does the heat map look like for just Europe?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/heatMaps/{heatMapType} (set topLeft/botRight to EU bounding box)
- "How do I check if Real User Metrics is enabled for my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys
- "How do I enable Real User Metrics collection?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys
- "How do I turn off Real User Metrics and delete the key?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys
- "How do I rotate my Real User Metrics key?" -> DELETE then PUT /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys
- "What traffic patterns is my Traffic Manager profile seeing?" -> GET heatMaps endpoint with heatMapType=default
- "Can I get traffic data for a bounding box around North America?" -> GET heatMaps with topLeft and botRight coordinates
- "How do I set up end-user traffic analytics for Traffic Manager?" -> PUT trafficManagerUserMetricsKeys, then GET heatMaps after data collection
- "Is my Real User Metrics key still active?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys
- "How do I stop collecting user metrics without deleting the profile?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys

## Response Tips

- **Heat Maps**: Response contains geographic traffic data points; empty results mean insufficient Real User Metrics data has been collected yet. Coordinate params (topLeft, botRight) expect comma-separated lat/long pairs.
- **User Metrics Keys (GET)**: Returns the current key object or indicates no key exists; check for error response if Real User Metrics was never enabled.
- **User Metrics Keys (PUT)**: Returns 201 (created, not 200) with the new key; store the key value immediately as it may not be retrievable in full later.
- **User Metrics Keys (DELETE)**: Returns 200 on success; idempotent-safe -- deleting a nonexistent key should not error.

## Anomaly Flags

- **PUT returns non-201 status**: Key creation may have failed silently; surface to user and suggest retrying.
- **Heat map returns empty data**: Likely means Real User Metrics collection is not enabled or has not gathered enough samples yet -- prompt user to check key status via GET trafficManagerUserMetricsKeys.
- **api-version mismatch**: This is a preview API (2017-09-01-preview); flag if user omits or uses a different api-version, as behavior may differ or fail.
- **Bounding box coordinates inverted**: If topLeft longitude is east of botRight, or topLeft latitude is south of botRight, the query is malformed -- flag before sending.
- **Key deletion without awareness**: If a DELETE is issued, warn that all in-flight Real User Metrics collection will stop and any JavaScript snippets using the old key will break.

## Playbook

### 1. Enable Real User Metrics from Scratch

1. PUT /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys to create a new metrics key
2. Note the returned key value from the 201 response
3. Embed the key in your client-side JavaScript snippet on target web pages
4. Wait for data collection (typically 24-48 hours for meaningful data)
5. GET the heat map endpoint to view collected traffic patterns

### 2. View Traffic Patterns for a Specific Region

1. GET /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys to confirm metrics collection is active
2. Determine bounding box coordinates (e.g., US: topLeft=49.0,-125.0 botRight=24.0,-66.0)
3. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/heatMaps/{heatMapType} with topLeft and botRight query params
4. Parse the response for endpoint-level traffic distribution within the region

### 3. Rotate the Real User Metrics Key

1. GET /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys to confirm current key exists
2. DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys to revoke the old key
3. PUT /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys to generate a new key
4. Update all client-side JavaScript snippets with the new key value
5. Verify collection resumes by checking heat map data after 24 hours

### 4. Disable Real User Metrics Collection

1. DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys
2. Confirm 200 response indicating successful deletion
3. Remove the JavaScript snippet from client-side pages to stop unnecessary network calls
4. Note: historical heat map data may still be available for a period after key deletion


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
