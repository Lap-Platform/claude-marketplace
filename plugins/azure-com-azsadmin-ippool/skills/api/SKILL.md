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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools/{ipPool} | Return the requested IP pool. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools/{ipPool} | Create an IP pool.  Once created an IP pool cannot be deleted. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools | Returns a list of all IP pools at a certain location. |

## Enhanced Skill Content
## Question Mapping

- "What IP pools exist in my fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools
- "Show me details for a specific IP pool" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools/{ipPool}
- "Does IP pool X exist in my fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools/{ipPool}
- "Create a new IP pool in my fabric location" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools/{ipPool}
- "Update the configuration of an existing IP pool" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools/{ipPool}
- "How many IP pools are configured in location X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools
- "What address ranges does IP pool Y use?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools/{ipPool}
- "Replace the pool definition for an IP pool" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools/{ipPool}
- "List all IP pools across a specific resource group and location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools
- "Verify an IP pool was created successfully" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools/{ipPool}
- "Check if a pool name is already taken before creating one" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools/{ipPool}
- "Provision IP capacity for a fabric deployment" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/ipPools/{ipPool}

## Response Tips

- **IP Pool detail (GET single):** Response is a single resource object with properties nested under `properties`. A 404 means the pool name does not exist in that location -- do not retry, check the name and location path segments.
- **IP Pool list (GET collection):** Response wraps results in a `value` array. Check for a `nextLink` field for pagination; keep following it until absent. An empty `value` array is valid (no pools configured).
- **IP Pool create/update (PUT):** A 200 means the operation completed synchronously. A 202 means the operation is asynchronous -- read the `Location` or `Azure-AsyncOperation` header and poll until terminal state. Treat both as success-in-progress.

## Anomaly Flags

- **202 Accepted without polling URL:** If a PUT returns 202 but the response lacks both `Location` and `Azure-AsyncOperation` headers, surface this immediately -- the agent cannot track completion.
- **404 on list endpoint:** A 404 on the collection GET (not the single-resource GET) suggests the fabric location or resource group path is wrong, not that there are zero pools. Flag the distinction.
- **Stale async operations:** If polling an async PUT operation exceeds 10 minutes without reaching a terminal state, alert the user that the provisioning may be stuck.
- **Pool property drift:** When a GET after a PUT shows property values that differ from what was submitted, flag the discrepancy -- the platform may have normalized or rejected fields silently.
- **Missing api-version query parameter:** All Azure ARM calls require `?api-version=2016-05-01`. If a request fails with 400, check this first and surface it.

## Playbook

### 1. Create a New IP Pool

1. List existing pools with GET on the collection endpoint to confirm the desired name is not taken.
2. Build the `pool` map body with required address ranges and configuration.
3. Send PUT with the pool name in the path and the body payload.
4. If response is 200, the pool is ready. If 202, extract the async operation URL from response headers.
5. Poll the async URL until the status is `Succeeded` or a terminal failure.
6. Confirm creation by issuing a GET on the new pool's resource path.

### 2. Audit All IP Pools in a Location

1. Issue GET on the collection endpoint for the target subscription, resource group, and location.
2. Collect the `value` array from the response.
3. If `nextLink` is present, follow it and append results until no more pages.
4. For each pool, inspect the `properties` object for address ranges, status, and metadata.
5. Summarize pool count, total address space, and any pools in a non-healthy state.

### 3. Update an Existing IP Pool Configuration

1. GET the current pool definition by name to retrieve the full resource object.
2. Modify only the fields that need to change within the `properties` block.
3. PUT the updated full resource body back (Azure ARM uses full-replace semantics on PUT).
4. Handle 200 (immediate) or 202 (async) as in the create playbook.
5. GET the pool again to verify the updated properties match expectations.

### 4. Validate Pool Existence Before Dependent Operations

1. Issue GET on the specific pool by name.
2. If 200, the pool exists -- proceed with the dependent operation (e.g., assigning it to infrastructure).
3. If 404, either create the pool first (see Playbook 1) or alert the user that the prerequisite is missing.
4. Never assume a pool exists based on a prior list call -- always re-check immediately before dependent writes to avoid race conditions.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
