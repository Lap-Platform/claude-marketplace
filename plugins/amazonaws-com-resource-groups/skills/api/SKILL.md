---
name: aws-resource-groups
description: "AWS Resource Groups API skill. Use when working with AWS Resource Groups for groups, delete-group, get-account-settings. Covers 18 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Resource Groups
API version: 2017-11-27

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /resources/{Arn}/tags -- verify access
3. POST /groups -- create first groups

## Endpoints

18 endpoints across 15 groups. See references/api-spec.lap for full details.

### groups
| Method | Path | Description |
|--------|------|-------------|
| POST | /groups | Creates a resource group with the specified name and description. You can optionally include either a resource query or a service configuration. For more information about constructing a resource query, see Build queries and groups in Resource Groups in the Resource Groups User Guide. For more information about service-linked groups and service configurations, see Service configurations for Resource Groups.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:CreateGroup |

### delete-group
| Method | Path | Description |
|--------|------|-------------|
| POST | /delete-group | Deletes the specified resource group. Deleting a resource group does not delete any resources that are members of the group; it only deletes the group structure.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:DeleteGroup |

### get-account-settings
| Method | Path | Description |
|--------|------|-------------|
| POST | /get-account-settings | Retrieves the current status of optional features in Resource Groups. |

### get-group
| Method | Path | Description |
|--------|------|-------------|
| POST | /get-group | Returns information about a specified resource group.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:GetGroup |

### get-group-configuration
| Method | Path | Description |
|--------|------|-------------|
| POST | /get-group-configuration | Retrieves the service configuration associated with the specified resource group. For details about the service configuration syntax, see Service configurations for Resource Groups.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:GetGroupConfiguration |

### get-group-query
| Method | Path | Description |
|--------|------|-------------|
| POST | /get-group-query | Retrieves the resource query associated with the specified resource group. For more information about resource queries, see Create a tag-based group in Resource Groups.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:GetGroupQuery |

### resources
| Method | Path | Description |
|--------|------|-------------|
| GET | /resources/{Arn}/tags | Returns a list of tags that are associated with a resource group, specified by an ARN.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:GetTags |
| POST | /resources/search | Returns a list of Amazon Web Services resource identifiers that matches the specified query. The query uses the same format as a resource query in a CreateGroup or UpdateGroupQuery operation.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:SearchResources     cloudformation:DescribeStacks     cloudformation:ListStackResources     tag:GetResources |
| PUT | /resources/{Arn}/tags | Adds tags to a resource group with the specified ARN. Existing tags on a resource group are not changed if they are not specified in the request parameters.  Do not store personally identifiable information (PII) or other confidential or sensitive information in tags. We use tags to provide you with billing and administration services. Tags are not intended to be used for private or sensitive data.   Minimum permissions  To run this command, you must have the following permissions:    resource-groups:Tag |
| PATCH | /resources/{Arn}/tags | Deletes tags from a specified resource group.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:Untag |

### group-resources
| Method | Path | Description |
|--------|------|-------------|
| POST | /group-resources | Adds the specified resources to the specified group.  You can use this operation with only resource groups that are configured with the following types:    AWS::EC2::HostManagement     AWS::EC2::CapacityReservationPool    Other resource group type and resource types aren't currently supported by this operation.   Minimum permissions  To run this command, you must have the following permissions:    resource-groups:GroupResources |

### list-group-resources
| Method | Path | Description |
|--------|------|-------------|
| POST | /list-group-resources | Returns a list of ARNs of the resources that are members of a specified resource group.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:ListGroupResources     cloudformation:DescribeStacks     cloudformation:ListStackResources     tag:GetResources |

### groups-list
| Method | Path | Description |
|--------|------|-------------|
| POST | /groups-list | Returns a list of existing Resource Groups in your account.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:ListGroups |

### put-group-configuration
| Method | Path | Description |
|--------|------|-------------|
| POST | /put-group-configuration | Attaches a service configuration to the specified group. This occurs asynchronously, and can take time to complete. You can use GetGroupConfiguration to check the status of the update.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:PutGroupConfiguration |

### ungroup-resources
| Method | Path | Description |
|--------|------|-------------|
| POST | /ungroup-resources | Removes the specified resources from the specified group. This operation works only with static groups that you populated using the GroupResources operation. It doesn't work with any resource groups that are automatically populated by tag-based or CloudFormation stack-based queries.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:UngroupResources |

### update-account-settings
| Method | Path | Description |
|--------|------|-------------|
| POST | /update-account-settings | Turns on or turns off optional features in Resource Groups. The preceding example shows that the request to turn on group lifecycle events is IN_PROGRESS. You can call the GetAccountSettings operation to check for completion by looking for GroupLifecycleEventsStatus to change to ACTIVE. |

### update-group
| Method | Path | Description |
|--------|------|-------------|
| POST | /update-group | Updates the description for an existing group. You cannot update the name of a resource group.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:UpdateGroup |

