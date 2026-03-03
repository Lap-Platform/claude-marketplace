---
name: aws-service-catalog-app-registry
description: "AWS Service Catalog App Registry API skill. Use when working with AWS Service Catalog App Registry for applications, attribute-groups, configuration. Covers 24 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Service Catalog App Registry
API version: 2020-06-24

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /configuration -- verify access
3. POST /applications -- create first applications

## Endpoints

24 endpoints across 5 groups. See references/api-spec.lap for full details.

### applications
| Method | Path | Description |
|--------|------|-------------|
| PUT | /applications/{application}/attribute-groups/{attributeGroup} | Associates an attribute group with an application to augment the application's metadata with the group's attributes. This feature enables applications to be described with user-defined details that are machine-readable, such as third-party integrations. |
| PUT | /applications/{application}/resources/{resourceType}/{resource} | Associates a resource with an application. The resource can be specified by its ARN or name. The application can be specified by ARN, ID, or name.   Minimum permissions   You must have the following permissions to associate a resource using the OPTIONS parameter set to APPLY_APPLICATION_TAG.     tag:GetResources     tag:TagResources     You must also have these additional permissions if you don't use the AWSServiceCatalogAppRegistryFullAccess policy. For more information, see AWSServiceCatalogAppRegistryFullAccess in the AppRegistry Administrator Guide.     resource-groups:AssociateResource     cloudformation:UpdateStack     cloudformation:DescribeStacks      In addition, you must have the tagging permission defined by the Amazon Web Services service that creates the resource. For more information, see TagResources in the Resource Groups Tagging API Reference. |
| POST | /applications | Creates a new application that is the top-level node in a hierarchy of related cloud resource abstractions. |
| DELETE | /applications/{application} | Deletes an application that is specified either by its application ID, name, or ARN. All associated attribute groups and resources must be disassociated from it before deleting an application. |
| DELETE | /applications/{application}/attribute-groups/{attributeGroup} | Disassociates an attribute group from an application to remove the extra attributes contained in the attribute group from the application's metadata. This operation reverts AssociateAttributeGroup. |
| DELETE | /applications/{application}/resources/{resourceType}/{resource} | Disassociates a resource from application. Both the resource and the application can be specified either by ID or name.   Minimum permissions   You must have the following permissions to remove a resource that's been associated with an application using the APPLY_APPLICATION_TAG option for AssociateResource.     tag:GetResources     tag:UntagResources     You must also have the following permissions if you don't use the AWSServiceCatalogAppRegistryFullAccess policy. For more information, see AWSServiceCatalogAppRegistryFullAccess in the AppRegistry Administrator Guide.     resource-groups:DisassociateResource     cloudformation:UpdateStack     cloudformation:DescribeStacks      In addition, you must have the tagging permission defined by the Amazon Web Services service that creates the resource. For more information, see UntagResources in the Resource Groups Tagging API Reference. |
| GET | /applications/{application} | Retrieves metadata information about one of your applications. The application can be specified by its ARN, ID, or name (which is unique within one account in one region at a given point in time). Specify by ARN or ID in automated workflows if you want to make sure that the exact same application is returned or a ResourceNotFoundException is thrown, avoiding the ABA addressing problem. |
| GET | /applications/{application}/resources/{resourceType}/{resource} | Gets the resource associated with the application. |
| GET | /applications | Retrieves a list of all of your applications. Results are paginated. |
| GET | /applications/{application}/attribute-groups | Lists all attribute groups that are associated with specified application. Results are paginated. |
| GET | /applications/{application}/resources | Lists all of the resources that are associated with the specified application. Results are paginated.    If you share an application, and a consumer account associates a tag query to the application, all of the users who can access the application can also view the tag values in all accounts that are associated with it using this API. |
| GET | /applications/{application}/attribute-group-details | Lists the details of all attribute groups associated with a specific application. The results display in pages. |
| PATCH | /applications/{application} | Updates an existing application with new attributes. |

