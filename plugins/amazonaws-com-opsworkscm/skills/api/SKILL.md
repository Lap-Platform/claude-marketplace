---
name: aws-opsworks-cm
description: "AWS OpsWorks CM API skill. Use when working with AWS OpsWorks CM for root. Covers 19 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS OpsWorks CM
API version: 2016-11-01

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

19 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Associates a new node with the server. For more information about how to disassociate a node, see DisassociateNode.  On a Chef server: This command is an alternative to knife bootstrap.  Example (Chef): aws opsworks-cm associate-node --server-name MyServer --node-name MyManagedNode --engine-attributes "Name=CHEF_ORGANIZATION,Value=default" "Name=CHEF_NODE_PUBLIC_KEY,Value=public-key-pem"   On a Puppet server, this command is an alternative to the puppet cert sign command that signs a Puppet node CSR.   Example (Puppet): aws opsworks-cm associate-node --server-name MyServer --node-name MyManagedNode --engine-attributes "Name=PUPPET_NODE_CSR,Value=csr-pem"   A node can can only be associated with servers that are in a HEALTHY state. Otherwise, an InvalidStateException is thrown. A ResourceNotFoundException is thrown when the server does not exist. A ValidationException is raised when parameters of the request are not valid. The AssociateNode API call can be integrated into Auto Scaling configurations, AWS Cloudformation templates, or the user data of a server's instance. |
| POST | / | Creates an application-level backup of a server. While the server is in the BACKING_UP state, the server cannot be changed, and no additional backup can be created.   Backups can be created for servers in RUNNING, HEALTHY, and UNHEALTHY states. By default, you can create a maximum of 50 manual backups.   This operation is asynchronous.   A LimitExceededException is thrown when the maximum number of manual backups is reached. An InvalidStateException is thrown when the server is not in any of the following states: RUNNING, HEALTHY, or UNHEALTHY. A ResourceNotFoundException is thrown when the server is not found. A ValidationException is thrown when parameters of the request are not valid. |
| POST | / | Creates and immedately starts a new server. The server is ready to use when it is in the HEALTHY state. By default, you can create a maximum of 10 servers.   This operation is asynchronous.   A LimitExceededException is thrown when you have created the maximum number of servers (10). A ResourceAlreadyExistsException is thrown when a server with the same name already exists in the account. A ResourceNotFoundException is thrown when you specify a backup ID that is not valid or is for a backup that does not exist. A ValidationException is thrown when parameters of the request are not valid.   If you do not specify a security group by adding the SecurityGroupIds parameter, AWS OpsWorks creates a new security group.   Chef Automate: The default security group opens the Chef server to the world on TCP port 443. If a KeyName is present, AWS OpsWorks enables SSH access. SSH is also open to the world on TCP port 22.   Puppet Enterprise: The default security group opens TCP ports 22, 443, 4433, 8140, 8142, 8143, and 8170. If a KeyName is present, AWS OpsWorks enables SSH access. SSH is also open to the world on TCP port 22.  By default, your server is accessible from any IP address. We recommend that you update your security group rules to allow access from known IP addresses and address ranges only. To edit security group rules, open Security Groups in the navigation pane of the EC2 management console.  To specify your own domain for a server, and provide your own self-signed or CA-signed certificate and private key, specify values for CustomDomain, CustomCertificate, and CustomPrivateKey. |
| POST | / | Deletes a backup. You can delete both manual and automated backups. This operation is asynchronous.   An InvalidStateException is thrown when a backup deletion is already in progress. A ResourceNotFoundException is thrown when the backup does not exist. A ValidationException is thrown when parameters of the request are not valid. |
| POST | / | Deletes the server and the underlying AWS CloudFormation stacks (including the server's EC2 instance). When you run this command, the server state is updated to DELETING. After the server is deleted, it is no longer returned by DescribeServer requests. If the AWS CloudFormation stack cannot be deleted, the server cannot be deleted.   This operation is asynchronous.   An InvalidStateException is thrown when a server deletion is already in progress. A ResourceNotFoundException is thrown when the server does not exist. A ValidationException is raised when parameters of the request are not valid. |
| POST | / | Describes your OpsWorks-CM account attributes.   This operation is synchronous. |
| POST | / | Describes backups. The results are ordered by time, with newest backups first. If you do not specify a BackupId or ServerName, the command returns all backups.   This operation is synchronous.   A ResourceNotFoundException is thrown when the backup does not exist. A ValidationException is raised when parameters of the request are not valid. |
| POST | / | Describes events for a specified server. Results are ordered by time, with newest events first.   This operation is synchronous.   A ResourceNotFoundException is thrown when the server does not exist. A ValidationException is raised when parameters of the request are not valid. |
| POST | / | Returns the current status of an existing association or disassociation request.   A ResourceNotFoundException is thrown when no recent association or disassociation request with the specified token is found, or when the server does not exist. A ValidationException is raised when parameters of the request are not valid. |
| POST | / | Lists all configuration management servers that are identified with your account. Only the stored results from Amazon DynamoDB are returned. AWS OpsWorks CM does not query other services.   This operation is synchronous.   A ResourceNotFoundException is thrown when the server does not exist. A ValidationException is raised when parameters of the request are not valid. |
| POST | / | Disassociates a node from an AWS OpsWorks CM server, and removes the node from the server's managed nodes. After a node is disassociated, the node key pair is no longer valid for accessing the configuration manager's API. For more information about how to associate a node, see AssociateNode.  A node can can only be disassociated from a server that is in a HEALTHY state. Otherwise, an InvalidStateException is thrown. A ResourceNotFoundException is thrown when the server does not exist. A ValidationException is raised when parameters of the request are not valid. |
| POST | / | Exports a specified server engine attribute as a base64-encoded string. For example, you can export user data that you can use in EC2 to associate nodes with a server.   This operation is synchronous.   A ValidationException is raised when parameters of the request are not valid. A ResourceNotFoundException is thrown when the server does not exist. An InvalidStateException is thrown when the server is in any of the following states: CREATING, TERMINATED, FAILED or DELETING. |
| POST | / | Returns a list of tags that are applied to the specified AWS OpsWorks for Chef Automate or AWS OpsWorks for Puppet Enterprise servers or backups. |
| POST | / | Restores a backup to a server that is in a CONNECTION_LOST, HEALTHY, RUNNING, UNHEALTHY, or TERMINATED state. When you run RestoreServer, the server's EC2 instance is deleted, and a new EC2 instance is configured. RestoreServer maintains the existing server endpoint, so configuration management of the server's client devices (nodes) should continue to work.  Restoring from a backup is performed by creating a new EC2 instance. If restoration is successful, and the server is in a HEALTHY state, AWS OpsWorks CM switches traffic over to the new instance. After restoration is finished, the old EC2 instance is maintained in a Running or Stopped state, but is eventually terminated.  This operation is asynchronous.   An InvalidStateException is thrown when the server is not in a valid state. A ResourceNotFoundException is thrown when the server does not exist. A ValidationException is raised when parameters of the request are not valid. |
| POST | / | Manually starts server maintenance. This command can be useful if an earlier maintenance attempt failed, and the underlying cause of maintenance failure has been resolved. The server is in an UNDER_MAINTENANCE state while maintenance is in progress.   Maintenance can only be started on servers in HEALTHY and UNHEALTHY states. Otherwise, an InvalidStateException is thrown. A ResourceNotFoundException is thrown when the server does not exist. A ValidationException is raised when parameters of the request are not valid. |
| POST | / | Applies tags to an AWS OpsWorks for Chef Automate or AWS OpsWorks for Puppet Enterprise server, or to server backups. |
| POST | / | Removes specified tags from an AWS OpsWorks-CM server or backup. |
| POST | / | Updates settings for a server.   This operation is synchronous. |
| POST | / | Updates engine-specific attributes on a specified server. The server enters the MODIFYING state when this operation is in progress. Only one update can occur at a time. You can use this command to reset a Chef server's public key (CHEF_PIVOTAL_KEY) or a Puppet server's admin password (PUPPET_ADMIN_PASSWORD).   This operation is asynchronous.   This operation can only be called for servers in HEALTHY or UNHEALTHY states. Otherwise, an InvalidStateException is raised. A ResourceNotFoundException is thrown when the server does not exist. A ValidationException is raised when parameters of the request are not valid. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new Chef or Puppet server?" -> POST / (CreateServer)
- "How do I back up my OpsWorks CM server?" -> POST / (CreateBackup)
- "How do I restore a server from a backup?" -> POST / (RestoreServer)
- "How do I list all my servers?" -> POST / (DescribeServers)
- "How do I get details for a specific server?" -> POST / (DescribeServers with ServerName)
- "How do I delete a server I no longer need?" -> POST / (DeleteServer)
- "How do I register a node with my server?" -> POST / (AssociateNode)
- "How do I remove a node from my server?" -> POST / (DisassociateNode)
- "Is my node association finished yet?" -> POST / (DescribeNodeAssociationStatus)
- "How do I list all backups for a server?" -> POST / (DescribeBackups with ServerName)
- "How do I check what happened on my server recently?" -> POST / (DescribeEvents)
- "How do I change my server's maintenance window?" -> POST / (UpdateServer)
- "How do I export a server engine attribute like a starter kit?" -> POST / (ExportServerEngineAttribute)
- "How do I check my account limits and usage?" -> POST / (DescribeAccountAttributes)
- "How do I tag or untag my OpsWorks CM resources?" -> POST / (TagResource / UntagResource)

## Response Tips

- **Server objects**: Deeply nested -- always check `Server.Status` (`CREATING`, `RUNNING`, `FAILED`, `TERMINATED`) and `Server.MaintenanceStatus` before acting on other fields.
- **Backup objects**: `Backup.Status` drives availability (`IN_PROGRESS`, `OK`, `FAILED`); `S3DataUrl` and `S3LogUrl` are only populated once status is `OK`.
- **Paginated endpoints** (DescribeBackups, DescribeEvents, DescribeServers, ListTagsForResource): Loop while `NextToken` is present in the response; pass it back as `NextToken` in the next request with the same `MaxResults`.
- **Node association**: Returns a `NodeAssociationStatusToken` -- this is an async operation; poll `DescribeNodeAssociationStatus` until the status is `SUCCESS` or `FAILED`.
- **Void responses** (DeleteBackup, DeleteServer, TagResource, UntagResource): Success is indicated by a 200 with an empty or minimal body -- absence of error is the confirmation.

## Anomaly Flags

- **Server status `UNDER_MAINTENANCE` or `MODIFYING`**: Surface immediately -- mutating operations will fail until the server returns to `RUNNING`.
- **`MaintenanceStatus` set to `FAILED`**: Indicates a maintenance run failed; the server may be in a degraded state requiring manual intervention.
- **`StatusReason` populated on a Server object**: Always surface this -- it contains error details that explain non-healthy states.
- **Backup status `FAILED` or `DELETING`**: Alert the user; a failed backup cannot be used for restore, and a deleting backup will soon be unavailable.
- **Account attribute limits approaching**: After calling DescribeAccountAttributes, compare `Used` against `Maximum` for servers and backups; warn when usage exceeds 80%.
- **Node association stuck**: If polling DescribeNodeAssociationStatus returns `IN_PROGRESS` for more than 15 minutes, flag as potentially stuck.
- **Deprecated engine versions**: If `EngineVersion` on a server is older than the latest available, surface a recommendation to update.

## Playbook

### Provision a New Server and Register a Node

1. Call **DescribeAccountAttributes** to verify you have capacity for a new server.
2. Call **CreateServer** with Engine (`Chef` or `Puppet`), ServerName, InstanceProfileArn, InstanceType, and ServiceRoleArn. Optionally set backup and maintenance windows.
3. Poll **DescribeServers** with the ServerName until `Server.Status` is `RUNNING`.
4. Call **ExportServerEngineAttribute** with `ExportAttributeName: "Userdata"` to get the node bootstrap script.
5. Run the bootstrap script on your target node.
6. Call **AssociateNode** with ServerName, NodeName, and EngineAttributes from the bootstrap.
7. Poll **DescribeNodeAssociationStatus** with the returned token until status is `SUCCESS`.

### Backup and Restore a Server

1. Call **CreateBackup** with the ServerName (optionally add a Description).
2. Poll **DescribeBackups** with the returned BackupId until `Backup.Status` is `OK`.
3. When ready to restore, call **RestoreServer** with the BackupId and the target ServerName.
4. Poll **DescribeServers** until the server status returns to `RUNNING`.
5. Verify server health by calling **DescribeEvents** and checking for errors.

### Update Server Maintenance Settings

1. Call **DescribeServers** with ServerName to get current configuration.
2. Call **UpdateServer** with the desired changes (e.g., `PreferredMaintenanceWindow: "Tue:08:00"`, `BackupRetentionCount: 5`).
3. Confirm the returned Server object reflects the new settings.
4. Optionally call **StartMaintenance** to trigger an immediate maintenance run rather than waiting for the window.

### Tag Resources for Cost Tracking

1. Call **DescribeServers** to get the `ServerArn` for your target server.
2. Call **TagResource** with the ResourceArn and your Tags (e.g., `[{Key: "Environment", Value: "Production"}]`).
3. Verify tags by calling **ListTagsForResource** with the same ResourceArn.
4. To remove tags later, call **UntagResource** with the ResourceArn and the TagKeys to remove.

### Decommission a Server

1. Call **DescribeServers** with ServerName to confirm the server exists and check its status.
2. Call **CreateBackup** as a final safety backup before deletion.
3. Poll **DescribeBackups** until the backup status is `OK`.
4. Call **DisassociateNode** for each node registered to the server.
5. Poll **DescribeNodeAssociationStatus** for each disassociation until complete.
6. Call **DeleteServer** with the ServerName.
7. Optionally call **DeleteBackup** to clean up old backups you no longer need.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