### update-group-query
| Method | Path | Description |
|--------|------|-------------|
| POST | /update-group-query | Updates the resource query of a group. For more information about resource queries, see Create a tag-based group in Resource Groups.  Minimum permissions  To run this command, you must have the following permissions:    resource-groups:UpdateGroupQuery |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new resource group?" -> POST /groups
- "How do I delete a resource group?" -> POST /delete-group
- "What resource groups exist in my account?" -> POST /groups-list
- "What resources are in a specific group?" -> POST /list-group-resources
- "How do I add resources to a group?" -> POST /group-resources
- "How do I remove resources from a group?" -> POST /ungroup-resources
- "What tags are on a specific resource?" -> GET /resources/{Arn}/tags
- "How do I tag a resource?" -> PUT /resources/{Arn}/tags
- "How do I remove tags from a resource?" -> PATCH /resources/{Arn}/tags
- "How do I search for resources by query?" -> POST /resources/search
- "What is the configuration of a group?" -> POST /get-group-configuration
- "How do I update a group's resource query?" -> POST /update-group-query
- "How do I change a group's description?" -> POST /update-group
- "Are lifecycle events enabled on my account?" -> POST /get-account-settings
- "How do I enable group lifecycle events?" -> POST /update-account-settings

## Response Tips

- **Group CRUD** (`/groups`, `/get-group`, `/update-group`, `/delete-group`): All return a `Group` object with `GroupArn`, `Name`, and optional `Description`. A missing `Description` means none was set, not an error.
- **Listing & Search** (`/groups-list`, `/list-group-resources`, `/resources/search`): Paginated via `NextToken`/`MaxResults`. Keep calling with the returned `NextToken` until it is absent. Check `QueryErrors` array on resource listings for partial failures.
- **Membership** (`/group-resources`, `/ungroup-resources`): Responses split results into `Succeeded`, `Failed`, and `Pending` arrays. Always inspect `Failed` for partial failures even on 200.
- **Tags** (`GET/PUT/PATCH /resources/{Arn}/tags`): GET and PUT return current tags as a `map<str,str>`. PATCH (untag) returns the keys that were removed, not remaining tags.
- **Configuration** (`/get-group-configuration`, `/put-group-configuration`): `GroupConfiguration` contains both active `Configuration` and `ProposedConfiguration`. Check `Status` and `FailureReason` when proposed config differs from active.
- **Account Settings** (`/get-account-settings`, `/update-account-settings`): `GroupLifecycleEventsStatus` reflects actual state; `GroupLifecycleEventsDesiredStatus` reflects requested state. They may differ during propagation. Check `GroupLifecycleEventsStatusMessage` for details.

## Anomaly Flags

- **Partial membership failures**: When `/group-resources` or `/ungroup-resources` returns items in `Failed` or `Pending`, surface these immediately with the failure reasons -- a 200 status does not mean full success.
- **QueryErrors on resource listings**: `/list-group-resources` and `/resources/search` can return `QueryErrors` alongside valid results, indicating some resource types or regions could not be queried. Flag these as incomplete results.
- **Configuration drift**: When `get-group-configuration` shows a `ProposedConfiguration` that differs from `Configuration` with a non-empty `FailureReason`, surface this as a stuck or failed config update.
- **Lifecycle events propagation lag**: When `GroupLifecycleEventsDesiredStatus` does not match `GroupLifecycleEventsStatus` after `update-account-settings`, flag that the change is still propagating and include the `StatusMessage`.
- **Empty group results**: When `list-group-resources` returns an empty `Resources` array, proactively note that the group may have zero members or the resource query may be misconfigured.

## Playbook

### 1. Create a Tag-Based Resource Group and Verify Members

1. Call `POST /groups` with a `Name`, `Description`, and a `ResourceQuery` of type `TAG_FILTERS_1_0` targeting your desired tags.
2. Note the returned `GroupArn` for subsequent calls.
3. Call `POST /list-group-resources` with the group name to confirm the expected resources were matched.
4. Inspect `QueryErrors` in the response to ensure no resource types failed to resolve.

### 2. Manually Manage Group Membership

1. Call `POST /groups` with only a `Name` (no `ResourceQuery`) to create a manual group.
2. Call `POST /group-resources` with the group identifier and a list of `ResourceArns` to add.
3. Check the `Succeeded`, `Failed`, and `Pending` arrays in the response. Retry or investigate any `Failed` entries.
4. To remove resources later, call `POST /ungroup-resources` with the same group and the ARNs to remove.

### 3. Search and Tag Resources Across the Account

1. Call `POST /resources/search` with a `ResourceQuery` to find resources matching your criteria. Paginate with `NextToken` until all results are collected.
2. For each returned `ResourceIdentifier`, call `GET /resources/{Arn}/tags` to inspect existing tags.
3. Call `PUT /resources/{Arn}/tags` with the desired tags to apply. The response confirms the applied tags.
4. To clean up, call `PATCH /resources/{Arn}/tags` with the `Keys` to remove.

### 4. Update a Group's Query and Configuration

1. Call `POST /get-group-query` with the group name to inspect the current resource query.
2. Call `POST /update-group-query` with the modified `ResourceQuery` to change which resources are matched.
3. Call `POST /put-group-configuration` to apply or update the group's configuration items.
4. Call `POST /get-group-configuration` to verify the update took effect. If `Status` indicates failure, read `FailureReason` and adjust.

### 5. Enable and Monitor Group Lifecycle Events

1. Call `POST /get-account-settings` to check current lifecycle events status.
2. Call `POST /update-account-settings` with `GroupLifecycleEventsDesiredStatus` set to `ACTIVE`.
3. Call `POST /get-account-settings` again to confirm `GroupLifecycleEventsStatus` matches the desired state.
4. If status has not converged, check `GroupLifecycleEventsStatusMessage` for details and retry after a delay.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
