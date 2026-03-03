---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# ApplicationInsightsManagementClient
API version: 2015-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations | Gets the list of annotations for a component for given time range |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations | Create an Annotation of an Application Insights component. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations/{annotationId} | Delete an Annotation of an Application Insights component. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations/{annotationId} | Get the annotation for given id. |

## Enhanced Skill Content


## Question Mapping

- "What annotations exist for my Application Insights resource?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations
- "Show me annotations between two dates for my app component" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations
- "How do I add a deployment annotation to Application Insights?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations
- "Create a release marker on my Application Insights timeline" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations
- "How do I mark an incident window in Application Insights?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations
- "Remove a specific annotation from my app resource" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations/{annotationId}
- "Delete the deployment marker I just created" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations/{annotationId}
- "Get details of a specific annotation by ID" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations/{annotationId}
- "Look up a single annotation to see who created it" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations/{annotationId}
- "What annotations were added during last week's release?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations
- "How do I update an existing annotation?" -> DELETE then PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations (no PATCH; delete and recreate)
- "List all deployment annotations for a specific resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/Annotations

## Response Tips

- **List annotations (GET collection):** Returns an array of annotation objects. The `start` and `end` query parameters are required to scope the time range -- omitting them will error. Results are not paginated; all matching annotations within the window are returned in a single response.
- **Create annotation (PUT):** Returns the created annotation with a server-assigned `annotationId`. The `AnnotationProperties` map must include at minimum the annotation name and category. Check the response for the generated ID if you need to reference it later.
- **Delete annotation (DELETE):** Returns 200 on success with an empty or minimal body. A 404 means the annotationId does not exist or was already deleted.
- **Get single annotation (GET by ID):** Returns a single annotation object. A 404 indicates the ID is invalid or the annotation was removed.
- **All endpoints:** Errors follow Azure standard format with `error.code` and `error.message` fields. Watch for 401 (token expired), 403 (insufficient RBAC role), and 404 (wrong resource name or subscription).

## Anomaly Flags

- **OAuth token expiry:** Surface a warning when the bearer token is near expiry or a 401 is returned -- prompt the user to refresh credentials.
- **Missing time range:** The list endpoint requires `start` and `end` parameters. Flag if the user attempts a query without them to prevent a 400 error.
- **No PATCH support:** This API has no update endpoint. If a user asks to modify an annotation, proactively flag that the workflow requires delete + recreate.
- **Annotation ID not returned:** If a PUT response lacks an `annotationId`, flag this as unexpected -- it may indicate a partial failure or schema change.
- **Azure throttling (429):** Surface rate limit headers (`Retry-After`) if present. Azure ARM APIs enforce subscription-level throttling that can affect all management calls.
- **Deprecated API version:** The spec uses version `2015-05-01`. Flag if Azure documentation references a newer API version, as older versions may lose support.

## Playbook

### 1. Mark a Deployment Release

1. Authenticate with OAuth2 and obtain a bearer token with `Microsoft.Insights/components/write` permission.
2. Call PUT on the Annotations endpoint with `AnnotationProperties` containing the annotation name (e.g., "v2.4.1 Release"), category set to "Deployment", and a timestamp.
3. Capture the returned `annotationId` from the response.
4. Verify by calling GET with that `annotationId` to confirm it appears on the timeline.

### 2. Audit Annotations for a Time Window

1. Determine the start and end timestamps (ISO 8601) for the period of interest.
2. Call GET on the Annotations collection with `start` and `end` query parameters.
3. Review the returned array, filtering by category or creator as needed.
4. For any annotation that needs more detail, call GET with its specific `annotationId`.

### 3. Clean Up Stale Annotations

1. Call GET on the Annotations collection with a broad time range covering the cleanup period.
2. Identify annotations that are outdated, duplicated, or no longer relevant.
3. For each annotation to remove, call DELETE with its `annotationId`.
4. Confirm deletion by re-listing annotations for the same time range and verifying the count decreased.

### 4. Correct a Mis-labeled Annotation

1. Call GET with the `annotationId` of the annotation that needs correction.
2. Note down all its properties (name, category, timestamp, related items).
3. Call DELETE with that `annotationId` to remove the incorrect version.
4. Call PUT with the corrected `AnnotationProperties` (updated name, category, or other fields).
5. Store the new `annotationId` returned by the PUT response.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
