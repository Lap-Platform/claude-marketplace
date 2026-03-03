---
name: aws-resource-access-manager
description: "AWS Resource Access Manager API skill. Use when working with AWS Resource Access Manager for acceptresourceshareinvitation, associateresourceshare, associateresourcesharepermission. Covers 34 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Resource Access Manager
API version: 2018-01-04

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST /acceptresourceshareinvitation -- create first acceptresourceshareinvitation

## Endpoints

34 endpoints across 34 groups. See references/api-spec.lap for full details.

### acceptresourceshareinvitation
| Method | Path | Description |
|--------|------|-------------|
| POST | /acceptresourceshareinvitation | Accepts an invitation to a resource share from another Amazon Web Services account. After you accept the invitation, the resources included in the resource share are available to interact with in the relevant Amazon Web Services Management Consoles and tools. |

### associateresourceshare
| Method | Path | Description |
|--------|------|-------------|
| POST | /associateresourceshare | Adds the specified list of principals and list of resources to a resource share. Principals that already have access to this resource share immediately receive access to the added resources. Newly added principals immediately receive access to the resources shared in this resource share. |

### associateresourcesharepermission
| Method | Path | Description |
|--------|------|-------------|
| POST | /associateresourcesharepermission | Adds or replaces the RAM permission for a resource type included in a resource share. You can have exactly one permission associated with each resource type in the resource share. You can add a new RAM permission only if there are currently no resources of that resource type currently in the resource share. |

### createpermission
| Method | Path | Description |
|--------|------|-------------|
| POST | /createpermission | Creates a customer managed permission for a specified resource type that you can attach to resource shares. It is created in the Amazon Web Services Region in which you call the operation. |

### createpermissionversion
| Method | Path | Description |
|--------|------|-------------|
| POST | /createpermissionversion | Creates a new version of the specified customer managed permission. The new version is automatically set as the default version of the customer managed permission. New resource shares automatically use the default permission. Existing resource shares continue to use their original permission versions, but you can use ReplacePermissionAssociations to update them. If the specified customer managed permission already has the maximum of 5 versions, then you must delete one of the existing versions before you can create a new one. |

### createresourceshare
| Method | Path | Description |
|--------|------|-------------|
| POST | /createresourceshare | Creates a resource share. You can provide a list of the Amazon Resource Names (ARNs) for the resources that you want to share, a list of principals you want to share the resources with, and the permissions to grant those principals.  Sharing a resource makes it available for use by principals outside of the Amazon Web Services account that created the resource. Sharing doesn't change any permissions or quotas that apply to the resource in the account that created it. |

### deletepermission
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /deletepermission | Deletes the specified customer managed permission in the Amazon Web Services Region in which you call this operation. You can delete a customer managed permission only if it isn't attached to any resource share. The operation deletes all versions associated with the customer managed permission. |

### deletepermissionversion
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /deletepermissionversion | Deletes one version of a customer managed permission. The version you specify must not be attached to any resource share and must not be the default version for the permission. If a customer managed permission has the maximum of 5 versions, then you must delete at least one version before you can create another. |

### deleteresourceshare
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /deleteresourceshare | Deletes the specified resource share.  This doesn't delete any of the resources that were associated with the resource share; it only stops the sharing of those resources through this resource share. |

### disassociateresourceshare
| Method | Path | Description |
|--------|------|-------------|
| POST | /disassociateresourceshare | Removes the specified principals or resources from participating in the specified resource share. |

### disassociateresourcesharepermission
| Method | Path | Description |
|--------|------|-------------|
| POST | /disassociateresourcesharepermission | Removes a managed permission from a resource share. Permission changes take effect immediately. You can remove a managed permission from a resource share only if there are currently no resources of the relevant resource type currently attached to the resource share. |

### enablesharingwithawsorganization
| Method | Path | Description |
|--------|------|-------------|
| POST | /enablesharingwithawsorganization | Enables resource sharing within your organization in Organizations. This operation creates a service-linked role called AWSServiceRoleForResourceAccessManager that has the IAM managed policy named AWSResourceAccessManagerServiceRolePolicy attached. This role permits RAM to retrieve information about the organization and its structure. This lets you share resources with all of the accounts in the calling account's organization by specifying the organization ID, or all of the accounts in an organizational unit (OU) by specifying the OU ID. Until you enable sharing within the organization, you can specify only individual Amazon Web Services accounts, or for supported resource types, IAM roles and users. You must call this operation from an IAM role or user in the organization's management account. |

