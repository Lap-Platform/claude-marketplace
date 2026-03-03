---
name: aws-opsworks
description: "AWS OpsWorks API skill. Use when working with AWS OpsWorks for root. Covers 74 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS OpsWorks
API version: 2013-02-18

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

74 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Assign a registered instance to a layer.   You can assign registered on-premises instances to any layer type.   You can assign registered Amazon EC2 instances only to custom layers.   You cannot use this action with instances that were created with OpsWorks Stacks.    Required Permissions: To use this action, an Identity and Access Management (IAM) user must have a Manage permissions level for the stack or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Assigns one of the stack's registered Amazon EBS volumes to a specified instance. The volume must first be registered with the stack by calling RegisterVolume. After you register the volume, you must call UpdateVolume to specify a mount point before calling AssignVolume. For more information, see Resource Management.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Associates one of the stack's registered Elastic IP addresses with a specified instance. The address must first be registered with the stack by calling RegisterElasticIp. For more information, see Resource Management.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Attaches an Elastic Load Balancing load balancer to a specified layer. OpsWorks Stacks does not support Application Load Balancer. You can only use Classic Load Balancer with OpsWorks Stacks. For more information, see Elastic Load Balancing.  You must create the Elastic Load Balancing instance separately, by using the Elastic Load Balancing console, API, or CLI. For more information, see the Elastic Load Balancing Developer Guide.   Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Creates a clone of a specified stack. For more information, see Clone a Stack. By default, all parameters are set to the values used by the parent stack.  Required Permissions: To use this action, an IAM user must have an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Creates an app for a specified stack. For more information, see Creating Apps.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Runs deployment or stack commands. For more information, see Deploying Apps and Run Stack Commands.  Required Permissions: To use this action, an IAM user must have a Deploy or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Creates an instance in a specified stack. For more information, see Adding an Instance to a Layer.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Creates a layer. For more information, see How to Create a Layer.  You should use CreateLayer for noncustom layer types such as PHP App Server only if the stack does not have an existing layer of that type. A stack can have at most one instance of each noncustom layer; if you attempt to create a second instance, CreateLayer fails. A stack can have an arbitrary number of custom layers, so you can call CreateLayer as many times as you like for that layer type.   Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Creates a new stack. For more information, see Create a New Stack.  Required Permissions: To use this action, an IAM user must have an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Creates a new user profile.  Required Permissions: To use this action, an IAM user must have an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Deletes a specified app.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Deletes a specified instance, which terminates the associated Amazon EC2 instance. You must stop an instance before you can delete it. For more information, see Deleting Instances.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Deletes a specified layer. You must first stop and then delete all associated instances or unassign registered instances. For more information, see How to Delete a Layer.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Deletes a specified stack. You must first delete all instances, layers, and apps or deregister registered instances. For more information, see Shut Down a Stack.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Deletes a user profile.  Required Permissions: To use this action, an IAM user must have an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Deregisters a specified Amazon ECS cluster from a stack. For more information, see  Resource Management.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack or an attached policy that explicitly grants permissions. For more information on user permissions, see https://docs.aws.amazon.com/opsworks/latest/userguide/opsworks-security-users.html. |
| POST | / | Deregisters a specified Elastic IP address. The address can be registered by another stack after it is deregistered. For more information, see Resource Management.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Deregister an instance from OpsWorks Stacks. The instance can be a registered instance (Amazon EC2 or on-premises) or an instance created with OpsWorks. This action removes the instance from the stack and returns it to your control.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Deregisters an Amazon RDS instance.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Deregisters an Amazon EBS volume. The volume can then be registered by another stack. For more information, see Resource Management.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Describes the available OpsWorks Stacks agent versions. You must specify a stack ID or a configuration manager. DescribeAgentVersions returns a list of available agent versions for the specified stack or configuration manager. |
| POST | / | Requests a description of a specified set of apps.  This call accepts only one resource-identifying parameter.   Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Describes the results of specified commands.  This call accepts only one resource-identifying parameter.   Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Requests a description of a specified set of deployments.  This call accepts only one resource-identifying parameter.   Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Describes Amazon ECS clusters that are registered with a stack. If you specify only a stack ID, you can use the MaxResults and NextToken parameters to paginate the response. However, OpsWorks Stacks currently supports only one cluster per layer, so the result set has a maximum of one element.  Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack or an attached policy that explicitly grants permission. For more information about user permissions, see Managing User Permissions. This call accepts only one resource-identifying parameter. |
| POST | / | Describes Elastic IP addresses.  This call accepts only one resource-identifying parameter.   Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Describes a stack's Elastic Load Balancing instances.  This call accepts only one resource-identifying parameter.   Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Requests a description of a set of instances.  This call accepts only one resource-identifying parameter.   Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Requests a description of one or more layers in a specified stack.  This call accepts only one resource-identifying parameter.   Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Describes load-based auto scaling configurations for specified layers.  You must specify at least one of the parameters.   Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Describes a user's SSH information.  Required Permissions: To use this action, an IAM user must have self-management enabled or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Describes the operating systems that are supported by OpsWorks Stacks. |
| POST | / | Describes the permissions for a specified stack.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Describe an instance's RAID arrays.  This call accepts only one resource-identifying parameter.   Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Describes Amazon RDS instances.  Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. This call accepts only one resource-identifying parameter. |
| POST | / | Describes OpsWorks Stacks service errors.  Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. This call accepts only one resource-identifying parameter. |
| POST | / | Requests a description of a stack's provisioning parameters.  Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Describes the number of layers and apps in a specified stack, and the number of instances in each state, such as running_setup or online.  Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Requests a description of one or more stacks.  Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Describes time-based auto scaling configurations for specified instances.  You must specify at least one of the parameters.   Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Describe specified users.  Required Permissions: To use this action, an IAM user must have an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Describes an instance's Amazon EBS volumes.  This call accepts only one resource-identifying parameter.   Required Permissions: To use this action, an IAM user must have a Show, Deploy, or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Detaches a specified Elastic Load Balancing instance from its layer.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Disassociates an Elastic IP address from its instance. The address remains registered with the stack. For more information, see Resource Management.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Gets a generated host name for the specified layer, based on the current host name theme.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | This action can be used only with Windows stacks.  Grants RDP access to a Windows instance for a specified time period. |
| POST | / | Returns a list of tags that are applied to the specified stack or layer. |
| POST | / | Reboots a specified instance. For more information, see Starting, Stopping, and Rebooting Instances.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Registers a specified Amazon ECS cluster with a stack. You can register only one cluster with a stack. A cluster can be registered with only one stack. For more information, see  Resource Management.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack or an attached policy that explicitly grants permissions. For more information on user permissions, see  Managing User Permissions. |
| POST | / | Registers an Elastic IP address with a specified stack. An address can be registered with only one stack at a time. If the address is already registered, you must first deregister it by calling DeregisterElasticIp. For more information, see Resource Management.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Registers instances that were created outside of OpsWorks Stacks with a specified stack.  We do not recommend using this action to register instances. The complete registration operation includes two tasks: installing the OpsWorks Stacks agent on the instance, and registering the instance with the stack. RegisterInstance handles only the second step. You should instead use the CLI register command, which performs the entire registration operation. For more information, see  Registering an Instance with an OpsWorks Stacks Stack.  Registered instances have the same requirements as instances that are created by using the CreateInstance API. For example, registered instances must be running a supported Linux-based operating system, and they must have a supported instance type. For more information about requirements for instances that you want to register, see  Preparing the Instance.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Registers an Amazon RDS instance with a stack.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Registers an Amazon EBS volume with a specified stack. A volume can be registered with only one stack at a time. If the volume is already registered, you must first deregister it by calling DeregisterVolume. For more information, see Resource Management.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Specify the load-based auto scaling configuration for a specified layer. For more information, see Managing Load with Time-based and Load-based Instances.  To use load-based auto scaling, you must create a set of load-based auto scaling instances. Load-based auto scaling operates only on the instances from that set, so you must ensure that you have created enough instances to handle the maximum anticipated load.   Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Specifies a user's permissions. For more information, see Security and Permissions.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Specify the time-based auto scaling configuration for a specified instance. For more information, see Managing Load with Time-based and Load-based Instances.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Starts a specified instance. For more information, see Starting, Stopping, and Rebooting Instances.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Starts a stack's instances.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Stops a specified instance. When you stop a standard instance, the data disappears and must be reinstalled when you restart the instance. You can stop an Amazon EBS-backed instance without losing data. For more information, see Starting, Stopping, and Rebooting Instances.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Stops a specified stack.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Apply cost-allocation tags to a specified stack or layer in OpsWorks Stacks. For more information about how tagging works, see Tags in the OpsWorks User Guide. |
| POST | / | Unassigns a registered instance from all layers that are using the instance. The instance remains in the stack as an unassigned instance, and can be assigned to another layer as needed. You cannot use this action with instances that were created with OpsWorks Stacks.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Unassigns an assigned Amazon EBS volume. The volume remains registered with the stack. For more information, see Resource Management.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Removes tags from a specified stack or layer. |
| POST | / | Updates a specified app.  Required Permissions: To use this action, an IAM user must have a Deploy or Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Updates a registered Elastic IP address's name. For more information, see Resource Management.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Updates a specified instance.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Updates a specified layer.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Updates a user's SSH public key.  Required Permissions: To use this action, an IAM user must have self-management enabled or an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Updates an Amazon RDS instance.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Updates a specified stack.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |
| POST | / | Updates a specified user profile.  Required Permissions: To use this action, an IAM user must have an attached policy that explicitly grants permissions. For more information about user permissions, see Managing User Permissions. |
| POST | / | Updates an Amazon EBS volume's name or mount point. For more information, see Resource Management.  Required Permissions: To use this action, an IAM user must have a Manage permissions level for the stack, or an attached policy that explicitly grants permissions. For more information on user permissions, see Managing User Permissions. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new OpsWorks stack?" -> POST / (CreateStack: Name, Region, ServiceRoleArn, DefaultInstanceProfileArn required)
- "How do I launch an instance in a layer?" -> POST / (CreateInstance: StackId, LayerIds, InstanceType required)
- "How do I deploy an app to my stack?" -> POST / (CreateDeployment: StackId, Command required; optionally scope with AppId, InstanceIds, LayerIds)
- "What instances are running in my stack?" -> POST / (DescribeInstances: filter by StackId, LayerId, or InstanceIds)
- "How do I clone an existing stack?" -> POST / (CloneStack: SourceStackId, ServiceRoleArn required; toggle ClonePermissions, CloneAppIds)
- "How do I set up auto-scaling for a layer?" -> POST / (SetLoadBasedAutoScaling: LayerId required, Enable, UpScaling, DownScaling thresholds)
- "How do I get SSH access to an instance?" -> POST / (GrantAccess: InstanceId required; returns temporary username/password valid for ValidForInMinutes)
- "How do I register an external instance with my stack?" -> POST / (RegisterInstance: StackId required; provide Hostname, PublicIp, PrivateIp, InstanceIdentity)
- "How do I check what went wrong with a deployment?" -> POST / (DescribeCommands filtered by DeploymentId) then POST / (DescribeServiceErrors filtered by InstanceId or StackId)
- "How do I attach an Elastic IP to an instance?" -> POST / (AssociateElasticIp: ElasticIp required, InstanceId optional) or POST / (RegisterElasticIp: ElasticIp, StackId to register first)
- "How do I add a new layer to my stack?" -> POST / (CreateLayer: StackId, Type, Name, Shortname required)
- "How do I see the summary health of my stack?" -> POST / (DescribeStackSummary: StackId required; returns InstancesCount with per-status breakdowns)
- "How do I manage user permissions on a stack?" -> POST / (SetPermission: StackId, IamUserArn required; AllowSsh, AllowSudo, Level optional)
- "How do I tag my OpsWorks resources?" -> POST / (TagResource: ResourceArn, Tags required) and POST / (ListTags: ResourceArn required with pagination)
- "How do I safely delete a stack and its resources?" -> POST / (StopInstance for each instance) then POST / (DeleteInstance) then POST / (DeleteLayer) then POST / (DeleteApp) then POST / (DeleteStack: StackId)

