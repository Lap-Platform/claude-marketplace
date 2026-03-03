---
name: amazon-neptune
description: "Amazon Neptune API skill. Use when working with Amazon Neptune for root. Covers 69 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Neptune
API version: 2014-10-31

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

69 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Associates an Identity and Access Management (IAM) role with an Neptune DB cluster. |
| POST | / | Adds a source identifier to an existing event notification subscription. |
| POST | / | Adds metadata tags to an Amazon Neptune resource. These tags can also be used with cost allocation reporting to track cost associated with Amazon Neptune resources, or used in a Condition statement in an IAM policy for Amazon Neptune. |
| POST | / | Applies a pending maintenance action to a resource (for example, to a DB instance). |
| POST | / | Copies the specified DB cluster parameter group. |
| POST | / | Copies a snapshot of a DB cluster. To copy a DB cluster snapshot from a shared manual DB cluster snapshot, SourceDBClusterSnapshotIdentifier must be the Amazon Resource Name (ARN) of the shared DB cluster snapshot. |
| POST | / | Copies the specified DB parameter group. |
| POST | / | Creates a new Amazon Neptune DB cluster. You can use the ReplicationSourceIdentifier parameter to create the DB cluster as a Read Replica of another DB cluster or Amazon Neptune DB instance. Note that when you create a new cluster using CreateDBCluster directly, deletion protection is disabled by default (when you create a new production cluster in the console, deletion protection is enabled by default). You can only delete a DB cluster if its DeletionProtection field is set to false. |
| POST | / | Creates a new custom endpoint and associates it with an Amazon Neptune DB cluster. |
| POST | / | Creates a new DB cluster parameter group. Parameters in a DB cluster parameter group apply to all of the instances in a DB cluster.  A DB cluster parameter group is initially created with the default parameters for the database engine used by instances in the DB cluster. To provide custom values for any of the parameters, you must modify the group after creating it using ModifyDBClusterParameterGroup. Once you've created a DB cluster parameter group, you need to associate it with your DB cluster using ModifyDBCluster. When you associate a new DB cluster parameter group with a running DB cluster, you need to reboot the DB instances in the DB cluster without failover for the new DB cluster parameter group and associated settings to take effect.  After you create a DB cluster parameter group, you should wait at least 5 minutes before creating your first DB cluster that uses that DB cluster parameter group as the default parameter group. This allows Amazon Neptune to fully complete the create action before the DB cluster parameter group is used as the default for a new DB cluster. This is especially important for parameters that are critical when creating the default database for a DB cluster, such as the character set for the default database defined by the character_set_database parameter. You can use the Parameter Groups option of the Amazon Neptune console or the DescribeDBClusterParameters command to verify that your DB cluster parameter group has been created or modified. |
| POST | / | Creates a snapshot of a DB cluster. |
| POST | / | Creates a new DB instance. |
| POST | / | Creates a new DB parameter group. A DB parameter group is initially created with the default parameters for the database engine used by the DB instance. To provide custom values for any of the parameters, you must modify the group after creating it using ModifyDBParameterGroup. Once you've created a DB parameter group, you need to associate it with your DB instance using ModifyDBInstance. When you associate a new DB parameter group with a running DB instance, you need to reboot the DB instance without failover for the new DB parameter group and associated settings to take effect.  After you create a DB parameter group, you should wait at least 5 minutes before creating your first DB instance that uses that DB parameter group as the default parameter group. This allows Amazon Neptune to fully complete the create action before the parameter group is used as the default for a new DB instance. This is especially important for parameters that are critical when creating the default database for a DB instance, such as the character set for the default database defined by the character_set_database parameter. You can use the Parameter Groups option of the Amazon Neptune console or the DescribeDBParameters command to verify that your DB parameter group has been created or modified. |
| POST | / | Creates a new DB subnet group. DB subnet groups must contain at least one subnet in at least two AZs in the Amazon Region. |
| POST | / | Creates an event notification subscription. This action requires a topic ARN (Amazon Resource Name) created by either the Neptune console, the SNS console, or the SNS API. To obtain an ARN with SNS, you must create a topic in Amazon SNS and subscribe to the topic. The ARN is displayed in the SNS console. You can specify the type of source (SourceType) you want to be notified of, provide a list of Neptune sources (SourceIds) that triggers the events, and provide a list of event categories (EventCategories) for events you want to be notified of. For example, you can specify SourceType = db-instance, SourceIds = mydbinstance1, mydbinstance2 and EventCategories = Availability, Backup. If you specify both the SourceType and SourceIds, such as SourceType = db-instance and SourceIdentifier = myDBInstance1, you are notified of all the db-instance events for the specified source. If you specify a SourceType but do not specify a SourceIdentifier, you receive notice of the events for that source type for all your Neptune sources. If you do not specify either the SourceType nor the SourceIdentifier, you are notified of events generated from all Neptune sources belonging to your customer account. |
| POST | / | Creates a Neptune global database spread across multiple Amazon Regions. The global database contains a single primary cluster with read-write capability, and read-only secondary clusters that receive data from the primary cluster through high-speed replication performed by the Neptune storage subsystem. You can create a global database that is initially empty, and then add a primary cluster and secondary clusters to it, or you can specify an existing Neptune cluster during the create operation to become the primary cluster of the global database. |
| POST | / | The DeleteDBCluster action deletes a previously provisioned DB cluster. When you delete a DB cluster, all automated backups for that DB cluster are deleted and can't be recovered. Manual DB cluster snapshots of the specified DB cluster are not deleted. Note that the DB Cluster cannot be deleted if deletion protection is enabled. To delete it, you must first set its DeletionProtection field to False. |
| POST | / | Deletes a custom endpoint and removes it from an Amazon Neptune DB cluster. |
| POST | / | Deletes a specified DB cluster parameter group. The DB cluster parameter group to be deleted can't be associated with any DB clusters. |
| POST | / | Deletes a DB cluster snapshot. If the snapshot is being copied, the copy operation is terminated.  The DB cluster snapshot must be in the available state to be deleted. |
| POST | / | The DeleteDBInstance action deletes a previously provisioned DB instance. When you delete a DB instance, all automated backups for that instance are deleted and can't be recovered. Manual DB snapshots of the DB instance to be deleted by DeleteDBInstance are not deleted.  If you request a final DB snapshot the status of the Amazon Neptune DB instance is deleting until the DB snapshot is created. The API action DescribeDBInstance is used to monitor the status of this operation. The action can't be canceled or reverted once submitted. Note that when a DB instance is in a failure state and has a status of failed, incompatible-restore, or incompatible-network, you can only delete it when the SkipFinalSnapshot parameter is set to true. You can't delete a DB instance if it is the only instance in the DB cluster, or if it has deletion protection enabled. |
| POST | / | Deletes a specified DBParameterGroup. The DBParameterGroup to be deleted can't be associated with any DB instances. |
| POST | / | Deletes a DB subnet group.  The specified database subnet group must not be associated with any DB instances. |
| POST | / | Deletes an event notification subscription. |
| POST | / | Deletes a global database. The primary and all secondary clusters must already be detached or deleted first. |
| POST | / | Returns information about endpoints for an Amazon Neptune DB cluster.  This operation can also return information for Amazon RDS clusters and Amazon DocDB clusters. |
| POST | / | Returns a list of DBClusterParameterGroup descriptions. If a DBClusterParameterGroupName parameter is specified, the list will contain only the description of the specified DB cluster parameter group. |
| POST | / | Returns the detailed parameter list for a particular DB cluster parameter group. |
| POST | / | Returns a list of DB cluster snapshot attribute names and values for a manual DB cluster snapshot. When sharing snapshots with other Amazon accounts, DescribeDBClusterSnapshotAttributes returns the restore attribute and a list of IDs for the Amazon accounts that are authorized to copy or restore the manual DB cluster snapshot. If all is included in the list of values for the restore attribute, then the manual DB cluster snapshot is public and can be copied or restored by all Amazon accounts. To add or remove access for an Amazon account to copy or restore a manual DB cluster snapshot, or to make the manual DB cluster snapshot public or private, use the ModifyDBClusterSnapshotAttribute API action. |
| POST | / | Returns information about DB cluster snapshots. This API action supports pagination. |
| POST | / | Returns information about provisioned DB clusters, and supports pagination.  This operation can also return information for Amazon RDS clusters and Amazon DocDB clusters. |
| POST | / | Returns a list of the available DB engines. |
| POST | / | Returns information about provisioned instances, and supports pagination.  This operation can also return information for Amazon RDS instances and Amazon DocDB instances. |
| POST | / | Returns a list of DBParameterGroup descriptions. If a DBParameterGroupName is specified, the list will contain only the description of the specified DB parameter group. |
| POST | / | Returns the detailed parameter list for a particular DB parameter group. |
| POST | / | Returns a list of DBSubnetGroup descriptions. If a DBSubnetGroupName is specified, the list will contain only the descriptions of the specified DBSubnetGroup. For an overview of CIDR ranges, go to the Wikipedia Tutorial. |
| POST | / | Returns the default engine and system parameter information for the cluster database engine. |
| POST | / | Returns the default engine and system parameter information for the specified database engine. |
| POST | / | Displays a list of categories for all event source types, or, if specified, for a specified source type. |
| POST | / | Lists all the subscription descriptions for a customer account. The description for a subscription includes SubscriptionName, SNSTopicARN, CustomerID, SourceType, SourceID, CreationTime, and Status. If you specify a SubscriptionName, lists the description for that subscription. |
| POST | / | Returns events related to DB instances, DB security groups, DB snapshots, and DB parameter groups for the past 14 days. Events specific to a particular DB instance, DB security group, database snapshot, or DB parameter group can be obtained by providing the name as a parameter. By default, the past hour of events are returned. |
| POST | / | Returns information about Neptune global database clusters. This API supports pagination. |
| POST | / | Returns a list of orderable DB instance options for the specified engine. |
| POST | / | Returns a list of resources (for example, DB instances) that have at least one pending maintenance action. |
| POST | / | You can call DescribeValidDBInstanceModifications to learn what modifications you can make to your DB instance. You can use this information when you call ModifyDBInstance. |
| POST | / | Forces a failover for a DB cluster. A failover for a DB cluster promotes one of the Read Replicas (read-only instances) in the DB cluster to be the primary instance (the cluster writer). Amazon Neptune will automatically fail over to a Read Replica, if one exists, when the primary instance fails. You can force a failover when you want to simulate a failure of a primary instance for testing. Because each instance in a DB cluster has its own endpoint address, you will need to clean up and re-establish any existing connections that use those endpoint addresses when the failover is complete. |
| POST | / | Initiates the failover process for a Neptune global database. A failover for a Neptune global database promotes one of secondary read-only DB clusters to be the primary DB cluster and demotes the primary DB cluster to being a secondary (read-only) DB cluster. In other words, the role of the current primary DB cluster and the selected target secondary DB cluster are switched. The selected secondary DB cluster assumes full read/write capabilities for the Neptune global database.  This action applies only to Neptune global databases. This action is only intended for use on healthy Neptune global databases with healthy Neptune DB clusters and no region-wide outages, to test disaster recovery scenarios or to reconfigure the global database topology. |
| POST | / | Lists all tags on an Amazon Neptune resource. |
| POST | / | Modify a setting for a DB cluster. You can change one or more database configuration parameters by specifying these parameters and the new values in the request. |
| POST | / | Modifies the properties of an endpoint in an Amazon Neptune DB cluster. |
| POST | / | Modifies the parameters of a DB cluster parameter group. To modify more than one parameter, submit a list of the following: ParameterName, ParameterValue, and ApplyMethod. A maximum of 20 parameters can be modified in a single request.  Changes to dynamic parameters are applied immediately. Changes to static parameters require a reboot without failover to the DB cluster associated with the parameter group before the change can take effect.   After you create a DB cluster parameter group, you should wait at least 5 minutes before creating your first DB cluster that uses that DB cluster parameter group as the default parameter group. This allows Amazon Neptune to fully complete the create action before the parameter group is used as the default for a new DB cluster. This is especially important for parameters that are critical when creating the default database for a DB cluster, such as the character set for the default database defined by the character_set_database parameter. You can use the Parameter Groups option of the Amazon Neptune console or the DescribeDBClusterParameters command to verify that your DB cluster parameter group has been created or modified. |
| POST | / | Adds an attribute and values to, or removes an attribute and values from, a manual DB cluster snapshot. To share a manual DB cluster snapshot with other Amazon accounts, specify restore as the AttributeName and use the ValuesToAdd parameter to add a list of IDs of the Amazon accounts that are authorized to restore the manual DB cluster snapshot. Use the value all to make the manual DB cluster snapshot public, which means that it can be copied or restored by all Amazon accounts. Do not add the all value for any manual DB cluster snapshots that contain private information that you don't want available to all Amazon accounts. If a manual DB cluster snapshot is encrypted, it can be shared, but only by specifying a list of authorized Amazon account IDs for the ValuesToAdd parameter. You can't use all as a value for that parameter in this case. To view which Amazon accounts have access to copy or restore a manual DB cluster snapshot, or whether a manual DB cluster snapshot public or private, use the DescribeDBClusterSnapshotAttributes API action. |
| POST | / | Modifies settings for a DB instance. You can change one or more database configuration parameters by specifying these parameters and the new values in the request. To learn what modifications you can make to your DB instance, call DescribeValidDBInstanceModifications before you call ModifyDBInstance. |
| POST | / | Modifies the parameters of a DB parameter group. To modify more than one parameter, submit a list of the following: ParameterName, ParameterValue, and ApplyMethod. A maximum of 20 parameters can be modified in a single request.  Changes to dynamic parameters are applied immediately. Changes to static parameters require a reboot without failover to the DB instance associated with the parameter group before the change can take effect.   After you modify a DB parameter group, you should wait at least 5 minutes before creating your first DB instance that uses that DB parameter group as the default parameter group. This allows Amazon Neptune to fully complete the modify action before the parameter group is used as the default for a new DB instance. This is especially important for parameters that are critical when creating the default database for a DB instance, such as the character set for the default database defined by the character_set_database parameter. You can use the Parameter Groups option of the Amazon Neptune console or the DescribeDBParameters command to verify that your DB parameter group has been created or modified. |
| POST | / | Modifies an existing DB subnet group. DB subnet groups must contain at least one subnet in at least two AZs in the Amazon Region. |
| POST | / | Modifies an existing event notification subscription. Note that you can't modify the source identifiers using this call; to change source identifiers for a subscription, use the AddSourceIdentifierToSubscription and RemoveSourceIdentifierFromSubscription calls. You can see a list of the event categories for a given SourceType by using the DescribeEventCategories action. |
| POST | / | Modify a setting for an Amazon Neptune global cluster. You can change one or more database configuration parameters by specifying these parameters and their new values in the request. |
| POST | / | Not supported. |
| POST | / | You might need to reboot your DB instance, usually for maintenance reasons. For example, if you make certain modifications, or if you change the DB parameter group associated with the DB instance, you must reboot the instance for the changes to take effect. Rebooting a DB instance restarts the database engine service. Rebooting a DB instance results in a momentary outage, during which the DB instance status is set to rebooting. |
| POST | / | Detaches a Neptune DB cluster from a Neptune global database. A secondary cluster becomes a normal standalone cluster with read-write capability instead of being read-only, and no longer receives data from a the primary cluster. |
| POST | / | Disassociates an Identity and Access Management (IAM) role from a DB cluster. |
| POST | / | Removes a source identifier from an existing event notification subscription. |
| POST | / | Removes metadata tags from an Amazon Neptune resource. |
| POST | / | Modifies the parameters of a DB cluster parameter group to the default value. To reset specific parameters submit a list of the following: ParameterName and ApplyMethod. To reset the entire DB cluster parameter group, specify the DBClusterParameterGroupName and ResetAllParameters parameters.  When resetting the entire group, dynamic parameters are updated immediately and static parameters are set to pending-reboot to take effect on the next DB instance restart or RebootDBInstance request. You must call RebootDBInstance for every DB instance in your DB cluster that you want the updated static parameter to apply to. |
| POST | / | Modifies the parameters of a DB parameter group to the engine/system default value. To reset specific parameters, provide a list of the following: ParameterName and ApplyMethod. To reset the entire DB parameter group, specify the DBParameterGroup name and ResetAllParameters parameters. When resetting the entire group, dynamic parameters are updated immediately and static parameters are set to pending-reboot to take effect on the next DB instance restart or RebootDBInstance request. |
| POST | / | Creates a new DB cluster from a DB snapshot or DB cluster snapshot. If a DB snapshot is specified, the target DB cluster is created from the source DB snapshot with a default configuration and default security group. If a DB cluster snapshot is specified, the target DB cluster is created from the source DB cluster restore point with the same configuration as the original source DB cluster, except that the new DB cluster is created with the default security group. |
| POST | / | Restores a DB cluster to an arbitrary point in time. Users can restore to any point in time before LatestRestorableTime for up to BackupRetentionPeriod days. The target DB cluster is created from the source DB cluster with the same configuration as the original DB cluster, except that the new DB cluster is created with the default DB security group.  This action only restores the DB cluster, not the DB instances for that DB cluster. You must invoke the CreateDBInstance action to create DB instances for the restored DB cluster, specifying the identifier of the restored DB cluster in DBClusterIdentifier. You can create DB instances only after the RestoreDBClusterToPointInTime action has completed and the DB cluster is available. |
| POST | / | Starts an Amazon Neptune DB cluster that was stopped using the Amazon console, the Amazon CLI stop-db-cluster command, or the StopDBCluster API. |
| POST | / | Stops an Amazon Neptune DB cluster. When you stop a DB cluster, Neptune retains the DB cluster's metadata, including its endpoints and DB parameter groups. Neptune also retains the transaction logs so you can do a point-in-time restore if necessary. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new Neptune cluster?" -> POST / (CreateDBCluster: DBClusterIdentifier + Engine required)
- "How do I add a DB instance to my cluster?" -> POST / (CreateDBInstance: DBInstanceIdentifier + DBInstanceClass + Engine + DBClusterIdentifier required)
- "What Neptune clusters do I have?" -> POST / (DescribeDBClusters: all params optional, paginated via Marker/MaxRecords)
- "How do I take a snapshot of my cluster?" -> POST / (CreateDBClusterSnapshot: DBClusterSnapshotIdentifier + DBClusterIdentifier required)
- "How do I restore a cluster from a snapshot?" -> POST / (RestoreDBClusterFromSnapshot: DBClusterIdentifier + SnapshotIdentifier + Engine required)
- "How do I restore a cluster to a specific point in time?" -> POST / (RestoreDBClusterToPointInTime: DBClusterIdentifier + SourceDBClusterIdentifier required, set RestoreToTime or UseLatestRestorableTime)
- "How do I delete a Neptune cluster safely?" -> POST / (DeleteDBCluster: DBClusterIdentifier required; set SkipFinalSnapshot=false and provide FinalDBSnapshotIdentifier)
- "How do I set up event notifications for my cluster?" -> POST / (CreateEventSubscription: SubscriptionName + SnsTopicArn required)
- "How do I enable IAM authentication on an existing cluster?" -> POST / (ModifyDBCluster: DBClusterIdentifier required, EnableIAMDatabaseAuthentication=true)
- "How do I check pending maintenance for my resources?" -> POST / (DescribePendingMaintenanceActions: all params optional, filter by ResourceIdentifier)
- "How do I create a global database for cross-region replication?" -> POST / (CreateGlobalCluster: GlobalClusterIdentifier required, optionally link SourceDBClusterIdentifier)
- "What instance classes are available for Neptune?" -> POST / (DescribeOrderableDBInstanceOptions: Engine required)
- "How do I trigger a failover on my cluster?" -> POST / (FailoverDBCluster: optional DBClusterIdentifier + TargetDBInstanceIdentifier)
- "How do I copy a cluster snapshot to another region?" -> POST / (CopyDBClusterSnapshot: SourceDBClusterSnapshotIdentifier + TargetDBClusterSnapshotIdentifier required, use PreSignedUrl for cross-region)
- "How do I stop and start a Neptune cluster?" -> POST / (StopDBCluster / StartDBCluster: DBClusterIdentifier required)

