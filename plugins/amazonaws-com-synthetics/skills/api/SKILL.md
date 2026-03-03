---
name: synthetics
description: "Synthetics API skill. Use when working with Synthetics for group, canary, canaries. Covers 21 endpoints."
version: 1.0.0
generator: lapsh
---

# Synthetics
API version: 2017-10-11

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /canary/{name} -- verify access
3. POST /canary -- create first canary

## Endpoints

21 endpoints across 7 groups. See references/api-spec.lap for full details.

### group
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /group/{groupIdentifier}/associate | Associates a canary with a group. Using groups can help you with managing and automating your canaries, and you can also view aggregated run results and statistics for all canaries in a group.  You must run this operation in the Region where the canary exists. |
| POST | /group | Creates a group which you can use to associate canaries with each other, including cross-Region canaries. Using groups can help you with managing and automating your canaries, and you can also view aggregated run results and statistics for all canaries in a group.  Groups are global resources. When you create a group, it is replicated across Amazon Web Services Regions, and you can view it and add canaries to it from any Region. Although the group ARN format reflects the Region name where it was created, a group is not constrained to any Region. This means that you can put canaries from multiple Regions into the same group, and then use that group to view and manage all of those canaries in a single view. Groups are supported in all Regions except the Regions that are disabled by default. For more information about these Regions, see Enabling a Region. Each group can contain as many as 10 canaries. You can have as many as 20 groups in your account. Any single canary can be a member of up to 10 groups. |
| DELETE | /group/{groupIdentifier} | Deletes a group. The group doesn't need to be empty to be deleted. If there are canaries in the group, they are not deleted when you delete the group.  Groups are a global resource that appear in all Regions, but the request to delete a group must be made from its home Region. You can find the home Region of a group within its ARN. |
| PATCH | /group/{groupIdentifier}/disassociate | Removes a canary from a group. You must run this operation in the Region where the canary exists. |
| GET | /group/{groupIdentifier} | Returns information about one group. Groups are a global resource, so you can use this operation from any Region. |
| POST | /group/{groupIdentifier}/resources | This operation returns a list of the ARNs of the canaries that are associated with the specified group. |

### canary
| Method | Path | Description |
|--------|------|-------------|
| POST | /canary | Creates a canary. Canaries are scripts that monitor your endpoints and APIs from the outside-in. Canaries help you check the availability and latency of your web services and troubleshoot anomalies by investigating load time data, screenshots of the UI, logs, and metrics. You can set up a canary to run continuously or just once.  Do not use CreateCanary to modify an existing canary. Use UpdateCanary instead. To create canaries, you must have the CloudWatchSyntheticsFullAccess policy. If you are creating a new IAM role for the canary, you also need the iam:CreateRole, iam:CreatePolicy and iam:AttachRolePolicy permissions. For more information, see Necessary Roles and Permissions. Do not include secrets or proprietary information in your canary names. The canary name makes up part of the Amazon Resource Name (ARN) for the canary, and the ARN is included in outbound calls over the internet. For more information, see Security Considerations for Synthetics Canaries. |
| DELETE | /canary/{name} | Permanently deletes the specified canary. If you specify DeleteLambda to true, CloudWatch Synthetics also deletes the Lambda functions and layers that are used by the canary. Other resources used and created by the canary are not automatically deleted. After you delete a canary that you do not intend to use again, you should also delete the following:   The CloudWatch alarms created for this canary. These alarms have a name of Synthetics-SharpDrop-Alarm-MyCanaryName .   Amazon S3 objects and buckets, such as the canary's artifact location.   IAM roles created for the canary. If they were created in the console, these roles have the name  role/service-role/CloudWatchSyntheticsRole-MyCanaryName .   CloudWatch Logs log groups created for the canary. These logs groups have the name /aws/lambda/cwsyn-MyCanaryName .    Before you delete a canary, you might want to use GetCanary to display the information about this canary. Make note of the information returned by this operation so that you can delete these resources after you delete the canary. |
| GET | /canary/{name} | Retrieves complete information about one canary. You must specify the name of the canary that you want. To get a list of canaries and their names, use DescribeCanaries. |
| POST | /canary/{name}/runs | Retrieves a list of runs for a specified canary. |
| POST | /canary/{name}/start | Use this operation to run a canary that has already been created. The frequency of the canary runs is determined by the value of the canary's Schedule. To see a canary's schedule, use GetCanary. |
| POST | /canary/{name}/stop | Stops the canary to prevent all future runs. If the canary is currently running,the run that is in progress completes on its own, publishes metrics, and uploads artifacts, but it is not recorded in Synthetics as a completed run. You can use StartCanary to start it running again with the canary’s current schedule at any point in the future. |
| PATCH | /canary/{name} | Updates the configuration of a canary that has already been created. You can't use this operation to update the tags of an existing canary. To change the tags of an existing canary, use TagResource. |

