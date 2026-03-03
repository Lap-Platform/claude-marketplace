---
name: fabricadminclient
description: "FabricAdminClient API skill. Use when working with FabricAdminClient for subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# FabricAdminClient
API version: 2016-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles/{infraRole}/Restart -- create first Restart

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles/{infraRole} | Returns the requested infrastructure role description. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles | Returns a list of all infrastructure roles at a location. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles/{infraRole}/Restart | Restarts the requested infrastructure role. |

## Enhanced Skill Content
## Question Mapping

- "What infrastructure roles exist in my fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles
- "Get details about a specific infrastructure role" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles/{infraRole}
- "What is the status of the AzS-ACS01 role?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles/{infraRole}
- "Restart an infrastructure role" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles/{infraRole}/Restart
- "Is a specific infrastructure role running?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles/{infraRole}
- "List all infra roles for a given Azure Stack location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles
- "How many infrastructure role instances are active?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles
- "Reboot a misbehaving fabric infrastructure role" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles/{infraRole}/Restart
- "Does a specific infrastructure role exist in my deployment?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles/{infraRole}
- "Which infrastructure roles are in my resource group's fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles
- "Force restart a role after a failed health check" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles/{infraRole}/Restart
- "Check infrastructure health by enumerating all roles and their states" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/infraRoles

## Response Tips

- **Single role GET**: Returns the full infrastructure role resource object; check the `properties` nested object for runtime state, instance count, and role type.
- **List roles GET**: Returns a `value` array of role objects; may include a `nextLink` field for pagination -- follow it until absent.
- **Restart POST**: Returns 200 for synchronous completion or 202 for accepted-async; on 202, check the `Location` or `Azure-AsyncOperation` header to poll for completion.
- **Errors**: 404 means the role name, location, or resource group does not exist; verify all path segments before retrying.

## Anomaly Flags

- **202 on Restart**: The restart was accepted but has not completed. Surface this to the user and recommend polling the async operation URL from response headers.
- **404 on role lookup**: The infrastructure role name may be misspelled or the fabric location may be incorrect. Proactively suggest listing all roles to discover valid names.
- **Unexpected role state**: After listing roles, flag any role whose status is not "Running" or healthy -- this may indicate infrastructure degradation.
- **Repeated restart failures**: If a restart returns 202 but the subsequent poll never reaches a terminal state, flag a potential stuck operation.
- **Missing nextLink on large deployments**: If the list response contains many items but no `nextLink`, all results fit in one page. If `nextLink` is present, warn the user that results are partial until all pages are fetched.

## Playbook

### 1. Audit all infrastructure roles in a fabric location

1. Call GET `/infraRoles` to list all roles for the target subscription, resource group, and location.
2. If the response contains a `nextLink`, follow it to retrieve additional pages.
3. For each role, inspect `properties.instances` and `properties.restartable` to build a health summary.
4. Flag any role not in a healthy running state.

### 2. Investigate and restart an unhealthy role

1. Call GET `/infraRoles/{infraRole}` to retrieve current details and confirm the role exists.
2. Review the `properties` block for status indicators and instance counts.
3. If the role is unhealthy, call POST `/infraRoles/{infraRole}/Restart`.
4. If the response is 202, extract the async operation URL from the `Location` or `Azure-AsyncOperation` header.
5. Poll the operation URL until it reports success or failure.
6. Call GET `/infraRoles/{infraRole}` again to verify the role has recovered.

### 3. Validate fabric location setup after deployment

1. Call GET `/infraRoles` to enumerate all infrastructure roles.
2. Verify the expected roles are present (compare against the deployment template).
3. For each expected role, call GET `/infraRoles/{infraRole}` to confirm its properties match expectations.
4. Report any missing roles or roles with unexpected configuration.

### 4. Scheduled health check with auto-remediation

1. Call GET `/infraRoles` to list all roles.
2. For each role, check if its state indicates degradation or failure.
3. For any unhealthy role where `restartable` is true, call POST `/infraRoles/{infraRole}/Restart`.
4. Track 202 responses and poll their async operation URLs to completion.
5. After all restarts complete, re-list roles with GET `/infraRoles` to confirm recovery.
6. Surface any roles that remain unhealthy after restart for manual investigation.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