## Response Tips

- **Describe/List endpoints**: All return paginated results -- check `Marker` in the response; if non-null, pass it back as `Marker` in the next request. Use `MaxRecords` (default 100, max varies) to control page size.
- **Cluster operations**: Responses wrap the cluster in a `DBCluster` object with deeply nested sub-objects (`PendingModifiedValues`, `ServerlessV2ScalingConfiguration`, `VpcSecurityGroups[]`). Always check `Status` for the cluster's current lifecycle state.
- **Instance operations**: The `DBInstance` response nests `Endpoint` (with Address/Port/HostedZoneId), `DBSubnetGroup` (with Subnets[]), and `PendingModifiedValues`. Extract `Endpoint.Address` and `Endpoint.Port` for connection strings.
- **Snapshot operations**: `PercentProgress` (int) indicates copy/create progress; `Status` transitions through `creating` -> `available`. `StorageEncrypted` and `KmsKeyId` confirm encryption state.
- **Global cluster operations**: `GlobalClusterMembers[]` contains the member clusters with their ARNs and `IsWriter` flag to identify the primary.
- **Event subscriptions**: Check `Status` field (e.g., `active`, `creating`, `deleting`) and `Enabled` (bool) separately -- a subscription can exist but be disabled.
- **Parameter groups**: Modify/Reset return only the group name as confirmation, not the full parameter list. Re-describe to verify changes.

