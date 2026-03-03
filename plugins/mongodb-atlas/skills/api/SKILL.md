---
name: mongodb-atlas-administration-api
description: "MongoDB Atlas Administration API skill. Use when working with MongoDB Atlas Administration for api. Covers 504 endpoints."
version: 1.0.0
generator: lapsh
---

# MongoDB Atlas Administration API
API version: 2.0

## Auth
Bearer digest | OAuth2

## Base URL
https://cloud.mongodb.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /api/atlas/v2 -- verify access
3. POST /api/atlas/v2/federationSettings/{federationSettingsId}/connectedOrgConfigs/{orgId}/roleMappings -- create first roleMappings

## Endpoints

504 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/atlas/v2 | Return the Status of This MongoDB Application |
| GET | /api/atlas/v2/alertConfigs/matchers/fieldNames | Return All Alert Configuration Matchers Field Names |
| GET | /api/atlas/v2/clusters | Return All Authorized Clusters in All Projects |
| GET | /api/atlas/v2/eventTypes | Return All Event Types |
| DELETE | /api/atlas/v2/federationSettings/{federationSettingsId} | Delete One Federation Settings Instance |
| GET | /api/atlas/v2/federationSettings/{federationSettingsId}/connectedOrgConfigs | Return All Organization Configurations from One Federation |
| DELETE | /api/atlas/v2/federationSettings/{federationSettingsId}/connectedOrgConfigs/{orgId} | Remove One Organization Configuration from One Federation |
| GET | /api/atlas/v2/federationSettings/{federationSettingsId}/connectedOrgConfigs/{orgId} | Return One Organization Configuration from One Federation |
| PATCH | /api/atlas/v2/federationSettings/{federationSettingsId}/connectedOrgConfigs/{orgId} | Update One Organization Configuration in One Federation |
| GET | /api/atlas/v2/federationSettings/{federationSettingsId}/connectedOrgConfigs/{orgId}/roleMappings | Return All Role Mappings from One Organization |
| POST | /api/atlas/v2/federationSettings/{federationSettingsId}/connectedOrgConfigs/{orgId}/roleMappings | Create One Role Mapping in One Organization Configuration |
| DELETE | /api/atlas/v2/federationSettings/{federationSettingsId}/connectedOrgConfigs/{orgId}/roleMappings/{id} | Remove One Role Mapping from One Organization |
| GET | /api/atlas/v2/federationSettings/{federationSettingsId}/connectedOrgConfigs/{orgId}/roleMappings/{id} | Return One Role Mapping from One Organization |
| PUT | /api/atlas/v2/federationSettings/{federationSettingsId}/connectedOrgConfigs/{orgId}/roleMappings/{id} | Update One Role Mapping in One Organization |
| GET | /api/atlas/v2/federationSettings/{federationSettingsId}/identityProviders | Return All Identity Providers in One Federation |
| POST | /api/atlas/v2/federationSettings/{federationSettingsId}/identityProviders | Create One Identity Provider |
| DELETE | /api/atlas/v2/federationSettings/{federationSettingsId}/identityProviders/{identityProviderId} | Delete One Identity Provider |
| GET | /api/atlas/v2/federationSettings/{federationSettingsId}/identityProviders/{identityProviderId} | Return One Identity Provider by ID |
| PATCH | /api/atlas/v2/federationSettings/{federationSettingsId}/identityProviders/{identityProviderId} | Update One Identity Provider |
| DELETE | /api/atlas/v2/federationSettings/{federationSettingsId}/identityProviders/{identityProviderId}/jwks | Revoke JWKS from One OIDC Identity Provider |
| GET | /api/atlas/v2/federationSettings/{federationSettingsId}/identityProviders/{identityProviderId}/metadata.xml | Return Metadata of One Identity Provider |
| GET | /api/atlas/v2/groups | Return All Projects |
| POST | /api/atlas/v2/groups | Create One Project |
| DELETE | /api/atlas/v2/groups/{groupId} | Remove One Project |
| GET | /api/atlas/v2/groups/{groupId} | Return One Project |
| PATCH | /api/atlas/v2/groups/{groupId} | Update One Project |
| POST | /api/atlas/v2/groups/{groupId}/access | Add One MongoDB Cloud User to One Project |
| GET | /api/atlas/v2/groups/{groupId}/accessList | Return All Project IP Access List Entries |
| POST | /api/atlas/v2/groups/{groupId}/accessList | Add Entries to Project IP Access List |
| DELETE | /api/atlas/v2/groups/{groupId}/accessList/{entryValue} | Remove One Entry from One Project IP Access List |
| GET | /api/atlas/v2/groups/{groupId}/accessList/{entryValue} | Return One Project IP Access List Entry |
| GET | /api/atlas/v2/groups/{groupId}/accessList/{entryValue}/status | Return Status of One Project IP Access List Entry |
| GET | /api/atlas/v2/groups/{groupId}/activityFeed | Return Pre-Filtered Activity Feed Link for One Project |
| GET | /api/atlas/v2/groups/{groupId}/aiModelApiKeys | Return AI Model API Keys for One Group |
| POST | /api/atlas/v2/groups/{groupId}/aiModelApiKeys | Create New AI Model API Key |
| DELETE | /api/atlas/v2/groups/{groupId}/aiModelApiKeys/{apiKeyId} | Delete Existing AI Model API Key |
| GET | /api/atlas/v2/groups/{groupId}/aiModelApiKeys/{apiKeyId} | Return Single AI Model API Key for One Group |
| PATCH | /api/atlas/v2/groups/{groupId}/aiModelApiKeys/{apiKeyId} | Update Existing AI Model API Key |
| GET | /api/atlas/v2/groups/{groupId}/aiModelRateLimits | Return AI Model Rate Limits for One Group |
| GET | /api/atlas/v2/groups/{groupId}/aiModelRateLimits/{modelGroupName} | Return Single AI Model Rate Limit for One Group |
| PATCH | /api/atlas/v2/groups/{groupId}/aiModelRateLimits/{modelGroupName} | Update AI Model Rate Limit |
| POST | /api/atlas/v2/groups/{groupId}/aiModelRateLimits:reset | Reset AI Model Rate Limits for Group |
| GET | /api/atlas/v2/groups/{groupId}/alertConfigs | Return All Alert Configurations in One Project |
| POST | /api/atlas/v2/groups/{groupId}/alertConfigs | Create One Alert Configuration in One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/alertConfigs/{alertConfigId} | Remove One Alert Configuration from One Project |
| GET | /api/atlas/v2/groups/{groupId}/alertConfigs/{alertConfigId} | Return One Alert Configuration from One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/alertConfigs/{alertConfigId} | Toggle State of One Alert Configuration in One Project |
| PUT | /api/atlas/v2/groups/{groupId}/alertConfigs/{alertConfigId} | Update One Alert Configuration in One Project |
| GET | /api/atlas/v2/groups/{groupId}/alertConfigs/{alertConfigId}/alerts | Return All Open Alerts for One Alert Configuration |
| GET | /api/atlas/v2/groups/{groupId}/alerts | Return All Alerts from One Project |
| GET | /api/atlas/v2/groups/{groupId}/alerts/{alertId} | Return One Alert from One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/alerts/{alertId} | Acknowledge One Alert from One Project |
| GET | /api/atlas/v2/groups/{groupId}/alerts/{alertId}/alertConfigs | Return All Alert Configurations Set for One Alert |
| GET | /api/atlas/v2/groups/{groupId}/apiKeys | Return All Organization API Keys Assigned to One Project |
| POST | /api/atlas/v2/groups/{groupId}/apiKeys | Create and Assign One Organization API Key to One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/apiKeys/{apiUserId} | Unassign One Organization API Key from One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/apiKeys/{apiUserId} | Update Organization API Key Roles for One Project |
| POST | /api/atlas/v2/groups/{groupId}/apiKeys/{apiUserId} | Assign One Organization API Key to One Project |
| GET | /api/atlas/v2/groups/{groupId}/auditLog | Return Auditing Configuration for One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/auditLog | Update Auditing Configuration for One Project |
| GET | /api/atlas/v2/groups/{groupId}/awsCustomDNS | Return One Custom DNS Configuration for Atlas Clusters on AWS |
| PATCH | /api/atlas/v2/groups/{groupId}/awsCustomDNS | Update State of One Custom DNS Configuration for Atlas Clusters on AWS |
| GET | /api/atlas/v2/groups/{groupId}/backup/{cloudProvider}/privateEndpoints | Return Object Storage Private Endpoints for Cloud Backups for One Cloud Provider in One Project |
| POST | /api/atlas/v2/groups/{groupId}/backup/{cloudProvider}/privateEndpoints | Create One Object Storage Private Endpoint for Cloud Backups for One Cloud Provider in One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/backup/{cloudProvider}/privateEndpoints/{endpointId} | Delete One Object Storage Private Endpoint for Cloud Backups for One Cloud Provider from One Project |
| GET | /api/atlas/v2/groups/{groupId}/backup/{cloudProvider}/privateEndpoints/{endpointId} | Return One Object Storage Private Endpoint for Cloud Backups for One Cloud Provider in One Project |
| GET | /api/atlas/v2/groups/{groupId}/backup/exportBuckets | Return All Snapshot Export Buckets |
| POST | /api/atlas/v2/groups/{groupId}/backup/exportBuckets | Create One Snapshot Export Bucket |
| DELETE | /api/atlas/v2/groups/{groupId}/backup/exportBuckets/{exportBucketId} | Delete One Snapshot Export Bucket |
| GET | /api/atlas/v2/groups/{groupId}/backup/exportBuckets/{exportBucketId} | Return One Snapshot Export Bucket |
| PATCH | /api/atlas/v2/groups/{groupId}/backup/exportBuckets/{exportBucketId} | Update One Export Bucket Private Networking Settings |
| DELETE | /api/atlas/v2/groups/{groupId}/backupCompliancePolicy | Disable Backup Compliance Policy Settings |
| GET | /api/atlas/v2/groups/{groupId}/backupCompliancePolicy | Return Backup Compliance Policy Settings |
| PUT | /api/atlas/v2/groups/{groupId}/backupCompliancePolicy | Update Backup Compliance Policy Settings |
| GET | /api/atlas/v2/groups/{groupId}/cloudProviderAccess | Return All Cloud Provider Access Roles |
| POST | /api/atlas/v2/groups/{groupId}/cloudProviderAccess | Create One Cloud Provider Access Role |
| DELETE | /api/atlas/v2/groups/{groupId}/cloudProviderAccess/{cloudProvider}/{roleId} | Deauthorize One Cloud Provider Access Role |
| GET | /api/atlas/v2/groups/{groupId}/cloudProviderAccess/{roleId} | Return One Cloud Provider Access Role |
| PATCH | /api/atlas/v2/groups/{groupId}/cloudProviderAccess/{roleId} | Authorize One Cloud Provider Access Role |
| GET | /api/atlas/v2/groups/{groupId}/clusters | Return All Clusters in One Project |
| POST | /api/atlas/v2/groups/{groupId}/clusters | Create One Cluster in One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName} | Remove One Cluster from One Project |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName} | Return One Cluster from One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName} | Update One Cluster in One Project |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/{clusterView}/{databaseName}/{collectionName}/collStats/measurements | Return Cluster-Level Query Latency |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/{clusterView}/collStats/namespaces | Return Ranked Namespaces from One Cluster |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/autoScalingConfiguration | Return Auto Scaling Configuration for One Sharded Cluster |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/exports | Return All Snapshot Export Jobs |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/exports | Create One Snapshot Export Job |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/exports/{exportId} | Return One Snapshot Export Job |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/restoreJobs | Return All Restore Jobs for One Cluster |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/restoreJobs | Create One Restore Job of One Cluster |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/restoreJobs/{restoreJobId} | Cancel One Restore Job for One Cluster |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/restoreJobs/{restoreJobId} | Return One Restore Job for One Cluster |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/schedule | Remove All Cloud Backup Schedules |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/schedule | Return One Cloud Backup Schedule |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/schedule | Update Cloud Backup Schedule for One Cluster |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/snapshots | Return All Replica Set Cloud Backups |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/snapshots | Take One On-Demand Snapshot |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/snapshots/{snapshotId} | Remove One Replica Set Cloud Backup |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/snapshots/{snapshotId} | Return One Replica Set Cloud Backup |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/snapshots/{snapshotId} | Update Expiration Date for One Cloud Backup |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/snapshots/shardedCluster/{snapshotId} | Remove One Sharded Cluster Cloud Backup |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/snapshots/shardedCluster/{snapshotId} | Return One Sharded Cluster Cloud Backup |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/snapshots/shardedClusters | Return All Sharded Cluster Cloud Backups |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/tenant/download | Download One M2 or M5 Cluster Snapshot |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/tenant/restore | Create One Restore Job for One M2 or M5 Cluster |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/tenant/restores | Return All Restore Jobs for One M2 or M5 Cluster |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/tenant/restores/{restoreId} | Return One Restore Job for One M2 or M5 Cluster |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/tenant/snapshots | Return All Snapshots for One M2 or M5 Cluster |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/tenant/snapshots/{snapshotId} | Return One Snapshot of One M2 or M5 Cluster |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backupCheckpoints | Return All Legacy Backup Checkpoints |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backupCheckpoints/{checkpointId} | Return One Legacy Backup Checkpoint |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/collStats/pinned | Return Pinned Namespaces |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/collStats/pinned | Add Pinned Namespaces |
| PUT | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/collStats/pinned | Pin Namespaces |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/collStats/unpin | Unpin Namespaces |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/fts/indexes | Create One Atlas Search Index |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/fts/indexes/{databaseName}/{collectionName} | Return All Atlas Search Indexes for One Collection |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/fts/indexes/{indexId} | Remove One Atlas Search Index |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/fts/indexes/{indexId} | Return One Atlas Search Index |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/fts/indexes/{indexId} | Update One Atlas Search Index |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/globalWrites | Return One Managed Namespace in One Global Cluster |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/globalWrites/customZoneMapping | Remove All Custom Zone Mappings from One Global Cluster |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/globalWrites/customZoneMapping | Add One Custom Zone Mapping to One Global Cluster |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/globalWrites/managedNamespaces | Remove One Managed Namespace from One Global Cluster |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/globalWrites/managedNamespaces | Create One Managed Namespace in One Global Cluster |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/index | Create One Rolling Index |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/onlineArchives | Return All Online Archives for One Cluster |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/onlineArchives | Create One Online Archive |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/onlineArchives/{archiveId} | Remove One Online Archive |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/onlineArchives/{archiveId} | Return One Online Archive |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/onlineArchives/{archiveId} | Update One Online Archive |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/onlineArchives/queryLogs.gz | Download Online Archive Query Logs |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/outageSimulation | End One Outage Simulation |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/outageSimulation | Return One Outage Simulation |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/outageSimulation | Start One Outage Simulation |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/performanceAdvisor/dropIndexSuggestions | Return All Suggested Indexes to Drop |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/performanceAdvisor/schemaAdvice | Return Schema Advice |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/performanceAdvisor/suggestedIndexes | Return All Suggested Indexes |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/processArgs | Return Advanced Configuration Options for One Cluster |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/processArgs | Update Advanced Configuration Options for One Cluster |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/queryShapeInsights/{queryShapeHash}/details | Return Query Shape Details |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/queryShapeInsights/summaries | Return Query Statistic Summaries |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/queryShapes | Return All Query Shapes |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/queryShapes/{queryShapeHash} | Return One Query Shape |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/queryShapes/{queryShapeHash} | Update Query Shape Rejection Status |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/restartPrimaries | Test Failover for One Cluster |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/restoreJobs | Return All Legacy Backup Restore Jobs |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/restoreJobs | Create One Legacy Backup Restore Job |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/restoreJobs/{jobId} | Return One Legacy Backup Restore Job |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/deployment | Delete Search Nodes |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/deployment | Return All Search Nodes |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/deployment | Update Search Nodes |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/deployment | Create Search Nodes |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/indexes | Return All Atlas Search Indexes for One Cluster |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/indexes | Create One Atlas Search Index |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/indexes/{databaseName}/{collectionName} | Return All Atlas Search Indexes for One Collection |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/indexes/{databaseName}/{collectionName}/{indexName} | Remove One Atlas Search Index by Name |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/indexes/{databaseName}/{collectionName}/{indexName} | Return One Atlas Search Index by Name |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/indexes/{databaseName}/{collectionName}/{indexName} | Update One Atlas Search Index by Name |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/indexes/{indexId} | Remove One Atlas Search Index by ID |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/indexes/{indexId} | Return One Atlas Search Index by ID |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/indexes/{indexId} | Update One Atlas Search Index by ID |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/snapshotSchedule | Return One Snapshot Schedule |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/snapshotSchedule | Update Snapshot Schedule for One Cluster |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/snapshots | Return All Legacy Backup Snapshots |
| DELETE | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/snapshots/{snapshotId} | Remove One Legacy Backup Snapshot |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/snapshots/{snapshotId} | Return One Legacy Backup Snapshot |
| PATCH | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/snapshots/{snapshotId} | Update Expiration Date for One Legacy Backup Snapshot |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/status | Return Status of All Cluster Operations |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}:grantMongoDBEmployeeAccess | Grant MongoDB Employee Cluster Access for One Cluster |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}:pinFeatureCompatibilityVersion | Pin Feature Compatibility Version for One Cluster in One Project |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}:revokeMongoDBEmployeeAccess | Revoke MongoDB Employee Cluster Access for One Cluster |
| POST | /api/atlas/v2/groups/{groupId}/clusters/{clusterName}:unpinFeatureCompatibilityVersion | Unpin Feature Compatibility Version for One Cluster in One Project |
| GET | /api/atlas/v2/groups/{groupId}/clusters/{hostName}/logs/{logName}.gz | Download Logs for One Cluster Host in One Project |
| GET | /api/atlas/v2/groups/{groupId}/clusters/provider/regions | Return All Cloud Provider Regions |
| POST | /api/atlas/v2/groups/{groupId}/clusters/tenantUpgrade | Upgrade One Shared-Tier Cluster |
| POST | /api/atlas/v2/groups/{groupId}/clusters/tenantUpgradeToServerless | Upgrade One Shared-Tier Cluster to One Serverless Instance |
| GET | /api/atlas/v2/groups/{groupId}/collStats/metrics | Return All Metric Names |
| GET | /api/atlas/v2/groups/{groupId}/containers | Return All Network Peering Containers in One Project for One Cloud Provider |
| POST | /api/atlas/v2/groups/{groupId}/containers | Create One Network Peering Container |
| DELETE | /api/atlas/v2/groups/{groupId}/containers/{containerId} | Remove One Network Peering Container |
| GET | /api/atlas/v2/groups/{groupId}/containers/{containerId} | Return One Network Peering Container |
| PATCH | /api/atlas/v2/groups/{groupId}/containers/{containerId} | Update One Network Peering Container |
| GET | /api/atlas/v2/groups/{groupId}/containers/all | Return All Network Peering Containers in One Project |
| GET | /api/atlas/v2/groups/{groupId}/customDBRoles/roles | Return All Custom Roles in One Project |
| POST | /api/atlas/v2/groups/{groupId}/customDBRoles/roles | Create One Custom Role |
| DELETE | /api/atlas/v2/groups/{groupId}/customDBRoles/roles/{roleName} | Remove One Custom Role from One Project |
| GET | /api/atlas/v2/groups/{groupId}/customDBRoles/roles/{roleName} | Return One Custom Role in One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/customDBRoles/roles/{roleName} | Update One Custom Role in One Project |
| GET | /api/atlas/v2/groups/{groupId}/dataFederation | Return All Federated Database Instances in One Project |
| POST | /api/atlas/v2/groups/{groupId}/dataFederation | Create One Federated Database Instance in One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/dataFederation/{tenantName} | Remove One Federated Database Instance from One Project |
| GET | /api/atlas/v2/groups/{groupId}/dataFederation/{tenantName} | Return One Federated Database Instance in One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/dataFederation/{tenantName} | Update One Federated Database Instance in One Project |
| GET | /api/atlas/v2/groups/{groupId}/dataFederation/{tenantName}/limits | Return All Query Limits for One Federated Database Instance |
| DELETE | /api/atlas/v2/groups/{groupId}/dataFederation/{tenantName}/limits/{limitName} | Delete One Query Limit for One Federated Database Instance |
| GET | /api/atlas/v2/groups/{groupId}/dataFederation/{tenantName}/limits/{limitName} | Return One Federated Database Instance Query Limit for One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/dataFederation/{tenantName}/limits/{limitName} | Configure One Query Limit for One Federated Database Instance |
| GET | /api/atlas/v2/groups/{groupId}/dataFederation/{tenantName}/queryLogs.gz | Download Query Logs for One Federated Database Instance |
| GET | /api/atlas/v2/groups/{groupId}/databaseUsers | Return All Database Users in One Project |
| POST | /api/atlas/v2/groups/{groupId}/databaseUsers | Create One Database User in One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/databaseUsers/{databaseName}/{username} | Remove One Database User from One Project |
| GET | /api/atlas/v2/groups/{groupId}/databaseUsers/{databaseName}/{username} | Return One Database User from One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/databaseUsers/{databaseName}/{username} | Update One Database User in One Project |
| GET | /api/atlas/v2/groups/{groupId}/databaseUsers/{username}/certs | Return All X.509 Certificates Assigned to One Database User |
| POST | /api/atlas/v2/groups/{groupId}/databaseUsers/{username}/certs | Create One X.509 Certificate for One Database User |
| GET | /api/atlas/v2/groups/{groupId}/dbAccessHistory/clusters/{clusterName} | Return Database Access History for One Cluster by Cluster Name |
| GET | /api/atlas/v2/groups/{groupId}/dbAccessHistory/processes/{hostname} | Return Database Access History for One Cluster by Hostname |
| GET | /api/atlas/v2/groups/{groupId}/encryptionAtRest | Return One Configuration for Encryption at Rest Using Customer-Managed Keys for One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/encryptionAtRest | Update Encryption at Rest Configuration in One Project |
| GET | /api/atlas/v2/groups/{groupId}/encryptionAtRest/{cloudProvider}/privateEndpoints | Return Private Endpoints for Encryption at Rest Using Customer Key Management for One Cloud Provider in One Project |
| POST | /api/atlas/v2/groups/{groupId}/encryptionAtRest/{cloudProvider}/privateEndpoints | Create One Private Endpoint for Encryption at Rest Using Customer Key Management for One Cloud Provider in One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/encryptionAtRest/{cloudProvider}/privateEndpoints/{endpointId} | Delete One Private Endpoint for Encryption at Rest Using Customer Key Management for One Cloud Provider from One Project |
| GET | /api/atlas/v2/groups/{groupId}/encryptionAtRest/{cloudProvider}/privateEndpoints/{endpointId} | Return One Private Endpoint for Encryption at Rest Using Customer Key Management for One Cloud Provider in One Project |
| GET | /api/atlas/v2/groups/{groupId}/events | Return Events from One Project |
| GET | /api/atlas/v2/groups/{groupId}/events/{eventId} | Return One Event from One Project |
| GET | /api/atlas/v2/groups/{groupId}/flexClusters | Return All Flex Clusters from One Project |
| POST | /api/atlas/v2/groups/{groupId}/flexClusters | Create One Flex Cluster in One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/flexClusters/{name} | Remove One Flex Cluster from One Project |
| GET | /api/atlas/v2/groups/{groupId}/flexClusters/{name} | Return One Flex Cluster from One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/flexClusters/{name} | Update One Flex Cluster in One Project |
| POST | /api/atlas/v2/groups/{groupId}/flexClusters/{name}/backup/download | Download One Flex Cluster Snapshot |
| GET | /api/atlas/v2/groups/{groupId}/flexClusters/{name}/backup/restoreJobs | Return All Restore Jobs for One Flex Cluster |
| POST | /api/atlas/v2/groups/{groupId}/flexClusters/{name}/backup/restoreJobs | Create One Restore Job for One Flex Cluster |
| GET | /api/atlas/v2/groups/{groupId}/flexClusters/{name}/backup/restoreJobs/{restoreJobId} | Return One Restore Job for One Flex Cluster |
| GET | /api/atlas/v2/groups/{groupId}/flexClusters/{name}/backup/snapshots | Return All Snapshots for One Flex Cluster |
| GET | /api/atlas/v2/groups/{groupId}/flexClusters/{name}/backup/snapshots/{snapshotId} | Return One Snapshot for One Flex Cluster |
| POST | /api/atlas/v2/groups/{groupId}/flexClusters:tenantUpgrade | Upgrade One Flex Cluster |
| GET | /api/atlas/v2/groups/{groupId}/hosts/{processId}/fts/metrics | Return All Atlas Search Metric Types for One Process |
| GET | /api/atlas/v2/groups/{groupId}/hosts/{processId}/fts/metrics/indexes/{databaseName}/{collectionName}/{indexName}/measurements | Return Atlas Search Metrics for One Index in One Namespace |
| GET | /api/atlas/v2/groups/{groupId}/hosts/{processId}/fts/metrics/indexes/{databaseName}/{collectionName}/measurements | Return All Atlas Search Index Metrics for One Namespace |
| GET | /api/atlas/v2/groups/{groupId}/hosts/{processId}/fts/metrics/measurements | Return Atlas Search Hardware and Status Metrics |
| GET | /api/atlas/v2/groups/{groupId}/integrations | Return All Active Third-Party Service Integrations |
| DELETE | /api/atlas/v2/groups/{groupId}/integrations/{integrationType} | Remove One Third-Party Service Integration |
| GET | /api/atlas/v2/groups/{groupId}/integrations/{integrationType} | Return One Third-Party Service Integration |
| POST | /api/atlas/v2/groups/{groupId}/integrations/{integrationType} | Create One Third-Party Service Integration |
| PUT | /api/atlas/v2/groups/{groupId}/integrations/{integrationType} | Update One Third-Party Service Integration |
| GET | /api/atlas/v2/groups/{groupId}/invites | Return All Invitations in One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/invites | Update One Invitation in One Project |
| POST | /api/atlas/v2/groups/{groupId}/invites | Create Invitation for One MongoDB Cloud User in One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/invites/{invitationId} | Remove One Invitation from One Project |
| GET | /api/atlas/v2/groups/{groupId}/invites/{invitationId} | Return One Invitation in One Project by Invitation ID |
| PATCH | /api/atlas/v2/groups/{groupId}/invites/{invitationId} | Update One Invitation in One Project by Invitation ID |
| GET | /api/atlas/v2/groups/{groupId}/ipAddresses | Return All IP Addresses for One Project |
| GET | /api/atlas/v2/groups/{groupId}/limits | Return All Limits for One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/limits/{limitName} | Remove One Project Limit |
| GET | /api/atlas/v2/groups/{groupId}/limits/{limitName} | Return One Limit for One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/limits/{limitName} | Set One Project Limit |
| POST | /api/atlas/v2/groups/{groupId}/liveMigrations | Create One Migration for One Local Managed Cluster to MongoDB Atlas |
| GET | /api/atlas/v2/groups/{groupId}/liveMigrations/{liveMigrationId} | Return One Migration Job |
| PUT | /api/atlas/v2/groups/{groupId}/liveMigrations/{liveMigrationId}/cutover | Cut Over One Migrated Cluster |
| POST | /api/atlas/v2/groups/{groupId}/liveMigrations/validate | Validate One Migration Request |
| GET | /api/atlas/v2/groups/{groupId}/liveMigrations/validate/{validationId} | Return One Migration Validation Job |
| GET | /api/atlas/v2/groups/{groupId}/logIntegrations | Return All Active Log Integrations |
| POST | /api/atlas/v2/groups/{groupId}/logIntegrations | Create One Log Integration |
| DELETE | /api/atlas/v2/groups/{groupId}/logIntegrations/{id} | Remove One Log Integration |
| GET | /api/atlas/v2/groups/{groupId}/logIntegrations/{id} | Return One Log Integration |
| PUT | /api/atlas/v2/groups/{groupId}/logIntegrations/{id} | Update One Log Integration |
| DELETE | /api/atlas/v2/groups/{groupId}/maintenanceWindow | Reset One Maintenance Window for One Project |
| GET | /api/atlas/v2/groups/{groupId}/maintenanceWindow | Return One Maintenance Window for One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/maintenanceWindow | Update One Maintenance Window for One Project |
| POST | /api/atlas/v2/groups/{groupId}/maintenanceWindow/autoDefer | Toggle Automatic Deferral of Maintenance for One Project |
| POST | /api/atlas/v2/groups/{groupId}/maintenanceWindow/defer | Defer One Maintenance Window for One Project |
| GET | /api/atlas/v2/groups/{groupId}/managedSlowMs | Return Managed Slow Operation Threshold Status |
| DELETE | /api/atlas/v2/groups/{groupId}/managedSlowMs/disable | Disable Managed Slow Operation Threshold |
| POST | /api/atlas/v2/groups/{groupId}/managedSlowMs/enable | Enable Managed Slow Operation Threshold |
| GET | /api/atlas/v2/groups/{groupId}/mongoDBVersions | Return All Available MongoDB LTS Versions for Clusters in One Project |
| GET | /api/atlas/v2/groups/{groupId}/peers | Return All Network Peering Connections in One Project |
| POST | /api/atlas/v2/groups/{groupId}/peers | Create One Network Peering Connection |
| DELETE | /api/atlas/v2/groups/{groupId}/peers/{peerId} | Remove One Network Peering Connection |
| GET | /api/atlas/v2/groups/{groupId}/peers/{peerId} | Return One Network Peering Connection in One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/peers/{peerId} | Update One Network Peering Connection |
| GET | /api/atlas/v2/groups/{groupId}/pipelines | Return All Data Lake Pipelines in One Project |
| POST | /api/atlas/v2/groups/{groupId}/pipelines | Create One Data Lake Pipeline |
| DELETE | /api/atlas/v2/groups/{groupId}/pipelines/{pipelineName} | Remove One Data Lake Pipeline |
| GET | /api/atlas/v2/groups/{groupId}/pipelines/{pipelineName} | Return One Data Lake Pipeline |
| PATCH | /api/atlas/v2/groups/{groupId}/pipelines/{pipelineName} | Update One Data Lake Pipeline |
| GET | /api/atlas/v2/groups/{groupId}/pipelines/{pipelineName}/availableSchedules | Return All Ingestion Schedules for One Data Lake Pipeline |
| GET | /api/atlas/v2/groups/{groupId}/pipelines/{pipelineName}/availableSnapshots | Return All Backup Snapshots for One Data Lake Pipeline |
| POST | /api/atlas/v2/groups/{groupId}/pipelines/{pipelineName}/pause | Pause One Data Lake Pipeline |
| POST | /api/atlas/v2/groups/{groupId}/pipelines/{pipelineName}/resume | Resume One Data Lake Pipeline |
| GET | /api/atlas/v2/groups/{groupId}/pipelines/{pipelineName}/runs | Return All Data Lake Pipeline Runs in One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/pipelines/{pipelineName}/runs/{pipelineRunId} | Delete One Pipeline Run Dataset |
| GET | /api/atlas/v2/groups/{groupId}/pipelines/{pipelineName}/runs/{pipelineRunId} | Return One Data Lake Pipeline Run |
| POST | /api/atlas/v2/groups/{groupId}/pipelines/{pipelineName}/trigger | Trigger On-Demand Snapshot Ingestion |
| GET | /api/atlas/v2/groups/{groupId}/privateEndpoint/{cloudProvider}/endpointService | Return All Private Endpoint Services for One Provider |
| DELETE | /api/atlas/v2/groups/{groupId}/privateEndpoint/{cloudProvider}/endpointService/{endpointServiceId} | Remove One Private Endpoint Service for One Provider |
| GET | /api/atlas/v2/groups/{groupId}/privateEndpoint/{cloudProvider}/endpointService/{endpointServiceId} | Return One Private Endpoint Service for One Provider |
| POST | /api/atlas/v2/groups/{groupId}/privateEndpoint/{cloudProvider}/endpointService/{endpointServiceId}/endpoint | Create One Private Endpoint for One Provider |
| DELETE | /api/atlas/v2/groups/{groupId}/privateEndpoint/{cloudProvider}/endpointService/{endpointServiceId}/endpoint/{endpointId} | Remove One Private Endpoint for One Provider |
| GET | /api/atlas/v2/groups/{groupId}/privateEndpoint/{cloudProvider}/endpointService/{endpointServiceId}/endpoint/{endpointId} | Return One Private Endpoint for One Provider |
| POST | /api/atlas/v2/groups/{groupId}/privateEndpoint/endpointService | Create One Private Endpoint Service for One Provider |
| GET | /api/atlas/v2/groups/{groupId}/privateEndpoint/regionalMode | Return Regionalized Private Endpoint Status |
| PATCH | /api/atlas/v2/groups/{groupId}/privateEndpoint/regionalMode | Toggle Regionalized Private Endpoint Status |
| GET | /api/atlas/v2/groups/{groupId}/privateEndpoint/serverless/instance/{instanceName}/endpoint | Return All Private Endpoints for One Serverless Instance |
| POST | /api/atlas/v2/groups/{groupId}/privateEndpoint/serverless/instance/{instanceName}/endpoint | Create One Private Endpoint for One Serverless Instance |
| DELETE | /api/atlas/v2/groups/{groupId}/privateEndpoint/serverless/instance/{instanceName}/endpoint/{endpointId} | Remove One Private Endpoint for One Serverless Instance |
| GET | /api/atlas/v2/groups/{groupId}/privateEndpoint/serverless/instance/{instanceName}/endpoint/{endpointId} | Return One Private Endpoint for One Serverless Instance |
| PATCH | /api/atlas/v2/groups/{groupId}/privateEndpoint/serverless/instance/{instanceName}/endpoint/{endpointId} | Update One Private Endpoint for One Serverless Instance |
| GET | /api/atlas/v2/groups/{groupId}/privateIpMode | Verify Connect via Peering-Only Mode for One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/privateIpMode | Disable Connect via Peering-Only Mode for One Project |
| GET | /api/atlas/v2/groups/{groupId}/privateNetworkSettings/endpointIds | Return All Federated Database Instance and Online Archive Private Endpoints in One Project |
| POST | /api/atlas/v2/groups/{groupId}/privateNetworkSettings/endpointIds | Create One Federated Database Instance and Online Archive Private Endpoint for One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/privateNetworkSettings/endpointIds/{endpointId} | Remove One Federated Database Instance and Online Archive Private Endpoint from One Project |
| GET | /api/atlas/v2/groups/{groupId}/privateNetworkSettings/endpointIds/{endpointId} | Return One Federated Database Instance and Online Archive Private Endpoint in One Project |
| GET | /api/atlas/v2/groups/{groupId}/processes | Return All MongoDB Processes in One Project |
| GET | /api/atlas/v2/groups/{groupId}/processes/{processId} | Return One MongoDB Process by ID |
| GET | /api/atlas/v2/groups/{groupId}/processes/{processId}/{databaseName}/{collectionName}/collStats/measurements | Return Host-Level Query Latency |
| GET | /api/atlas/v2/groups/{groupId}/processes/{processId}/collStats/namespaces | Return Ranked Namespaces from One Host |
| GET | /api/atlas/v2/groups/{groupId}/processes/{processId}/databases | Return Available Databases for One MongoDB Process |
| GET | /api/atlas/v2/groups/{groupId}/processes/{processId}/databases/{databaseName} | Return One Database for One MongoDB Process |
| GET | /api/atlas/v2/groups/{groupId}/processes/{processId}/databases/{databaseName}/measurements | Return Measurements for One Database in One MongoDB Process |
| GET | /api/atlas/v2/groups/{groupId}/processes/{processId}/disks | Return Available Disks for One MongoDB Process |
| GET | /api/atlas/v2/groups/{groupId}/processes/{processId}/disks/{partitionName} | Return Measurements for One Disk |
| GET | /api/atlas/v2/groups/{groupId}/processes/{processId}/disks/{partitionName}/measurements | Return Measurements of One Disk for One MongoDB Process |
| GET | /api/atlas/v2/groups/{groupId}/processes/{processId}/measurements | Return Measurements for One MongoDB Process |
| GET | /api/atlas/v2/groups/{groupId}/processes/{processId}/performanceAdvisor/namespaces | Return All Namespaces for One Host |
| GET | /api/atlas/v2/groups/{groupId}/processes/{processId}/performanceAdvisor/slowQueryLogs | Return Slow Queries |
| GET | /api/atlas/v2/groups/{groupId}/processes/{processId}/performanceAdvisor/suggestedIndexes | Return All Suggested Indexes |
| DELETE | /api/atlas/v2/groups/{groupId}/pushBasedLogExport | Disable Push-Based Log Export for One Project |
| GET | /api/atlas/v2/groups/{groupId}/pushBasedLogExport | Return One Push-Based Log Export Configuration in One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/pushBasedLogExport | Update One Push-Based Log Export Configuration in One Project |
| POST | /api/atlas/v2/groups/{groupId}/pushBasedLogExport | Create One Push-Based Log Export Configuration in One Project |
| POST | /api/atlas/v2/groups/{groupId}/sampleDatasetLoad/{name} | Load Sample Dataset into One Cluster |
| GET | /api/atlas/v2/groups/{groupId}/sampleDatasetLoad/{sampleDatasetId} | Return Status of Sample Dataset Load for One Cluster |
| GET | /api/atlas/v2/groups/{groupId}/sandbox/{sandboxConfigId}:generateClusterDescription | Return Cluster Description from Sandbox Template Configuration |
| GET | /api/atlas/v2/groups/{groupId}/serverless | Return All Serverless Instances in One Project |
| POST | /api/atlas/v2/groups/{groupId}/serverless | Create One Serverless Instance in One Project |
| GET | /api/atlas/v2/groups/{groupId}/serverless/{clusterName}/backup/restoreJobs | Return All Restore Jobs for One Serverless Instance |
| POST | /api/atlas/v2/groups/{groupId}/serverless/{clusterName}/backup/restoreJobs | Create One Restore Job for One Serverless Instance |
| GET | /api/atlas/v2/groups/{groupId}/serverless/{clusterName}/backup/restoreJobs/{restoreJobId} | Return One Restore Job for One Serverless Instance |
| GET | /api/atlas/v2/groups/{groupId}/serverless/{clusterName}/backup/snapshots | Return All Snapshots of One Serverless Instance |
| GET | /api/atlas/v2/groups/{groupId}/serverless/{clusterName}/backup/snapshots/{snapshotId} | Return One Snapshot of One Serverless Instance |
| GET | /api/atlas/v2/groups/{groupId}/serverless/{clusterName}/performanceAdvisor/autoIndexing | Return Serverless Auto-Indexing Status |
| POST | /api/atlas/v2/groups/{groupId}/serverless/{clusterName}/performanceAdvisor/autoIndexing | Set Serverless Auto-Indexing Status |
| DELETE | /api/atlas/v2/groups/{groupId}/serverless/{name} | Remove One Serverless Instance from One Project |
| GET | /api/atlas/v2/groups/{groupId}/serverless/{name} | Return One Serverless Instance from One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/serverless/{name} | Update One Serverless Instance in One Project |
| GET | /api/atlas/v2/groups/{groupId}/serviceAccounts | Return All Project Service Accounts |
| POST | /api/atlas/v2/groups/{groupId}/serviceAccounts | Create One Project Service Account |
| DELETE | /api/atlas/v2/groups/{groupId}/serviceAccounts/{clientId} | Remove One Project Service Account |
| GET | /api/atlas/v2/groups/{groupId}/serviceAccounts/{clientId} | Return One Project Service Account |
| PATCH | /api/atlas/v2/groups/{groupId}/serviceAccounts/{clientId} | Update One Project Service Account |
| GET | /api/atlas/v2/groups/{groupId}/serviceAccounts/{clientId}/accessList | Return All Access List Entries for One Project Service Account |
| POST | /api/atlas/v2/groups/{groupId}/serviceAccounts/{clientId}/accessList | Add Access List Entries for One Project Service Account |
| DELETE | /api/atlas/v2/groups/{groupId}/serviceAccounts/{clientId}/accessList/{ipAddress} | Remove One Access List Entry from One Project Service Account |
| POST | /api/atlas/v2/groups/{groupId}/serviceAccounts/{clientId}/secrets | Create One Project Service Account Secret |
| DELETE | /api/atlas/v2/groups/{groupId}/serviceAccounts/{clientId}/secrets/{secretId} | Delete One Project Service Account Secret |
| POST | /api/atlas/v2/groups/{groupId}/serviceAccounts/{clientId}:invite | Assign One Service Account to One Project |
| GET | /api/atlas/v2/groups/{groupId}/settings | Return Project Settings |
| PATCH | /api/atlas/v2/groups/{groupId}/settings | Update Project Settings |
| GET | /api/atlas/v2/groups/{groupId}/standbyLinks | Return All Standby Links for One Project |
| POST | /api/atlas/v2/groups/{groupId}/standbyLinks | Create Standby Link |
| DELETE | /api/atlas/v2/groups/{groupId}/standbyLinks/{standbyLinkId} | Delete Standby Link |
| GET | /api/atlas/v2/groups/{groupId}/standbyLinks/{standbyLinkId} | Return One Standby Link |
| GET | /api/atlas/v2/groups/{groupId}/standbyLinks/{standbyLinkId}/failovers | Return All Standby Link Failovers |
| POST | /api/atlas/v2/groups/{groupId}/standbyLinks/{standbyLinkId}/failovers | Create Standby Link Failover |
| GET | /api/atlas/v2/groups/{groupId}/standbyLinks/{standbyLinkId}/failovers/{failoverId} | Return One Standby Link Failover |
| GET | /api/atlas/v2/groups/{groupId}/streams | Return All Stream Workspaces in One Project |
| POST | /api/atlas/v2/groups/{groupId}/streams | Create One Stream Workspace |
| DELETE | /api/atlas/v2/groups/{groupId}/streams/{tenantName} | Delete One Stream Workspace |
| GET | /api/atlas/v2/groups/{groupId}/streams/{tenantName} | Return One Stream Workspace |
| PATCH | /api/atlas/v2/groups/{groupId}/streams/{tenantName} | Update One Stream Workspace |
| GET | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/auditLogs | Download Audit Logs for One Atlas Stream Processing Workspace |
| GET | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/connections | Return All Connections of the Stream Workspaces |
| POST | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/connections | Create One Stream Connection |
| DELETE | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/connections/{connectionName} | Delete One Stream Connection |
| GET | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/connections/{connectionName} | Return One Stream Connection |
| PATCH | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/connections/{connectionName} | Update One Stream Connection |
| POST | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/processor | Create One Stream Processor |
| DELETE | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/processor/{processorName} | Delete One Stream Processor |
| GET | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/processor/{processorName} | Return One Stream Processor |
| PATCH | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/processor/{processorName} | Update One Stream Processor |
| POST | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/processor/{processorName}:start | Start One Stream Processor |
| POST | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/processor/{processorName}:startWith | Start One Stream Processor With Options |
| POST | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/processor/{processorName}:stop | Stop One Stream Processor |
| GET | /api/atlas/v2/groups/{groupId}/streams/{tenantName}/processors | Return All Stream Processors in One Stream Workspace |
| GET | /api/atlas/v2/groups/{groupId}/streams/{tenantName}:downloadOperationalLogs | Download Operational Logs for One Atlas Stream Processing Workspace |
| GET | /api/atlas/v2/groups/{groupId}/streams/accountDetails | Return Account ID and VPC ID for One Project and Region |
| GET | /api/atlas/v2/groups/{groupId}/streams/activeVpcPeeringConnections | Return All Active Incoming VPC Peering Connections |
| GET | /api/atlas/v2/groups/{groupId}/streams/privateLinkConnections | Return All Private Link Connections |
| POST | /api/atlas/v2/groups/{groupId}/streams/privateLinkConnections | Create One Private Link Connection |
| DELETE | /api/atlas/v2/groups/{groupId}/streams/privateLinkConnections/{connectionId} | Delete One Private Link Connection |
| GET | /api/atlas/v2/groups/{groupId}/streams/privateLinkConnections/{connectionId} | Return One Private Link Connection |
| GET | /api/atlas/v2/groups/{groupId}/streams/vpcPeeringConnections | Return All VPC Peering Connections |
| DELETE | /api/atlas/v2/groups/{groupId}/streams/vpcPeeringConnections/{id} | Delete One VPC Peering Connection |
| POST | /api/atlas/v2/groups/{groupId}/streams/vpcPeeringConnections/{id}:accept | Accept One Incoming VPC Peering Connection |
| POST | /api/atlas/v2/groups/{groupId}/streams/vpcPeeringConnections/{id}:reject | Reject One Incoming VPC Peering Connection |
| POST | /api/atlas/v2/groups/{groupId}/streams:withSampleConnections | Create One Stream Workspace with Sample Connections |
| GET | /api/atlas/v2/groups/{groupId}/teams | Return All Teams in One Project |
| POST | /api/atlas/v2/groups/{groupId}/teams | Add Multiple Teams to One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/teams/{teamId} | Remove One Team from One Project |
| GET | /api/atlas/v2/groups/{groupId}/teams/{teamId} | Return One Team in One Project |
| PATCH | /api/atlas/v2/groups/{groupId}/teams/{teamId} | Update Team Roles in One Project |
| GET | /api/atlas/v2/groups/{groupId}/userSecurity | Return LDAP or X.509 Configuration |
| PATCH | /api/atlas/v2/groups/{groupId}/userSecurity | Update LDAP or X.509 Configuration |
| DELETE | /api/atlas/v2/groups/{groupId}/userSecurity/customerX509 | Disable Customer-Managed X.509 |
| DELETE | /api/atlas/v2/groups/{groupId}/userSecurity/ldap/userToDNMapping | Remove LDAP User to DN Mapping |
| POST | /api/atlas/v2/groups/{groupId}/userSecurity/ldap/verify | Verify LDAP Configuration in One Project |
| GET | /api/atlas/v2/groups/{groupId}/userSecurity/ldap/verify/{requestId} | Return Status of LDAP Configuration Verification in One Project |
| GET | /api/atlas/v2/groups/{groupId}/users | Return All MongoDB Cloud Users in One Project |
| POST | /api/atlas/v2/groups/{groupId}/users | Add One MongoDB Cloud User to One Project |
| DELETE | /api/atlas/v2/groups/{groupId}/users/{userId} | Remove One MongoDB Cloud User from One Project |
| GET | /api/atlas/v2/groups/{groupId}/users/{userId} | Return One MongoDB Cloud User in One Project |
| PUT | /api/atlas/v2/groups/{groupId}/users/{userId}/roles | Update Project Roles for One MongoDB Cloud User |
| POST | /api/atlas/v2/groups/{groupId}/users/{userId}:addRole | Add One Project Role to One MongoDB Cloud User |
| POST | /api/atlas/v2/groups/{groupId}/users/{userId}:removeRole | Remove One Project Role from One MongoDB Cloud User |
| POST | /api/atlas/v2/groups/{groupId}:migrate | Migrate One Project to Another Organization |
| GET | /api/atlas/v2/groups/byName/{groupName} | Return One Project by Name |
| GET | /api/atlas/v2/orgs | Return All Organizations |
| POST | /api/atlas/v2/orgs | Create One Organization |
| DELETE | /api/atlas/v2/orgs/{orgId} | Remove One Organization |
| GET | /api/atlas/v2/orgs/{orgId} | Return One Organization |
| PATCH | /api/atlas/v2/orgs/{orgId} | Update One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/activityFeed | Return Pre-Filtered Activity Feed Link for One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/aiModelApiKeys | Return AI Model API Keys for One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/aiModelApiKeys/{apiKeyId} | Return Single AI Model API Key for One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/aiModelRateLimits | Return AI Model Rate Limits for One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/aiModelRateLimits/{modelGroupName} | Return Single AI Model Rate Limit for One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/apiKeys | Return All Organization API Keys |
| POST | /api/atlas/v2/orgs/{orgId}/apiKeys | Create One Organization API Key |
| DELETE | /api/atlas/v2/orgs/{orgId}/apiKeys/{apiUserId} | Remove One Organization API Key |
| GET | /api/atlas/v2/orgs/{orgId}/apiKeys/{apiUserId} | Return One Organization API Key |
| PATCH | /api/atlas/v2/orgs/{orgId}/apiKeys/{apiUserId} | Update One Organization API Key |
| GET | /api/atlas/v2/orgs/{orgId}/apiKeys/{apiUserId}/accessList | Return All Access List Entries for One Organization API Key |
| POST | /api/atlas/v2/orgs/{orgId}/apiKeys/{apiUserId}/accessList | Create One Access List Entry for One Organization API Key |
| DELETE | /api/atlas/v2/orgs/{orgId}/apiKeys/{apiUserId}/accessList/{ipAddress} | Remove One Access List Entry for One Organization API Key |
| GET | /api/atlas/v2/orgs/{orgId}/apiKeys/{apiUserId}/accessList/{ipAddress} | Return One Access List Entry for One Organization API Key |
| GET | /api/atlas/v2/orgs/{orgId}/associatedInvoices | Return Associated Invoices |
| POST | /api/atlas/v2/orgs/{orgId}/billing/costExplorer/usage | Create One Cost Explorer Query Process |
| GET | /api/atlas/v2/orgs/{orgId}/billing/costExplorer/usage/{token} | Return Usage Details for One Cost Explorer Query |
| GET | /api/atlas/v2/orgs/{orgId}/events | Return Events from One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/events/{eventId} | Return One Event from One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/federationSettings | Return Federation Settings for One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/groups | Return All Projects in One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/invites | Return All Invitations in One Organization |
| PATCH | /api/atlas/v2/orgs/{orgId}/invites | Update One Invitation in One Organization |
| POST | /api/atlas/v2/orgs/{orgId}/invites | Create Invitation for One MongoDB Cloud User in One Organization |
| DELETE | /api/atlas/v2/orgs/{orgId}/invites/{invitationId} | Remove One Invitation from One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/invites/{invitationId} | Return One Invitation in One Organization by Invitation ID |
| PATCH | /api/atlas/v2/orgs/{orgId}/invites/{invitationId} | Update One Invitation in One Organization by Invitation ID |
| GET | /api/atlas/v2/orgs/{orgId}/invoices | Return All Invoices for One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/invoices/{invoiceId} | Return One Invoice for One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/invoices/{invoiceId}/csv | Return One Invoice as CSV for One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/invoices/{invoiceId}/lineItems:search | Return All Line Items for One Invoice by Invoice ID |
| POST | /api/atlas/v2/orgs/{orgId}/invoices/{invoiceId}:generateAndDownloadReport | Generate and Download Invoice Report |
| GET | /api/atlas/v2/orgs/{orgId}/invoices/pending | Return All Pending Invoices for One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/liveMigrations/availableProjects | Return All Projects Available for Migration |
| DELETE | /api/atlas/v2/orgs/{orgId}/liveMigrations/linkTokens | Remove One Link-Token |
| POST | /api/atlas/v2/orgs/{orgId}/liveMigrations/linkTokens | Create One Link-Token |
| GET | /api/atlas/v2/orgs/{orgId}/nonCompliantResources | Return All Non-Compliant Resources |
| GET | /api/atlas/v2/orgs/{orgId}/resourcePolicies | Return All Atlas Resource Policies |
| POST | /api/atlas/v2/orgs/{orgId}/resourcePolicies | Create One Atlas Resource Policy |
| DELETE | /api/atlas/v2/orgs/{orgId}/resourcePolicies/{resourcePolicyId} | Delete One Atlas Resource Policy |
| GET | /api/atlas/v2/orgs/{orgId}/resourcePolicies/{resourcePolicyId} | Return One Atlas Resource Policy |
| PATCH | /api/atlas/v2/orgs/{orgId}/resourcePolicies/{resourcePolicyId} | Update One Atlas Resource Policy |
| POST | /api/atlas/v2/orgs/{orgId}/resourcePolicies:validate | Validate One Atlas Resource Policy |
| GET | /api/atlas/v2/orgs/{orgId}/sandboxConfig | Return Sandbox Configuration IDs for an Organization |
| POST | /api/atlas/v2/orgs/{orgId}/sandboxConfig | Create One Sandbox Configuration for an Organization |
| DELETE | /api/atlas/v2/orgs/{orgId}/sandboxConfig/{sandboxConfigId} | Delete the Default Sandbox Configuration and Disable Sandbox |
| GET | /api/atlas/v2/orgs/{orgId}/sandboxConfig/{sandboxConfigId} | Return Default Sandbox Configuration for One Organization |
| PATCH | /api/atlas/v2/orgs/{orgId}/sandboxConfig/{sandboxConfigId} | Update an Existing Sandbox Configuration |
| GET | /api/atlas/v2/orgs/{orgId}/serviceAccounts | Return All Organization Service Accounts |
| POST | /api/atlas/v2/orgs/{orgId}/serviceAccounts | Create One Organization Service Account |
| DELETE | /api/atlas/v2/orgs/{orgId}/serviceAccounts/{clientId} | Delete One Organization Service Account |
| GET | /api/atlas/v2/orgs/{orgId}/serviceAccounts/{clientId} | Return One Organization Service Account |
| PATCH | /api/atlas/v2/orgs/{orgId}/serviceAccounts/{clientId} | Update One Organization Service Account |
| GET | /api/atlas/v2/orgs/{orgId}/serviceAccounts/{clientId}/accessList | Return All Access List Entries for One Organization Service Account |
| POST | /api/atlas/v2/orgs/{orgId}/serviceAccounts/{clientId}/accessList | Add Access List Entries for One Organization Service Account |
| DELETE | /api/atlas/v2/orgs/{orgId}/serviceAccounts/{clientId}/accessList/{ipAddress} | Remove One Access List Entry from One Organization Service Account |
| GET | /api/atlas/v2/orgs/{orgId}/serviceAccounts/{clientId}/groups | Return All Service Account Project Assignments |
| POST | /api/atlas/v2/orgs/{orgId}/serviceAccounts/{clientId}/secrets | Create One Organization Service Account Secret |
| DELETE | /api/atlas/v2/orgs/{orgId}/serviceAccounts/{clientId}/secrets/{secretId} | Delete One Organization Service Account Secret |
| GET | /api/atlas/v2/orgs/{orgId}/settings | Return Settings for One Organization |
| PATCH | /api/atlas/v2/orgs/{orgId}/settings | Update Settings for One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/teams | Return All Teams in One Organization |
| POST | /api/atlas/v2/orgs/{orgId}/teams | Create One Team in One Organization |
| DELETE | /api/atlas/v2/orgs/{orgId}/teams/{teamId} | Remove One Team from One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/teams/{teamId} | Return One Team by ID |
| PATCH | /api/atlas/v2/orgs/{orgId}/teams/{teamId} | Rename One Team |
| GET | /api/atlas/v2/orgs/{orgId}/teams/{teamId}/users | Return All MongoDB Cloud Users Assigned to One Team |
| POST | /api/atlas/v2/orgs/{orgId}/teams/{teamId}/users | Assign MongoDB Cloud Users in One Organization to One Team |
| DELETE | /api/atlas/v2/orgs/{orgId}/teams/{teamId}/users/{userId} | Remove One MongoDB Cloud User from One Team |
| POST | /api/atlas/v2/orgs/{orgId}/teams/{teamId}:addUser | Add One MongoDB Cloud User to One Team |
| POST | /api/atlas/v2/orgs/{orgId}/teams/{teamId}:removeUser | Remove One MongoDB Cloud User from One Team |
| GET | /api/atlas/v2/orgs/{orgId}/teams/byName/{teamName} | Return One Team by Name |
| GET | /api/atlas/v2/orgs/{orgId}/users | Return All MongoDB Cloud Users in One Organization |
| POST | /api/atlas/v2/orgs/{orgId}/users | Add One MongoDB Cloud User to One Organization |
| DELETE | /api/atlas/v2/orgs/{orgId}/users/{userId} | Remove One MongoDB Cloud User from One Organization |
| GET | /api/atlas/v2/orgs/{orgId}/users/{userId} | Return One MongoDB Cloud User in One Organization |
| PATCH | /api/atlas/v2/orgs/{orgId}/users/{userId} | Update One MongoDB Cloud User in One Organization |
| PUT | /api/atlas/v2/orgs/{orgId}/users/{userId}/roles | Update Organization Roles for One MongoDB Cloud User |
| POST | /api/atlas/v2/orgs/{orgId}/users/{userId}:addRole | Add One Organization Role to One MongoDB Cloud User |
| POST | /api/atlas/v2/orgs/{orgId}/users/{userId}:removeRole | Remove One Organization Role from One MongoDB Cloud User |
| GET | /api/atlas/v2/rateLimits | Return All Rate Limits |
| GET | /api/atlas/v2/rateLimits/{endpointSetId} | Return One Rate Limit |
| GET | /api/atlas/v2/skus | Return All Stock Keeping Units |
| GET | /api/atlas/v2/skus/{skuId} | Return One Stock Keeping Unit |
| GET | /api/atlas/v2/unauth/controlPlaneIPAddresses | Return All Control Plane IP Addresses |
| POST | /api/atlas/v2/users | Create One MongoDB Cloud User |
| GET | /api/atlas/v2/users/{userId} | Return One MongoDB Cloud User by ID |
| GET | /api/atlas/v2/users/byName/{userName} | Return One MongoDB Cloud User by Username |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my Atlas clusters?" -> GET /api/atlas/v2/groups/{groupId}/clusters
- "What projects (groups) do I have access to?" -> GET /api/atlas/v2/groups
- "How do I create a new cluster in my project?" -> POST /api/atlas/v2/groups/{groupId}/clusters
- "How do I whitelist an IP address for database access?" -> POST /api/atlas/v2/groups/{groupId}/accessList
- "What alerts are currently open for my project?" -> GET /api/atlas/v2/groups/{groupId}/alerts with status=OPEN
- "How do I add a database user?" -> POST /api/atlas/v2/groups/{groupId}/databaseUsers
- "How do I check the backup snapshots for a cluster?" -> GET /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/snapshots
- "How do I restore a cluster from a snapshot?" -> POST /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/restoreJobs
- "What organizations do I belong to?" -> GET /api/atlas/v2/orgs
- "How do I get performance recommendations for slow queries?" -> GET /api/atlas/v2/groups/{groupId}/processes/{processId}/performanceAdvisor/suggestedIndexes
- "How do I scale or resize my cluster?" -> PATCH /api/atlas/v2/groups/{groupId}/clusters/{clusterName}
- "How do I set up a VPC peering connection?" -> POST /api/atlas/v2/groups/{groupId}/peers
- "What is my current billing invoice?" -> GET /api/atlas/v2/orgs/{orgId}/invoices/pending
- "How do I configure a maintenance window?" -> PATCH /api/atlas/v2/groups/{groupId}/maintenanceWindow
- "How do I set up Atlas Search indexes on a collection?" -> POST /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/search/indexes

