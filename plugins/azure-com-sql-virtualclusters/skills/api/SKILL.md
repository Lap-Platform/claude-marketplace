---
name: sqlmanagementclient
description: "SqlManagementClient API skill. Use when working with SqlManagementClient for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# SqlManagementClient
API version: 2015-05-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Sql/virtualClusters -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Sql/virtualClusters | Gets a list of all virtualClusters in the subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/virtualClusters | Gets a list of virtual clusters in a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/virtualClusters/{virtualClusterName} | Gets a virtual cluster. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/virtualClusters/{virtualClusterName} | Deletes a virtual cluster. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/virtualClusters/{virtualClusterName} | Updates a virtual cluster. |

## Enhanced Skill Content
## Question Mapping

- "List all virtual clusters in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Sql/virtualClusters
- "What virtual clusters exist in resource group X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/virtualClusters
- "Show me details for a specific virtual cluster?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/virtualClusters/{virtualClusterName}
- "Delete a virtual cluster?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/virtualClusters/{virtualClusterName}
- "Update a virtual cluster's properties?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/virtualClusters/{virtualClusterName}
- "How many virtual clusters do I have across all resource groups?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Sql/virtualClusters
- "Is my virtual cluster delete still in progress?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/virtualClusters/{virtualClusterName} (check 202 status)
- "Move a virtual cluster to a different subnet?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/virtualClusters/{virtualClusterName}
- "Which resource group contains virtual cluster Y?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Sql/virtualClusters (scan results)
- "Remove all virtual clusters from a resource group?" -> GET (list) then DELETE (each) in resource group scope
- "Check if a virtual cluster exists before creating managed instances?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/virtualClusters/{virtualClusterName}
- "What tags are on my virtual cluster?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/virtualClusters/{virtualClusterName}
- "Update tags on a virtual cluster without changing other properties?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/virtualClusters/{virtualClusterName}

## Response Tips

- **List endpoints (subscription/resource group scope):** Response contains a `value` array of virtual cluster objects. Check for `nextLink` property for pagination -- follow it until absent. Each item includes `id`, `name`, `type`, `location`, and `properties`.
- **Get single cluster:** Returns a flat resource object. Key fields are under `properties` (e.g., `subnetId`, `childResources`, `state`). A 404 means the cluster does not exist.
- **Delete:** 200 means completed synchronously, 202 means accepted (long-running operation -- check the `Location` or `Azure-AsyncOperation` header to poll), 204 means the resource was already gone.
- **Patch/Update:** 200 means the update completed immediately, 202 means it is a long-running operation. Poll the async operation URL from response headers until terminal state.

## Anomaly Flags

- **202 Accepted on DELETE or PATCH:** The operation is long-running. Surface this to the user and offer to poll the async operation URL from the response headers.
- **204 on DELETE:** The virtual cluster was already deleted or never existed. Flag this if the user expected it to exist.
- **Missing `nextLink` after unexpectedly short list:** If the user expects many clusters but the list is short with no pagination, flag a possible scope mismatch (wrong subscription or resource group).
- **`state` property not "Ready":** If a virtual cluster's provisioning state is anything other than Ready (e.g., InProgress, Failed), proactively warn the user before they attempt modifications or deletions.
- **api-version mismatch:** This spec uses `2015-05-01-preview` (a preview API). Flag that newer stable versions may be available and behavior could differ.
- **Empty `childResources`:** If deleting a virtual cluster that still has child managed instances, the operation will fail. Check and warn before attempting deletion.

## Playbook

### 1. Inventory All Virtual Clusters in a Subscription

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Sql/virtualClusters` with `api-version=2015-05-01-preview`
2. Parse the `value` array from the response
3. If `nextLink` is present, follow it with a GET request and append results
4. Repeat until no `nextLink` remains
5. Summarize: count, locations, resource groups, and provisioning states

### 2. Safely Delete a Virtual Cluster

1. Call GET on the specific virtual cluster to confirm it exists and check `properties.childResources`
2. If `childResources` is non-empty, warn the user that dependent managed instances must be removed first
3. Call DELETE on the virtual cluster
4. If response is 200: done. If 202: extract the `Azure-AsyncOperation` or `Location` header
5. Poll the async URL with GET every 15-30 seconds until status is `Succeeded` or `Failed`
6. Confirm deletion by calling GET on the cluster (expect 404)

### 3. Update Virtual Cluster Tags

1. Call GET on the specific virtual cluster to retrieve current properties
2. Construct a PATCH body with only the `tags` field: `{"tags": {"env": "prod", "team": "data"}}`
3. Call PATCH with the `parameters` body
4. If response is 200, the update applied immediately -- verify tags in response body
5. If response is 202, poll the async operation until complete, then GET the cluster to confirm

### 4. Find Which Resource Group Hosts a Virtual Cluster

1. Call GET at subscription scope to list all virtual clusters
2. Parse the `id` field of each result (format: `/subscriptions/.../resourceGroups/{rgName}/providers/...`)
3. Extract the resource group name from the matching cluster's `id`
4. Optionally call the resource-group-scoped GET to confirm and list sibling clusters

### 5. Audit Virtual Cluster Health Across Resource Groups

1. Call GET at subscription scope to retrieve all virtual clusters
2. For each cluster, inspect `properties.state` -- bucket into Ready, InProgress, Failed
3. Flag any clusters in Failed or non-Ready state
4. For Failed clusters, call GET on each individually to capture detailed error information in `properties`
5. Report findings: total count, healthy vs unhealthy, and affected resource groups


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
