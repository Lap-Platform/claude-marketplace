---
name: aws-elemental-mediapackage-vod
description: "AWS Elemental MediaPackage VOD API skill. Use when working with AWS Elemental MediaPackage VOD for packaging_groups, assets, packaging_configurations. Covers 17 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Elemental MediaPackage VOD
API version: 2018-11-07

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /assets -- verify access
3. POST /assets -- create first assets

## Endpoints

17 endpoints across 4 groups. See references/api-spec.lap for full details.

### packaging_groups
| Method | Path | Description |
|--------|------|-------------|
| PUT | /packaging_groups/{id}/configure_logs | Changes the packaging group's properities to configure log subscription |
| POST | /packaging_groups | Creates a new MediaPackage VOD PackagingGroup resource. |
| DELETE | /packaging_groups/{id} | Deletes a MediaPackage VOD PackagingGroup resource. |
| GET | /packaging_groups/{id} | Returns a description of a MediaPackage VOD PackagingGroup resource. |
| GET | /packaging_groups | Returns a collection of MediaPackage VOD PackagingGroup resources. |
| PUT | /packaging_groups/{id} | Updates a specific packaging group. You can't change the id attribute or any other system-generated attributes. |

### assets
| Method | Path | Description |
|--------|------|-------------|
| POST | /assets | Creates a new MediaPackage VOD Asset resource. |
| DELETE | /assets/{id} | Deletes an existing MediaPackage VOD Asset resource. |
| GET | /assets/{id} | Returns a description of a MediaPackage VOD Asset resource. |
| GET | /assets | Returns a collection of MediaPackage VOD Asset resources. |

### packaging_configurations
| Method | Path | Description |
|--------|------|-------------|
| POST | /packaging_configurations | Creates a new MediaPackage VOD PackagingConfiguration resource. |
| DELETE | /packaging_configurations/{id} | Deletes a MediaPackage VOD PackagingConfiguration resource. |
| GET | /packaging_configurations/{id} | Returns a description of a MediaPackage VOD PackagingConfiguration resource. |
| GET | /packaging_configurations | Returns a collection of MediaPackage VOD PackagingConfiguration resources. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{resource-arn} | Returns a list of the tags assigned to the specified resource. |
| POST | /tags/{resource-arn} | Adds tags to the specified resource. You can specify one or more tags to add. |
| DELETE | /tags/{resource-arn} | Removes tags from the specified resource. You can specify one or more tags to remove. |

## Enhanced Skill Content
## Question Mapping

- "How do I ingest a new VOD asset?" -> POST /assets
- "List all my VOD assets" -> GET /assets
- "Get details for a specific asset" -> GET /assets/{id}
- "Delete a VOD asset" -> DELETE /assets/{id}
- "Create a new packaging group" -> POST /packaging_groups
- "List all packaging groups" -> GET /packaging_groups
- "How many assets are in a packaging group?" -> GET /packaging_groups/{id}
- "Update CDN authorization on a packaging group" -> PUT /packaging_groups/{id}
- "Enable egress access logging for a packaging group" -> PUT /packaging_groups/{id}/configure_logs
- "Create an HLS packaging configuration with encryption" -> POST /packaging_configurations
- "What packaging configurations exist for a given group?" -> GET /packaging_configurations
- "Get the encryption settings for a packaging configuration" -> GET /packaging_configurations/{id}
- "Tag a resource by ARN" -> POST /tags/{resource-arn}
- "Remove specific tags from a resource" -> DELETE /tags/{resource-arn}
- "List all tags on a packaging group or asset" -> GET /tags/{resource-arn}

## Response Tips

- **Assets**: List responses return `Assets` array with `NextToken` for pagination; individual asset responses include `EgressEndpoints` array with playback URLs.
- **Packaging Groups**: `ApproximateAssetCount` is only present on GET/PUT single group, not on list responses; `DomainName` gives the CDN origin hostname.
- **Packaging Configurations**: Responses contain deeply nested package-type objects (`CmafPackage`, `DashPackage`, `HlsPackage`, `MssPackage`) -- only the one matching the created type is populated, others are null.
- **Tags**: All tag values are `map<str,str>`; DELETE requires `tagKeys` as a query-string array, not a body.
- **Pagination**: All list endpoints accept `maxResults` and `nextToken`; keep calling until `NextToken` is null.
- **Errors**: Non-200 responses are not detailed in the spec -- expect standard AWS error shapes (`__type`, `message`).

