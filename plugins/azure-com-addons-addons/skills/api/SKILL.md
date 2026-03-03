---
name: azure-addons-resource-provider
description: "Azure Addons Resource Provider API skill. Use when working with Azure Addons Resource Provider for providers, subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Azure Addons Resource Provider
API version: 2017-05-15

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Addons/operations -- verify access

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
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes | Returns the Canonical Support Plans. |

## Enhanced Skill Content


## Question Mapping

- "What operations are available in the Azure Addons resource provider?" -> GET /providers/Microsoft.Addons/operations
- "How do I check my current support plan?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "What support plans do I have with a specific provider?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes
- "How do I create a new support plan?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "How do I update an existing support plan?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "How do I cancel or remove a support plan?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "What support providers are available for my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes
- "Does a specific support plan exist for my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "How do I switch from one support plan to another?" -> DELETE then PUT /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}
- "What API version should I use for Azure Addons?" -> All endpoints require `api-version=2017-05-15`
- "How do I verify a support plan was successfully deleted?" -> DELETE returns 202 (accepted) or 204 (no content), then GET to confirm 404
- "Can I list all plan types across all support providers?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes (repeat per provider)

## Response Tips

- **Operations (providers):** Returns a flat list of available operations; no pagination. Each operation includes resource provider, operation name, and display metadata.
- **Support plan GET (single):** Returns the full plan object on 200; a 404 means the plan does not exist for the given provider/subscription combination -- do not treat as an error if checking existence.
- **Support plan PUT (create/update):** 200 means updated in place, 201 means newly created -- check the status code to distinguish. Request body must include the full plan definition.
- **Support plan DELETE:** 202 means deletion accepted but still processing (async), 204 means already gone or immediately removed -- both are success states.
- **Support plan LIST:** Returns an array of plan type objects for the given provider; empty array means no plans configured, not an error.

## Anomaly Flags

- **404 on GET/PUT:** The support provider name or plan type name may be misspelled or unsupported -- surface the exact path parameters used and suggest the user verify provider/plan names via the list endpoint.
- **202 on DELETE without follow-up:** Deletion is asynchronous; proactively suggest polling the GET endpoint to confirm the plan has been fully removed.
- **Missing api-version parameter:** All endpoints require `api-version` -- if omitted, the request will fail. Flag immediately if the parameter is absent.
- **PUT returning 200 vs 201:** Surface which status was returned so the user knows whether they created a new plan or modified an existing one.
- **OAuth2 token expiry:** Auth is OAuth2; if repeated 401s occur, proactively flag that the token may need refresh before retrying.
- **Deprecated API version:** The spec uses `2017-05-15` -- flag if Azure documentation indicates a newer API version is available.

## Playbook

### 1. Check and Create a Support Plan

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes/{planTypeName}` to check if the plan exists.
2. If 404, call PUT on the same path with the plan definition in the request body.
3. Confirm creation by checking for a 201 response status.
4. Optionally call GET again to verify the plan details.

### 2. List and Review All Support Plans for a Provider

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Addons/supportProviders/{providerName}/supportPlanTypes` to list all plans.
2. Inspect the response array for each plan's name, status, and configuration.
3. For detailed info on any specific plan, call GET on the individual plan endpoint.

### 3. Switch Support Plans

1. Call GET on the current plan to confirm its details and existence.
2. Call DELETE on the current plan to remove it.
3. If DELETE returns 202, poll with GET until the plan returns 404 (confirmed removed).
4. Call PUT on the new plan's path with the desired configuration in the body.
5. Verify the new plan was created by checking for a 200 or 201 response.

### 4. Clean Removal of a Support Plan

1. Call GET on the plan to confirm it exists (expect 200).
2. Call DELETE on the plan path.
3. If 204, the plan is already removed -- done.
4. If 202, the deletion is in progress -- poll GET every few seconds until 404 is returned.
5. Log the final confirmation for audit purposes.

### 5. Discover Available Operations

1. Call GET `/providers/Microsoft.Addons/operations` with the `api-version` parameter.
2. Review the returned operations list to understand what actions the resource provider supports.
3. Use the operation names and resource types to inform subsequent API calls.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
