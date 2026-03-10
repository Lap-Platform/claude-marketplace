---
name: security-center
description: "Security Center API skill. Use when working with Security Center for {resourceId}. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Security Center
API version: 2019-08-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /{resourceId}/providers/Microsoft.Security/deviceSecurityGroups -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### {resourceId}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{resourceId}/providers/Microsoft.Security/deviceSecurityGroups | Use this method get the list of device security groups for the specified IoT Hub resource. |
| GET | /{resourceId}/providers/Microsoft.Security/deviceSecurityGroups/{deviceSecurityGroupName} | Use this method to get the device security group for the specified IoT Hub resource. |
| PUT | /{resourceId}/providers/Microsoft.Security/deviceSecurityGroups/{deviceSecurityGroupName} | Use this method to creates or updates the device security group on a specified IoT Hub resource. |
| DELETE | /{resourceId}/providers/Microsoft.Security/deviceSecurityGroups/{deviceSecurityGroupName} | User this method to deletes the device security group. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all deviceSecurityGroups?" -> GET /{resourceId}/providers/Microsoft.Security/deviceSecurityGroups
- "Get deviceSecurityGroup details?" -> GET /{resourceId}/providers/Microsoft.Security/deviceSecurityGroups/{deviceSecurityGroupName}
- "Update a deviceSecurityGroup?" -> PUT /{resourceId}/providers/Microsoft.Security/deviceSecurityGroups/{deviceSecurityGroupName}
- "Delete a deviceSecurityGroup?" -> DELETE /{resourceId}/providers/Microsoft.Security/deviceSecurityGroups/{deviceSecurityGroupName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