### canaries
| Method | Path | Description |
|--------|------|-------------|
| POST | /canaries | This operation returns a list of the canaries in your account, along with full details about each canary. This operation supports resource-level authorization using an IAM policy and the Names parameter. If you specify the Names parameter, the operation is successful only if you have authorization to view all the canaries that you specify in your request. If you do not have permission to view any of the canaries, the request fails with a 403 response. You are required to use the Names parameter if you are logged on to a user or role that has an IAM policy that restricts which canaries that you are allowed to view. For more information, see  Limiting a user to viewing specific canaries. |
| POST | /canaries/last-run | Use this operation to see information from the most recent run of each canary that you have created. This operation supports resource-level authorization using an IAM policy and the Names parameter. If you specify the Names parameter, the operation is successful only if you have authorization to view all the canaries that you specify in your request. If you do not have permission to view any of the canaries, the request fails with a 403 response. You are required to use the Names parameter if you are logged on to a user or role that has an IAM policy that restricts which canaries that you are allowed to view. For more information, see  Limiting a user to viewing specific canaries. |

### runtime-versions
| Method | Path | Description |
|--------|------|-------------|
| POST | /runtime-versions | Returns a list of Synthetics canary runtime versions. For more information, see  Canary Runtime Versions. |

### resource
| Method | Path | Description |
|--------|------|-------------|
| POST | /resource/{resourceArn}/groups | Returns a list of the groups that the specified canary is associated with. The canary that you specify must be in the current Region. |

### groups
| Method | Path | Description |
|--------|------|-------------|
| POST | /groups | Returns a list of all groups in the account, displaying their names, unique IDs, and ARNs. The groups from all Regions are returned. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{resourceArn} | Displays the tags associated with a canary or group. |
| POST | /tags/{resourceArn} | Assigns one or more tags (key-value pairs) to the specified canary or group.  Tags can help you organize and categorize your resources. You can also use them to scope user permissions, by granting a user permission to access or change only resources with certain tag values. Tags don't have any semantic meaning to Amazon Web Services and are interpreted strictly as strings of characters. You can use the TagResource action with a resource that already has tags. If you specify a new tag key for the resource, this tag is appended to the list of tags associated with the resource. If you specify a tag key that is already associated with the resource, the new tag value that you specify replaces the previous value for that tag. You can associate as many as 50 tags with a canary or group. |
| DELETE | /tags/{resourceArn} | Removes one or more tags from the specified resource. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new canary?" -> POST /canary
- "How do I delete a canary?" -> DELETE /canary/{name}
- "How do I get details about a specific canary?" -> GET /canary/{name}
- "How do I list all my canaries?" -> POST /canaries
- "How do I check the last run status of my canaries?" -> POST /canaries/last-run
- "How do I see all runs for a specific canary?" -> POST /canary/{name}/runs
- "How do I start a canary?" -> POST /canary/{name}/start
- "How do I stop a running canary?" -> POST /canary/{name}/stop
- "How do I update a canary's schedule or code?" -> PATCH /canary/{name}
- "How do I create a group and add canaries to it?" -> POST /group, then PATCH /group/{groupIdentifier}/associate
- "How do I remove a canary from a group?" -> PATCH /group/{groupIdentifier}/disassociate
- "What runtime versions are available for canaries?" -> POST /runtime-versions
- "Which groups does a specific resource belong to?" -> POST /resource/{resourceArn}/groups
- "How do I tag or untag a canary or group?" -> POST /tags/{resourceArn} or DELETE /tags/{resourceArn}
- "How do I list all resources in a group?" -> POST /group/{groupIdentifier}/resources

## Response Tips