## Response Tips

- **Paginated lists** (clusters, users, alerts, snapshots, etc.): Responses include `totalCount`, `results[]`, and `links[]` for next/prev pages. Default is 100 items per page (`itemsPerPage`), page 1. Always check `totalCount` against `results.length` to know if more pages exist.
- **Cluster operations** (create, update, delete): Returns may be 200, 201, or 202 depending on whether the operation is synchronous or asynchronous. A 202 means the operation was accepted but not completed -- poll the cluster status endpoint to track progress.
- **Delete operations**: Most return 204 (no content) on success. Do not attempt to parse a response body.
- **Error responses**: All endpoints share a common error envelope with `errorCode`, `detail`, and `reason` fields. A 409 typically means a conflicting operation is in progress (e.g., cluster is already scaling).
- **Measurements/metrics endpoints**: Responses contain nested `measurements[].dataPoints[]` arrays with timestamp/value pairs. The `granularity` parameter controls resolution.
- **Federation/identity provider endpoints**: Responses may include SAML metadata as XML (the `metadata.xml` endpoint) rather than JSON.
- **Invoice endpoints**: Line items can be deeply nested with per-SKU breakdowns. Use the CSV endpoint for simpler consumption.

## Anomaly Flags

- **429 Too Many Requests**: Every endpoint can return 429. Surface rate limit headers (`Retry-After`) immediately and back off. The `/api/atlas/v2/rateLimits` endpoint can proactively check current limits.
- **402 Payment Required**: Returned by cluster create/upgrade endpoints when billing limits are hit. Flag this as requiring account-level action before retrying.
- **409 Conflict on cluster operations**: Indicates an in-progress modification (scaling, patching, migration). Surface the conflicting state and suggest polling cluster status before retrying.
- **405 Method Not Allowed**: Returned by select endpoints (identity provider PATCH, managed namespace POST, restore job DELETE). Indicates the resource type does not support that operation -- flag as a spec/tier mismatch.
- **503 on Search Index endpoints**: Atlas Search indexes may temporarily return 503 during index builds. Surface this as transient and suggest retry.
- **Cluster deletion with `retainBackups` parameter**: If a user deletes a cluster without explicitly setting `retainBackups=true`, surface a warning that backups will be permanently lost.
- **`overwriteBackupPolicies` defaulting to true**: When updating backup compliance policy, this flag defaults to true, which silently overwrites existing policies. Flag when the user has not explicitly set it.
- **Encryption at rest changes**: PATCH to `/encryptionAtRest` can cause cluster restarts. Proactively warn before execution.
- **Live migration cutover**: The PUT to `liveMigrations/{id}/cutover` is irreversible. Always confirm before proceeding.

