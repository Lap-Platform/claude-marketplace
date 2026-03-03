---
name: azure-addons-resource-provider
description: "Azure Addons Resource Provider API skill. Use when working with Azure Addons Resource Provider for providers, subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Azure Addons Resource Provider
API version: 2018-03-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Addons/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/canonical/listSupportPlanInfo -- create first listSupportPlanInfo

## Endpoints

5 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Addons/operations | Lists all of the available Addons RP operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName} | Returns whether or not the canonical support plan of type {type} is enabled for the subscription. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName} | Creates or updates the Canonical support plan of type {type} for the subscription. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName} | Cancels the Canonical support plan of type {type} for the subscription. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/canonical/listSupportPlanInfo | Returns the canonical support plan information for all types for the subscription. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for the Addons resource provider?" -> GET /providers/Microsoft.Addons/operations
- "How do I check my current support plan?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "What support plan type is active for a specific provider?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "How do I create a new support plan?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "How do I update an existing support plan?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "How do I remove a support plan from my subscription?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "How do I cancel a support plan?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "What support plans are available from the canonical provider?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/canonical/listSupportPlanInfo
- "How do I list all support plan info for my subscription?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/canonical/listSupportPlanInfo
- "Does a specific support plan exist for my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "How do I switch from one support plan to another?" -> PUT (create new) then DELETE (remove old) on /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "What API version should I use for Addons operations?" -> GET /providers/Microsoft.Addons/operations (inspect api-version values)

## Response Tips

- **Operations (GET /providers/.../operations):** Returns a list of available ARM operations; each entry includes name, display info, and whether it is a data action.
- **Support plan GET:** 200 returns the full plan object; 404 means the plan type does not exist for that provider/subscription combo -- check providerName and planTypeName spelling.
- **Support plan PUT:** 200 means an existing plan was updated; 201 means a new plan was created -- check the status code to distinguish create vs update.
- **Support plan DELETE:** 202 means deletion is accepted and processing asynchronously (check Location/Azure-AsyncOperation headers); 204 means the resource was already gone -- both are success.
- **List support plan info (POST):** Returns an array of available plan metadata; 404 means the subscription ID is invalid or the subscription is not registered with Microsoft.Addons.

## Anomaly Flags

- **404 on GET/PUT/POST:** Surface immediately -- likely indicates an unregistered subscription or misspelled providerName/planTypeName. Suggest running `GET /providers/Microsoft.Addons/operations` to verify the provider is available.
- **202 on DELETE without async headers:** If the response lacks `Location` or `Azure-AsyncOperation` headers, flag that deletion status cannot be tracked.
- **api-version mismatch:** If the server returns an error about unsupported api-version, surface available versions and recommend `2018-03-01`.
- **Subscription not registered:** If multiple endpoints return 404, proactively suggest registering the subscription with the Microsoft.Addons resource provider via `PUT /subscriptions/{id}/providers/Microsoft.Addons/register`.
- **201 on PUT when 200 was expected:** Flag when a plan was unexpectedly created rather than updated -- the user may have targeted the wrong planTypeName.

## Playbook

### 1. Check and create a support plan

1. Call `POST /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/canonical/listSupportPlanInfo` to see available plans.
2. Pick the desired `providerName` and `planTypeName` from the response.
3. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}` to check if it already exists.
4. If 404, call `PUT` on the same path with the plan body to create it.
5. Confirm the response is 201 (created).

### 2. Switch support plan types

1. Call `GET` on the current plan path to confirm it exists (200).
2. Call `PUT` on the new plan path to create or update the replacement plan.
3. Verify the PUT returns 200 or 201.
4. Call `DELETE` on the old plan path to remove it.
5. If DELETE returns 202, poll the async operation URL until complete.

### 3. Audit support plan status for a subscription

1. Call `POST /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/canonical/listSupportPlanInfo` to get all available plan types.
2. For each plan type returned, call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}`.
3. Record which return 200 (active) vs 404 (not enrolled).
4. Surface a summary of active vs available plans.

### 4. Clean up all support plans

1. Call `POST .../canonical/listSupportPlanInfo` to enumerate all plan types.
2. For each plan, call `GET` to check if it is active (200).
3. For each active plan, call `DELETE` to remove it.
4. Track any 202 responses and poll their async operations to completion.
5. Verify cleanup by re-running GET on each -- expect 404 for all.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
