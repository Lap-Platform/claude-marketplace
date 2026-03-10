---
name: azure-reservation-api
description: "Azure Reservation API skill. Use when working with Azure Reservation for subscriptions. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# Azure Reservation API
API version: 2019-07-19-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/resourceProviders/{providerId}/locations/{location}/serviceLimits -- verify access

## Endpoints

8 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/resourceProviders/{providerId}/locations/{location}/serviceLimits/{resourceName} | Gets the current service limits (quotas) and usage of a resource. The response from Get API can be leveraged to submit quota update requests. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/resourceProviders/{providerId}/locations/{location}/serviceLimits/{resourceName} | Create or update the service limits (quota) of a resource to requested value. |
| PATCH | /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/resourceProviders/{providerId}/locations/{location}/serviceLimits/{resourceName} | Update the service limits (quota) of a resource to requested value. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/resourceProviders/{providerId}/locations/{location}/serviceLimits | Get a list of current service limits (quota) and usages of all the resources. The response from List API can be leveraged to submit quota update requests. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/resourceProviders/{providerId}/locations/{location}/serviceLimitsRequests/{id} | Gets the QuotaRequest details and status by the quota request Id for the resources for the resource provider at a specific location. The requestId is returned as response to the Put requests for serviceLimits. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/resourceProviders/{providerId}/locations/{location}/serviceLimitsRequests | For the specified location and Resource provider gets the current quota requests under the subscription over the time period of one year ago from now to one year back. oData filter can be used to select quota requests. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/autoQuotaIncrease | Gets the Auto Quota Increase enrollment details for the specified subscription. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/autoQuotaIncrease | Sets the Auto Quota Increase enrollment properties for the specified subscription. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get serviceLimit details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/resourceProviders/{providerId}/locations/{location}/serviceLimits/{resourceName}
- "Update a serviceLimit?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/resourceProviders/{providerId}/locations/{location}/serviceLimits/{resourceName}
- "Partially update a serviceLimit?" -> PATCH /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/resourceProviders/{providerId}/locations/{location}/serviceLimits/{resourceName}
- "List all serviceLimits?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/resourceProviders/{providerId}/locations/{location}/serviceLimits
- "Get serviceLimitsRequest details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/resourceProviders/{providerId}/locations/{location}/serviceLimitsRequests/{id}
- "List all serviceLimitsRequests?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/resourceProviders/{providerId}/locations/{location}/serviceLimitsRequests
- "List all autoQuotaIncrease?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Capacity/autoQuotaIncrease
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