## Response Tips

- **Describe* endpoints**: All return nullable arrays (e.g., `Instances: [Instance]?`). An empty result means the array is null or empty, not an error. Always nil-check before iterating.
- **Create* endpoints**: Return a single nullable ID string (e.g., `{StackId: str?}`). A null ID after a 200 response is abnormal; treat as a silent failure.
- **DescribeEcsClusters / ListTags**: Only paginated endpoints. Use `NextToken` from the response to fetch additional pages; stop when `NextToken` is null.
- **DescribeStackSummary**: The `InstancesCount` object nests 17 status counters (Online, Stopped, SetupFailed, etc.). Sum relevant fields for aggregate health checks rather than just checking `Online`.
- **GrantAccess**: Returns `TemporaryCredential` with a time-limited password. Cache the `ValidForInMinutes` value and refresh before expiry.
- **Delete/Deregister endpoints**: Return no body on success (void 200). Confirm success by the HTTP status alone.

## Anomaly Flags

- **SetupFailed or StartFailed counts > 0** in DescribeStackSummary: Surface immediately. Instances stuck in failed states need manual intervention.
- **ConnectionLost instances**: DescribeStackSummary showing `ConnectionLost > 0` indicates agent communication failure. Flag for investigation.
- **Deployment with no InstanceIds or LayerIds**: CreateDeployment scoped to whole stack. Warn the user if they omit scoping parameters, as the command runs everywhere.
- **DeleteInstance with DeleteElasticIp/DeleteVolumes = true**: Destructive cascade. Always confirm before issuing with these flags enabled.
- **GrantAccess credentials expiring**: If `ValidForInMinutes` is low (default or explicit), remind the user of the expiry window.
- **StopInstance with Force = true**: Hard stop can cause data loss. Surface a warning before executing.
- **DescribeServiceErrors returning results**: Any non-empty response indicates active problems. Proactively surface error details, especially during or after deployments.
- **CloneStack without ClonePermissions**: The cloned stack won't inherit IAM permissions. Flag if the user likely expects permission parity.
- **Null IDs in Create responses**: A 200 with a null StackId/InstanceId/LayerId is unexpected. Flag as a potential silent failure.

