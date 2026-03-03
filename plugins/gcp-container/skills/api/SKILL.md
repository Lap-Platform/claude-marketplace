---
name: kubernetes-engine-api
description: "Kubernetes Engine API skill. Use when working with Kubernetes Engine for projects, {name}, {name}:cancel. Covers 60 endpoints."
version: 1.0.0
generator: lapsh
---

# Kubernetes Engine API
API version: v1

## Auth
OAuth2 | OAuth2

## Base URL
https://container.googleapis.com/

## Setup
1. Configure auth: OAuth2 | OAuth2
2. GET /v1/projects/{projectId}/zones/{zone}/clusters -- verify access
3. POST /v1/projects/{projectId}/zones/{zone}/clusters -- create first clusters

## Endpoints

60 endpoints across 21 groups. See references/api-spec.lap for full details.

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/projects/{projectId}/zones/{zone}/clusters | Lists all clusters owned by a project in either the specified zone or all zones. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters | Creates a cluster, consisting of the specified number and type of Google Compute Engine instances. By default, the cluster is created in the project's [default network](https://cloud.google.com/compute/docs/networks-and-firewalls#networks). One firewall is added for the cluster. After cluster creation, the Kubelet creates routes for each node to allow the containers on that node to communicate with all other instances in the cluster. Finally, an entry is added to the project's global metadata indicating which CIDR range the cluster is using. |
| DELETE | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId} | Deletes the cluster, including the Kubernetes endpoint and all worker nodes. Firewalls and routes that were configured during cluster creation are also deleted. Other Google Compute Engine resources that might be in use by the cluster, such as load balancer resources, are not deleted if they weren't present when the cluster was initially created. |
| GET | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId} | Gets the details of a specific cluster. |
| PUT | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId} | Updates the settings of a specific cluster. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/addons | Sets the addons for a specific cluster. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/legacyAbac | Enables or disables the ABAC authorization mechanism on a cluster. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/locations | Sets the locations for a specific cluster. Deprecated. Use [projects.locations.clusters.update](https://cloud.google.com/kubernetes-engine/docs/reference/rest/v1/projects.locations.clusters/update) instead. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/logging | Sets the logging service for a specific cluster. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/master | Updates the master for a specific cluster. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/monitoring | Sets the monitoring service for a specific cluster. |
| GET | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/nodePools | Lists the node pools for a cluster. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/nodePools | Creates a node pool for a cluster. |
| DELETE | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/nodePools/{nodePoolId} | Deletes a node pool from a cluster. |
| GET | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/nodePools/{nodePoolId} | Retrieves the requested node pool. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/nodePools/{nodePoolId}/autoscaling | Sets the autoscaling settings for the specified node pool. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/nodePools/{nodePoolId}/setManagement | Sets the NodeManagement options for a node pool. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/nodePools/{nodePoolId}/setSize | Sets the size for a specific node pool. The new size will be used for all replicas, including future replicas created by modifying NodePool.locations. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/nodePools/{nodePoolId}/update | Updates the version and/or image type for the specified node pool. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/nodePools/{nodePoolId}:rollback | Rolls back a previously Aborted or Failed NodePool upgrade. This makes no changes if the last upgrade successfully completed. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}/resourceLabels | Sets labels on a cluster. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}:completeIpRotation | Completes master IP rotation. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}:setMaintenancePolicy | Sets the maintenance policy for a cluster. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}:setMasterAuth | Sets master auth materials. Currently supports changing the admin password or a specific cluster, either via password generation or explicitly setting the password. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}:setNetworkPolicy | Enables or disables Network Policy for a cluster. |
| POST | /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}:startIpRotation | Starts master IP rotation. |
| GET | /v1/projects/{projectId}/zones/{zone}/operations | Lists all operations in a project in a specific zone or all zones. |
| GET | /v1/projects/{projectId}/zones/{zone}/operations/{operationId} | Gets the specified operation. |
| POST | /v1/projects/{projectId}/zones/{zone}/operations/{operationId}:cancel | Cancels the specified operation. |
| GET | /v1/projects/{projectId}/zones/{zone}/serverconfig | Returns configuration info about the Google Kubernetes Engine service. |

### {name}
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /v1/{name} | Deletes a node pool from a cluster. |
| GET | /v1/{name} | Gets the specified operation. |
| PUT | /v1/{name} | Updates the version and/or image type for the specified node pool. |
| GET | /v1/{name}/serverConfig | Returns configuration info about the Google Kubernetes Engine service. |

### {name}:cancel
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:cancel | Cancels the specified operation. |

### {name}:completeIpRotation
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:completeIpRotation | Completes master IP rotation. |

