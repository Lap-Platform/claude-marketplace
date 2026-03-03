---
name: datalakeanalyticsaccountmanagementclient
description: "DataLakeAnalyticsAccountManagementClient API skill. Use when working with DataLakeAnalyticsAccountManagementClient for subscriptions, providers. Covers 31 endpoints."
version: 1.0.0
generator: lapsh
---

# DataLakeAnalyticsAccountManagementClient
API version: 2016-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.DataLakeAnalytics/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/storageAccounts/{storageAccountName}/containers/{containerName}/listSasTokens -- create first listSasTokens

## Endpoints

31 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.DataLakeAnalytics/accounts | Gets the first page of Data Lake Analytics accounts, if any, within the current subscription. This includes a link to the next page, if any. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts | Gets the first page of Data Lake Analytics accounts, if any, within a specific resource group. This includes a link to the next page, if any. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName} | Creates the specified Data Lake Analytics account. This supplies the user with computation services for Data Lake Analytics workloads. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName} | Gets details of the specified Data Lake Analytics account. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName} | Updates the Data Lake Analytics account object specified by the accountName with the contents of the account object. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName} | Begins the delete process for the Data Lake Analytics account object specified by the account name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/dataLakeStoreAccounts | Gets the first page of Data Lake Store accounts linked to the specified Data Lake Analytics account. The response includes a link to the next page, if any. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/dataLakeStoreAccounts/{dataLakeStoreAccountName} | Updates the specified Data Lake Analytics account to include the additional Data Lake Store account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/dataLakeStoreAccounts/{dataLakeStoreAccountName} | Gets the specified Data Lake Store account details in the specified Data Lake Analytics account. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/dataLakeStoreAccounts/{dataLakeStoreAccountName} | Updates the Data Lake Analytics account specified to remove the specified Data Lake Store account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/storageAccounts | Gets the first page of Azure Storage accounts, if any, linked to the specified Data Lake Analytics account. The response includes a link to the next page, if any. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/storageAccounts/{storageAccountName} | Updates the specified Data Lake Analytics account to add an Azure Storage account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/storageAccounts/{storageAccountName} | Gets the specified Azure Storage account linked to the given Data Lake Analytics account. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/storageAccounts/{storageAccountName} | Updates the Data Lake Analytics account to replace Azure Storage blob account details, such as the access key and/or suffix. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/storageAccounts/{storageAccountName} | Updates the specified Data Lake Analytics account to remove an Azure Storage account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/storageAccounts/{storageAccountName}/containers | Lists the Azure Storage containers, if any, associated with the specified Data Lake Analytics and Azure Storage account combination. The response includes a link to the next page of results, if any. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/storageAccounts/{storageAccountName}/containers/{containerName} | Gets the specified Azure Storage container associated with the given Data Lake Analytics and Azure Storage accounts. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/storageAccounts/{storageAccountName}/containers/{containerName}/listSasTokens | Gets the SAS token associated with the specified Data Lake Analytics and Azure Storage account and container combination. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/computePolicies | Lists the Data Lake Analytics compute policies within the specified Data Lake Analytics account. An account supports, at most, 50 policies |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/computePolicies/{computePolicyName} | Creates or updates the specified compute policy. During update, the compute policy with the specified name will be replaced with this new compute policy. An account supports, at most, 50 policies |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/computePolicies/{computePolicyName} | Gets the specified Data Lake Analytics compute policy. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/computePolicies/{computePolicyName} | Updates the specified compute policy. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/computePolicies/{computePolicyName} | Deletes the specified compute policy from the specified Data Lake Analytics account |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/firewallRules | Lists the Data Lake Analytics firewall rules within the specified Data Lake Analytics account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/firewallRules/{firewallRuleName} | Creates or updates the specified firewall rule. During update, the firewall rule with the specified name will be replaced with this new firewall rule. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/firewallRules/{firewallRuleName} | Gets the specified Data Lake Analytics firewall rule. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/firewallRules/{firewallRuleName} | Updates the specified firewall rule. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/firewallRules/{firewallRuleName} | Deletes the specified firewall rule from the specified Data Lake Analytics account |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.DataLakeAnalytics/locations/{location}/capability | Gets subscription-level properties and limits for Data Lake Analytics specified by resource location. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.DataLakeAnalytics/locations/{location}/checkNameAvailability | Checks whether the specified account name is available or taken. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.DataLakeAnalytics/operations | Lists all of the available Data Lake Analytics REST API operations. |

## Enhanced Skill Content
## Question Mapping

- "What Data Lake Analytics accounts exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DataLakeAnalytics/accounts
- "List all Data Lake Analytics accounts in a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts
- "How do I create a new Data Lake Analytics account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}
- "Get details of a specific Data Lake Analytics account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}
- "How do I delete a Data Lake Analytics account?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}
- "What Data Lake Store accounts are linked to my analytics account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/dataLakeStoreAccounts
- "How do I add an Azure Storage account as a data source?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/storageAccounts/{storageAccountName}
- "How do I get a SAS token for a storage container?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/storageAccounts/{storageAccountName}/containers/{containerName}/listSasTokens
- "What compute policies are configured on my account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/computePolicies
- "How do I add a firewall rule to my Data Lake Analytics account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/firewallRules/{firewallRuleName}
- "Is this account name available in my region?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.DataLakeAnalytics/locations/{location}/checkNameAvailability
- "What Data Lake Analytics capabilities are available in a given region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DataLakeAnalytics/locations/{location}/capability
- "What operations does the Data Lake Analytics resource provider support?" -> GET /providers/Microsoft.DataLakeAnalytics/operations
- "How do I list storage containers linked to my analytics account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/storageAccounts/{storageAccountName}/containers
- "How do I update compute policy limits without recreating the policy?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataLakeAnalytics/accounts/{accountName}/computePolicies/{computePolicyName}