### getpermission
| Method | Path | Description |
|--------|------|-------------|
| POST | /getpermission | Retrieves the contents of a managed permission in JSON format. |

### getresourcepolicies
| Method | Path | Description |
|--------|------|-------------|
| POST | /getresourcepolicies | Retrieves the resource policies for the specified resources that you own and have shared. |

### getresourceshareassociations
| Method | Path | Description |
|--------|------|-------------|
| POST | /getresourceshareassociations | Retrieves the lists of resources and principals that associated for resource shares that you own. |

### getresourceshareinvitations
| Method | Path | Description |
|--------|------|-------------|
| POST | /getresourceshareinvitations | Retrieves details about invitations that you have received for resource shares. |

### getresourceshares
| Method | Path | Description |
|--------|------|-------------|
| POST | /getresourceshares | Retrieves details about the resource shares that you own or that are shared with you. |

### listpendinginvitationresources
| Method | Path | Description |
|--------|------|-------------|
| POST | /listpendinginvitationresources | Lists the resources in a resource share that is shared with you but for which the invitation is still PENDING. That means that you haven't accepted or rejected the invitation and the invitation hasn't expired. |

### listpermissionassociations
| Method | Path | Description |
|--------|------|-------------|
| POST | /listpermissionassociations | Lists information about the managed permission and its associations to any resource shares that use this managed permission. This lets you see which resource shares use which versions of the specified managed permission. |

### listpermissionversions
| Method | Path | Description |
|--------|------|-------------|
| POST | /listpermissionversions | Lists the available versions of the specified RAM permission. |

### listpermissions
| Method | Path | Description |
|--------|------|-------------|
| POST | /listpermissions | Retrieves a list of available RAM permissions that you can use for the supported resource types. |

### listprincipals
| Method | Path | Description |
|--------|------|-------------|
| POST | /listprincipals | Lists the principals that you are sharing resources with or that are sharing resources with you. |

### listreplacepermissionassociationswork
| Method | Path | Description |
|--------|------|-------------|
| POST | /listreplacepermissionassociationswork | Retrieves the current status of the asynchronous tasks performed by RAM when you perform the ReplacePermissionAssociationsWork operation. |

### listresourcesharepermissions
| Method | Path | Description |
|--------|------|-------------|
| POST | /listresourcesharepermissions | Lists the RAM permissions that are associated with a resource share. |

### listresourcetypes
| Method | Path | Description |
|--------|------|-------------|
| POST | /listresourcetypes | Lists the resource types that can be shared by RAM. |

### listresources
| Method | Path | Description |
|--------|------|-------------|
| POST | /listresources | Lists the resources that you added to a resource share or the resources that are shared with you. |

### promotepermissioncreatedfrompolicy
| Method | Path | Description |
|--------|------|-------------|
| POST | /promotepermissioncreatedfrompolicy | When you attach a resource-based policy to a resource, RAM automatically creates a resource share of featureSet=CREATED_FROM_POLICY with a managed permission that has the same IAM permissions as the original resource-based policy. However, this type of managed permission is visible to only the resource share owner, and the associated resource share can't be modified by using RAM. This operation creates a separate, fully manageable customer managed permission that has the same IAM permissions as the original resource-based policy. You can associate this customer managed permission to any resource shares. Before you use PromoteResourceShareCreatedFromPolicy, you should first run this operation to ensure that you have an appropriate customer managed permission that can be associated with the promoted resource share.    The original CREATED_FROM_POLICY policy isn't deleted, and resource shares using that original policy aren't automatically updated.   You can't modify a CREATED_FROM_POLICY resource share so you can't associate the new customer managed permission by using ReplacePermsissionAssociations. However, if you use PromoteResourceShareCreatedFromPolicy, that operation automatically associates the fully manageable customer managed permission to the newly promoted STANDARD resource share.   After you promote a resource share, if the original CREATED_FROM_POLICY managed permission has no other associations to A resource share, then RAM automatically deletes it. |

