---
name: amazonmq
description: "AmazonMQ API skill. Use when working with AmazonMQ for brokers, configurations, tags. Covers 23 endpoints."
version: 1.0.0
generator: lapsh
---

# AmazonMQ
API version: 2017-11-27

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /v1/broker-engine-types -- verify access
3. POST /v1/brokers -- create first brokers

## Endpoints

23 endpoints across 5 groups. See references/api-spec.lap for full details.

### brokers
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/brokers | Creates a broker. Note: This API is asynchronous. To create a broker, you must either use the AmazonMQFullAccess IAM policy or include the following EC2 permissions in your IAM policy. ec2:CreateNetworkInterface This permission is required to allow Amazon MQ to create an elastic network interface (ENI) on behalf of your account. ec2:CreateNetworkInterfacePermission This permission is required to attach the ENI to the broker instance. ec2:DeleteNetworkInterface ec2:DeleteNetworkInterfacePermission ec2:DetachNetworkInterface ec2:DescribeInternetGateways ec2:DescribeNetworkInterfaces ec2:DescribeNetworkInterfacePermissions ec2:DescribeRouteTables ec2:DescribeSecurityGroups ec2:DescribeSubnets ec2:DescribeVpcs For more information, see Create an IAM User and Get Your Amazon Web Services Credentials and Never Modify or Delete the Amazon MQ Elastic Network Interface in the Amazon MQ Developer Guide. |
| POST | /v1/brokers/{broker-id}/users/{username} | Creates an ActiveMQ user. Do not add personally identifiable information (PII) or other confidential or sensitive information in broker usernames. Broker usernames are accessible to other Amazon Web Services services, including CloudWatch Logs. Broker usernames are not intended to be used for private or sensitive data. |
| DELETE | /v1/brokers/{broker-id} | Deletes a broker. Note: This API is asynchronous. |
| DELETE | /v1/brokers/{broker-id}/users/{username} | Deletes an ActiveMQ user. |
| GET | /v1/brokers/{broker-id} | Returns information about the specified broker. |
| GET | /v1/brokers/{broker-id}/users/{username} | Returns information about an ActiveMQ user. |
| GET | /v1/brokers | Returns a list of all brokers. |
| GET | /v1/brokers/{broker-id}/users | Returns a list of all ActiveMQ users. |
| POST | /v1/brokers/{broker-id}/promote | Promotes a data replication replica broker to the primary broker role. |
| POST | /v1/brokers/{broker-id}/reboot | Reboots a broker. Note: This API is asynchronous. |
| PUT | /v1/brokers/{broker-id} | Adds a pending configuration change to a broker. |
| PUT | /v1/brokers/{broker-id}/users/{username} | Updates the information for an ActiveMQ user. |

### configurations
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/configurations | Creates a new configuration for the specified configuration name. Amazon MQ uses the default configuration (the engine type and version). |
| GET | /v1/configurations/{configuration-id} | Returns information about the specified configuration. |
| GET | /v1/configurations/{configuration-id}/revisions/{configuration-revision} | Returns the specified configuration revision for the specified configuration. |
| GET | /v1/configurations/{configuration-id}/revisions | Returns a list of all revisions for the specified configuration. |
| GET | /v1/configurations | Returns a list of all configurations. |
| PUT | /v1/configurations/{configuration-id} | Updates the specified configuration. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/tags/{resource-arn} | Add a tag to a resource. |
| DELETE | /v1/tags/{resource-arn} | Removes a tag from a resource. |
| GET | /v1/tags/{resource-arn} | Lists tags for a resource. |

### broker-engine-types
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/broker-engine-types | Describe available engine types and versions. |

### broker-instance-options
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/broker-instance-options | Describe available broker instance options. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new message broker?" -> POST /v1/brokers
- "List all my brokers" -> GET /v1/brokers
- "What are the details of a specific broker?" -> GET /v1/brokers/{broker-id}
- "How do I delete a broker?" -> DELETE /v1/brokers/{broker-id}
- "How do I update broker settings like engine version or maintenance window?" -> PUT /v1/brokers/{broker-id}
- "How do I reboot a broker?" -> POST /v1/brokers/{broker-id}/reboot
- "How do I add a user to a broker?" -> POST /v1/brokers/{broker-id}/users/{username}
- "List all users on a broker" -> GET /v1/brokers/{broker-id}/users
- "What instance types and engine versions are available?" -> GET /v1/broker-engine-types
- "What instance options are available for a given engine type?" -> GET /v1/broker-instance-options
- "How do I create a configuration?" -> POST /v1/configurations
- "How do I update a configuration's XML data?" -> PUT /v1/configurations/{configuration-id}
- "How do I view a specific revision of a configuration?" -> GET /v1/configurations/{configuration-id}/revisions/{configuration-revision}
- "How do I tag a broker or configuration?" -> POST /v1/tags/{resource-arn}
- "How do I promote a standby broker in a data replication pair?" -> POST /v1/brokers/{broker-id}/promote

## Response Tips

