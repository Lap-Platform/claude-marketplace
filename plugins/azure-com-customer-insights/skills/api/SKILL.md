---
name: customerinsightsmanagementclient
description: "CustomerInsightsManagementClient API skill. Use when working with CustomerInsightsManagementClient for providers, subscriptions. Covers 66 endpoints."
version: 1.0.0
generator: lapsh
---

# CustomerInsightsManagementClient
API version: 2017-04-26

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.CustomerInsights/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/profiles/{profileName}/getEnrichingKpis -- create first getEnrichingKpis

## Endpoints

66 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.CustomerInsights/operations | Lists all of the available Customer Insights REST API operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName} | Creates a hub, or updates an existing hub. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName} | Updates a Hub. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName} | Deletes the specified hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName} | Gets information about the specified hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs | Gets all the hubs in a resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.CustomerInsights/hubs | Gets all hubs in the specified subscription. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/profiles/{profileName} | Creates a profile within a Hub, or updates an existing profile. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/profiles/{profileName} | Gets information about the specified profile. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/profiles/{profileName} | Deletes a profile within a hub |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/profiles | Gets all profile in the hub. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/profiles/{profileName}/getEnrichingKpis | Gets the KPIs that enrich the profile Type identified by the supplied name. Enrichment happens through participants of the Interaction on an Interaction KPI and through Relationships for Profile KPIs. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/interactions/{interactionName} | Creates an interaction or updates an existing interaction within a hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/interactions/{interactionName} | Gets information about the specified interaction. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/interactions | Gets all interactions in the hub. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/interactions/{interactionName}/suggestRelationshipLinks | Suggests relationships to create relationship links. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/relationships/{relationshipName} | Creates a relationship or updates an existing relationship within a hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/relationships/{relationshipName} | Gets information about the specified relationship. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/relationships/{relationshipName} | Deletes a relationship within a hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/relationships | Gets all relationships in the hub. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/relationshipLinks/{relationshipLinkName} | Creates a relationship link or updates an existing relationship link within a hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/relationshipLinks/{relationshipLinkName} | Gets information about the specified relationship Link. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/relationshipLinks/{relationshipLinkName} | Deletes a relationship link within a hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/relationshipLinks | Gets all relationship links in the hub. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/authorizationPolicies/{authorizationPolicyName} | Creates an authorization policy or updates an existing authorization policy. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/authorizationPolicies/{authorizationPolicyName} | Gets an authorization policy in the hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/authorizationPolicies | Gets all the authorization policies in a specified hub. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/authorizationPolicies/{authorizationPolicyName}/regeneratePrimaryKey | Regenerates the primary policy key of the specified authorization policy. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/authorizationPolicies/{authorizationPolicyName}/regenerateSecondaryKey | Regenerates the secondary policy key of the specified authorization policy. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/connectors/{connectorName} | Creates a connector or updates an existing connector in the hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/connectors/{connectorName} | Gets a connector in the hub. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/connectors/{connectorName} | Deletes a connector in the hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/connectors | Gets all the connectors in the specified hub. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/connectors/{connectorName}/mappings/{mappingName} | Creates a connector mapping or updates an existing connector mapping in the connector. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/connectors/{connectorName}/mappings/{mappingName} | Gets a connector mapping in the connector. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/connectors/{connectorName}/mappings/{mappingName} | Deletes a connector mapping in the connector. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/connectors/{connectorName}/mappings | Gets all the connector mappings in the specified connector. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/kpi/{kpiName} | Creates a KPI or updates an existing KPI in the hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/kpi/{kpiName} | Gets a KPI in the hub. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/kpi/{kpiName} | Deletes a KPI in the hub. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/kpi/{kpiName}/reprocess | Reprocesses the Kpi values of the specified KPI. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/kpi | Gets all the KPIs in the specified hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/widgetTypes | Gets all available widget types in the specified hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/widgetTypes/{widgetTypeName} | Gets a widget type in the specified hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/views | Gets all available views for given user in the specified hub. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/views/{viewName} | Creates a view or updates an existing view in the hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/views/{viewName} | Gets a view in the hub. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/views/{viewName} | Deletes a view in the specified hub. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/links/{linkName} | Creates a link or updates an existing link in the hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/links/{linkName} | Gets a link in the hub. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/links/{linkName} | Deletes a link in the hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/links | Gets all the links in the specified hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/roles | Gets all the roles for the hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/roleAssignments | Gets all the role assignments for the specified hub. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/roleAssignments/{assignmentName} | Creates or updates a role assignment in the hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/roleAssignments/{assignmentName} | Gets the role assignment in the hub. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/roleAssignments/{assignmentName} | Deletes the role assignment in the hub. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/images/getEntityTypeImageUploadUrl | Gets entity type (profile or interaction) image upload URL. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/images/getDataImageUploadUrl | Gets data image upload URL. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/predictions/{predictionName} | Creates a Prediction or updates an existing Prediction in the hub. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/predictions/{predictionName} | Gets a Prediction in the hub. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/predictions/{predictionName} | Deletes a Prediction in the hub. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/predictions/{predictionName}/getTrainingResults | Gets training results. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/predictions/{predictionName}/getModelStatus | Gets model status of the prediction. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/predictions/{predictionName}/modelStatus | Creates or updates the model status of prediction. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/predictions | Gets all the predictions in the specified hub. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Customer Insights?" -> GET /providers/Microsoft.CustomerInsights/operations
- "How do I create a new Customer Insights hub?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}
- "List all hubs in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.CustomerInsights/hubs
- "How do I define a customer profile in my hub?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/profiles/{profileName}
- "What KPIs are configured for my hub?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/kpi
- "How do I set up a data connector?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/connectors/{connectorName}
- "How do I map connector data to a profile or interaction?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/connectors/{connectorName}/mappings/{mappingName}
- "How do I create a relationship between two profiles?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/relationships/{relationshipName}
- "How do I regenerate an authorization policy key?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/authorizationPolicies/{authorizationPolicyName}/regeneratePrimaryKey
- "How do I assign a role to a user in my hub?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/roleAssignments/{assignmentName}
- "What predictions are running in my hub?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/predictions
- "How do I check the training status of a prediction model?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/predictions/{predictionName}/getModelStatus
- "How do I get an image upload URL for an entity type?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/images/getEntityTypeImageUploadUrl
- "What interactions are tracked in my hub?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/interactions
- "How do I get suggested relationship links for an interaction?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CustomerInsights/hubs/{hubName}/interactions/{interactionName}/suggestRelationshipLinks