### attribute-groups
| Method | Path | Description |
|--------|------|-------------|
| POST | /attribute-groups | Creates a new attribute group as a container for user-defined attributes. This feature enables users to have full control over their cloud application's metadata in a rich machine-readable format to facilitate integration with automated workflows and third-party tools. |
| DELETE | /attribute-groups/{attributeGroup} | Deletes an attribute group, specified either by its attribute group ID, name, or ARN. |
| GET | /attribute-groups/{attributeGroup} | Retrieves an attribute group by its ARN, ID, or name. The attribute group can be specified by its ARN, ID, or name. |
| GET | /attribute-groups | Lists all attribute groups which you have access to. Results are paginated. |
| PATCH | /attribute-groups/{attributeGroup} | Updates an existing attribute group with new details. |

### configuration
| Method | Path | Description |
|--------|------|-------------|
| GET | /configuration | Retrieves a TagKey configuration from an account. |
| PUT | /configuration | Associates a TagKey configuration to an account. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{resourceArn} | Lists all of the tags on the resource. |
| POST | /tags/{resourceArn} | Assigns one or more tags (key-value pairs) to the specified resource. Each tag consists of a key and an optional value. If a tag with the same key is already associated with the resource, this action updates its value. This operation returns an empty response if the call was successful. |
| DELETE | /tags/{resourceArn} | Removes tags from a resource. This operation returns an empty response if the call was successful. |

### sync
| Method | Path | Description |
|--------|------|-------------|
| POST | /sync/{resourceType}/{resource} | Syncs the resource with current AppRegistry records. Specifically, the resource’s AppRegistry system tags sync with its associated application. We remove the resource's AppRegistry system tags if it does not associate with the application. The caller must have permissions to read and update the resource. |

## Enhanced Skill Content
## Question Mapping

- "How do I register a new application in the service catalog?" -> POST /applications
- "What applications exist in my account?" -> GET /applications
- "How do I get details about a specific application?" -> GET /applications/{application}
- "How do I rename or update an application's description?" -> PATCH /applications/{application}
- "How do I delete an application?" -> DELETE /applications/{application}
- "How do I create an attribute group with custom metadata?" -> POST /attribute-groups
- "How do I attach an attribute group to an application?" -> PUT /applications/{application}/attribute-groups/{attributeGroup}
- "What attribute groups are associated with my application?" -> GET /applications/{application}/attribute-groups
- "How do I add a resource (like a CloudFormation stack) to an application?" -> PUT /applications/{application}/resources/{resourceType}/{resource}
- "What resources belong to a specific application?" -> GET /applications/{application}/resources
- "How do I check the tag-based resource sync status for a resource?" -> POST /sync/{resourceType}/{resource}
- "How do I tag an application or attribute group?" -> POST /tags/{resourceArn}
- "How do I remove specific tags from a resource?" -> DELETE /tags/{resourceArn}
- "What is the current App Registry tag query configuration?" -> GET /configuration
- "How do I get full attribute group details (including attributes JSON) for an application?" -> GET /applications/{application}/attribute-group-details

## Response Tips

- **Applications & Attribute Groups (list endpoints):** Paginated via `nextToken` + `maxResults`. Always check for `nextToken` in response; if present, pass it in the next request to get more results.
- **Single resource GETs:** Return nullable wrapper objects (`application`, `attributeGroup`, `resource`); always null-check the top-level key before accessing nested fields.
- **Association endpoints (PUT/DELETE for linking):** Return only ARN pairs (`applicationArn`, `resourceArn` or `attributeGroupArn`), not full objects -- use a follow-up GET if you need details.
- **Sync endpoint:** Returns `actionTaken` (e.g., `START_SYNC`, `NO_ACTION`) indicating whether a sync was triggered; a 200 with `NO_ACTION` is not an error.
- **Tags:** `GET /tags/{resourceArn}` returns a flat `map<str,str>`; tag keys and values are always strings.
- **Timestamps:** All `creationTime` and `lastUpdateTime` fields are ISO 8601 strings, not epoch integers.

