---
name: amazon-s3-on-outposts
description: "Amazon S3 on Outposts API skill. Use when working with Amazon S3 on Outposts for S3Outposts. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon S3 on Outposts
API version: 2017-07-25

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /S3Outposts/ListEndpoints -- verify access
3. POST /S3Outposts/CreateEndpoint -- create first CreateEndpoint

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### S3Outposts
| Method | Path | Description |
|--------|------|-------------|
| POST | /S3Outposts/CreateEndpoint | Creates an endpoint and associates it with the specified Outpost.  It can take up to 5 minutes for this action to finish.   Related actions include:    DeleteEndpoint     ListEndpoints |
| DELETE | /S3Outposts/DeleteEndpoint | Deletes an endpoint.  It can take up to 5 minutes for this action to finish.   Related actions include:    CreateEndpoint     ListEndpoints |
| GET | /S3Outposts/ListEndpoints | Lists endpoints associated with the specified Outpost.  Related actions include:    CreateEndpoint     DeleteEndpoint |
| GET | /S3Outposts/ListOutpostsWithS3 | Lists the Outposts with S3 on Outposts capacity for your Amazon Web Services account. Includes S3 on Outposts that you have access to as the Outposts owner, or as a shared user from Resource Access Manager (RAM). |
| GET | /S3Outposts/ListSharedEndpoints | Lists all endpoints associated with an Outpost that has been shared by Amazon Web Services Resource Access Manager (RAM). Related actions include:    CreateEndpoint     DeleteEndpoint |

## Enhanced Skill Content
## Question Mapping

- "How do I create an S3 endpoint on my Outpost?" -> POST /S3Outposts/CreateEndpoint
- "How do I delete an S3 Outposts endpoint?" -> DELETE /S3Outposts/DeleteEndpoint
- "What endpoints exist on my Outposts?" -> GET /S3Outposts/ListEndpoints
- "Which of my Outposts have S3 capability?" -> GET /S3Outposts/ListOutpostsWithS3
- "What shared endpoints are available on a specific Outpost?" -> GET /S3Outposts/ListSharedEndpoints
- "Can I use a customer-owned IP pool for my endpoint?" -> POST /S3Outposts/CreateEndpoint (use CustomerOwnedIpv4Pool)
- "How do I set up a private access endpoint on an Outpost?" -> POST /S3Outposts/CreateEndpoint (set AccessType to Private)
- "How do I paginate through all my Outpost endpoints?" -> GET /S3Outposts/ListEndpoints (use nextToken)
- "I need to decommission an endpoint -- what identifiers do I need?" -> DELETE /S3Outposts/DeleteEndpoint (requires endpointId + outpostId)
- "Which Outposts support S3 storage?" -> GET /S3Outposts/ListOutpostsWithS3
- "How do I find endpoints shared with my account on a given Outpost?" -> GET /S3Outposts/ListSharedEndpoints
- "What security group should I associate with a new endpoint?" -> POST /S3Outposts/CreateEndpoint (SecurityGroupId is required)
- "How do I get the ARN of a newly created endpoint?" -> POST /S3Outposts/CreateEndpoint (check EndpointArn in 200 response)

## Response Tips

- **Create**: Returns `EndpointArn` (nullable) -- a missing ARN may indicate async provisioning; poll ListEndpoints to confirm the endpoint becomes active.
- **Delete**: No response body on success; confirm removal by listing endpoints afterward.
- **List endpoints/shared endpoints**: Both return `Endpoints` array (nullable) and `NextToken`; always check for `NextToken` to retrieve additional pages. An empty or null `Endpoints` means no results, not an error.
- **List Outposts with S3**: Returns `Outposts` array (nullable) with `NextToken` pagination; null array means no S3-capable Outposts exist.
- **All list operations**: Use `maxResults` to control page size and `nextToken` from previous responses to advance pages.

## Anomaly Flags

- **Null EndpointArn after create**: The endpoint may be provisioning asynchronously -- surface this and suggest polling ListEndpoints for status.
- **Empty Endpoints or Outposts arrays**: Proactively confirm whether the user expected results, as this may indicate wrong outpostId, region mismatch, or missing permissions.
- **Pagination loop detection**: If the same `NextToken` is returned repeatedly, flag a potential API issue.
- **Delete without prior list**: If a user attempts to delete without first confirming the endpoint exists, suggest listing endpoints first to verify the endpointId.
- **AccessType mismatch**: If a user specifies `CustomerOwnedIpv4Pool` without setting `AccessType` to a compatible value, flag the potential configuration conflict.
- **AWS SigV4 auth failures (403)**: Surface credential or region misconfiguration as the likely cause before retrying.

## Playbook

### 1. Provision a New S3 Endpoint on an Outpost

1. Call `GET /S3Outposts/ListOutpostsWithS3` to confirm the target Outpost supports S3.
2. Identify the `OutpostId` from the response.
3. Call `POST /S3Outposts/CreateEndpoint` with `OutpostId`, `SubnetId`, and `SecurityGroupId`. Optionally set `AccessType` and `CustomerOwnedIpv4Pool`.
4. Capture the `EndpointArn` from the response.
5. Call `GET /S3Outposts/ListEndpoints` and verify the new endpoint appears and is active.

### 2. Decommission an Endpoint

1. Call `GET /S3Outposts/ListEndpoints` to find the target endpoint and note its `endpointId` and `outpostId`.
2. Call `DELETE /S3Outposts/DeleteEndpoint` with `endpointId` and `outpostId`.
3. Call `GET /S3Outposts/ListEndpoints` again to confirm the endpoint no longer appears.

### 3. Inventory All Endpoints Across Outposts

1. Call `GET /S3Outposts/ListOutpostsWithS3` (paginate with `nextToken` until all Outposts are collected).
2. For each Outpost, call `GET /S3Outposts/ListEndpoints` (paginate fully).
3. Optionally call `GET /S3Outposts/ListSharedEndpoints` with each `outpostId` to include shared endpoints.
4. Aggregate results for a complete endpoint inventory.

### 4. Audit Shared Endpoints on an Outpost

1. Identify the target `outpostId` (from ListOutpostsWithS3 or known infrastructure).
2. Call `GET /S3Outposts/ListSharedEndpoints` with the `outpostId`.
3. Paginate through all results using `nextToken`.
4. Compare shared endpoints against your owned endpoints from `ListEndpoints` to identify cross-account access patterns.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
