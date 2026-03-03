---
name: subscriptionsmanagementclient
description: "SubscriptionsManagementClient API skill. Use when working with SubscriptionsManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionsManagementClient
API version: 2015-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations | Get the list of offer delegations. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations/{offerDelegationName} | Get the specified offer delegation. |
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations/{offerDelegationName} | Create or update the offer delegation. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations/{offerDelegationName} | Delete the specified offer delegation. |

## Enhanced Skill Content
## Question Mapping

- "What offer delegations exist for this offer?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations
- "List all delegations under offer X in resource group Y?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations
- "Get details of a specific offer delegation?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations/{offerDelegationName}
- "Does delegation Z exist on this offer?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations/{offerDelegationName}
- "Create a new offer delegation?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations/{offerDelegationName}
- "Update an existing offer delegation's definition?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations/{offerDelegationName}
- "Assign a delegated provider to an offer?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations/{offerDelegationName}
- "Remove an offer delegation?" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations/{offerDelegationName}
- "Revoke a delegated provider's access to an offer?" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations/{offerDelegationName}
- "Replace the full definition of a delegation?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations/{offerDelegationName}
- "Check if a delegation was already cleaned up?" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations/{offerDelegationName}
- "How many delegations does an offer have?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/offers/{offer}/offerDelegations

## Response Tips

- **List (GET collection):** Response is a JSON object with a `value` array; check for `nextLink` property for pagination across large delegation sets.
- **Get single (GET by name):** Returns the full delegation resource object including `properties`, `id`, `name`, and `type` fields; a 404 means the delegation does not exist.
- **Create/Update (PUT):** Returns 200 if the delegation was updated in place, 201 if a new delegation was created -- branch logic on status code to distinguish create vs update.
- **Delete (DELETE):** Returns 200 if the resource was deleted, 204 if it was already gone (idempotent) -- treat both as success without re-checking.

## Anomaly Flags

- **404 on GET single:** The offer delegation name may be misspelled or the parent offer/resource group path is wrong -- surface the full resource path for the user to verify.
- **409 Conflict on PUT:** Another operation may be in progress on the same delegation; retry after a short delay.
- **201 vs 200 on PUT:** If the caller expected an update but got 201, a new resource was created unexpectedly -- flag that the delegation name may not have matched an existing one.
- **204 on DELETE:** The resource was already absent; surface this as informational since it may indicate a stale reference or duplicate cleanup attempt.
- **Azure throttling (429):** Surface `Retry-After` header value and pause before retrying; Azure ARM has per-subscription rate limits that can silently queue requests.
- **Auth errors (401/403):** OAuth2 token may be expired or the service principal lacks the `Microsoft.Subscriptions.Admin` provider permissions -- prompt re-authentication or role check.

## Playbook

### 1. Delegate an Offer to a Provider

1. Confirm the target offer exists by listing its current delegations: GET the collection endpoint.
2. Construct the `offerDelegationDefinition` map with the delegated provider's subscription ID and any scope restrictions.
3. PUT the new delegation using a descriptive `offerDelegationName`.
4. Verify creation succeeded by checking for a 201 status code.
5. GET the delegation by name to confirm the stored properties match intent.

### 2. Audit All Delegations on an Offer

1. GET the delegations collection for the target offer.
2. If the response contains a `nextLink`, follow it to retrieve all pages.
3. For each delegation in the `value` array, extract `properties.subscriptionId` and delegation scope.
4. Compile results into a summary, flagging any delegations to unexpected or unknown providers.

### 3. Revoke a Delegation

1. GET the specific delegation by name to confirm it exists and capture its current definition.
2. DELETE the delegation by name.
3. If the response is 200, the delegation was actively removed. If 204, it was already gone.
4. Re-list the collection to verify the delegation no longer appears.

### 4. Update a Delegation's Definition

1. GET the existing delegation by name to retrieve its current `offerDelegationDefinition`.
2. Modify the relevant fields in the definition map (e.g., change scope or provider reference).
3. PUT the updated delegation using the same `offerDelegationName`.
4. Confirm a 200 response (update) rather than 201 (accidental create under a different name).
5. GET the delegation again to verify the changes persisted correctly.

### 5. Clean Up All Delegations Before Retiring an Offer

1. GET the full delegations collection, following any `nextLink` pagination.
2. For each delegation, issue a DELETE call by name.
3. Collect status codes: 200 = deleted, 204 = already absent.
4. After all deletes complete, GET the collection once more to confirm the `value` array is empty.
5. Proceed with offer retirement knowing no orphaned delegations remain.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
