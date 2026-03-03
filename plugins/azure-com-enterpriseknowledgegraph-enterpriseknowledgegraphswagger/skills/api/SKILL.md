---
name: azure-enterprise-knowledge-graph-service
description: "Azure Enterprise Knowledge Graph Service API skill. Use when working with Azure Enterprise Knowledge Graph Service for subscriptions, providers. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# Azure Enterprise Knowledge Graph Service
API version: 2018-12-03

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.EnterpriseKnowledgeGraph/operations -- verify access

## Endpoints

7 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName} | Creates a EnterpriseKnowledgeGraph Service. EnterpriseKnowledgeGraph Service is a resource group wide resource type. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName} | Updates a EnterpriseKnowledgeGraph Service |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName} | Deletes a EnterpriseKnowledgeGraph Service from the resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName} | Returns a EnterpriseKnowledgeGraph service specified by the parameters. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services | Returns all the resources of a particular type belonging to a resource group |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.EnterpriseKnowledgeGraph/services | Returns all the resources of a particular type belonging to a subscription. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.EnterpriseKnowledgeGraph/operations | Lists all the available EnterpriseKnowledgeGraph services operations. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new Enterprise Knowledge Graph service?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName}
- "How do I update an existing Knowledge Graph service?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName}
- "How do I delete a Knowledge Graph service?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName}
- "How do I get details about a specific Knowledge Graph service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName}
- "How do I list all Knowledge Graph services in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services
- "How do I list all Knowledge Graph services in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.EnterpriseKnowledgeGraph/services
- "What operations are available for the Enterprise Knowledge Graph provider?" -> GET /providers/Microsoft.EnterpriseKnowledgeGraph/operations
- "How do I replace the full configuration of a Knowledge Graph service?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName}
- "How do I partially update a Knowledge Graph service without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName}
- "How do I check if a Knowledge Graph service exists?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName}
- "How do I migrate a Knowledge Graph service by recreating it?" -> DELETE then PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName}
- "How do I audit which Knowledge Graph services exist across all my resource groups?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.EnterpriseKnowledgeGraph/services

## Response Tips

- **CRUD operations (PUT/PATCH):** 200 means the resource was updated in place; 201 means a new resource was created. Check the response body for the final provisioning state.
- **DELETE:** 200 confirms deletion completed; 204 means the resource was already gone (idempotent). Both are success cases.
- **GET (single resource):** Returns the full resource object including properties, SKU, tags, and provisioning state. A missing resource returns 404 with an Azure error envelope.
- **GET (list endpoints):** Returns a `value` array of resources. May include a `nextLink` property for pagination -- follow it with subsequent GET requests until `nextLink` is absent.
- **Operations list:** Returns available ARM operations with display metadata. Use this to validate RBAC permissions before attempting resource modifications.
- **All endpoints:** Errors follow the Azure error envelope format (`error.code`, `error.message`). Always include `api-version=2018-12-03` as a query parameter.

## Anomaly Flags

- **Provisioning state not "Succeeded":** After PUT or PATCH, if the returned `properties.provisioningState` is "Failed" or "Canceled", surface this immediately -- the operation did not complete as expected.
- **204 on DELETE:** While valid, a 204 indicates the resource was already absent. Flag this if the caller expected the resource to exist.
- **Missing `nextLink` awareness:** If a list response contains a `nextLink` but only partial results were processed, warn that not all services have been retrieved.
- **Deprecated API version:** The spec uses `2018-12-03`. If Azure returns a warning header about newer API versions, surface the recommendation to upgrade.
- **Throttling (429):** Azure ARM endpoints enforce rate limits. If a 429 response or `Retry-After` header appears, surface the wait time and pause before retrying.
- **Unexpected 404 on GET:** If a service that was recently created returns 404, flag a possible propagation delay or incorrect resource group / service name.

## Playbook

### 1. Provision a New Knowledge Graph Service

1. Call GET on the subscription-level list to confirm the service name is not already in use.
2. Call PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName}` with the full `parameters` body (SKU, location, tags, properties).
3. Check the response: 201 confirms creation started.
4. Poll with GET on the specific resource until `provisioningState` equals "Succeeded".
5. On failure, inspect `provisioningState` for "Failed" and review the error details.

### 2. Update Service Configuration

1. Call GET on the specific resource to retrieve its current state.
2. Identify the properties to change and construct a partial update body.
3. Call PATCH `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName}` with only the changed fields.
4. Verify the response (200 or 201) and confirm updated properties in the returned body.

### 3. Decommission a Knowledge Graph Service

1. Call GET on the specific resource to confirm it exists and capture its current state for audit.
2. Call DELETE `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.EnterpriseKnowledgeGraph/services/{resourceName}`.
3. Expect 200 (deleted) or 204 (already absent).
4. Optionally call GET to confirm the resource returns 404.

### 4. Inventory All Knowledge Graph Services Across a Subscription

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.EnterpriseKnowledgeGraph/services` to list all services.
2. If the response contains a `nextLink`, follow it with additional GET requests until no `nextLink` is returned.
3. Aggregate the `value` arrays from all pages into a complete inventory.
4. For each service, note its resource group, location, SKU, and provisioning state.

### 5. Validate Permissions Before Operating

1. Call GET `/providers/Microsoft.EnterpriseKnowledgeGraph/operations` to retrieve all supported operations.
2. Cross-reference the operation names with the caller's RBAC role assignments.
3. If the required operation (e.g., `Microsoft.EnterpriseKnowledgeGraph/services/write`) is missing from the caller's permissions, surface the gap before attempting the action.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