### {name}:completeUpgrade
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:completeUpgrade | CompleteNodePoolUpgrade will signal an on-going node pool upgrade to complete. |

### {name}:rollback
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:rollback | Rolls back a previously Aborted or Failed NodePool upgrade. This makes no changes if the last upgrade successfully completed. |

### {name}:setAddons
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:setAddons | Sets the addons for a specific cluster. |

### {name}:setAutoscaling
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:setAutoscaling | Sets the autoscaling settings for the specified node pool. |

### {name}:setLegacyAbac
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:setLegacyAbac | Enables or disables the ABAC authorization mechanism on a cluster. |

### {name}:setLocations
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:setLocations | Sets the locations for a specific cluster. Deprecated. Use [projects.locations.clusters.update](https://cloud.google.com/kubernetes-engine/docs/reference/rest/v1/projects.locations.clusters/update) instead. |

### {name}:setLogging
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:setLogging | Sets the logging service for a specific cluster. |

### {name}:setMaintenancePolicy
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:setMaintenancePolicy | Sets the maintenance policy for a cluster. |

### {name}:setManagement
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:setManagement | Sets the NodeManagement options for a node pool. |

### {name}:setMasterAuth
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:setMasterAuth | Sets master auth materials. Currently supports changing the admin password or a specific cluster, either via password generation or explicitly setting the password. |

### {name}:setMonitoring
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:setMonitoring | Sets the monitoring service for a specific cluster. |

### {name}:setNetworkPolicy
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:setNetworkPolicy | Enables or disables Network Policy for a cluster. |

### {name}:setResourceLabels
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:setResourceLabels | Sets labels on a cluster. |

### {name}:setSize
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:setSize | Sets the size for a specific node pool. The new size will be used for all replicas, including future replicas created by modifying NodePool.locations. |

### {name}:startIpRotation
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:startIpRotation | Starts master IP rotation. |

### {name}:updateMaster
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/{name}:updateMaster | Updates the master for a specific cluster. |

### {parent}
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/{parent}/.well-known/openid-configuration | Gets the OIDC discovery document for the cluster. See the [OpenID Connect Discovery 1.0 specification](https://openid.net/specs/openid-connect-discovery-1_0.html) for details. This API is not yet intended for general use, and is not available for all clusters. |
| GET | /v1/{parent}/aggregated/usableSubnetworks | Lists subnetworks that are usable for creating clusters in a project. |
| GET | /v1/{parent}/clusters | Lists all clusters owned by a project in either the specified zone or all zones. |
| POST | /v1/{parent}/clusters | Creates a cluster, consisting of the specified number and type of Google Compute Engine instances. By default, the cluster is created in the project's [default network](https://cloud.google.com/compute/docs/networks-and-firewalls#networks). One firewall is added for the cluster. After cluster creation, the Kubelet creates routes for each node to allow the containers on that node to communicate with all other instances in the cluster. Finally, an entry is added to the project's global metadata indicating which CIDR range the cluster is using. |
| GET | /v1/{parent}/jwks | Gets the public component of the cluster signing keys in JSON Web Key format. This API is not yet intended for general use, and is not available for all clusters. |
| GET | /v1/{parent}/nodePools | Lists the node pools for a cluster. |
| POST | /v1/{parent}/nodePools | Creates a node pool for a cluster. |
| GET | /v1/{parent}/operations | Lists all operations in a project in a specific zone or all zones. |

## Enhanced Skill Content
## Question Mapping

- "What clusters are running in my project?" -> GET /v1/{parent}/clusters
- "How do I create a new GKE cluster?" -> POST /v1/{parent}/clusters
- "What are the details of a specific cluster?" -> GET /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}
- "How do I delete a cluster?" -> DELETE /v1/projects/{projectId}/zones/{zone}/clusters/{clusterId}
- "What node pools exist in my cluster?" -> GET /v1/{parent}/nodePools
- "How do I add a node pool to a cluster?" -> POST /v1/{parent}/nodePools
- "How do I scale a node pool up or down?" -> POST /v1/{name}:setSize
- "How do I upgrade the master version of my cluster?" -> POST /v1/{name}:updateMaster
- "What Kubernetes versions are available in my zone?" -> GET /v1/{parent}/serverConfig
- "How do I enable or disable cluster autoscaling?" -> POST /v1/{name}:setAutoscaling
- "What operations are currently running on my cluster?" -> GET /v1/{parent}/operations
- "How do I cancel a long-running cluster operation?" -> POST /v1/{name}:cancel
- "How do I rotate my cluster's IP addresses and credentials?" -> POST /v1/{name}:startIpRotation
- "How do I set a maintenance window for my cluster?" -> POST /v1/{name}:setMaintenancePolicy
- "How do I enable network policy on my cluster?" -> POST /v1/{name}:setNetworkPolicy

## Response Tips

- **Cluster lists**: Check `missingZones` array -- non-empty means some zones were unreachable and results are partial.
- **Mutating operations** (create, delete, update, scale): All return an Operation object; poll `status` field (`RUNNING`, `DONE`, `ABORTING`) via GET /v1/{name} until completion.
- **Operation errors**: Inspect `error.code` and `error.details[]` for structured failure reasons; `statusMessage` may contain a human-readable summary but can be empty.
- **Server config**: `validMasterVersions` and `validNodeVersions` are ordered arrays; `channels[]` maps release channels (RAPID, REGULAR, STABLE) to their supported versions.
- **Node pool details**: `management.upgradeOptions.autoUpgradeStartTime` is only populated when an auto-upgrade is actually scheduled.
- **OIDC/JWKS**: `cacheHeader.age` and `cacheHeader.expires` indicate upstream caching; respect these to avoid unnecessary re-fetches.

## Anomaly Flags

- **Cluster status not RUNNING**: Surface immediately if `status` is `DEGRADED`, `ERROR`, `RECONCILING`, or `STOPPING` -- the cluster may be unhealthy or mid-transition.
- **Operation stuck**: Flag any operation where `status` remains `RUNNING` for an extended period without `progress.stages` advancing.
- **Legacy ABAC enabled**: If `legacyAbac.enabled` is true, warn the user -- this is a deprecated, less-secure authorization mode.
- **Missing zones in list responses**: A non-empty `missingZones` array means the API could not reach some zones; results are incomplete.
- **Master/node version skew**: If `currentMasterVersion` and `currentNodeVersion` differ by more than two minor versions, flag a potential compatibility risk.
- **Expiring clusters**: If `expireTime` is set and approaching, the cluster will be auto-deleted.
- **Shielded nodes disabled**: If `shieldedNodes.enabled` is false, recommend enabling for improved node integrity.
- **Basic auth credentials present**: If `masterAuth.username` or `masterAuth.password` are non-empty, warn about deprecated basic authentication.
- **Condition codes**: Surface any entries in `conditions[]` or `clusterConditions[]` with non-OK `canonicalCode` values.

## Playbook

### 1. Create a cluster and verify it is ready

1. GET /v1/{parent}/serverConfig to find the latest valid master version and available image types.
2. POST /v1/{parent}/clusters with your desired cluster config (name, node count, machine type, network settings).
3. Capture the returned operation `name`.
4. Poll GET /v1/{name} until `status` is `DONE`. Check `error` for failures.
5. GET /v1/{parent}/clusters and confirm the new cluster appears with `status: RUNNING`.

### 2. Scale a node pool

1. GET /v1/{parent}/nodePools to list pools and identify the target `nodePoolId`.
2. POST /v1/{name}:setSize with the desired `nodeCount`.
3. Poll the returned operation via GET /v1/{name} until `status` is `DONE`.
4. GET the node pool detail to confirm `initialNodeCount` reflects the new size and `status` is `RUNNING`.

### 3. Upgrade master and nodes

1. GET /v1/{parent}/serverConfig to find available versions in `validMasterVersions`.
2. POST /v1/{name}:updateMaster with the target `masterVersion`.
3. Poll the operation until `DONE`.
4. For each node pool, POST /v1/{name} (PUT update) or use the node pool update endpoint with the target `nodeVersion`.
5. Poll each node pool operation until `DONE`.
6. GET the cluster detail and verify `currentMasterVersion` and `currentNodeVersion` match expectations.

### 4. Rotate cluster IP addresses and credentials

1. POST /v1/{name}:startIpRotation (set `rotateCredentials: true` to also rotate credentials).
2. Poll the returned operation until `DONE`.
3. Update all clients and kubeconfig to use the new endpoint/credentials.
4. POST /v1/{name}:completeIpRotation to finalize and drop the old IP.
5. Poll until `DONE`, then verify connectivity with the new endpoint.

### 5. Set up a maintenance window

1. GET the cluster to read the current `maintenancePolicy` and note the `resourceVersion`.
2. POST /v1/{name}:setMaintenancePolicy with a `window` containing either a `dailyMaintenanceWindow` (start time + duration) or a `recurringWindow` (RRULE recurrence + time window). Include `maintenanceExclusions` for blackout periods.
3. Poll the operation until `DONE`.
4. GET the cluster again and confirm `maintenancePolicy.window` reflects your settings.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