## Response Tips

- **Hubs (CRUD):** 201 on create, 200 on update/get; DELETE returns 202 for async deletion in progress and 204 when already gone -- check both.
- **Profiles & Interactions:** PUT returns 202 when provisioning is async; poll the GET endpoint until `provisioningState` reaches a terminal value.
- **Connectors & Mappings:** List endpoints return paged arrays with a `nextLink` property; follow it to retrieve all results.
- **KPIs:** POST .../reprocess returns only 202 (no body) -- the reprocess is fire-and-forget; check KPI status via GET afterward.
- **Authorization Policies:** Regenerate key endpoints return the full policy object including the new key in the 200 response body.
- **Predictions:** getTrainingResults and getModelStatus return nested objects with scoring metrics and status enums -- inspect `status` and `scoringResults` fields.
- **Views:** GET requires a `userId` query parameter even for list operations -- omitting it produces a 400.
- **Role Assignments:** DELETE may return 200, 202, or 204 depending on timing; treat all three as success.

## Anomaly Flags

- **202 Accepted on mutations:** Surface to user that the operation is async. Recommend polling the corresponding GET endpoint until provisioning completes.
- **204 on DELETE:** Indicate the resource was already deleted or never existed -- not an error, but worth noting if the caller expected it to exist.
- **Missing `api-version` query parameter:** All endpoints require `api-version=2017-04-26` as a common field. Omission causes 400 errors that may be cryptic.
- **Stale API version (2017-04-26):** This is a legacy API version. Flag that newer versions may be available and some features could be deprecated.
- **OAuth2 token expiry:** Surface proactively if repeated 401 responses occur -- token may need refresh.
- **Provisioning state stuck:** If a profile, interaction, connector, or prediction stays in a non-terminal provisioning state across multiple polls, flag it as potentially failed.
- **Prediction model status regressions:** If getModelStatus returns a worse status than previously observed (e.g., moved from "Succeeded" back to "Failed"), surface immediately.
- **Rate limiting from Azure Resource Manager:** ARM applies per-subscription throttling; surface 429 responses with retry-after headers.

## Playbook

### 1. Set Up a New Customer Insights Hub with a Profile

1. PUT .../hubs/{hubName} with hub configuration parameters to create the hub
2. GET .../hubs/{hubName} to confirm provisioning completed (check `provisioningState`)
3. PUT .../hubs/{hubName}/profiles/{profileName} to define a customer profile schema
4. GET .../hubs/{hubName}/profiles/{profileName} to verify the profile is provisioned
5. PUT .../hubs/{hubName}/authorizationPolicies/{policyName} to create an access policy for the hub

### 2. Connect a Data Source and Map It to a Profile

1. PUT .../hubs/{hubName}/connectors/{connectorName} with connection parameters (e.g., blob storage credentials)
2. GET .../hubs/{hubName}/connectors/{connectorName} to confirm connector provisioning
3. PUT .../hubs/{hubName}/connectors/{connectorName}/mappings/{mappingName} with field mappings from source to profile
4. GET .../hubs/{hubName}/connectors/{connectorName}/mappings to verify all mappings are active

### 3. Build and Monitor a Prediction Model

1. GET .../hubs/{hubName}/profiles to identify available profile types for prediction input
2. GET .../hubs/{hubName}/kpi to review existing KPIs that can serve as prediction targets
3. PUT .../hubs/{hubName}/predictions/{predictionName} with model definition and target KPI
4. POST .../hubs/{hubName}/predictions/{predictionName}/getModelStatus to monitor training progress
5. POST .../hubs/{hubName}/predictions/{predictionName}/getTrainingResults to review accuracy and scoring metrics once complete

### 4. Configure Relationships and Links Between Profiles

1. GET .../hubs/{hubName}/profiles to list available profiles
2. PUT .../hubs/{hubName}/relationships/{relationshipName} to define a relationship between two profile types
3. PUT .../hubs/{hubName}/relationshipLinks/{linkName} to create a link that maps interaction data into the relationship
4. POST .../hubs/{hubName}/interactions/{interactionName}/suggestRelationshipLinks to discover additional link candidates automatically
5. GET .../hubs/{hubName}/relationships to verify the full relationship graph

### 5. Manage Access Control and Key Rotation

1. GET .../hubs/{hubName}/roles to list available role definitions
2. PUT .../hubs/{hubName}/roleAssignments/{assignmentName} to assign a role to a principal
3. GET .../hubs/{hubName}/authorizationPolicies to review current policies
4. POST .../hubs/{hubName}/authorizationPolicies/{policyName}/regeneratePrimaryKey to rotate the primary key
5. POST .../hubs/{hubName}/authorizationPolicies/{policyName}/regenerateSecondaryKey to rotate the secondary key (do this on a staggered schedule from primary)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