## Response Tips

- **Account listings** (`GET .../accounts`): Paginated via `nextLink`; use `$top`, `$skip`, and `$filter` OData params to control page size and filtering. The `$count` param returns total count alongside results.
- **Create/Update accounts** (`PUT`/`PATCH .../accounts/{accountName}`): 200 means completed synchronously; 201/202 means the operation is asynchronous -- poll the `Location` or `Azure-AsyncOperation` header URL until terminal state.
- **Delete operations** (`DELETE`): 200 = deleted, 202 = deletion in progress (poll async), 204 = resource already gone (idempotent, not an error).
- **SAS token listing** (`POST .../listSasTokens`): Returns an array of token objects; tokens are time-bound so check expiry fields before use.
- **Location capability** (`GET .../capability`): 404 means the region does not support Data Lake Analytics at all -- not a transient error.
- **Name availability** (`POST .../checkNameAvailability`): Response includes `nameAvailable` boolean and a `reason`/`message` when unavailable.

## Anomaly Flags

- **202 Accepted on create/update/delete**: The operation is long-running. Surface the async operation URL and remind the user to poll for completion status before assuming success.
- **204 on delete**: The resource was already absent. Flag this if the user expected the resource to exist, as it may indicate a naming mismatch or prior deletion.
- **404 on location capability**: The requested Azure region does not support Data Lake Analytics. Proactively suggest checking supported regions.
- **OData filter/pagination ignored**: If a list call returns more items than `$top` specified, or filtering appears ineffective, flag possible server-side OData support limitations.
- **API version drift**: This spec targets `2016-11-01`. If Azure returns errors about unsupported API versions, surface that the client may need updating to a newer API version.
- **Provisioning state not "Succeeded"**: After account creation (201), the account may be in a `Creating` or `Failed` provisioning state. Alert the user if GET on the account shows a non-terminal state.
- **Firewall rule conflicts**: When adding firewall rules, flag if the IP range overlaps with or contradicts existing rules that could lock out access.

## Playbook

### 1. Create a New Data Lake Analytics Account

1. Check name availability: `POST .../locations/{location}/checkNameAvailability` with the desired account name
2. Verify the response `nameAvailable` is `true`; if not, choose a different name based on the `reason` field
3. Create the account: `PUT .../accounts/{accountName}` with required `parameters` body (location, default Data Lake Store, etc.)
4. If response is 201, poll the async operation URL from the response headers until provisioning completes
5. Confirm creation: `GET .../accounts/{accountName}` and verify `provisioningState` is `Succeeded`

### 2. Link Storage and Generate SAS Tokens

1. Add a storage account: `PUT .../accounts/{accountName}/storageAccounts/{storageAccountName}` with access key in `parameters`
2. List containers: `GET .../storageAccounts/{storageAccountName}/containers`
3. Pick the target container and generate SAS tokens: `POST .../containers/{containerName}/listSasTokens`
4. Use the returned SAS token for data access within its validity window

### 3. Configure Network Security with Firewall Rules

1. List existing rules: `GET .../accounts/{accountName}/firewallRules`
2. Create a new rule: `PUT .../firewallRules/{firewallRuleName}` with `startIpAddress` and `endIpAddress` in the parameters body
3. Verify the rule: `GET .../firewallRules/{firewallRuleName}`
4. To modify the range later: `PATCH .../firewallRules/{firewallRuleName}` with updated IP range
5. To remove access: `DELETE .../firewallRules/{firewallRuleName}`

### 4. Set Up Compute Policies for Job Governance

1. List current policies: `GET .../accounts/{accountName}/computePolicies`
2. Create a policy: `PUT .../computePolicies/{computePolicyName}` with `objectId`, `objectType`, and limits (`maxDegreeOfParallelismPerJob`, `minPriorityPerJob`) in the parameters body
3. Verify: `GET .../computePolicies/{computePolicyName}`
4. Adjust limits as needed: `PATCH .../computePolicies/{computePolicyName}` with updated parameters
5. Remove a policy when no longer needed: `DELETE .../computePolicies/{computePolicyName}`

### 5. Audit and Inventory All Accounts Across Subscription

1. List all accounts subscription-wide: `GET .../providers/Microsoft.DataLakeAnalytics/accounts` with `$select` to limit returned fields
2. Page through results using `$top` and `$skip` if the account count exceeds a single page
3. For each account, get details: `GET .../accounts/{accountName}` to inspect provisioning state, linked stores, and configuration
4. List linked Data Lake Store accounts: `GET .../accounts/{accountName}/dataLakeStoreAccounts`
5. List linked Storage accounts: `GET .../accounts/{accountName}/storageAccounts`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
