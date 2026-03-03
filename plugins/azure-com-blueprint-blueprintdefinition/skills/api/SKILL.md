---
name: blueprintclient
description: "BlueprintClient API skill. Use when working with BlueprintClient for {resourceScope}. Covers 14 endpoints."
version: 1.0.0
generator: lapsh
---

# BlueprintClient
API version: 2018-11-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /{resourceScope}/providers/Microsoft.Blueprint/blueprints -- verify access

## Endpoints

14 endpoints across 1 groups. See references/api-spec.lap for full details.

### {resourceScope}
| Method | Path | Description |
|--------|------|-------------|
| PUT | /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName} | Create or update a blueprint definition. |
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName} | Get a blueprint definition. |
| DELETE | /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName} | Delete a blueprint definition. |
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprints | List blueprint definitions. |
| PUT | /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/artifacts/{artifactName} | Create or update blueprint artifact. |
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/artifacts/{artifactName} | Get a blueprint artifact. |
| DELETE | /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/artifacts/{artifactName} | Delete a blueprint artifact. |
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/artifacts | List artifacts for a given blueprint definition. |
| PUT | /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/versions/{versionId} | Publish a new version of the blueprint definition with the latest artifacts. Published blueprint definitions are immutable. |
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/versions/{versionId} | Get a published version of a blueprint definition. |
| DELETE | /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/versions/{versionId} | Delete a published version of a blueprint definition. |
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/versions | List published versions of given blueprint definition. |
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/versions/{versionId}/artifacts/{artifactName} | Get an artifact for a published blueprint definition. |
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/versions/{versionId}/artifacts | List artifacts for a version of a published blueprint definition. |

## Enhanced Skill Content


## Question Mapping

- "How do I create a new blueprint?" -> PUT /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}
- "How do I update an existing blueprint?" -> PUT /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}
- "How do I get the details of a specific blueprint?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}
- "How do I delete a blueprint?" -> DELETE /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}
- "How do I list all blueprints in a scope?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprints
- "How do I add a policy artifact to a blueprint?" -> PUT /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/artifacts/{artifactName}
- "How do I view a specific artifact in a blueprint?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/artifacts/{artifactName}
- "How do I remove an artifact from a blueprint?" -> DELETE /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/artifacts/{artifactName}
- "How do I list all artifacts in a blueprint?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/artifacts
- "How do I publish a version of a blueprint?" -> PUT /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/versions/{versionId}
- "How do I check the details of a published version?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/versions/{versionId}
- "How do I unpublish or remove a blueprint version?" -> DELETE /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/versions/{versionId}
- "How do I list all published versions of a blueprint?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/versions
- "How do I view an artifact from a specific published version?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/versions/{versionId}/artifacts/{artifactName}
- "How do I see what artifacts were included in a published version?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}/versions/{versionId}/artifacts

## Response Tips

- **Blueprints (CRUD):** 201 on create/update (PUT), 200 on GET/DELETE success, 204 on DELETE when resource was already absent. Response body includes `properties.status` indicating draft vs published state.
- **Artifacts (CRUD):** Same 201/200/204 pattern. Artifact `kind` field distinguishes between `template`, `roleAssignment`, and `policyAssignment` types -- always check this to determine the shape of `properties`.
- **Versions (publish/list):** PUT returns 201 with the published snapshot. List endpoints return paginated results with `nextLink` -- follow it until null to retrieve all versions.
- **Published version artifacts:** Read-only views. These are immutable snapshots; the response shape matches draft artifacts but `properties` may include resolved parameter values.
- **Errors:** Azure returns `CloudError` with `error.code` and `error.message`. Common codes: `BlueprintNotFound`, `ArtifactNotFound`, `InvalidBlueprintArtifact`. Always surface the inner `error.details[]` array when present.

## Anomaly Flags

- **204 on DELETE:** Indicates the resource was already gone. Surface this as "resource not found -- it may have been previously deleted or never existed at this scope."
- **resourceScope mismatch:** If a blueprint is created at management group scope but queried at subscription scope (or vice versa), the API returns 404. Flag when the scope pattern changes between related calls.
- **Unpublished blueprint references:** If a user tries to GET a version or version artifact for a blueprint that has never been published, surface that the blueprint must be published first via PUT .../versions/{versionId}.
- **Missing api-version parameter:** All calls require the `api-version` query parameter (2018-11-01-preview). Flag if omitted -- the error message from Azure can be cryptic.
- **Preview API version:** This is a preview API (2018-11-01-preview). Surface a note that behavior may change and this version may be deprecated. Recommend checking for GA availability.
- **Large artifact counts:** If listing artifacts returns many items, flag that blueprint complexity may affect assignment time and recommend reviewing whether all artifacts are necessary.

## Playbook

### 1. Create and Publish a Blueprint

1. Choose a `resourceScope` (subscription: `/subscriptions/{id}` or management group: `/providers/Microsoft.Management/managementGroups/{id}`)
2. PUT `/{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}` with the blueprint body (description, target scope, parameters, resource groups)
3. Add artifacts by calling PUT `.../{blueprintName}/artifacts/{artifactName}` for each policy assignment, role assignment, or ARM template
4. Verify the draft by calling GET `.../{blueprintName}/artifacts` and reviewing all artifacts
5. Publish by calling PUT `.../{blueprintName}/versions/{versionId}` (e.g., `v1.0`) to create an immutable snapshot

### 2. Update a Blueprint and Release a New Version

1. GET `/{resourceScope}/providers/Microsoft.Blueprint/blueprints/{blueprintName}` to review the current draft
2. PUT the blueprint again with updated properties (description, parameters, resource groups)
3. Add, update, or DELETE artifacts as needed using the artifacts endpoints
4. Verify changes by listing artifacts with GET `.../{blueprintName}/artifacts`
5. Publish the new version with PUT `.../{blueprintName}/versions/{v2.0}`
6. Confirm by listing versions with GET `.../{blueprintName}/versions`

### 3. Audit a Published Blueprint Version

1. GET `.../{blueprintName}/versions/{versionId}` to retrieve the published version metadata
2. GET `.../{blueprintName}/versions/{versionId}/artifacts` to list all artifacts frozen in that version
3. For each artifact of interest, GET `.../{blueprintName}/versions/{versionId}/artifacts/{artifactName}` to inspect the full definition
4. Compare against the current draft artifacts (GET `.../{blueprintName}/artifacts`) to identify drift

### 4. Clean Up a Blueprint and All Its Versions

1. GET `.../{blueprintName}/versions` to list all published versions
2. DELETE each version: DELETE `.../{blueprintName}/versions/{versionId}` (repeat for all)
3. GET `.../{blueprintName}/artifacts` to list all draft artifacts
4. DELETE each artifact: DELETE `.../{blueprintName}/artifacts/{artifactName}` (repeat for all)
5. DELETE the blueprint itself: DELETE `.../{blueprintName}`
6. Confirm cleanup with GET `.../{blueprintName}` -- expect a 404

### 5. Inventory All Blueprints Across a Scope

1. GET `/{resourceScope}/providers/Microsoft.Blueprint/blueprints` to list all blueprints
2. For each blueprint, GET `.../{blueprintName}/versions` to enumerate published versions
3. For each blueprint, GET `.../{blueprintName}/artifacts` to count and categorize artifacts
4. Compile results into a summary: blueprint name, number of versions, number of artifacts, latest version ID


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
