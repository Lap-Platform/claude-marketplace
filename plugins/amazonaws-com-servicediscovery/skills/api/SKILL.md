---
name: aws-cloud-map
description: "AWS Cloud Map API skill. Use when working with AWS Cloud Map for root. Covers 27 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Cloud Map
API version: 2017-03-14

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

27 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Creates an HTTP namespace. Service instances registered using an HTTP namespace can be discovered using a DiscoverInstances request but can't be discovered using DNS. For the current quota on the number of namespaces that you can create using the same Amazon Web Services account, see Cloud Map quotas in the Cloud Map Developer Guide. |
| POST | / | Creates a private namespace based on DNS, which is visible only inside a specified Amazon VPC. The namespace defines your service naming scheme. For example, if you name your namespace example.com and name your service backend, the resulting DNS name for the service is backend.example.com. Service instances that are registered using a private DNS namespace can be discovered using either a DiscoverInstances request or using DNS. For the current quota on the number of namespaces that you can create using the same Amazon Web Services account, see Cloud Map quotas in the Cloud Map Developer Guide. |
| POST | / | Creates a public namespace based on DNS, which is visible on the internet. The namespace defines your service naming scheme. For example, if you name your namespace example.com and name your service backend, the resulting DNS name for the service is backend.example.com. You can discover instances that were registered with a public DNS namespace by using either a DiscoverInstances request or using DNS. For the current quota on the number of namespaces that you can create using the same Amazon Web Services account, see Cloud Map quotas in the Cloud Map Developer Guide.  The CreatePublicDnsNamespace API operation is not supported in the Amazon Web Services GovCloud (US) Regions. |
| POST | / | Creates a service. This action defines the configuration for the following entities:   For public and private DNS namespaces, one of the following combinations of DNS records in Amazon Route 53:    A     AAAA     A and AAAA     SRV     CNAME      Optionally, a health check   After you create the service, you can submit a RegisterInstance request, and Cloud Map uses the values in the configuration to create the specified entities. For the current quota on the number of instances that you can register using the same namespace and using the same service, see Cloud Map quotas in the Cloud Map Developer Guide. |
| POST | / | Deletes a namespace from the current account. If the namespace still contains one or more services, the request fails. |
| POST | / | Deletes a specified service. If the service still contains one or more registered instances, the request fails. |
| POST | / | Deletes the Amazon Route 53 DNS records and health check, if any, that Cloud Map created for the specified instance. |
| POST | / | Discovers registered instances for a specified namespace and service. You can use DiscoverInstances to discover instances for any type of namespace. DiscoverInstances returns a randomized list of instances allowing customers to distribute traffic evenly across instances. For public and private DNS namespaces, you can also use DNS queries to discover instances. |
| POST | / | Discovers the increasing revision associated with an instance. |
| POST | / | Gets information about a specified instance. |
| POST | / | Gets the current health status (Healthy, Unhealthy, or Unknown) of one or more instances that are associated with a specified service.  There's a brief delay between when you register an instance and when the health status for the instance is available. |
| POST | / | Gets information about a namespace. |
| POST | / | Gets information about any operation that returns an operation ID in the response, such as a CreateHttpNamespace request.  To get a list of operations that match specified criteria, see ListOperations. |
| POST | / | Gets the settings for a specified service. |
| POST | / | Lists summary information about the instances that you registered by using a specified service. |
| POST | / | Lists summary information about the namespaces that were created by the current Amazon Web Services account. |
| POST | / | Lists operations that match the criteria that you specify. |
| POST | / | Lists summary information for all the services that are associated with one or more namespaces. |
| POST | / | Lists tags for the specified resource. |
| POST | / | Creates or updates one or more records and, optionally, creates a health check based on the settings in a specified service. When you submit a RegisterInstance request, the following occurs:   For each DNS record that you define in the service that's specified by ServiceId, a record is created or updated in the hosted zone that's associated with the corresponding namespace.   If the service includes HealthCheckConfig, a health check is created based on the settings in the health check configuration.   The health check, if any, is associated with each of the new or updated records.    One RegisterInstance request must complete before you can submit another request and specify the same service ID and instance ID.  For more information, see CreateService. When Cloud Map receives a DNS query for the specified DNS name, it returns the applicable value:    If the health check is healthy: returns all the records    If the health check is unhealthy: returns the applicable value for the last healthy instance    If you didn't specify a health check configuration: returns all the records   For the current quota on the number of instances that you can register using the same namespace and using the same service, see Cloud Map quotas in the Cloud Map Developer Guide. |
| POST | / | Adds one or more tags to the specified resource. |
| POST | / | Removes one or more tags from the specified resource. |
| POST | / | Updates an HTTP namespace. |
| POST | / | Submits a request to change the health status of a custom health check to healthy or unhealthy. You can use UpdateInstanceCustomHealthStatus to change the status only for custom health checks, which you define using HealthCheckCustomConfig when you create a service. You can't use it to change the status for Route 53 health checks, which you define using HealthCheckConfig. For more information, see HealthCheckCustomConfig. |
| POST | / | Updates a private DNS namespace. |
| POST | / | Updates a public DNS namespace. |
| POST | / | Submits a request to perform the following operations:   Update the TTL setting for existing DnsRecords configurations   Add, update, or delete HealthCheckConfig for a specified service  You can't add, update, or delete a HealthCheckCustomConfig configuration.    For public and private DNS namespaces, note the following:   If you omit any existing DnsRecords or HealthCheckConfig configurations from an UpdateService request, the configurations are deleted from the service.   If you omit an existing HealthCheckCustomConfig configuration from an UpdateService request, the configuration isn't deleted from the service.   When you update settings for a service, Cloud Map also updates the corresponding settings in all the records and health checks that were created by using the specified service. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new namespace for my microservices?" -> POST / (CreateHttpNamespace, CreatePrivateDnsNamespace, or CreatePublicDnsNamespace depending on type)
- "How do I register a service instance with its IP address?" -> POST / (RegisterInstance with ServiceId, InstanceId, and Attributes)
- "Which instances are healthy for a given service?" -> POST / (DiscoverInstances with NamespaceName, ServiceName, and HealthStatus filter)
- "What is the current status of my namespace creation?" -> POST / (GetOperation with the OperationId returned from create)
- "How do I list all namespaces in my account?" -> POST / (ListNamespaces, with optional Filters)
- "How do I remove an instance from service discovery?" -> POST / (DeregisterInstance with ServiceId and InstanceId)
- "How do I look up details about a specific service?" -> POST / (GetService with Id)
- "How do I delete a namespace I no longer need?" -> POST / (DeleteNamespace with Id)
- "How do I tag my Cloud Map resources for cost tracking?" -> POST / (TagResource with ResourceARN and Tags)
- "How do I check if a long-running operation completed?" -> POST / (GetOperation with OperationId, check Status field)
- "How do I create a service with custom health checks?" -> POST / (CreateService with HealthCheckConfig or HealthCheckCustomConfig)
- "How do I update health status for an instance manually?" -> POST / (UpdateInstanceCustomHealthStatus with ServiceId, InstanceId, Status)
- "How do I find all instances registered to a service?" -> POST / (ListInstances with ServiceId)
- "Has the set of instances changed since I last checked?" -> POST / (DiscoverInstancesRevision with NamespaceName, ServiceName -- compare InstancesRevision value)

