---
name: datafactorymanagementclient
description: "DataFactoryManagementClient API skill. Use when working with DataFactoryManagementClient for providers, subscriptions. Covers 102 endpoints."
version: 1.0.0
generator: lapsh
---

# DataFactoryManagementClient
API version: 2018-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.DataFactory/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.DataFactory/locations/{locationId}/configureFactoryRepo -- create first configureFactoryRepo

## Endpoints

102 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.DataFactory/operations | Lists the available Azure Data Factory API operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.DataFactory/factories | Lists factories under the specified subscription. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.DataFactory/locations/{locationId}/configureFactoryRepo | Updates a factory's repo information. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.DataFactory/locations/{locationId}/getFeatureValue | Get exposure control feature for specific location. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/getFeatureValue | Get exposure control feature for specific factory. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/queryFeaturesValue | Get list of exposure control features for specific factory. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories | Lists factories. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName} | Creates or updates a factory. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName} | Updates a factory. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName} | Gets a factory. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName} | Deletes a factory. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/getGitHubAccessToken | Get GitHub Access Token. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/getDataPlaneAccess | Get Data Plane access. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes | Lists integration runtimes. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName} | Creates or updates an integration runtime. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName} | Gets an integration runtime. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName} | Updates an integration runtime. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName} | Deletes an integration runtime. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/getStatus | Gets detailed status information for an integration runtime. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/outboundNetworkDependenciesEndpoints | Gets the list of outbound network dependencies for a given Azure-SSIS integration runtime. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/getConnectionInfo | Gets the on-premises integration runtime connection information for encrypting the on-premises data source credentials. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/regenerateAuthKey | Regenerates the authentication key for an integration runtime. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/listAuthKeys | Retrieves the authentication keys for an integration runtime. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/start | Starts a ManagedReserved type integration runtime. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/stop | Stops a ManagedReserved type integration runtime. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/syncCredentials | Force the integration runtime to synchronize credentials across integration runtime nodes, and this will override the credentials across all worker nodes with those available on the dispatcher node. If you already have the latest credential backup file, you should manually import it (preferred) on any self-hosted integration runtime node than using this API directly. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/monitoringData | Get the integration runtime monitoring data, which includes the monitor data for all the nodes under this integration runtime. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/upgrade | Upgrade self-hosted integration runtime to latest version if availability. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/removeLinks | Remove all linked integration runtimes under specific data factory in a self-hosted integration runtime. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/linkedIntegrationRuntime | Create a linked integration runtime entry in a shared integration runtime. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/refreshObjectMetadata | Refresh a SSIS integration runtime object metadata. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/getObjectMetadata | Get a SSIS integration runtime object metadata by specified path. The return is pageable metadata list. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/nodes/{nodeName} | Gets a self-hosted integration runtime node. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/nodes/{nodeName} | Deletes a self-hosted integration runtime node. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/nodes/{nodeName} | Updates a self-hosted integration runtime node. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/nodes/{nodeName}/ipAddress | Get the IP address of self-hosted integration runtime node. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/linkedservices | Lists linked services. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/linkedservices/{linkedServiceName} | Creates or updates a linked service. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/linkedservices/{linkedServiceName} | Gets a linked service. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/linkedservices/{linkedServiceName} | Deletes a linked service. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/datasets | Lists datasets. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/datasets/{datasetName} | Creates or updates a dataset. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/datasets/{datasetName} | Gets a dataset. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/datasets/{datasetName} | Deletes a dataset. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelines | Lists pipelines. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelines/{pipelineName} | Creates or updates a pipeline. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelines/{pipelineName} | Gets a pipeline. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelines/{pipelineName} | Deletes a pipeline. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelines/{pipelineName}/createRun | Creates a run of a pipeline. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/queryPipelineRuns | Query pipeline runs in the factory based on input filter conditions. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns/{runId} | Get a pipeline run by its run ID. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns/{runId}/queryActivityruns | Query activity runs based on input filter conditions. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns/{runId}/cancel | Cancel a pipeline run by its run ID. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/triggers | Lists triggers. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/querytriggers | Query triggers. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/triggers/{triggerName} | Creates or updates a trigger. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/triggers/{triggerName} | Gets a trigger. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/triggers/{triggerName} | Deletes a trigger. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/triggers/{triggerName}/subscribeToEvents | Subscribe event trigger to events. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/triggers/{triggerName}/getEventSubscriptionStatus | Get a trigger's event subscription status. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/triggers/{triggerName}/unsubscribeFromEvents | Unsubscribe event trigger from events. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/triggers/{triggerName}/start | Starts a trigger. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/triggers/{triggerName}/stop | Stops a trigger. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/triggers/{triggerName}/triggerRuns/{runId}/rerun | Rerun single trigger instance by runId. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/triggers/{triggerName}/triggerRuns/{runId}/cancel | Cancel a single trigger instance by runId. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/queryTriggerRuns | Query trigger runs. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/dataflows/{dataFlowName} | Creates or updates a data flow. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/dataflows/{dataFlowName} | Gets a data flow. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/dataflows/{dataFlowName} | Deletes a data flow. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/dataflows | Lists data flows. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/createDataFlowDebugSession | Creates a data flow debug session. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/queryDataFlowDebugSessions | Query all active data flow debug sessions. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/addDataFlowToDebugSession | Add a data flow into debug session. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/deleteDataFlowDebugSession | Deletes a data flow debug session. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/executeDataFlowDebugCommand | Execute a data flow debug command. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/managedVirtualNetworks | Lists managed Virtual Networks. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/managedVirtualNetworks/{managedVirtualNetworkName} | Creates or updates a managed Virtual Network. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/managedVirtualNetworks/{managedVirtualNetworkName} | Gets a managed Virtual Network. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/managedVirtualNetworks/{managedVirtualNetworkName}/managedPrivateEndpoints | Lists managed private endpoints. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/credentials | List credentials. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/credentials/{credentialName} | Creates or updates a credential. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/credentials/{credentialName} | Gets a credential. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/credentials/{credentialName} | Deletes a credential. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/managedVirtualNetworks/{managedVirtualNetworkName}/managedPrivateEndpoints/{managedPrivateEndpointName} | Creates or updates a managed private endpoint. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/managedVirtualNetworks/{managedVirtualNetworkName}/managedPrivateEndpoints/{managedPrivateEndpointName} | Gets a managed private endpoint. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/managedVirtualNetworks/{managedVirtualNetworkName}/managedPrivateEndpoints/{managedPrivateEndpointName} | Deletes a managed private endpoint. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/privateEndPointConnections | Lists Private endpoint connections |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/privateEndpointConnections/{privateEndpointConnectionName} | Approves or rejects a private endpoint connection |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/privateEndpointConnections/{privateEndpointConnectionName} | Gets a private endpoint connection |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/privateEndpointConnections/{privateEndpointConnectionName} | Deletes a private endpoint connection |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/privateLinkResources | Gets the private link resources |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/globalParameters | Lists Global parameters |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/globalParameters/{globalParameterName} | Gets a Global parameter |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/globalParameters/{globalParameterName} | Creates or updates a Global parameter |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/globalParameters/{globalParameterName} | Deletes a Global parameter |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/adfcdcs | Lists all resources of type change data capture. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/adfcdcs/{changeDataCaptureName} | Creates or updates a change data capture resource. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/adfcdcs/{changeDataCaptureName} | Gets a change data capture. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/adfcdcs/{changeDataCaptureName} | Deletes a change data capture. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/adfcdcs/{changeDataCaptureName}/start | Starts a change data capture. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/adfcdcs/{changeDataCaptureName}/stop | Stops a change data capture. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/adfcdcs/{changeDataCaptureName}/status | Gets the current status for the change data capture resource. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available in the Data Factory resource provider?" -> GET /providers/Microsoft.DataFactory/operations
- "List all data factories in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DataFactory/factories
- "List data factories in a specific resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories
- "Create or update a data factory" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}
- "Delete a data factory" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}
- "Run a pipeline in my data factory" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelines/{pipelineName}/createRun
- "Check the status of a pipeline run" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns/{runId}
- "Cancel a running pipeline" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns/{runId}/cancel
- "What activity runs happened in a pipeline run?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns/{runId}/queryActivityruns
- "List all triggers in my factory" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/triggers
- "Start or stop a trigger" -> POST .../triggers/{triggerName}/start and POST .../triggers/{triggerName}/stop
- "Get the status of an integration runtime" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/getStatus
- "Connect my factory to a GitHub repo" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.DataFactory/locations/{locationId}/configureFactoryRepo
- "Start a data flow debug session" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/createDataFlowDebugSession
- "Check the status of a change data capture" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/adfcdcs/{changeDataCaptureName}/status

