---
name: azurestack-azure-bridge-client
description: "AzureStack Azure Bridge Client API skill. Use when working with AzureStack Azure Bridge Client for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# AzureStack Azure Bridge Client
API version: 2017-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions | Returns a list of products. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionName} | Returns the specified product. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionName} | Deletes a customer subscription under a registration. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionName} | Creates a new customer subscription under a registration. |

## Enhanced Skill Content
## Question Mapping

- "What customer subscriptions exist under my AzureStack registration?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions
- "List all customer subscriptions for registration X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions
- "Get details for a specific customer subscription?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionName}
- "Does customer subscription Y exist in my registration?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionName}
- "How do I register a new customer subscription with AzureStack?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionName}
- "Update an existing customer subscription's parameters?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionName}
- "Remove a customer subscription from my AzureStack registration?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionName}
- "How do I clean up unused customer subscriptions?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionName}
- "How do I migrate a customer subscription to a new registration?" -> GET then PUT (read from source, create on target)
- "How do I verify a customer subscription was created successfully?" -> PUT then GET (create, then confirm)
- "How do I replace a customer subscription's configuration entirely?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionName}
- "How many customer subscriptions are linked to my registration?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions

## Response Tips

- **List endpoint**: Response is paginated via `nextLink` property -- follow it until absent to retrieve all customer subscriptions. Results are in the `value` array.
- **GET single**: Returns the full customer subscription resource including `id`, `name`, `type`, and `properties`. A 404 means the subscription name does not exist under that registration.
- **PUT create/update**: Returns the created or updated resource (200). The `customerCreationParameters` map is required in the request body -- omitting it produces a 400. This is an idempotent upsert.
- **DELETE**: Returns 200 if deleted, 204 if the resource was already absent (idempotent). No response body on 204.
- **All endpoints**: Errors follow the standard Azure error envelope: `{ "error": { "code": "...", "message": "..." } }`. Watch for 409 (conflict) on concurrent modifications.

## Anomaly Flags

- **204 on DELETE**: The customer subscription was already gone -- surface this so the caller knows they may be targeting a stale resource name.
- **Pagination truncation**: If the list response contains a `nextLink` but subsequent pages return errors, flag incomplete enumeration.
- **Missing properties bag**: If a GET response returns a customer subscription with a null or empty `properties` object, flag it as potentially orphaned or partially provisioned.
- **Slow PUT responses**: Azure Resource Manager operations can be long-running. If the response includes an `Azure-AsyncOperation` or `Location` header, surface that the operation is asynchronous and needs polling.
- **Auth token expiry**: OAuth2 tokens have finite lifetimes. Flag 401 responses with a reminder to refresh the bearer token.
- **Resource group or registration not found**: A 404 at the parent path level (registration) is distinct from a missing customer subscription -- surface which segment of the path is unresolved.

## Playbook

### 1. Onboard a New Customer Subscription

1. Confirm the target registration exists by listing current customer subscriptions under it (GET list endpoint).
2. Choose a unique `customerSubscriptionName` that does not appear in the list results.
3. Build the `customerCreationParameters` map with the required tenant and subscription details.
4. Call PUT with the chosen name and parameters.
5. Verify creation by calling GET on the new customer subscription name and confirming the returned properties match.

### 2. Audit All Customer Subscriptions

1. Call GET on the list endpoint to retrieve the first page of customer subscriptions.
2. If the response contains a `nextLink`, follow it to fetch subsequent pages. Repeat until no `nextLink` is present.
3. For each subscription in the aggregated `value` array, inspect the `properties` for status, tenant ID, and any anomalies.
4. Surface any subscriptions with null or unexpected property values for review.

### 3. Remove a Customer Subscription Safely

1. Call GET on the specific customer subscription to confirm it exists and capture its current state.
2. Optionally record or export the subscription's properties for rollback purposes.
3. Call DELETE on the customer subscription.
4. If the response is 200, deletion succeeded. If 204, the subscription was already absent -- investigate whether it was deleted by another process.
5. Confirm removal by calling GET again and verifying a 404 response.

### 4. Migrate a Customer Subscription Between Registrations

1. Call GET on the source registration's customer subscription to retrieve its full properties.
2. Extract the `customerCreationParameters` equivalent from the response properties.
3. Call PUT on the target registration with the same (or new) customer subscription name and the extracted parameters.
4. Verify the new subscription exists under the target registration via GET.
5. Call DELETE on the source registration's customer subscription to clean up.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
