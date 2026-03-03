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
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans | Get a collection of all acquired plans that subscription has access to. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans/{planAcquisitionId} | Gets the specified plan acquired by a subscription consuming the offer. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans/{planAcquisitionId} | Deletes an acquired plan. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans/{planAcquisitionId} | Creates an acquired plan. |

## Enhanced Skill Content
## Question Mapping

- "What plans has this subscription acquired?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans
- "List all acquired plans for subscription X" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans
- "Show me the details of a specific acquired plan" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans/{planAcquisitionId}
- "Look up acquired plan by its acquisition ID" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans/{planAcquisitionId}
- "Remove an acquired plan from a subscription" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans/{planAcquisitionId}
- "Delete plan acquisition for a target subscription" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans/{planAcquisitionId}
- "Assign a plan to a subscription" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans/{planAcquisitionId}
- "Create a new plan acquisition for subscription X" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans/{planAcquisitionId}
- "Update an existing acquired plan definition" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans/{planAcquisitionId}
- "Does subscription X have plan Y?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans then filter results
- "How many plans are acquired under this subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans
- "Replace the definition of an acquired plan" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans/{planAcquisitionId}
- "Clean up all acquired plans for a decommissioned subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/subscriptions/{targetSubscriptionId}/acquiredPlans then DELETE each

## Response Tips

- **List acquired plans (GET collection):** Returns 200 with an array; check for `nextLink` property for pagination across large plan sets. Results may be wrapped in a `value` array.
- **Get single plan (GET by ID):** Returns 200 with the full plan acquisition object; a 404 means the planAcquisitionId is invalid or the plan was already removed.
- **Delete plan (DELETE):** Returns 200 if the resource was deleted, 204 if it was already absent (idempotent). Treat both as success.
- **Create/Update plan (PUT):** Returns 201 for newly created acquisitions, 200 for updates to existing ones. The `acquiredPlanDefinition` map in the request body defines the plan properties. Inspect the response body to confirm the final state.

## Anomaly Flags

- **204 on DELETE without prior confirmation:** Surface when a delete returns 204 (resource already gone) as the plan may have been removed by another process or admin.
- **201 vs 200 on PUT:** Flag when a PUT returns 201 unexpectedly, indicating a new resource was created rather than updating an existing one -- the planAcquisitionId may not have matched.
- **OAuth2 token expiry:** Proactively warn when repeated 401 responses occur, suggesting the OAuth2 token needs refresh.
- **Mismatched subscriptionId and targetSubscriptionId:** Surface when both IDs are identical, as the admin context subscription and the target subscription are typically different in Azure Stack scenarios.
- **Large plan lists without pagination:** If the list endpoint returns a high count without a `nextLink`, flag that all results were returned in a single page which may indicate an unusually broad query.
- **5xx from Azure Resource Manager:** Surface Azure-side errors (500, 502, 503) with retry guidance, as these are often transient in the management plane.

## Playbook

### 1. Audit All Acquired Plans for a Subscription

1. Call GET on the acquired plans collection with the target subscription ID.
2. If the response contains a `nextLink`, follow it to retrieve additional pages.
3. For each plan in the results, note the `planAcquisitionId` and plan properties.
4. Optionally call GET on each individual plan to retrieve full details.
5. Compile the list for review or export.

### 2. Provision a New Plan for a Subscription

1. Determine the `planAcquisitionId` to use (generate or use a known identifier).
2. Build the `acquiredPlanDefinition` map with the required plan properties.
3. Call PUT with the target subscription ID, plan acquisition ID, and definition body.
4. Confirm the response is 201 (created). If 200, the plan already existed and was updated.
5. Call GET on the specific plan to verify the final persisted state.

### 3. Remove a Plan Acquisition

1. Call GET on the specific acquired plan to confirm it exists and review its details.
2. Call DELETE with the target subscription ID and plan acquisition ID.
3. If 200 is returned, the plan was successfully removed. If 204, it was already absent.
4. Optionally call GET on the plan to confirm a 404 is returned, verifying deletion.

### 4. Migrate Plans Between Subscriptions

1. Call GET on the acquired plans collection for the source target subscription.
2. For each plan, capture the full plan definition from the response body.
3. For each plan, call PUT on the destination target subscription with the same `acquiredPlanDefinition`.
4. Confirm each PUT returns 200 or 201.
5. Once all plans are confirmed on the destination, call DELETE for each plan on the source subscription.
6. Verify the source subscription's plan list is empty with a final GET.

### 5. Update an Existing Plan Definition

1. Call GET on the specific acquired plan to retrieve the current definition.
2. Modify the desired fields in the `acquiredPlanDefinition` map.
3. Call PUT with the updated definition, using the same target subscription and plan acquisition IDs.
4. Confirm the response is 200 (updated, not 201 which would indicate a new resource).
5. Call GET again to verify the changes were applied correctly.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