## Response Tips

- **List endpoints** (factories, pipelines, datasets, triggers, linked services, data flows, CDCs): Responses are paginated via `nextLink`; keep fetching until `nextLink` is absent. Items are in a `value` array.
- **GET single resource**: Returns the full resource object with `id`, `name`, `type`, `properties`, and `etag`. A 304 means the resource has not changed since your `If-None-Match` ETag -- no body is returned.
- **PUT/PATCH resource**: Returns the updated resource object. Use the returned `etag` for subsequent conditional updates via `If-Match`.
- **DELETE resource**: 200 means deleted; 204 means the resource did not exist (already deleted). Both are success.
- **Pipeline createRun**: Returns a `runId` string -- save this to query run status and activity runs afterward.
- **Query endpoints** (queryPipelineRuns, queryActivityruns, queryTriggerRuns): Accept `filterParameters` with `lastUpdatedAfter`, `lastUpdatedBefore`, and optional `filters`/`orderBy`. Responses include `value` array and optional `continuationToken`.
- **Async operations** (integration runtime start/stop, trigger subscribe/unsubscribe, debug sessions): 202 means the operation was accepted but is still running. Poll the `Location` or `Azure-AsyncOperation` header URL until completion.

## Anomaly Flags

- **304 Not Modified on GETs**: Surface when a conditional GET returns 304 -- the cached version is still current, no body to parse.
- **202 Accepted on long-running operations**: Flag that integration runtime start/stop, trigger event subscriptions, debug session creation, and metadata refresh are async. Prompt the user to poll for completion.
- **204 on DELETE**: Proactively note when a delete returns 204 (resource already gone) vs 200 (actually deleted) so the user knows the prior state.
- **ETag drift**: If a PUT with `If-Match` fails with 412 Precondition Failed, surface that another process modified the resource -- the user needs to re-read and retry.
- **Missing nextLink misinterpreted as complete**: Warn if a list response has exactly the page-size number of items but no `nextLink` -- this edge case can mask truncated results.
- **Feature flags and exposure control**: Responses from getFeatureValue/queryFeaturesValue may return features that are not yet GA. Flag any feature with `"state": "Off"` or unexpected values.
- **Integration runtime node disappearance**: When listing or getting integration runtime nodes, flag if node count drops compared to a prior call -- may indicate infrastructure issues.
- **Trigger in failed subscription state**: After calling getEventSubscriptionStatus, flag if the status is not "Enabled" since the trigger will silently miss events.