## Anomaly Flags

- **DeletionProtection is false**: Surface when describing clusters or instances where `DeletionProtection` is `false` -- the resource can be accidentally deleted.
- **StorageEncrypted is false**: Flag unencrypted clusters and snapshots, especially in production contexts.
- **PendingModifiedValues is non-empty**: A cluster or instance has unapplied changes waiting for the next maintenance window or restart. Surface the specific pending fields.
- **PendingMaintenanceActions detected**: When `DescribePendingMaintenanceActions` returns results, alert the user with action descriptions and deadlines (`AutoAppliedAfterDate`, `ForcedApplyDate`).
- **IAMDatabaseAuthenticationEnabled is false**: Flag clusters using only password auth when IAM auth could strengthen security posture.
- **PubliclyAccessible is true on DB instances**: Warn when instances are exposed to the public internet.
- **BackupRetentionPeriod is 1 (default minimum)**: Low retention means limited point-in-time restore window. Recommend increasing for production workloads.
- **Snapshot shared publicly**: When `DescribeDBClusterSnapshotAttributes` returns `AttributeName=restore` with `all` in values, the snapshot is public.
- **AutoMinorVersionUpgrade is false**: Instance will miss security patches from automatic minor version upgrades.
- **ServerlessV2ScalingConfiguration bounds**: If `MinCapacity` equals `MaxCapacity`, the cluster cannot scale -- effectively fixed capacity running as serverless.