## Anomaly Flags

- **Missing EgressEndpoints**: If a newly created asset returns an empty `EgressEndpoints` array, the packaging group may lack configurations -- surface this immediately.
- **ApproximateAssetCount = 0**: When deleting a packaging group succeeds but it had assets, warn that orphaned assets may remain.
- **No encryption configured**: If a packaging configuration is created without any `Encryption` block inside its package type, flag that content will be delivered unencrypted.
- **Authorization block absent**: When a packaging group lacks `Authorization` (CDN auth), warn that content may be accessible without CDN token verification.
- **Stale NextToken**: If a pagination token returns an empty result set, the underlying data may have changed mid-pagination -- flag potential inconsistency.
- **SpekeKeyProvider URL unreachable**: If the SPEKE key provider URL in an encryption config points to an unusual or non-HTTPS endpoint, flag as a potential DRM misconfiguration.

## Playbook

### 1. Set Up a Complete VOD Workflow from Scratch

1. Create a packaging group: `POST /packaging_groups` with a unique `Id`
2. Configure CDN authorization on the group: `PUT /packaging_groups/{id}` with `Authorization.CdnIdentifierSecret` and `SecretsRoleArn`
3. Create one or more packaging configurations: `POST /packaging_configurations` with the desired package type (`HlsPackage`, `DashPackage`, `CmafPackage`, or `MssPackage`) referencing the group's `Id`
4. Ingest an asset: `POST /assets` with `SourceArn` (S3 location), `SourceRoleArn` (IAM role), and `PackagingGroupId`
5. Retrieve the asset: `GET /assets/{id}` and read `EgressEndpoints` for playback URLs

### 2. Add Encrypted HLS Packaging to an Existing Group

1. Retrieve the packaging group: `GET /packaging_groups/{id}` to confirm it exists
2. Create the configuration: `POST /packaging_configurations` with `HlsPackage.Encryption.SpekeKeyProvider` populated (set `RoleArn`, `SystemIds`, and DRM key server `Url`)
3. Verify: `GET /packaging_configurations/{id}` and confirm `HlsPackage.Encryption` is present
4. Ingest a test asset: `POST /assets` targeting that group, then check `EgressEndpoints` for the encrypted HLS stream

### 3. Audit and Clean Up Unused Resources

1. List all packaging groups: `GET /packaging_groups` (paginate with `nextToken`)
2. For each group, check `ApproximateAssetCount` via `GET /packaging_groups/{id}` -- flag groups with zero assets
3. List packaging configurations per group: `GET /packaging_configurations?packagingGroupId={id}`
4. Delete unused configurations: `DELETE /packaging_configurations/{id}`
5. Delete empty packaging groups: `DELETE /packaging_groups/{id}`

### 4. Enable Egress Access Logging

1. Ensure a CloudWatch Log Group exists for your region
2. Configure logging: `PUT /packaging_groups/{id}/configure_logs` with `EgressAccessLogs.LogGroupName` set to the log group name
3. Verify: `GET /packaging_groups/{id}` and confirm `EgressAccessLogs.LogGroupName` is populated
4. Tag the group for tracking: `POST /tags/{resource-arn}` with `{"logging": "enabled"}`

### 5. Bulk-Tag Resources for Cost Allocation

1. List all assets: `GET /assets` (paginate fully)
2. List all packaging groups: `GET /packaging_groups` (paginate fully)
3. For each resource, read its `Arn` from the response
4. Apply tags: `POST /tags/{resource-arn}` with cost-allocation tags (e.g., `{"project": "vod-platform", "environment": "prod"}`)
5. Verify: `GET /tags/{resource-arn}` on a sample to confirm tags applied


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