## Playbook

### 1. Provision a Full Stack from Scratch

1. **CreateStack** with Name, Region, ServiceRoleArn, DefaultInstanceProfileArn. Note the returned `StackId`.
2. **CreateLayer** with the StackId, specifying Type (e.g., `custom`, `rails-app`), Name, and Shortname. Note the returned `LayerId`.
3. **CreateApp** with the StackId, app Name, and Type (e.g., `other`, `rails`). Configure AppSource for your code repo. Note the returned `AppId`.
4. **CreateInstance** with the StackId, LayerIds (array with your LayerId), and InstanceType. Note the returned `InstanceId`.
5. **StartInstance** with the InstanceId. Wait for the instance to reach `online` status.
6. **CreateDeployment** with the StackId, AppId, and Command `{Name: "deploy"}` to deploy the app.
7. **DescribeDeployments** to monitor deployment progress until status is `successful`.

### 2. Investigate and Recover from a Failed Deployment

1. **DescribeDeployments** filtered by StackId or DeploymentIds to find the failed deployment and its status.
2. **DescribeCommands** filtered by the DeploymentId to see per-instance command results and exit codes.
3. **DescribeServiceErrors** filtered by StackId to get detailed error messages and timestamps.
4. **DescribeInstances** to check if any instances are in `setup_failed` or `start_failed` state.
5. Fix the root cause (e.g., update app source, fix recipes), then **CreateDeployment** again to re-deploy.

