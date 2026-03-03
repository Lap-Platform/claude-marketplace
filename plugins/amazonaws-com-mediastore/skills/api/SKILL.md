---
name: aws-elemental-mediastore
description: "AWS Elemental MediaStore API skill. Use when working with AWS Elemental MediaStore for root. Covers 21 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Elemental MediaStore
API version: 2017-09-01

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

21 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Creates a storage container to hold objects. A container is similar to a bucket in the Amazon S3 service. |
| POST | / | Deletes the specified container. Before you make a DeleteContainer request, delete any objects in the container or in any folders in the container. You can delete only empty containers. |
| POST | / | Deletes the access policy that is associated with the specified container. |
| POST | / | Deletes the cross-origin resource sharing (CORS) configuration information that is set for the container. To use this operation, you must have permission to perform the MediaStore:DeleteCorsPolicy action. The container owner has this permission by default and can grant this permission to others. |
| POST | / | Removes an object lifecycle policy from a container. It takes up to 20 minutes for the change to take effect. |
| POST | / | Deletes the metric policy that is associated with the specified container. If there is no metric policy associated with the container, MediaStore doesn't send metrics to CloudWatch. |
| POST | / | Retrieves the properties of the requested container. This request is commonly used to retrieve the endpoint of a container. An endpoint is a value assigned by the service when a new container is created. A container's endpoint does not change after it has been assigned. The DescribeContainer request returns a single Container object based on ContainerName. To return all Container objects that are associated with a specified AWS account, use ListContainers. |
| POST | / | Retrieves the access policy for the specified container. For information about the data that is included in an access policy, see the AWS Identity and Access Management User Guide. |
| POST | / | Returns the cross-origin resource sharing (CORS) configuration information that is set for the container. To use this operation, you must have permission to perform the MediaStore:GetCorsPolicy action. By default, the container owner has this permission and can grant it to others. |
| POST | / | Retrieves the object lifecycle policy that is assigned to a container. |
| POST | / | Returns the metric policy for the specified container. |
| POST | / | Lists the properties of all containers in AWS Elemental MediaStore.  You can query to receive all the containers in one response. Or you can include the MaxResults parameter to receive a limited number of containers in each response. In this case, the response includes a token. To get the next set of containers, send the command again, this time with the NextToken parameter (with the returned token as its value). The next set of responses appears, with a token if there are still more containers to receive.  See also DescribeContainer, which gets the properties of one container. |
| POST | / | Returns a list of the tags assigned to the specified container. |
| POST | / | Creates an access policy for the specified container to restrict the users and clients that can access it. For information about the data that is included in an access policy, see the AWS Identity and Access Management User Guide. For this release of the REST API, you can create only one policy for a container. If you enter PutContainerPolicy twice, the second command modifies the existing policy. |
| POST | / | Sets the cross-origin resource sharing (CORS) configuration on a container so that the container can service cross-origin requests. For example, you might want to enable a request whose origin is http://www.example.com to access your AWS Elemental MediaStore container at my.example.container.com by using the browser's XMLHttpRequest capability. To enable CORS on a container, you attach a CORS policy to the container. In the CORS policy, you configure rules that identify origins and the HTTP methods that can be executed on your container. The policy can contain up to 398,000 characters. You can add up to 100 rules to a CORS policy. If more than one rule applies, the service uses the first applicable rule listed. To learn more about CORS, see Cross-Origin Resource Sharing (CORS) in AWS Elemental MediaStore. |
| POST | / | Writes an object lifecycle policy to a container. If the container already has an object lifecycle policy, the service replaces the existing policy with the new policy. It takes up to 20 minutes for the change to take effect. For information about how to construct an object lifecycle policy, see Components of an Object Lifecycle Policy. |
| POST | / | The metric policy that you want to add to the container. A metric policy allows AWS Elemental MediaStore to send metrics to Amazon CloudWatch. It takes up to 20 minutes for the new policy to take effect. |
| POST | / | Starts access logging on the specified container. When you enable access logging on a container, MediaStore delivers access logs for objects stored in that container to Amazon CloudWatch Logs. |
| POST | / | Stops access logging on the specified container. When you stop access logging on a container, MediaStore stops sending access logs to Amazon CloudWatch Logs. These access logs are not saved and are not retrievable. |
| POST | / | Adds tags to the specified AWS Elemental MediaStore container. Tags are key:value pairs that you can associate with AWS resources. For example, the tag key might be "customer" and the tag value might be "companyA." You can specify one or more tags to add to each container. You can add up to 50 tags to each container. For more information about tagging, including naming and usage conventions, see Tagging Resources in MediaStore. |
| POST | / | Removes tags from the specified container. You can specify one or more tags to remove. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new MediaStore container?" -> POST / (CreateContainer: ContainerName + optional Tags)
- "How do I delete a MediaStore container?" -> POST / (DeleteContainer: ContainerName)
- "What containers do I have?" -> POST / (ListContainers: optional NextToken, MaxResults)
- "What's the status of my container?" -> POST / (DescribeContainer: optional ContainerName)
- "How do I set a container access policy?" -> POST / (PutContainerPolicy: ContainerName + Policy)
- "What policy is attached to my container?" -> POST / (GetContainerPolicy: ContainerName)
- "How do I enable CORS on my container?" -> POST / (PutCorsPolicy: ContainerName + CorsPolicy)
- "What CORS rules are on my container?" -> POST / (GetCorsPolicy: ContainerName)
- "How do I set a lifecycle policy for auto-expiring objects?" -> POST / (PutLifecyclePolicy: ContainerName + LifecyclePolicy)
- "How do I enable CloudWatch metrics for my container?" -> POST / (PutMetricPolicy: ContainerName + MetricPolicy)
- "How do I turn on access logging?" -> POST / (StartAccessLogging: ContainerName)
- "How do I stop access logging?" -> POST / (StopAccessLogging: ContainerName)
- "How do I tag a MediaStore resource?" -> POST / (TagResource: Resource ARN + Tags)
- "What tags are on my resource?" -> POST / (ListTagsForResource: Resource ARN)
- "How do I remove tags from a resource?" -> POST / (UntagResource: Resource ARN + TagKeys)

