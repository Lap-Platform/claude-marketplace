---
name: aws-server-migration-service
description: "AWS Server Migration Service API skill. Use when working with AWS Server Migration Service for root. Covers 35 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Server Migration Service
API version: 2016-10-24

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

35 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Creates an application. An application consists of one or more server groups. Each server group contain one or more servers. |
| POST | / | Creates a replication job. The replication job schedules periodic replication runs to replicate your server to Amazon Web Services. Each replication run creates an Amazon Machine Image (AMI). |
| POST | / | Deletes the specified application. Optionally deletes the launched stack associated with the application and all Server Migration Service replication jobs for servers in the application. |
| POST | / | Deletes the launch configuration for the specified application. |
| POST | / | Deletes the replication configuration for the specified application. |
| POST | / | Deletes the validation configuration for the specified application. |
| POST | / | Deletes the specified replication job. After you delete a replication job, there are no further replication runs. Amazon Web Services deletes the contents of the Amazon S3 bucket used to store Server Migration Service artifacts. The AMIs created by the replication runs are not deleted. |
| POST | / | Deletes all servers from your server catalog. |
| POST | / | Disassociates the specified connector from Server Migration Service. After you disassociate a connector, it is no longer available to support replication jobs. |
| POST | / | Generates a target change set for a currently launched stack and writes it to an Amazon S3 object in the customer’s Amazon S3 bucket. |
| POST | / | Generates an CloudFormation template based on the current launch configuration and writes it to an Amazon S3 object in the customer’s Amazon S3 bucket. |
| POST | / | Retrieve information about the specified application. |
| POST | / | Retrieves the application launch configuration associated with the specified application. |
| POST | / | Retrieves the application replication configuration associated with the specified application. |
| POST | / | Retrieves information about a configuration for validating an application. |
| POST | / | Retrieves output from validating an application. |
| POST | / | Describes the connectors registered with the Server Migration Service. |
| POST | / | Describes the specified replication job or all of your replication jobs. |
| POST | / | Describes the replication runs for the specified replication job. |
| POST | / | Describes the servers in your server catalog. Before you can describe your servers, you must import them using ImportServerCatalog. |
| POST | / | Allows application import from Migration Hub. |
| POST | / | Gathers a complete list of on-premises servers. Connectors must be installed and monitoring all servers to import. This call returns immediately, but might take additional time to retrieve all the servers. |
| POST | / | Launches the specified application as a stack in CloudFormation. |
| POST | / | Retrieves summaries for all applications. |
| POST | / | Provides information to Server Migration Service about whether application validation is successful. |
| POST | / | Creates or updates the launch configuration for the specified application. |
| POST | / | Creates or updates the replication configuration for the specified application. |
| POST | / | Creates or updates a validation configuration for the specified application. |
| POST | / | Starts replicating the specified application by creating replication jobs for each server in the application. |
| POST | / | Starts an on-demand replication run for the specified application. |
| POST | / | Starts an on-demand replication run for the specified replication job. This replication run starts immediately. This replication run is in addition to the ones already scheduled. There is a limit on the number of on-demand replications runs that you can request in a 24-hour period. |
| POST | / | Stops replicating the specified application by deleting the replication job for each server in the application. |
| POST | / | Terminates the stack for the specified application. |
| POST | / | Updates the specified application. |
| POST | / | Updates the specified settings for the specified replication job. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a migration application with server groups?" -> POST / (CreateApp)
- "How do I start replicating a server to AWS?" -> POST / (CreateReplicationJob)
- "How do I list all my migration applications?" -> POST / (ListApps)
- "What servers are available in my on-premises catalog?" -> POST / (GetServers)
- "How do I check the status of a replication job?" -> POST / (GetReplicationJobs)
- "How do I see individual replication run results for a job?" -> POST / (GetReplicationRuns)
- "How do I launch a migrated application into AWS?" -> POST / (LaunchApp)
- "How do I generate a CloudFormation template for my app?" -> POST / (GenerateTemplate)
- "How do I generate a changeset for my application?" -> POST / (GenerateChangeSet)
- "How do I update replication settings like frequency or encryption?" -> POST / (UpdateReplicationJob)
- "How do I configure launch settings for server groups?" -> POST / (PutAppLaunchConfiguration)
- "How do I validate my application before migration?" -> POST / (PutAppValidationConfiguration + GetAppValidationOutput)
- "How do I trigger an immediate replication run outside the schedule?" -> POST / (StartOnDemandReplicationRun)
- "How do I clean up and delete a migration app and its resources?" -> POST / (DeleteApp with forceStopAppReplication + forceTerminateApp)
- "What connectors are registered in my environment?" -> POST / (GetConnectors)