## Playbook

### 1. Provision a New Neptune Cluster with Instances

1. **Create a DB subnet group**: POST / CreateDBSubnetGroup with `DBSubnetGroupName`, `DBSubnetGroupDescription`, and `SubnetIds` spanning at least 2 AZs.
2. **Create a cluster parameter group** (optional): POST / CreateDBClusterParameterGroup with `DBParameterGroupFamily=neptune1.x` and custom description.
3. **Create the cluster**: POST / CreateDBCluster with `DBClusterIdentifier`, `Engine=neptune`, `DBSubnetGroupName`, `StorageEncrypted=true`, `DeletionProtection=true`, and `EnableCloudwatchLogsExports=["audit"]`.
4. **Wait for cluster status `available`**: POST / DescribeDBClusters filtering by `DBClusterIdentifier` until `Status=available`.
5. **Add a writer instance**: POST / CreateDBInstance with `DBClusterIdentifier`, `DBInstanceIdentifier`, `DBInstanceClass=db.r5.large`, `Engine=neptune`.
6. **Add a reader instance**: Repeat step 5 with a different `DBInstanceIdentifier` and optionally set `PromotionTier` to control failover priority.
7. **Verify endpoints**: Extract `Endpoint` (writer) and `ReaderEndpoint` from the DescribeDBClusters response.