## Response Tips

- **Async operations** (Create/Delete/Update namespace, Register/Deregister instance): Return an `OperationId` -- poll with GetOperation until `Status` is `SUCCESS` or `FAIL`. Do not assume completion on 200.
- **List endpoints** (ListNamespaces, ListServices, ListInstances, ListOperations): Paginate via `NextToken`; absence of `NextToken` in response means last page. Respect `MaxResults` (default varies).
- **DiscoverInstances**: Returns `HttpInstanceSummary` objects with attributes map -- keys like `AWS_INSTANCE_IPV4`, `AWS_INSTANCE_PORT` are conventional but user-defined.
- **GetOperation**: The `Targets` map uses string keys like `NAMESPACE`, `SERVICE`, `INSTANCE` pointing to resource IDs -- use these to correlate.
- **Error responses**: AWS standard error shape with `__type` and `message` fields. Watch for `NamespaceAlreadyExists`, `ServiceAlreadyExists`, `ResourceLimitExceeded`.

## Anomaly Flags

- **Operation stuck**: If GetOperation returns `Status: SUBMITTED` for more than 5 minutes, surface a warning -- namespace or instance operations rarely take that long.
- **Operation failed**: If `Status` is `FAIL`, immediately surface `ErrorCode` and `ErrorMessage` -- common codes are `ACCESS_DENIED` and `RESOURCE_LIMIT_EXCEEDED`.
- **ResourceLimitExceeded**: Flag when any create/register call fails with this error -- user may be hitting account-level quotas on namespaces (default 3), services (default 100 per namespace), or instances.
- **HealthStatus UNHEALTHY**: When DiscoverInstances returns instances but all have unhealthy status, proactively warn that no healthy endpoints are available for the service.
- **Empty DiscoverInstances**: If the response returns zero instances, flag that either the service has no registered instances or all are filtered out by HealthStatus -- suggest checking ListInstances to compare.
- **Deprecated DnsConfig.NamespaceId**: This field in DnsConfig is deprecated (read-only) -- flag if a user attempts to set it during CreateService.
- **CreatorRequestId reuse**: If a create call returns an existing resource instead of creating a new one, the idempotency token matched -- surface this so the user knows no new resource was created.