## Playbook

### 1. Create a Factory and Run Your First Pipeline

1. PUT a new factory: `PUT .../factories/{factoryName}` with the `factory` body (location, identity, optional git config).
2. Create a linked service for your data source: `PUT .../linkedservices/{linkedServiceName}` with connection properties.
3. Create source and sink datasets: `PUT .../datasets/{datasetName}` for each, referencing the linked service.
4. Create a pipeline with a copy activity: `PUT .../pipelines/{pipelineName}` with activities referencing the datasets.
5. Trigger the pipeline: `POST .../pipelines/{pipelineName}/createRun`. Save the returned `runId`.
6. Monitor the run: `GET .../pipelineruns/{runId}` until `status` is `Succeeded` or `Failed`.
7. Inspect activity details: `POST .../pipelineruns/{runId}/queryActivityruns` with a time-range filter.

### 2. Set Up and Manage an Integration Runtime

1. Create the integration runtime: `PUT .../integrationRuntimes/{irName}` with type (`Managed`, `SelfHosted`).
2. For self-hosted: retrieve auth keys with `POST .../integrationRuntimes/{irName}/listAuthKeys` and install the agent on your machine.
3. Start the runtime: `POST .../integrationRuntimes/{irName}/start` (returns 202 -- poll until ready).
4. Check status: `POST .../integrationRuntimes/{irName}/getStatus` to confirm it is `Online`.
5. Monitor nodes: `GET .../integrationRuntimes/{irName}/nodes/{nodeName}` for health and version info.
6. Upgrade when available: `POST .../integrationRuntimes/{irName}/upgrade`.
7. To decommission: `POST .../integrationRuntimes/{irName}/stop`, then `DELETE .../integrationRuntimes/{irName}`.

### 3. Configure Triggers and Monitor Trigger Runs

1. Create a trigger: `PUT .../triggers/{triggerName}` with schedule or event properties.
2. For event-based triggers, subscribe: `POST .../triggers/{triggerName}/subscribeToEvents` (async -- poll 202).
3. Verify subscription: `POST .../triggers/{triggerName}/getEventSubscriptionStatus` -- ensure status is `Enabled`.
4. Start the trigger: `POST .../triggers/{triggerName}/start`.
5. Query trigger runs: `POST .../queryTriggerRuns` with time-range filters to see execution history.
6. Rerun a failed trigger run: `POST .../triggers/{triggerName}/triggerRuns/{runId}/rerun`.
7. To disable: `POST .../triggers/{triggerName}/stop`, then optionally `POST .../triggers/{triggerName}/unsubscribeFromEvents`.

### 4. Debug a Data Flow Interactively

1. Start a debug session: `POST .../createDataFlowDebugSession` with compute and TTL settings (returns 202 -- poll).
2. List active sessions: `POST .../queryDataFlowDebugSessions` to get the session ID.
3. Add your data flow to the session: `POST .../addDataFlowToDebugSession` with the data flow definition and linked services.
4. Execute a debug command: `POST .../executeDataFlowDebugCommand` with the command type (preview, stats, expression) -- poll the 202 response.
5. Iterate: modify the data flow, re-add, and re-execute commands as needed.
6. Clean up: `POST .../deleteDataFlowDebugSession` when done to free compute resources.

### 5. Set Up Change Data Capture (CDC)

1. Create a CDC resource: `PUT .../adfcdcs/{changeDataCaptureName}` with source, sink, and mapping configuration.
2. Verify the configuration: `GET .../adfcdcs/{changeDataCaptureName}` to confirm properties are correct.
3. Start the CDC: `POST .../adfcdcs/{changeDataCaptureName}/start`.
4. Monitor status: `GET .../adfcdcs/{changeDataCaptureName}/status` -- check for latency and error counts.
5. To pause: `POST .../adfcdcs/{changeDataCaptureName}/stop`. To resume, call start again.
6. To remove: `DELETE .../adfcdcs/{changeDataCaptureName}` (returns 200 if existed, 204 if already gone).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