### promoteresourcesharecreatedfrompolicy
| Method | Path | Description |
|--------|------|-------------|
| POST | /promoteresourcesharecreatedfrompolicy | When you attach a resource-based policy to a resource, RAM automatically creates a resource share of featureSet=CREATED_FROM_POLICY with a managed permission that has the same IAM permissions as the original resource-based policy. However, this type of managed permission is visible to only the resource share owner, and the associated resource share can't be modified by using RAM. This operation promotes the resource share to a STANDARD resource share that is fully manageable in RAM. When you promote a resource share, you can then manage the resource share in RAM and it becomes visible to all of the principals you shared it with.  Before you perform this operation, you should first run PromotePermissionCreatedFromPolicyto ensure that you have an appropriate customer managed permission that can be associated with this resource share after its is promoted. If this operation can't find a managed permission that exactly matches the existing CREATED_FROM_POLICY permission, then this operation fails. |

### rejectresourceshareinvitation
| Method | Path | Description |
|--------|------|-------------|
| POST | /rejectresourceshareinvitation | Rejects an invitation to a resource share from another Amazon Web Services account. |

### replacepermissionassociations
| Method | Path | Description |
|--------|------|-------------|
| POST | /replacepermissionassociations | Updates all resource shares that use a managed permission to a different managed permission. This operation always applies the default version of the target managed permission. You can optionally specify that the update applies to only resource shares that currently use a specified version. This enables you to update to the latest version, without changing the which managed permission is used. You can use this operation to update all of your resource shares to use the current default version of the permission by specifying the same value for the fromPermissionArn and toPermissionArn parameters. You can use the optional fromPermissionVersion parameter to update only those resources that use a specified version of the managed permission to the new managed permission.  To successfully perform this operation, you must have permission to update the resource-based policy on all affected resource types. |

### setdefaultpermissionversion
| Method | Path | Description |
|--------|------|-------------|
| POST | /setdefaultpermissionversion | Designates the specified version number as the default version for the specified customer managed permission. New resource shares automatically use this new default permission. Existing resource shares continue to use their original permission version, but you can use ReplacePermissionAssociations to update them. |

### tagresource
| Method | Path | Description |
|--------|------|-------------|
| POST | /tagresource | Adds the specified tag keys and values to a resource share or managed permission. If you choose a resource share, the tags are attached to only the resource share, not to the resources that are in the resource share. The tags on a managed permission are the same for all versions of the managed permission. |

### untagresource
| Method | Path | Description |
|--------|------|-------------|
| POST | /untagresource | Removes the specified tag key and value pairs from the specified resource share or managed permission. |

### updateresourceshare
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateresourceshare | Modifies some of the properties of the specified resource share. |

## Enhanced Skill Content
## Question Mapping

- "How do I share a resource with another AWS account?" -> POST /createresourceshare
- "How do I accept a resource share invitation?" -> POST /acceptresourceshareinvitation
- "How do I reject a resource share invitation?" -> POST /rejectresourceshareinvitation
- "What resource shares do I own or have shared with me?" -> POST /getresourceshares
- "What pending invitations do I have?" -> POST /getresourceshareinvitations
- "What resources are in a pending invitation?" -> POST /listpendinginvitationresources
- "Who has access to my shared resources?" -> POST /listprincipals
- "How do I remove a principal from a resource share?" -> POST /disassociateresourceshare
- "What permissions are attached to a resource share?" -> POST /listresourcesharepermissions
- "How do I create a custom permission for sharing?" -> POST /createpermission
- "How do I enable RAM sharing across my AWS Organization?" -> POST /enablesharingwithawsorganization
- "What resource types can I share with RAM?" -> POST /listresourcetypes
- "How do I replace a permission on all associated resource shares?" -> POST /replacepermissionassociations
- "How do I tag a resource share?" -> POST /tagresource
- "How do I delete a resource share?" -> DELETE /deleteresourceshare

## Response Tips

- **Resource shares & invitations**: Top-level object wraps a nullable detail object (e.g., `resourceShare`, `resourceShareInvitation`) -- always null-check before accessing nested fields like `status` or `tags`.
- **List/Get endpoints with pagination**: Any response containing `nextToken` may have more results. Loop until `nextToken` is absent. Use `maxResults` (default varies) to control page size.
- **Association endpoints**: Return arrays of `ResourceShareAssociation` -- each entry has its own `status` (e.g., ASSOCIATING, ASSOCIATED, FAILED). Check per-item status, not just HTTP 200.
- **Mutation confirmations**: Endpoints like delete, disassociate, and set-default return `returnValue: bool?` -- a `false` or null here means the operation did not complete as expected.
- **Permission detail vs summary**: `getpermission` returns `ResourceSharePermissionDetail` (includes `permission` policy JSON), while list endpoints return `ResourceSharePermissionSummary` (metadata only). Fetch detail when you need the actual policy.
- **Timestamps**: All timestamp fields are ISO 8601 strings -- parse with standard date libraries, not integer epoch.

