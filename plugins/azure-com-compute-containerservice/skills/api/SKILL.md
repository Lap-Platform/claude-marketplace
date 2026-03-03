---
name: containerserviceclient
description: "ContainerServiceClient API skill. Use when working with ContainerServiceClient for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# ContainerServiceClient
API version: 2017-01-31

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.ContainerService/containerServices -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.ContainerService/containerServices | Gets a list of container services in the specified subscription. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName} | Creates or updates a container service. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName} | Gets the properties of the specified container service. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName} | Deletes the specified container service. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices | Gets a list of container services in the specified resource group. |

## Enhanced Skill Content
## Question Mapping

- "What container services exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.ContainerService/containerServices
- "List all container services in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices
- "Get details of a specific container service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName}
- "Create a new container service cluster?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName}
- "Update an existing container service?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName}
- "Delete a container service?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName}
- "How do I scale my container service agents?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName}
- "Is my container service provisioning complete?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName}
- "Which resource groups have container services?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.ContainerService/containerServices
- "How do I change the orchestrator type on my cluster?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName}
- "Remove a container service I no longer need?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName}
- "What orchestrator is my container service using?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName}
- "Deploy a Kubernetes cluster via ACS?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName}

## Response Tips

- **List endpoints (GET .../containerServices):** Returns a `value` array of container service objects. Check for `nextLink` property to handle pagination across large result sets.
- **Get single resource (GET .../containerServices/{name}):** Returns the full resource object. Inspect `properties.provisioningState` for deployment status (Succeeded, Failed, Creating, Updating, Deleting).
- **Create/Update (PUT):** 200 means updated in place, 201 means created, 202 means accepted for async processing -- check the `Azure-AsyncOperation` or `Location` response header to poll for completion.
- **Delete (DELETE):** 202 means deletion accepted and in progress (poll the operation URL), 204 means the resource was already gone -- both are success cases.
- **Errors:** Azure returns `{ "error": { "code": "...", "message": "..." } }` -- surface the `code` and `message` fields directly.

## Anomaly Flags

- **Provisioning stuck:** If `provisioningState` remains `Creating` or `Updating` for more than 30 minutes, surface a warning -- cluster deployment may be stalled.
- **202 without operation header:** If a PUT or DELETE returns 202 but no `Azure-AsyncOperation` or `Location` header, flag this -- there is no way to poll for completion.
- **Repeated 409 Conflict:** Indicates a concurrent operation on the same resource. Surface that another deployment or deletion may be in progress.
- **API version mismatch:** If a 400 error mentions `api-version`, flag that `2017-01-31` is a legacy version and suggest checking for newer API versions.
- **Subscription quota errors:** 429 or errors referencing core/VM quotas should be surfaced immediately -- the user needs to request a quota increase before retrying.
- **Delete returning 204 unexpectedly:** If the user expected the resource to exist but DELETE returns 204 (not found), flag that the resource may have already been removed or the name is incorrect.

## Playbook

### 1. Deploy a New Container Service Cluster

1. List existing services: GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices` to confirm the name is not taken.
2. Build the `parameters` body with orchestrator profile (Kubernetes, Swarm, or DCOS), agent pool profiles (VM size, count), master profile, and Linux SSH key.
3. Create the cluster: PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName}` with the parameters body.
4. If response is 202, poll the `Azure-AsyncOperation` URL until status is `Succeeded`.
5. Verify by fetching the resource: GET the same path and confirm `provisioningState` is `Succeeded`.

### 2. Scale an Existing Cluster's Agent Pool

1. Fetch current config: GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName}`.
2. Modify the `agentPoolProfiles[].count` value in the response body to the desired node count.
3. Submit the update: PUT the same path with the modified body.
4. Monitor the async operation if 202 is returned. Confirm `provisioningState` returns to `Succeeded`.

### 3. Safely Delete a Container Service

1. Verify the target: GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerService/containerServices/{containerServiceName}` to confirm you have the right cluster.
2. Issue the delete: DELETE the same path.
3. If 202, poll the operation URL until completion. If 204, the resource is already gone.
4. Confirm removal: GET the resource again -- expect a 404 response.

### 4. Audit All Container Services Across a Subscription

1. List all services subscription-wide: GET `/subscriptions/{subscriptionId}/providers/Microsoft.ContainerService/containerServices`.
2. Follow `nextLink` pagination until all results are collected.
3. For each service, inspect `provisioningState` and `orchestratorProfile.orchestratorType`.
4. Flag any clusters in `Failed` state or running deprecated orchestrator versions for follow-up.

### 5. Migrate Orchestrator Type (Replace Cluster)

1. Fetch the existing cluster config: GET the container service resource.
2. Record all configuration (agent pools, networking, SSH keys, tags).
3. Delete the old cluster: DELETE the resource path and wait for completion.
4. Create a new cluster with the updated orchestrator type: PUT with modified `orchestratorProfile.orchestratorType` in the parameters.
5. Verify the new cluster reaches `Succeeded` provisioning state before redeploying workloads.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