### 2. Snapshot and Restore for Disaster Recovery

1. **Create a manual snapshot**: POST / CreateDBClusterSnapshot with `DBClusterIdentifier` and `DBClusterSnapshotIdentifier`.
2. **Monitor progress**: POST / DescribeDBClusterSnapshots until `Status=available` and `PercentProgress=100`.
3. **Copy snapshot cross-region** (optional): POST / CopyDBClusterSnapshot with source/target identifiers and `KmsKeyId` for the destination region.
4. **Restore from snapshot**: POST / RestoreDBClusterFromSnapshot with a new `DBClusterIdentifier`, the `SnapshotIdentifier`, and `Engine=neptune`.
5. **Add instances to restored cluster**: POST / CreateDBInstance targeting the new cluster identifier.
6. **Update application connection strings** to point to the restored cluster's endpoint.

### 3. Set Up Global Database for Cross-Region Reads

1. **Create the global cluster**: POST / CreateGlobalCluster with `GlobalClusterIdentifier` and `SourceDBClusterIdentifier` pointing to the existing primary cluster.
2. **Verify global cluster status**: POST / DescribeGlobalClusters, confirm `Status=available` and the primary appears in `GlobalClusterMembers` with `IsWriter=true`.
3. **Create a secondary cluster** in the target region: POST / CreateDBCluster with `GlobalClusterIdentifier` set, `Engine=neptune`, and target region's subnet group.
4. **Add reader instances** to the secondary cluster in the target region.
5. **Test failover readiness**: POST / FailoverGlobalCluster with `GlobalClusterIdentifier` and `TargetDbClusterIdentifier` pointing to the secondary (only when ready to promote).