## Playbook

### 1. Set Up Service Discovery for a Microservice

1. Create a namespace: POST / (CreateHttpNamespace with `Name` for HTTP-only, or CreatePrivateDnsNamespace with `Name` and `Vpc` for DNS-based discovery)
2. Note the returned `OperationId` and poll with POST / (GetOperation) until `Status` is `SUCCESS`
3. Extract the namespace ID from `Operation.Targets["NAMESPACE"]`
4. Create a service: POST / (CreateService with `Name` and `NamespaceId` set to the namespace ID)
5. Register instances: POST / (RegisterInstance with `ServiceId`, a unique `InstanceId`, and `Attributes` like `{"AWS_INSTANCE_IPV4": "10.0.0.1", "AWS_INSTANCE_PORT": "8080"}`)
6. Poll the returned `OperationId` until the instance registration completes

### 2. Discover and Connect to a Service

1. Call POST / (DiscoverInstances with `NamespaceName` and `ServiceName`, optionally set `HealthStatus: "HEALTHY"` to filter)
2. Parse the `Instances` array -- each entry contains an `Attributes` map with connection details
3. Optionally pass `QueryParameters` to filter by custom attributes (e.g., `{"stage": "prod"}`)
4. Cache the `InstancesRevision` value, then periodically call POST / (DiscoverInstancesRevision) to check if instances have changed before re-fetching the full list

### 3. Implement Custom Health Checking

1. Create a service with `HealthCheckCustomConfig` and set `FailureThreshold` (e.g., 3): POST / (CreateService)
2. Register instances as normal: POST / (RegisterInstance)
3. From your application's health monitor, call POST / (UpdateInstanceCustomHealthStatus) with `Status: "HEALTHY"` or `Status: "UNHEALTHY"` for each instance
4. Cloud Map will mark instances unhealthy after the configured failure threshold of consecutive unhealthy reports

### 4. Clean Up and Tear Down Resources

1. List all instances for the service: POST / (ListInstances with `ServiceId`)
2. Deregister each instance: POST / (DeregisterInstance with `ServiceId` and `InstanceId`) -- poll each `OperationId` to confirm
3. Delete the service: POST / (DeleteService with `Id`) -- this fails if instances still exist
4. Delete the namespace: POST / (DeleteNamespace with `Id`) -- this fails if services still exist
5. Poll the returned `OperationId` until namespace deletion completes

### 5. Audit and Tag Cloud Map Resources

1. List all namespaces: POST / (ListNamespaces) -- paginate through all results
2. For each namespace, list services: POST / (ListServices with a `NamespaceFilter`)
3. Check existing tags: POST / (ListTagsForResource with the resource ARN)
4. Apply or update tags: POST / (TagResource with `ResourceARN` and `Tags` array)
5. Remove stale tags: POST / (UntagResource with `ResourceARN` and `TagKeys` to remove)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
