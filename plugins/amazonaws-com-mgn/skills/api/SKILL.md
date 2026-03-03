---
name: application-migration-service
description: "Application Migration Service API skill. Use when working with Application Migration Service for ArchiveApplication, ArchiveWave, AssociateApplications. Covers 70 endpoints."
version: 1.0.0
generator: lapsh
---

# Application Migration Service
API version: 2020-02-26

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /DescribeVcenterClients -- verify access
3. POST /ArchiveApplication -- create first ArchiveApplication

## Endpoints

70 endpoints across 68 groups. See references/api-spec.lap for full details.

### ArchiveApplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /ArchiveApplication | Archive application. |

### ArchiveWave
| Method | Path | Description |
|--------|------|-------------|
| POST | /ArchiveWave | Archive wave. |

### AssociateApplications
| Method | Path | Description |
|--------|------|-------------|
| POST | /AssociateApplications | Associate applications to wave. |

### AssociateSourceServers
| Method | Path | Description |
|--------|------|-------------|
| POST | /AssociateSourceServers | Associate source servers to application. |

### ChangeServerLifeCycleState
| Method | Path | Description |
|--------|------|-------------|
| POST | /ChangeServerLifeCycleState | Allows the user to set the SourceServer.LifeCycle.state property for specific Source Server IDs to one of the following: READY_FOR_TEST or READY_FOR_CUTOVER. This command only works if the Source Server is already launchable (dataReplicationInfo.lagDuration is not null.) |

### CreateApplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /CreateApplication | Create application. |

### CreateConnector
| Method | Path | Description |
|--------|------|-------------|
| POST | /CreateConnector | Create Connector. |

### CreateLaunchConfigurationTemplate
| Method | Path | Description |
|--------|------|-------------|
| POST | /CreateLaunchConfigurationTemplate | Creates a new Launch Configuration Template. |

### CreateReplicationConfigurationTemplate
| Method | Path | Description |
|--------|------|-------------|
| POST | /CreateReplicationConfigurationTemplate | Creates a new ReplicationConfigurationTemplate. |

### CreateWave
| Method | Path | Description |
|--------|------|-------------|
| POST | /CreateWave | Create wave. |

### DeleteApplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /DeleteApplication | Delete application. |

### DeleteConnector
| Method | Path | Description |
|--------|------|-------------|
| POST | /DeleteConnector | Delete Connector. |

### DeleteJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /DeleteJob | Deletes a single Job by ID. |

### DeleteLaunchConfigurationTemplate
| Method | Path | Description |
|--------|------|-------------|
| POST | /DeleteLaunchConfigurationTemplate | Deletes a single Launch Configuration Template by ID. |

### DeleteReplicationConfigurationTemplate
| Method | Path | Description |
|--------|------|-------------|
| POST | /DeleteReplicationConfigurationTemplate | Deletes a single Replication Configuration Template by ID |

### DeleteSourceServer
| Method | Path | Description |
|--------|------|-------------|
| POST | /DeleteSourceServer | Deletes a single source server by ID. |

### DeleteVcenterClient
| Method | Path | Description |
|--------|------|-------------|
| POST | /DeleteVcenterClient | Deletes a given vCenter client by ID. |

### DeleteWave
| Method | Path | Description |
|--------|------|-------------|
| POST | /DeleteWave | Delete wave. |

### DescribeJobLogItems
| Method | Path | Description |
|--------|------|-------------|
| POST | /DescribeJobLogItems | Retrieves detailed job log items with paging. |

### DescribeJobs
| Method | Path | Description |
|--------|------|-------------|
| POST | /DescribeJobs | Returns a list of Jobs. Use the JobsID and fromDate and toData filters to limit which jobs are returned. The response is sorted by creationDataTime - latest date first. Jobs are normally created by the StartTest, StartCutover, and TerminateTargetInstances APIs. Jobs are also created by DiagnosticLaunch and TerminateDiagnosticInstances, which are APIs available only to *Support* and only used in response to relevant support tickets. |