## Response Tips

- **Container operations**: Container objects include `Status` (CREATING, ACTIVE, DELETING) -- always check status before performing actions; `Endpoint` is null until status is ACTIVE.
- **List operations**: `ListContainers` paginates via `NextToken`; keep calling with the returned `NextToken` until it is absent from the response.
- **Policy operations**: `GetContainerPolicy` and `GetLifecyclePolicy` return policy as a JSON string -- parse it before presenting to the user.
- **CORS operations**: `GetCorsPolicy` returns an array of `CorsRule` objects; each rule may have different allowed origins, headers, and methods.
- **Metric operations**: `GetMetricPolicy` returns `ContainerLevelMetrics` (ENABLED/DISABLED) and an optional array of path-level `MetricPolicyRules`.
- **Tag operations**: Tags are key-value pairs on resource ARNs; `ListTagsForResource` may return null if no tags exist.
- **Errors**: All endpoints use standard AWS error shapes -- watch for `ContainerNotFoundException`, `PolicyNotFoundException`, `LimitExceededException`, and `ContainerInUseException`.

## Anomaly Flags

- **Container stuck in CREATING/DELETING**: If `DescribeContainer` returns a non-ACTIVE status for more than a few minutes, surface this -- the container may be stalled.
- **Missing endpoint URL**: A container with a null `Endpoint` field is not yet ready for data plane operations; warn the user before they attempt object uploads.
- **No policy attached**: If `GetContainerPolicy` throws `PolicyNotFoundException`, flag that the container has no access policy and is inaccessible to external callers.
- **Access logging disabled**: If `AccessLoggingEnabled` is false on a production container, proactively suggest enabling it for audit compliance.
- **Pagination truncation**: If `ListContainers` returns a `NextToken`, alert the user that results are incomplete and offer to fetch all pages.
- **Lifecycle policy risks**: When a user sets a lifecycle policy, warn that it will permanently delete objects matching the rules -- this is irreversible.
- **Tag limit approaching**: AWS limits tags per resource (typically 50); if `ListTagsForResource` returns a high count, flag it before `TagResource` calls fail.

## Playbook

### 1. Create and Configure a New Container

1. Call **CreateContainer** with the desired `ContainerName` and optional `Tags`.
2. Call **DescribeContainer** repeatedly until `Status` is `ACTIVE` and `Endpoint` is populated.
3. Call **PutContainerPolicy** to attach an access policy allowing your desired principals.
4. Call **PutCorsPolicy** if the container will serve browser-based clients.
5. Call **StartAccessLogging** if audit logging is required.

### 2. Set Up Monitoring and Lifecycle Management

1. Call **PutMetricPolicy** with `ContainerLevelMetrics: "ENABLED"` and optional path-level rules.
2. Call **PutLifecyclePolicy** with a JSON policy string defining object expiration rules.
3. Verify with **GetMetricPolicy** and **GetLifecyclePolicy** that both are applied correctly.

### 3. Audit and Review Container Configuration

1. Call **ListContainers** (paginate with `NextToken`) to enumerate all containers.
2. For each container, call **DescribeContainer** to check `Status` and `AccessLoggingEnabled`.
3. Call **GetContainerPolicy**, **GetCorsPolicy**, and **GetMetricPolicy** to review current settings.
4. Call **ListTagsForResource** with the container ARN to verify tagging compliance.

### 4. Tear Down a Container

1. Call **DeleteContainerPolicy** to remove the access policy.
2. Call **DeleteCorsPolicy** and **DeleteLifecyclePolicy** to remove attached policies.
3. Call **StopAccessLogging** if access logging is enabled.
4. Ensure all objects in the container are deleted via the data plane (not covered by this API).
5. Call **DeleteContainer** -- this will fail if objects still exist in the container.

### 5. Manage Resource Tags

1. Call **ListTagsForResource** with the resource ARN to see current tags.
2. Call **TagResource** with the ARN and an array of `{Key, Value}` pairs to add or update tags.
3. Call **UntagResource** with the ARN and an array of tag key strings to remove specific tags.
4. Call **ListTagsForResource** again to confirm the final tag state.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
