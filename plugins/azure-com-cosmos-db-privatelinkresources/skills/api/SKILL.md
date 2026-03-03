---
name: cosmos-db
description: "Cosmos DB API skill. Use when working with Cosmos DB for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Cosmos DB
API version: 2019-08-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources | Gets the private link resources that need to be created for a Cosmos DB account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources/{groupName} | Gets the private link resources that need to be created for a Cosmos DB account. |

## Enhanced Skill Content
## Question Mapping

- "What private link resources are available for my Cosmos DB account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources
- "List all private endpoint group types supported by this database account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources
- "Get details about a specific private link resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources/{groupName}
- "What required members does the 'Sql' private link group have?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources/{groupName}
- "Which DNS zones do I need for private endpoints on my Cosmos DB?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources/{groupName}
- "Can my Cosmos DB account support private endpoints?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources
- "What group IDs are valid when creating a private endpoint connection?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources
- "Show me the private link configuration for the MongoDB API on my account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources/{groupName}
- "How do I find the required zone names before setting up private DNS?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources/{groupName}
- "Verify that a private link group name exists for my Cosmos DB account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources/{groupName}
- "What are all the network isolation options for my database account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources
- "Compare private link resource groups across different Cosmos DB accounts" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{accountName}/privateLinkResources (call per account)

## Response Tips

- **List endpoint**: Returns a `value` array of private link resource objects; no pagination -- all results come in a single response since group types are finite (typically Sql, MongoDB, Cassandra, Gremlin, Table).
- **Get endpoint**: Returns a single private link resource with `properties.groupId`, `properties.requiredMembers` (array of connection string components), and `properties.requiredZoneNames` (DNS zones needed for private DNS integration).
- **Errors**: 4xx responses follow Azure ARM error format with `error.code` and `error.message`; 404 means the groupName is invalid for that account's API type. 401/403 indicate OAuth token issues or missing RBAC role (Reader minimum required).

## Anomaly Flags

- **Empty `value` array on list**: The account may not support private link (older SKU or unsupported region) -- surface this to the user immediately.
- **404 on group name lookup**: The requested groupName likely doesn't match the account's API kind (e.g., requesting "MongoDB" on a SQL API account) -- suggest listing all available groups first.
- **Preview API version (2019-08-01-preview)**: This is a preview version; behavior may change. Surface a note that stable API versions may be available and recommend checking for GA releases.
- **Missing `requiredZoneNames`**: If the field is empty or absent, private DNS zone setup cannot be automated -- flag this as requiring manual DNS configuration.
- **Throttling (429)**: Azure ARM applies subscription-level read throttling (12000 reads/hour); if responses include `Retry-After` headers, surface the wait time and remaining quota.

## Playbook

### 1. Discover Private Link Groups Before Creating a Private Endpoint

1. Call GET `.../privateLinkResources` to list all supported groups for the account.
2. Note the `groupId` values returned (e.g., "Sql", "MongoDB").
3. Pick the `groupId` matching your connectivity need.
4. Call GET `.../privateLinkResources/{groupName}` with that group ID.
5. Record `requiredMembers` and `requiredZoneNames` from the response.
6. Use these values when creating the private endpoint connection and DNS zone via the networking APIs.

### 2. Set Up Private DNS Zones for a Cosmos DB Private Endpoint

1. Call GET `.../privateLinkResources/{groupName}` for your target group (e.g., "Sql").
2. Extract the `requiredZoneNames` array from the response (e.g., `privatelink.documents.azure.com`).
3. For each zone name, create a Private DNS Zone in your resource group via Azure DNS APIs.
4. Link each DNS zone to the virtual network where your private endpoint resides.
5. After creating the private endpoint, verify DNS records resolve correctly.

### 3. Validate Private Link Support Across Multiple Accounts

1. Gather a list of Cosmos DB account names and their resource groups.
2. For each account, call GET `.../privateLinkResources`.
3. If the `value` array is non-empty, the account supports private link.
4. Compare the `groupId` values across accounts to confirm consistent API types.
5. Flag any accounts returning empty arrays for manual review or upgrade.

### 4. Troubleshoot a Failed Private Endpoint Connection

1. Call GET `.../privateLinkResources` to confirm the account supports private link at all.
2. Call GET `.../privateLinkResources/{groupName}` with the group used in the failed connection.
3. If 404: the group ID is wrong for this account type -- list available groups and correct.
4. If 200: verify that `requiredMembers` matches what was configured in the private endpoint.
5. Check that DNS zones from `requiredZoneNames` exist and are linked to the correct VNet.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