### DescribeLaunchConfigurationTemplates
| Method | Path | Description |
|--------|------|-------------|
| POST | /DescribeLaunchConfigurationTemplates | Lists all Launch Configuration Templates, filtered by Launch Configuration Template IDs |

### DescribeReplicationConfigurationTemplates
| Method | Path | Description |
|--------|------|-------------|
| POST | /DescribeReplicationConfigurationTemplates | Lists all ReplicationConfigurationTemplates, filtered by Source Server IDs. |

### DescribeSourceServers
| Method | Path | Description |
|--------|------|-------------|
| POST | /DescribeSourceServers | Retrieves all SourceServers or multiple SourceServers by ID. |

### DescribeVcenterClients
| Method | Path | Description |
|--------|------|-------------|
| GET | /DescribeVcenterClients | Returns a list of the installed vCenter clients. |

### DisassociateApplications
| Method | Path | Description |
|--------|------|-------------|
| POST | /DisassociateApplications | Disassociate applications from wave. |

### DisassociateSourceServers
| Method | Path | Description |
|--------|------|-------------|
| POST | /DisassociateSourceServers | Disassociate source servers from application. |

### DisconnectFromService
| Method | Path | Description |
|--------|------|-------------|
| POST | /DisconnectFromService | Disconnects specific Source Servers from Application Migration Service. Data replication is stopped immediately. All AWS resources created by Application Migration Service for enabling the replication of these source servers will be terminated / deleted within 90 minutes. Launched Test or Cutover instances will NOT be terminated. If the agent on the source server has not been prevented from communicating with the Application Migration Service service, then it will receive a command to uninstall itself (within approximately 10 minutes). The following properties of the SourceServer will be changed immediately: dataReplicationInfo.dataReplicationState will be set to DISCONNECTED; The totalStorageBytes property for each of dataReplicationInfo.replicatedDisks will be set to zero; dataReplicationInfo.lagDuration and dataReplicationInfo.lagDuration will be nullified. |

### FinalizeCutover
| Method | Path | Description |
|--------|------|-------------|
| POST | /FinalizeCutover | Finalizes the cutover immediately for specific Source Servers. All AWS resources created by Application Migration Service for enabling the replication of these source servers will be terminated / deleted within 90 minutes. Launched Test or Cutover instances will NOT be terminated. The AWS Replication Agent will receive a command to uninstall itself (within 10 minutes). The following properties of the SourceServer will be changed immediately: dataReplicationInfo.dataReplicationState will be changed to DISCONNECTED; The SourceServer.lifeCycle.state will be changed to CUTOVER; The totalStorageBytes property fo each of dataReplicationInfo.replicatedDisks will be set to zero; dataReplicationInfo.lagDuration and dataReplicationInfo.lagDuration will be nullified. |

### GetLaunchConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /GetLaunchConfiguration | Lists all LaunchConfigurations available, filtered by Source Server IDs. |

### GetReplicationConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /GetReplicationConfiguration | Lists all ReplicationConfigurations, filtered by Source Server ID. |

### InitializeService
| Method | Path | Description |
|--------|------|-------------|
| POST | /InitializeService | Initialize Application Migration Service. |

### ListApplications
| Method | Path | Description |
|--------|------|-------------|
| POST | /ListApplications | Retrieves all applications or multiple applications by ID. |

### ListConnectors
| Method | Path | Description |
|--------|------|-------------|
| POST | /ListConnectors | List Connectors. |

### ListExportErrors
| Method | Path | Description |
|--------|------|-------------|
| POST | /ListExportErrors | List export errors. |

### ListExports
| Method | Path | Description |
|--------|------|-------------|
| POST | /ListExports | List exports. |

### ListImportErrors
| Method | Path | Description |
|--------|------|-------------|
| POST | /ListImportErrors | List import errors. |

### ListImports
| Method | Path | Description |
|--------|------|-------------|
| POST | /ListImports | List imports. |