## Playbook

### 1. Provision a New Cluster with Network Access

1. List existing projects: GET /api/atlas/v2/groups
2. Create a project if needed: POST /api/atlas/v2/groups (provide `name` and `orgId`)
3. Check available provider regions: GET /api/atlas/v2/groups/{groupId}/clusters/provider/regions
4. Create the cluster: POST /api/atlas/v2/groups/{groupId}/clusters (specify provider, region, instance size, replication)
5. Poll cluster status until IDLE: GET /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/status
6. Add IP access list entry: POST /api/atlas/v2/groups/{groupId}/accessList (CIDR block or IP)
7. Create a database user: POST /api/atlas/v2/groups/{groupId}/databaseUsers (username, password, roles)
8. Retrieve connection string from cluster details: GET /api/atlas/v2/groups/{groupId}/clusters/{clusterName}

### 2. Back Up and Restore a Cluster

1. Check current backup schedule: GET /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/schedule
2. Optionally take an on-demand snapshot: POST /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/snapshots
3. List available snapshots: GET /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/snapshots
4. Identify the target snapshot by ID and timestamp
5. Initiate restore job: POST /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/restoreJobs (specify `snapshotId` and delivery type)
6. Monitor restore progress: GET /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/backup/restoreJobs/{restoreJobId}