- **Canary objects**: Deeply nested -- Status.State holds the current lifecycle state (CREATING, READY, RUNNING, STOPPED, ERROR, DELETING); Timeline contains timestamps as ISO strings. Always check Status.StateReason when State is ERROR.
- **List endpoints** (canaries, runs, groups, runtime-versions, group resources): All use token-based pagination via `NextToken`/`MaxResults` in the request body. Keep calling with the returned NextToken until it is absent or null.
- **Mutating endpoints** (start, stop, delete, update, associate, disassociate): Return empty 200 on success with no body. Absence of an error response means the operation was accepted.
- **Create endpoints** (POST /canary, POST /group): Return the created object wrapped in a top-level key (`Canary` or `Group`), both nullable -- a null value with a 200 status is unexpected and should be flagged.
- **Tags**: Returned as a flat `map<str,str>`. DELETE /tags requires `tagKeys` as a query-string array, not a body field.

## Anomaly Flags

- **Canary in ERROR or DELETING state**: Surface `Status.StateReason` and `Status.StateReasonCode` immediately when fetching canary details.
- **Deprecated runtime version**: After listing runtime versions, compare the canary's `RuntimeVersion` against available versions. Flag if the canary uses a version no longer in the list.
- **Canary never started**: If `Timeline.LastStarted` is null on a READY canary, the canary was created but never executed -- likely misconfigured or forgotten.
- **Pagination truncation**: If `NextToken` is present in a response but the caller does not paginate, warn that results are incomplete.
- **High failure retention with low success retention**: If `FailureRetentionPeriodInDays` greatly exceeds `SuccessRetentionPeriodInDays`, flag the imbalance as it may inflate storage costs.
- **VPC configuration without security groups**: If `VpcConfig.SubnetIds` is populated but `SecurityGroupIds` is empty, the canary may fail to reach endpoints.

## Playbook

### 1. Create and Launch a Canary

1. `POST /runtime-versions` -- list available runtimes, pick the latest stable version.
2. `POST /canary` -- provide Name, Code (S3 location + handler), ArtifactS3Location, ExecutionRoleArn, Schedule (cron/rate expression), and the chosen RuntimeVersion.
3. Confirm the returned `Canary.Status.State` is CREATING or READY.
4. `POST /canary/{name}/start` -- trigger the first run.
5. `GET /canary/{name}` -- poll until Status.State is RUNNING.

### 2. Investigate a Failing Canary

1. `POST /canaries/last-run` with `Names: ["{canaryName}"]` -- check `LastRun.Status` for the failure state.
2. `GET /canary/{name}` -- read `Status.StateReason` and `Status.StateReasonCode` for error details.
3. `POST /canary/{name}/runs` -- list recent runs to identify when failures began and whether they are intermittent.
4. Check the `ArtifactS3Location` from the canary details -- download logs and screenshots from S3 for root-cause analysis.
5. If needed, `PATCH /canary/{name}` to update code, timeout, or VPC config, then `POST /canary/{name}/start` to retry.

### 3. Organize Canaries into Groups

1. `POST /group` with a descriptive Name (e.g., "production-api-monitors").
2. `PATCH /group/{groupId}/associate` with the `ResourceArn` of each canary to add.
3. `POST /group/{groupId}/resources` -- verify the group membership list.
4. To reorganize, `PATCH /group/{groupId}/disassociate` to remove a canary, then associate it with a different group.

### 4. Audit and Manage Tags Across Resources

1. `POST /canaries` -- list all canaries, collect their ARNs from `EngineArn` or construct from name.
2. `GET /tags/{resourceArn}` for each resource -- collect current tags.
3. `POST /tags/{resourceArn}` -- apply missing or corrected tags.
4. `DELETE /tags/{resourceArn}` with `tagKeys` -- remove stale or incorrect tags.

### 5. Decommission a Canary

1. `POST /canary/{name}/stop` -- stop the canary if it is currently running.
2. `GET /canary/{name}` -- wait for Status.State to reach STOPPED.
3. `POST /resource/{canaryArn}/groups` -- find all groups the canary belongs to.
4. `PATCH /group/{groupId}/disassociate` for each group -- remove the canary from groups.
5. `DELETE /canary/{name}` with `deleteLambda: true` -- delete the canary and its underlying Lambda function.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