### ListManagedAccounts
| Method | Path | Description |
|--------|------|-------------|
| POST | /ListManagedAccounts | List Managed Accounts. |

### ListSourceServerActions
| Method | Path | Description |
|--------|------|-------------|
| POST | /ListSourceServerActions | List source server post migration custom actions. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{resourceArn} | List all tags for your Application Migration Service resources. |
| POST | /tags/{resourceArn} | Adds or overwrites only the specified tags for the specified Application Migration Service resource or resources. When you specify an existing tag key, the value is overwritten with the new value. Each resource can have a maximum of 50 tags. Each tag consists of a key and optional value. |
| DELETE | /tags/{resourceArn} | Deletes the specified set of tags from the specified set of Application Migration Service resources. |

### ListTemplateActions
| Method | Path | Description |
|--------|------|-------------|
| POST | /ListTemplateActions | List template post migration custom actions. |

### ListWaves
| Method | Path | Description |
|--------|------|-------------|
| POST | /ListWaves | Retrieves all waves or multiple waves by ID. |

### MarkAsArchived
| Method | Path | Description |
|--------|------|-------------|
| POST | /MarkAsArchived | Archives specific Source Servers by setting the SourceServer.isArchived property to true for specified SourceServers by ID. This command only works for SourceServers with a lifecycle. state which equals DISCONNECTED or CUTOVER. |

### PauseReplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /PauseReplication | Pause Replication. |

### PutSourceServerAction
| Method | Path | Description |
|--------|------|-------------|
| POST | /PutSourceServerAction | Put source server post migration custom action. |

### PutTemplateAction
| Method | Path | Description |
|--------|------|-------------|
| POST | /PutTemplateAction | Put template post migration custom action. |

### RemoveSourceServerAction
| Method | Path | Description |
|--------|------|-------------|
| POST | /RemoveSourceServerAction | Remove source server post migration custom action. |

### RemoveTemplateAction
| Method | Path | Description |
|--------|------|-------------|
| POST | /RemoveTemplateAction | Remove template post migration custom action. |

### ResumeReplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /ResumeReplication | Resume Replication. |

### RetryDataReplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /RetryDataReplication | Causes the data replication initiation sequence to begin immediately upon next Handshake for specified SourceServer IDs, regardless of when the previous initiation started. This command will not work if the SourceServer is not stalled or is in a DISCONNECTED or STOPPED state. |

### StartCutover
| Method | Path | Description |
|--------|------|-------------|
| POST | /StartCutover | Launches a Cutover Instance for specific Source Servers. This command starts a LAUNCH job whose initiatedBy property is StartCutover and changes the SourceServer.lifeCycle.state property to CUTTING_OVER. |

### StartExport
| Method | Path | Description |
|--------|------|-------------|
| POST | /StartExport | Start export. |

### StartImport
| Method | Path | Description |
|--------|------|-------------|
| POST | /StartImport | Start import. |

### StartReplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /StartReplication | Starts replication for SNAPSHOT_SHIPPING agents. |

### StartTest
| Method | Path | Description |
|--------|------|-------------|
| POST | /StartTest | Launches a Test Instance for specific Source Servers. This command starts a LAUNCH job whose initiatedBy property is StartTest and changes the SourceServer.lifeCycle.state property to TESTING. |

### StopReplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /StopReplication | Stop Replication. |

### TerminateTargetInstances
| Method | Path | Description |
|--------|------|-------------|
| POST | /TerminateTargetInstances | Starts a job that terminates specific launched EC2 Test and Cutover instances. This command will not work for any Source Server with a lifecycle.state of TESTING, CUTTING_OVER, or CUTOVER. |

### UnarchiveApplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /UnarchiveApplication | Unarchive application. |

### UnarchiveWave
| Method | Path | Description |
|--------|------|-------------|
| POST | /UnarchiveWave | Unarchive wave. |

### UpdateApplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /UpdateApplication | Update application. |

### UpdateConnector
| Method | Path | Description |
|--------|------|-------------|
| POST | /UpdateConnector | Update Connector. |

### UpdateLaunchConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /UpdateLaunchConfiguration | Updates multiple LaunchConfigurations by Source Server ID.  bootMode valid values are LEGACY_BIOS | UEFI |

### UpdateLaunchConfigurationTemplate
| Method | Path | Description |
|--------|------|-------------|
| POST | /UpdateLaunchConfigurationTemplate | Updates an existing Launch Configuration Template by ID. |

### UpdateReplicationConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /UpdateReplicationConfiguration | Allows you to update multiple ReplicationConfigurations by Source Server ID. |

### UpdateReplicationConfigurationTemplate
| Method | Path | Description |
|--------|------|-------------|
| POST | /UpdateReplicationConfigurationTemplate | Updates multiple ReplicationConfigurationTemplates by ID. |

### UpdateSourceServer
| Method | Path | Description |
|--------|------|-------------|
| POST | /UpdateSourceServer | Update Source Server. |

### UpdateSourceServerReplicationType
| Method | Path | Description |
|--------|------|-------------|
| POST | /UpdateSourceServerReplicationType | Allows you to change between the AGENT_BASED replication type and the SNAPSHOT_SHIPPING replication type. |

### UpdateWave
| Method | Path | Description |
|--------|------|-------------|
| POST | /UpdateWave | Update wave. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my source servers?" -> POST /DescribeSourceServers
- "What migration waves exist in my account?" -> POST /ListWaves
- "How do I group servers into an application?" -> POST /AssociateSourceServers
- "How do I start replicating a server?" -> POST /StartReplication
- "What is the replication status of my server?" -> POST /DescribeSourceServers (check `dataReplicationInfo.dataReplicationState`)
- "How do I kick off a cutover for a batch of servers?" -> POST /StartCutover
- "How do I test a migration before cutting over?" -> POST /StartTest
- "What jobs are running or completed?" -> POST /DescribeJobs
- "How do I see the logs for a specific migration job?" -> POST /DescribeJobLogItems
- "How do I add tags to a migration resource?" -> POST /tags/{resourceArn}
- "How do I create a wave and assign applications to it?" -> POST /CreateWave, then POST /AssociateApplications
- "How do I pause replication without losing progress?" -> POST /PauseReplication
- "How do I export my migration inventory to S3?" -> POST /StartExport
- "How do I import servers from a CSV in S3?" -> POST /StartImport
- "How do I finalize a cutover after validation?" -> POST /FinalizeCutover

## Response Tips

- **List/Describe endpoints** (`DescribeSourceServers`, `ListApplications`, `ListWaves`, `DescribeJobs`, etc.): All return `{items: [...], nextToken: str?}`. Page through results by passing `nextToken` back in subsequent requests with `maxResults` controlling page size.
- **Source server responses** (`StartReplication`, `PauseReplication`, `FinalizeCutover`, `ChangeServerLifeCycleState`, etc.): Return the full SourceServer object. Key nested objects are `dataReplicationInfo` (replication state, lag, ETA, errors), `lifeCycle` (cutover/test history with timestamps and jobIDs), and `sourceProperties` (OS, CPU, disks, network).
- **Job-returning endpoints** (`StartCutover`, `StartTest`, `TerminateTargetInstances`): Return a `job` wrapper containing `jobID`, `status`, `participatingServers[]`, and `type`. Use the `jobID` with `DescribeJobs`/`DescribeJobLogItems` to track progress.
- **Export/Import responses** (`StartExport`, `StartImport`): Return task objects with `progressPercentage` (float 0-100), `status`, and `summary` with created/modified counts. Poll `ListExports`/`ListImports` until status is terminal.
- **Void responses** (`AssociateApplications`, `DisassociateApplications`, `DeleteApplication`, `RemoveSourceServerAction`, etc.): Return empty 200 on success. Any non-200 indicates failure.

## Anomaly Flags