## Anomaly Flags

- **Integration errors:** Surface `integrations.resourceGroup.errorMessage` or `integrations.applicationTagResourceGroup.errorMessage` when state is not `ACTIVE` on GET /applications/{application} -- indicates a failed AWS Resource Groups sync.
- **Resource tag status mismatches:** When GET /applications/{application}/resources/{resourceType}/{resource} returns `applicationTagResult.applicationTagStatus` other than `SUCCESS`, flag the `errorMessage` and affected `resources` list.
- **associatedResourceCount = 0:** Warn when an application has zero associated resources, as it may be orphaned or misconfigured.
- **Sync no-ops:** If POST /sync returns `actionTaken: NO_ACTION` repeatedly, surface that the resource may already be in sync or may not be eligible for syncing.
- **Missing attributes:** When GET /attribute-groups/{attributeGroup} returns `attributes: null`, flag that the group has no metadata payload, which likely means it was created but never populated.
- **createdBy discrepancies:** Attribute group summaries include `createdBy`; surface when a group was created by a different principal than expected (possible cross-account or service-linked creation).

## Playbook

### 1. Set Up a New Application with Resources and Metadata

1. Create the application: `POST /applications` with `name`, `clientToken`, and optional `description`/`tags`.
2. Create an attribute group: `POST /attribute-groups` with `name`, `attributes` (JSON string of metadata), and `clientToken`.
3. Associate the attribute group: `PUT /applications/{application}/attribute-groups/{attributeGroup}`.
4. Associate resources (e.g., CloudFormation stacks): `PUT /applications/{application}/resources/{resourceType}/{resource}` for each resource.
5. Verify: `GET /applications/{application}` and confirm `associatedResourceCount` is correct and `integrations` show `ACTIVE` state.

### 2. Audit All Applications and Their Resources

1. List all applications: `GET /applications` (paginate with `nextToken` until exhausted).
2. For each application, fetch details: `GET /applications/{application}` to check `associatedResourceCount` and integration state.
3. List resources per application: `GET /applications/{application}/resources` (paginate).
4. List attribute groups per application: `GET /applications/{application}/attribute-group-details` for full metadata (paginate).
5. Flag any application with zero resources, non-`ACTIVE` integration states, or attribute groups with null `attributes`.

### 3. Clean Up an Application and Its Associations

1. List associated resources: `GET /applications/{application}/resources` (paginate to get all).
2. Disassociate each resource: `DELETE /applications/{application}/resources/{resourceType}/{resource}`.
3. List associated attribute groups: `GET /applications/{application}/attribute-groups` (paginate).
4. Disassociate each attribute group: `DELETE /applications/{application}/attribute-groups/{attributeGroup}`.
5. Delete the application: `DELETE /applications/{application}`.
6. Optionally delete orphaned attribute groups: `DELETE /attribute-groups/{attributeGroup}` for any groups no longer needed.

### 4. Tag Management Across Resources

1. Get current tags: `GET /tags/{resourceArn}` for the target resource.
2. Add or update tags: `POST /tags/{resourceArn}` with the desired `tags` map (existing keys are overwritten).
3. Remove specific tags: `DELETE /tags/{resourceArn}` with `tagKeys` array listing keys to remove.
4. Verify: `GET /tags/{resourceArn}` again to confirm final state.

### 5. Sync a Resource and Verify Status

1. Trigger sync: `POST /sync/{resourceType}/{resource}`.
2. Check `actionTaken` in the response -- if `START_SYNC`, proceed to monitor; if `NO_ACTION`, the resource is already current.
3. Retrieve the resource association: `GET /applications/{application}/resources/{resourceType}/{resource}`.
4. Inspect `resource.integrations.resourceGroup.state` -- wait for `ACTIVE`.
5. If state shows an error, read `errorMessage` and resolve the underlying issue (e.g., missing IAM permissions, deleted resource group).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