- **Broker lists and user lists**: Paginated via `NextToken` and `MaxResults` -- keep calling with the returned `NextToken` until it is null.
- **Broker detail** (`GET /v1/brokers/{broker-id}`): Deeply nested; check `Configurations.Pending` and `PendingEngineVersion` for in-flight changes not yet applied. `BrokerState` indicates lifecycle (CREATION_IN_PROGRESS, RUNNING, REBOOT_IN_PROGRESS, DELETION_IN_PROGRESS).
- **Configuration updates** (`PUT /v1/configurations/{configuration-id}`): Response may include a `Warnings` array of `SanitizationWarning` objects -- always surface these to the user.
- **User detail** (`GET .../users/{username}`): The `Pending` object shows queued changes and their `PendingChange` type (CREATE, UPDATE, DELETE) -- changes apply on next reboot.
- **Engine types and instance options**: Both paginated; filter server-side with `engineType`, `hostInstanceType`, and `storageType` query params to reduce pages.
- **Tags**: `GET /v1/tags/{resource-arn}` returns a flat `map<str,str>`; `DELETE` requires `tagKeys` as a query string array, not a body field.
- **All mutating operations** return 200 on success with minimal confirmation fields (often just `BrokerId`); absence of an error body means success.

## Anomaly Flags

- **BrokerState not RUNNING**: Surface immediately if `BrokerState` is `CREATION_FAILED`, `CRITICAL_ACTION_REQUIRED`, or `DELETION_IN_PROGRESS` -- these require user attention.
- **ActionsRequired non-empty**: The `ActionsRequired` array on broker detail signals mandatory actions (e.g., pending maintenance, security patches). Always display these.
- **Pending changes detected**: If `PendingEngineVersion`, `PendingHostInstanceType`, `PendingAuthenticationStrategy`, `PendingSecurityGroups`, or `PendingDataReplicationMode` are set, warn that a reboot is needed to apply changes.
- **SanitizationWarnings on config update**: If `Warnings` is non-empty after updating a configuration, surface each warning -- the broker may reject or alter the submitted XML.
- **Data replication anomalies**: If `DataReplicationMode` and `PendingDataReplicationMode` differ, or `DataReplicationRole` is unexpected, flag a possible replication state mismatch.
- **Pagination truncation**: If `NextToken` is returned but the caller does not paginate, warn that results are incomplete.
- **User pending changes**: If a user's `Pending.PendingChange` is `DELETE`, alert before making further modifications to that user.

## Playbook

### 1. Provision a New Broker End-to-End

1. Call `GET /v1/broker-engine-types` to find supported engine versions for your engine type (e.g., ACTIVEMQ or RABBITMQ).
2. Call `GET /v1/broker-instance-options` with `engineType` to find valid instance types and storage types.
3. Call `POST /v1/configurations` to create a configuration with default XML for your engine type.
4. Call `POST /v1/brokers` with the chosen engine type, version, instance type, configuration ID, deployment mode, at least one user, and network settings (SubnetIds, SecurityGroups, PubliclyAccessible).
5. Poll `GET /v1/brokers/{broker-id}` until `BrokerState` transitions from `CREATION_IN_PROGRESS` to `RUNNING`.
6. Retrieve the `BrokerInstances` array from the detail response to get connection endpoints.

### 2. Update a Broker Configuration and Apply It

1. Call `GET /v1/configurations/{configuration-id}` to get the current configuration details and latest revision number.
2. Call `GET /v1/configurations/{configuration-id}/revisions/{revision}` to retrieve the current XML `Data`.
3. Modify the XML as needed, then call `PUT /v1/configurations/{configuration-id}` with the new `Data` and a `Description`.
4. Check the response for any `Warnings` -- address sanitization issues before proceeding.
5. Call `PUT /v1/brokers/{broker-id}` with `Configuration: {Id, Revision}` pointing to the new revision.
6. Call `POST /v1/brokers/{broker-id}/reboot` to apply the pending configuration change.
7. Poll `GET /v1/brokers/{broker-id}` until `BrokerState` returns to `RUNNING` and `Configurations.Pending` is null.

### 3. Manage Broker Users

1. Call `GET /v1/brokers/{broker-id}/users` to list current users (paginate with `nextToken` if needed).
2. To add a user: call `POST /v1/brokers/{broker-id}/users/{username}` with `Password` and optional `Groups` or `ConsoleAccess`.
3. To modify a user: call `PUT /v1/brokers/{broker-id}/users/{username}` with updated fields.
4. To remove a user: call `DELETE /v1/brokers/{broker-id}/users/{username}`.
5. Verify pending state by calling `GET /v1/brokers/{broker-id}/users/{username}` and checking the `Pending` object.
6. Reboot the broker with `POST /v1/brokers/{broker-id}/reboot` to apply user changes.

### 4. Set Up Data Replication (Active/Standby)

1. Create the primary broker via `POST /v1/brokers` with `DeploymentMode` and `DataReplicationMode` set appropriately.
2. Create the standby broker in a different region, setting `DataReplicationPrimaryBrokerArn` to the primary's ARN.
3. Monitor replication status by checking `DataReplicationMetadata` on both brokers via `GET /v1/brokers/{broker-id}`.
4. If failover is needed, call `POST /v1/brokers/{broker-id}/promote` on the standby broker with the appropriate `Mode`.
5. Verify the promotion completed by checking the updated `DataReplicationRole` on both brokers.

### 5. Audit and Organize Resources with Tags

1. Call `GET /v1/tags/{resource-arn}` to view current tags on a broker or configuration.
2. Call `POST /v1/tags/{resource-arn}` with a `Tags` map to add or overwrite tags (e.g., environment, team, cost-center).
3. To remove specific tags, call `DELETE /v1/tags/{resource-arn}` with `tagKeys` listing the keys to remove.
4. Repeat across all brokers and configurations to enforce a consistent tagging strategy.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