- **Replication errors**: Surface `dataReplicationInfo.dataReplicationError` immediately when `error` is non-null -- indicates replication has stalled and needs `RetryDataReplication` or investigation.
- **Replication lag**: Flag when `dataReplicationInfo.lagDuration` exceeds a reasonable threshold (e.g., >1 hour) as it means the target is falling behind the source.
- **Stalled initiation**: If `dataReplicationInfo.dataReplicationState` stays in an initiation state while `dataReplicationInitiation.nextAttemptDateTime` is in the past, replication may be stuck.
- **Archived resources**: Warn if `isArchived` is `true` on a source server, application, or wave that the user is trying to act on -- most operations will fail on archived resources.
- **Missing application association**: Flag source servers with a null `applicationID` -- these servers are not grouped into any application and will be excluded from wave-based cutover workflows.
- **Job failures**: When `DescribeJobs` returns jobs with `status` indicating failure, proactively surface the jobID and suggest checking `DescribeJobLogItems` for details.
- **Cutover not finalized**: If `lifeCycle.lastCutover.initiated` exists but `lifeCycle.lastCutover.finalized` is null, the cutover is in limbo -- prompt the user to finalize or revert.
- **EBS encryption without KMS key**: If `ebsEncryption` is set to `CUSTOM` but `ebsEncryptionKeyArn` is empty, replication will fail at launch time.

## Playbook

### 1. First-time setup: Initialize and configure replication

1. Call `POST /InitializeService` to set up MGN in the account (idempotent, safe to call multiple times).
2. Call `POST /CreateReplicationConfigurationTemplate` with your subnet, security groups, instance type, encryption, and staging area tags.
3. Call `POST /CreateLaunchConfigurationTemplate` with boot mode, licensing, and post-launch action settings.
4. Install the AWS Replication Agent on each source server (outside API -- agent auto-registers with MGN).
5. Verify servers appear via `POST /DescribeSourceServers`.

### 2. Organize servers into waves and applications

1. Call `POST /CreateWave` with a descriptive name (e.g., "Wave 1 - Web Tier").
2. Call `POST /CreateApplication` for each logical application grouping (e.g., "Frontend App").
3. Call `POST /AssociateApplications` to link applications to the wave.
4. Call `POST /AssociateSourceServers` to assign source servers to each application.
5. Verify the hierarchy via `POST /ListWaves` and check `waveAggregatedStatus.totalApplications`.

### 3. Test migration before cutover

1. Confirm replication is healthy: `POST /DescribeSourceServers` and check `dataReplicationInfo.dataReplicationState` is `CONTINUOUS`.
2. Call `POST /StartTest` with the list of `sourceServerIDs` to launch test instances.
3. Track the test job: `POST /DescribeJobs` using the returned `jobID`, then `POST /DescribeJobLogItems` for details.
4. Validate the launched test instances in EC2 (check `launchedInstance.ec2InstanceID` on the source server response).
5. When done testing, call `POST /TerminateTargetInstances` to clean up test instances.

### 4. Execute cutover

1. Ensure replication lag is minimal: check `dataReplicationInfo.lagDuration` via `POST /DescribeSourceServers`.
2. Call `POST /StartCutover` with all `sourceServerIDs` in the batch.
3. Monitor the cutover job via `POST /DescribeJobs` and `POST /DescribeJobLogItems`.
4. Validate the new EC2 instances, update DNS, and redirect traffic.
5. Call `POST /FinalizeCutover` for each source server to mark migration complete -- this stops replication and cleans up staging resources.

### 5. Bulk export and import for inventory management

1. Call `POST /StartExport` with your target `s3Bucket` and `s3Key` to export the full migration inventory.
2. Poll `POST /ListExports` until `status` is `SUCCEEDED` and check `summary` for counts.
3. If errors occurred, call `POST /ListExportErrors` with the `exportID` to get details.
4. To import servers from a CSV, call `POST /StartImport` with an `S3BucketSource` pointing to your file.
5. Poll `POST /ListImports` until complete, then call `POST /ListImportErrors` if `status` indicates partial failure.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