## Anomaly Flags

- **Invitation status not ACCEPTED/REJECTED**: Surface if `status` is `EXPIRED` -- the user missed the acceptance window and must request a new share.
- **Association status FAILED**: After associate/disassociate calls, any `ResourceShareAssociation` with `status: "FAILED"` should be flagged with its `statusMessage`.
- **External principals on sensitive shares**: Warn when `allowExternalPrincipals: true` on a resource share -- resources are accessible outside the Organization.
- **Permission replacement work status**: When `replacepermissionassociations` returns a work item with `status: "FAILED"`, surface the `statusMessage` -- partial rollout may leave shares in inconsistent state.
- **Non-default permission versions**: Flag when `defaultVersion: false` on an active permission -- resource shares may be using an outdated policy.
- **Organization sharing not enabled**: If `enablesharingwithawsorganization` returns `returnValue: false`, warn that Organization-level sharing failed (likely missing Organizations trust).
- **clientToken mismatch**: If a response `clientToken` differs from the request, flag potential idempotency collision.

## Playbook

### 1. Share a Resource with Another AWS Account

1. Call `POST /createresourceshare` with a `name`, the `resourceArns` to share, and `principals` (target account IDs or Organization ARN).
2. Set `allowExternalPrincipals: true` if sharing outside your Organization.
3. Optionally attach `permissionArns` to control access level.
4. The target account receives an invitation -- confirm by calling `POST /getresourceshareinvitations` from the receiver's context.
5. Receiver calls `POST /acceptresourceshareinvitation` with the `resourceShareInvitationArn`.
6. Verify association status via `POST /getresourceshareassociations` with `associationType: "PRINCIPAL"`.

### 2. Create and Apply a Custom Permission

1. Call `POST /listresourcetypes` to find the exact `resourceType` string for your resource.
2. Call `POST /createpermission` with `name`, `resourceType`, and a `policyTemplate` (JSON policy document).
3. Note the returned `permission.arn` and `permission.version`.
4. Call `POST /associateresourcesharepermission` with the `resourceShareArn` and `permissionArn`. Set `replace: true` to swap out the existing default permission.
5. Verify via `POST /listresourcesharepermissions` that the new permission is active on the share.

### 3. Audit Who Has Access to Your Shared Resources

1. Call `POST /getresourceshares` with `resourceOwner: "SELF"` to list all shares you own. Paginate with `nextToken`.
2. For each share, call `POST /listprincipals` with `resourceOwner: "SELF"` and the `resourceShareArns`.
3. For each share, call `POST /listresources` with `resourceOwner: "SELF"` to see which resources are included.
4. Cross-reference principals against expected accounts. Flag any unknown `receiverAccountId` values.
5. Check `allowExternalPrincipals` on each share -- escalate if external sharing is unintended.

### 4. Replace a Permission Across All Resource Shares

1. Call `POST /createpermission` or `POST /createpermissionversion` to prepare the new permission.
2. Call `POST /setdefaultpermissionversion` to set the new version as default.
3. Call `POST /replacepermissionassociations` with `fromPermissionArn` and `toPermissionArn`.
4. Monitor the work item by calling `POST /listreplacepermissionassociationswork` with the returned `id`.
5. Repeat polling until `status` is `COMPLETED`. If `FAILED`, read `statusMessage` and remediate.

### 5. Clean Up a Resource Share

1. Call `POST /disassociateresourceshare` with `resourceShareArn` and the `principals` and `resourceArns` to remove.
2. Check each returned `ResourceShareAssociation` for `status: "DISASSOCIATED"`.
3. Call `POST /disassociateresourcesharepermission` to detach any custom permissions.
4. Call `POST /untagresource` to remove tags if needed.
5. Call `DELETE /deleteresourceshare` with the `resourceShareArn`.
6. Confirm deletion by calling `POST /getresourceshares` and verifying the share no longer appears (or has `status: "DELETED"`).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