## Response Tips

- **List endpoints** (ListApps, GetConnectors, GetServers, GetReplicationJobs): All return `nextToken` for pagination -- keep calling with the returned token until it is null. Use `maxResults` to control page size.
- **App detail endpoints** (GetApp, CreateApp, UpdateApp): Return nested `appSummary` with status fields (`status`, `replicationStatus`, `launchStatus`) that track overall migration progress. `LaunchDetails` is nested one level deeper.
- **Replication endpoints** (GetReplicationRuns): Return both a top-level `replicationJob` object and a separate `replicationRunList` array. The run list is also nested inside the job object -- prefer the top-level list for pagination.
- **Template/changeset endpoints** (GenerateTemplate, GenerateChangeSet): Return an `s3Location` with `bucket` and `key` -- you must fetch the actual artifact from S3 separately.
- **Void endpoints** (DeleteApp, LaunchApp, ImportServerCatalog, etc.): Return empty 200 responses on success. Any non-200 indicates an error.

## Anomaly Flags

- **Replication status stuck**: Surface when `replicationStatus` stays in a non-terminal state across multiple polls, or `statusMessage` contains error text.
- **Failed replication runs**: Flag any `ReplicationRun` entries with failed state in `replicationRunList` -- these may silently accumulate.
- **Stale server catalog**: If `lastModifiedOn` from GetServers is significantly old, the connector may have lost connectivity. Also check `serverCatalogStatus` for non-healthy values.
- **Encryption without KMS key**: If `encrypted` is true but `kmsKeyId` is empty on a replication job, the default EBS key is used -- flag this for security review.
- **Missing connectors**: If GetConnectors returns an empty `connectorList`, no on-premises agent is registered and replication cannot proceed.
- **Launch failure indicators**: When `launchStatus` shows failure or `launchStatusMessage` is non-empty, surface immediately -- CloudFormation stack issues may need manual intervention.
- **AMI retention risk**: If `numberOfRecentAmisToKeep` is set very low (e.g., 1), warn that rollback options are limited.

## Playbook

### 1. Initial Server Discovery and Catalog Import

1. Call ImportServerCatalog to trigger a sync from your on-premises connector.
2. Call GetConnectors to verify at least one connector is registered and active.
3. Call GetServers with pagination to retrieve the full server inventory.
4. Review the server list and note `serverId` values for servers you want to migrate.

### 2. Set Up a Full Application Migration

1. Call CreateApp with a `name`, `description`, and `serverGroups` containing your target servers.
2. Call PutAppReplicationConfiguration with `appId` and `serverGroupReplicationConfigurations` to set replication frequency, encryption, and license type per server group.
3. Call PutAppLaunchConfiguration with `appId` to configure launch settings (instance types, subnets, security groups) per server group.
4. Call StartAppReplication with the `appId` to begin replication across all server groups.
5. Poll GetApp periodically to monitor `replicationStatus` until all servers reach a ready state.

### 3. Validate and Launch a Migrated Application

1. Call PutAppValidationConfiguration with `appId` and validation rules for both app-level and server-group-level checks.
2. Call GetAppValidationOutput with `appId` to review validation results and confirm all checks pass.
3. Call GenerateTemplate to produce a CloudFormation template and review the output from S3.
4. Call LaunchApp with `appId` to deploy the application into AWS.
5. Call GetApp to monitor `launchStatus` and retrieve `launchDetails` (stack name, stack ID, launch time).

### 4. Trigger and Monitor an On-Demand Replication

1. Call StartOnDemandReplicationRun with `replicationJobId` and an optional `description`. Note the returned `replicationRunId`.
2. Call GetReplicationRuns with the `replicationJobId`, paginating if needed.
3. Find the run matching your `replicationRunId` and check its state and status message.
4. Once the run completes, call GetReplicationJobs to confirm `latestAmiId` has been updated.

### 5. Clean Up After Migration

1. Call StopAppReplication with `appId` to halt all ongoing replication for the application.
2. Call DeleteReplicationJob for each individual replication job if you need granular cleanup.
3. Call TerminateApp with `appId` to tear down launched AWS resources (CloudFormation stacks).
4. Call DeleteApp with `appId`, setting `forceStopAppReplication: true` and `forceTerminateApp: true` to remove the application and all associated resources in one call.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