### 4. Enable Monitoring and Event Notifications

1. **Create an SNS topic** (outside Neptune API) for notifications.
2. **Create event subscription**: POST / CreateEventSubscription with `SubscriptionName`, `SnsTopicArn`, `SourceType=db-cluster`, and relevant `EventCategories` (e.g., `["failover", "maintenance"]`).
3. **Add source identifiers**: POST / AddSourceIdentifierToSubscription to attach specific cluster identifiers to the subscription.
4. **Enable CloudWatch logs on the cluster**: POST / ModifyDBCluster with `CloudwatchLogsExportConfiguration` setting `EnableLogTypes=["audit", "slowquery"]`.
5. **Verify**: POST / DescribeEventSubscriptions to confirm `Status=active` and `Enabled=true`.

### 5. Safe Cluster Teardown

1. **List instances in the cluster**: POST / DescribeDBInstances, filter by `DBClusterIdentifier`.
2. **Delete all reader instances first**: POST / DeleteDBInstance for each reader (set `SkipFinalSnapshot=true` since the cluster snapshot covers data).
3. **Delete the writer instance**: POST / DeleteDBInstance for the last remaining instance.
4. **Create a final snapshot**: POST / DeleteDBCluster with `SkipFinalSnapshot=false` and `FinalDBSnapshotIdentifier` to capture data before deletion.
5. **Clean up parameter groups and subnet groups**: POST / DeleteDBClusterParameterGroup, DeleteDBParameterGroup, DeleteDBSubnetGroup.
6. **Remove from global cluster first** (if applicable): POST / RemoveFromGlobalCluster before deleting the cluster.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
