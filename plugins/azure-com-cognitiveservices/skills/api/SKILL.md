---
name: cognitiveservicesmanagementclient
description: "CognitiveServicesManagementClient API skill. Use when working with CognitiveServicesManagementClient for subscriptions, providers. Covers 19 endpoints."
version: 1.0.0
generator: lapsh
---

# CognitiveServicesManagementClient
API version: 2017-04-18

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.CognitiveServices/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/listKeys -- create first listKeys

## Endpoints

19 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName} | Create Cognitive Services Account. Accounts is a resource group wide resource type. It holds the keys for developer to access intelligent APIs. It's also the resource type for billing. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName} | Updates a Cognitive Services account |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName} | Deletes a Cognitive Services account from the resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName} | Returns a Cognitive Services account specified by the parameters. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts | Returns all the resources of a particular type belonging to a resource group |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.CognitiveServices/accounts | Returns all the resources of a particular type belonging to a subscription. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/listKeys | Lists the account keys for the specified Cognitive Services account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/regenerateKey | Regenerates the specified account key for the specified Cognitive Services account. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.CognitiveServices/skus | Gets the list of Microsoft.CognitiveServices SKUs available for your Subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/skus | List available SKUs for the requested Cognitive Services account |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/usages | Get usages for the requested Cognitive Services account |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.CognitiveServices/locations/{location}/checkSkuAvailability | Check available SKUs. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.CognitiveServices/checkDomainAvailability | Check whether a domain is available. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/privateEndpointConnections | Gets the private endpoint connections associated with the Cognitive Services account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName} | Gets the specified private endpoint connection associated with the Cognitive Services account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName} | Update the state of specified private endpoint connection associated with the Cognitive Services account. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName} | Deletes the specified private endpoint connection associated with the Cognitive Services account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/privateLinkResources | Gets the private link resources that need to be created for a Cognitive Services account. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.CognitiveServices/operations | Lists all the available Cognitive Services account operations. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new Cognitive Services account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}
- "How do I update an existing Cognitive Services account?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}
- "How do I delete a Cognitive Services account?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}
- "How do I get details for a specific Cognitive Services account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}
- "How do I list all Cognitive Services accounts in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts
- "How do I list all Cognitive Services accounts in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.CognitiveServices/accounts
- "How do I get the access keys for my Cognitive Services account?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/listKeys
- "How do I rotate or regenerate an access key?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/regenerateKey
- "What SKUs are available for Cognitive Services in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.CognitiveServices/skus
- "What SKUs are available for a specific account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/skus
- "How do I check current usage and quotas for my account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/usages
- "Is a specific SKU available in my region?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.CognitiveServices/locations/{location}/checkSkuAvailability
- "Is a custom domain name available?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.CognitiveServices/checkDomainAvailability
- "How do I set up a private endpoint connection for my account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/privateEndpointConnections/{privateEndpointConnectionName}
- "What operations does the Cognitive Services resource provider support?" -> GET /providers/Microsoft.CognitiveServices/operations

## Response Tips

- **Account CRUD (PUT/PATCH/DELETE):** 202 means the operation is async -- check the `Location` or `Azure-AsyncOperation` header to poll for completion. 204 on DELETE means the resource was already gone.
- **List endpoints (GET .../accounts):** Responses return a `value` array with `nextLink` for pagination. Keep following `nextLink` until it is null or absent.
- **Keys (listKeys/regenerateKey):** Response contains `key1` and `key2` at the top level. After regenerateKey, only the targeted key changes; the other stays the same.
- **SKUs and usages:** SKU responses nest under `value[]` with `resourceType` and `name`. Usage entries include `currentValue`, `limit`, and `unit` -- compare `currentValue` to `limit` for quota health.
- **Availability checks:** Both checkSkuAvailability and checkDomainAvailability return a boolean `isAvailable` plus a `reason` and `message` when unavailable.
- **Private endpoints:** Responses include a `properties.privateLinkServiceConnectionState` object with `status` (Pending/Approved/Rejected) and `description`.

## Anomaly Flags

- **Async operations (202 responses):** Surface when a PUT, PATCH, or DELETE returns 202 instead of 200 -- the caller must poll for completion and should not assume the operation succeeded immediately.
- **Usage approaching quota:** When `currentValue` exceeds 80% of `limit` on any usage metric, proactively warn that throttling or rejection may occur.
- **SKU unavailability:** If checkSkuAvailability returns `isAvailable: false`, surface the `reason` and `message` before the user attempts to create an account with that SKU.
- **Private endpoint in Pending state:** Flag when a private endpoint connection has `status: Pending` -- it requires manual approval before traffic flows.
- **Domain already taken:** When checkDomainAvailability returns `isAvailable: false`, alert immediately rather than letting a create call fail.
- **API version 2017-04-18:** This is a legacy API version. Surface a note that newer API versions may offer additional features (e.g., managed identity, network rules, commitment plans).

## Playbook

### 1. Provision a New Cognitive Services Account

1. Check SKU availability: POST `.../locations/{location}/checkSkuAvailability` with desired SKU and kind.
2. Optionally check custom domain: POST `.../checkDomainAvailability` if using a custom subdomain.
3. Create the account: PUT `.../accounts/{accountName}` with the `account` body including `sku`, `kind`, `location`, and `properties`.
4. If you receive 202, poll the async operation URL from the response header until the provisioning state is `Succeeded`.
5. Retrieve access keys: POST `.../accounts/{accountName}/listKeys`.

### 2. Rotate Access Keys Without Downtime

1. List current keys: POST `.../accounts/{accountName}/listKeys` -- note `key1` and `key2`.
2. Update all consuming applications to use `key2` (the key you are not rotating).
3. Regenerate `key1`: POST `.../accounts/{accountName}/regenerateKey` with `{"keyName": "Key1"}`.
4. Verify new key works by calling the Cognitive Services endpoint with the new `key1`.
5. Optionally update applications back to `key1`, then repeat for `key2` if both need rotation.

### 3. Set Up Private Endpoint Access

1. Get available private link resources: GET `.../accounts/{accountName}/privateLinkResources` to find supported group IDs.
2. Create or update the private endpoint connection: PUT `.../accounts/{accountName}/privateEndpointConnections/{connectionName}` with connection state set to `Approved`.
3. Verify the connection: GET `.../accounts/{accountName}/privateEndpointConnections/{connectionName}` and confirm `status` is `Approved`.
4. Optionally disable public network access by updating the account: PATCH `.../accounts/{accountName}` with `properties.publicNetworkAccess: "Disabled"`.

### 4. Audit All Accounts Across a Subscription

1. List all accounts: GET `.../providers/Microsoft.CognitiveServices/accounts` (subscription-wide).
2. For each account, fetch usage: GET `.../accounts/{accountName}/usages` to check quota consumption.
3. For each account, check SKU fit: GET `.../accounts/{accountName}/skus` to see available upgrade/downgrade options.
4. Flag any accounts where usage exceeds 80% of quota limits for review.
5. Flag any accounts with private endpoint connections in `Pending` state.

### 5. Decommission a Cognitive Services Account

1. List private endpoint connections: GET `.../accounts/{accountName}/privateEndpointConnections`.
2. Delete each private endpoint connection: DELETE `.../accounts/{accountName}/privateEndpointConnections/{connectionName}`.
3. Retrieve and revoke keys: POST `.../accounts/{accountName}/listKeys`, then update all consumers to stop using them.
4. Delete the account: DELETE `.../accounts/{accountName}`.
5. If you receive 202, poll the async operation until deletion completes. A 204 confirms the resource is gone.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