### 3. Investigate and Resolve Performance Issues

1. List processes in the project: GET /api/atlas/v2/groups/{groupId}/processes
2. Retrieve slow query logs: GET /api/atlas/v2/groups/{groupId}/processes/{processId}/performanceAdvisor/slowQueryLogs
3. Get suggested indexes: GET /api/atlas/v2/groups/{groupId}/processes/{processId}/performanceAdvisor/suggestedIndexes
4. Check for drop index suggestions: GET /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/performanceAdvisor/dropIndexSuggestions
5. Review collection-level metrics: GET /api/atlas/v2/groups/{groupId}/processes/{processId}/{databaseName}/{collectionName}/collStats/measurements
6. Create recommended index: POST /api/atlas/v2/groups/{groupId}/clusters/{clusterName}/index
7. If needed, scale the cluster: PATCH /api/atlas/v2/groups/{groupId}/clusters/{clusterName}

### 4. Set Up Monitoring Alerts with Third-Party Integration

1. List current alert configurations: GET /api/atlas/v2/groups/{groupId}/alertConfigs
2. Create a new alert config (e.g., disk usage > 80%): POST /api/atlas/v2/groups/{groupId}/alertConfigs
3. Configure a third-party integration: POST /api/atlas/v2/groups/{groupId}/integrations/{integrationType} (e.g., SLACK, PAGER_DUTY, DATADOG)
4. Verify integration is active: GET /api/atlas/v2/groups/{groupId}/integrations/{integrationType}
5. Review active alerts: GET /api/atlas/v2/groups/{groupId}/alerts?status=OPEN
6. Acknowledge or close an alert: PATCH /api/atlas/v2/groups/{groupId}/alerts/{alertId}

### 5. Configure Federation and SSO

1. Get federation settings for your org: GET /api/atlas/v2/orgs/{orgId}/federationSettings
2. List identity providers: GET /api/atlas/v2/federationSettings/{federationSettingsId}/identityProviders
3. Create a new identity provider (SAML/OIDC): POST /api/atlas/v2/federationSettings/{federationSettingsId}/identityProviders
4. Download SAML metadata for SP configuration: GET /api/atlas/v2/federationSettings/{federationSettingsId}/identityProviders/{identityProviderId}/metadata.xml
5. Connect your org to the federation: GET /api/atlas/v2/federationSettings/{federationSettingsId}/connectedOrgConfigs/{orgId} then PATCH to update
6. Set up role mappings: POST /api/atlas/v2/federationSettings/{federationSettingsId}/connectedOrgConfigs/{orgId}/roleMappings
7. Verify the configuration by checking connected org details: GET /api/atlas/v2/federationSettings/{federationSettingsId}/connectedOrgConfigs/{orgId}


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