### 3. Set Up Load-Based Auto Scaling for a Layer

1. **DescribeLayers** to confirm the target LayerId and review current configuration.
2. **SetLoadBasedAutoScaling** with the LayerId, `Enable: true`, and configure `UpScaling` thresholds (e.g., CPU > 80% for 5 minutes triggers scale-up) and `DownScaling` thresholds.
3. **CreateInstance** with `AutoScalingType: "load"` to add load-based instances to the layer's pool.
4. **DescribeLoadBasedAutoScaling** with the LayerIds to verify the configuration was applied correctly.

### 4. Grant Temporary SSH Access to an Instance

1. **DescribeInstances** filtered by StackId to find the target instance and confirm it is `online`.
2. **GrantAccess** with the InstanceId and optionally set `ValidForInMinutes` (default varies). Note the returned `TemporaryCredential`.
3. Use the returned `Username` and `Password` to SSH into the instance's public or private IP.
4. Credentials expire automatically after `ValidForInMinutes`. No cleanup needed.

### 5. Safely Tear Down a Stack

1. **DescribeInstances** filtered by StackId to list all instances.
2. **StopInstance** for each running instance. Wait until all reach `stopped` status via repeated DescribeInstances calls.
3. **DeleteInstance** for each instance (set `DeleteElasticIp: true` and `DeleteVolumes: true` only if those resources should be cleaned up).
4. **DescribeApps** filtered by StackId, then **DeleteApp** for each app.
5. **DescribeLayers** filtered by StackId, then **DeleteLayer** for each layer.
6. **DeleteStack** with the StackId. Confirm success by verifying DescribeStacks no longer returns it.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
