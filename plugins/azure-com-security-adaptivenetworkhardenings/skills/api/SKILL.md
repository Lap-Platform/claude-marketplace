---
name: microsoft-defender-for-cloud
description: "Microsoft Defender for Cloud API skill. Use when working with Microsoft Defender for Cloud for subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Microsoft Defender for Cloud
API version: 2015-06-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.Security/adaptiveNetworkHardenings -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.Security/adaptiveNetworkHardenings/{adaptiveNetworkHardeningResourceName}/{adaptiveNetworkHardeningEnforceAction} -- create first adaptiveNetworkHardenings

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.Security/adaptiveNetworkHardenings | Gets a list of Adaptive Network Hardenings resources in scope of an extended resource. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.Security/adaptiveNetworkHardenings/{adaptiveNetworkHardeningResourceName} | Gets a single Adaptive Network Hardening resource |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.Security/adaptiveNetworkHardenings/{adaptiveNetworkHardeningResourceName}/{adaptiveNetworkHardeningEnforceAction} | Enforces the given rules on the NSG(s) listed in the request |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all adaptiveNetworkHardenings?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.Security/adaptiveNetworkHardenings
- "Get adaptiveNetworkHardening details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceNamespace}/{resourceType}/{resourceName}/providers/Microsoft.Security/adaptiveNetworkHardenings/{adaptiveNetworkHardeningResourceName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
