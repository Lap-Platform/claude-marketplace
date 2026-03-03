---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 1 endpoint."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions | Lists all azure regions in which the service exists. |

## Enhanced Skill Content
## Question Mapping

- "What regions is my API Management service deployed to?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions
- "List all regions for a specific APIM instance" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions
- "Which Azure regions host my API gateway?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions
- "Is my API Management service deployed in East US?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions
- "How many regions is my APIM service running in?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions
- "Show the geographic distribution of my API Management deployment" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions
- "What is the multi-region setup for my APIM service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions
- "Verify my APIM service exists in a specific resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions
- "Get region info for API Management service {serviceName}" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions
- "Which regions should I check for APIM gateway health?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions
- "Compare expected vs actual regions for my APIM deployment" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions

## Response Tips

- **Regions listing (200):** Response contains a `value` array of region objects and may include a `nextLink` for pagination. Each region entry typically has `name`, `isMasterRegion`, and `isDeleted` fields. Always check `nextLink` and follow it to retrieve all pages. A 404 means the service name, resource group, or subscription is wrong. A 403 indicates missing RBAC permissions on the APIM resource.

## Anomaly Flags

- **Single region returned** when a Premium-tier multi-region deployment is expected -- may indicate misconfiguration or incomplete deployment.
- **`isDeleted: true`** on any region entry -- a region is being deprovisioned; surface this immediately.
- **`isMasterRegion` missing or false for all entries** -- no primary region identified, which is abnormal and warrants investigation.
- **404 or 403 responses** -- the APIM service may have been deleted, moved, or the caller lacks Reader/Contributor role on the resource. Surface the exact error code and suggest checking resource group and RBAC assignments.
- **429 (Too Many Requests)** -- Azure ARM throttling is active. Surface the `Retry-After` header value and pause before retrying.
- **Empty `value` array with 200 status** -- service exists but reports no regions, which is an inconsistent state worth flagging.

## Playbook

### 1. Verify Multi-Region Deployment

1. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/regions` with a valid OAuth2 bearer token.
2. Check the `value` array length -- it should match the expected number of regions.
3. Identify the master region by finding the entry where `isMasterRegion` is `true`.
4. Confirm no regions have `isDeleted: true`.
5. Compare the returned region names against your intended deployment configuration.

### 2. Audit Region Health Before Maintenance

1. List all regions using the regions endpoint.
2. Record each region's `name` and `isMasterRegion` status.
3. If `nextLink` is present, follow pagination until all regions are retrieved.
4. Flag any region marked `isDeleted` -- it may already be mid-deprovisioning.
5. Use the region list to scope subsequent health or diagnostics calls per region.

### 3. Troubleshoot Missing APIM Service

1. Attempt the regions call with the expected subscription, resource group, and service name.
2. If you receive a 404, confirm the `subscriptionId` is correct and active.
3. Verify the `resourceGroupName` exists under that subscription (use the Resource Groups API).
4. Check that the `serviceName` matches exactly (names are case-sensitive in the URL path).
5. If a 403 is returned instead, verify the calling identity has at least `Reader` role on the APIM resource or resource group.

### 4. Enumerate Regions for Capacity Planning

1. Retrieve all regions for the APIM service using the regions endpoint.
2. Follow any `nextLink` pagination to get the complete list.
3. Count total regions and identify the master region.
4. Cross-reference with Azure region availability and your organization's compliance requirements.
5. Use the output to decide whether to add or remove gateway regions via the APIM update API.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
