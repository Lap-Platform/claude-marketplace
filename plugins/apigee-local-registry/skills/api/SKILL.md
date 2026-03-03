---
name: registry-api
description: "Registry API skill. Use when working with Registry for projects. Covers 35 endpoints."
version: 1.0.0
generator: lapsh
---

# Registry API
API version: 0.0.1

## Auth
No authentication required.

## Base URL
https://apigeeregistry.googleapis.com

## Setup
1. No auth setup needed
2. GET /v1/projects/{project}/locations/{location}/apis -- verify access
3. POST /v1/projects/{project}/locations/{location}/apis -- create first apis

## Endpoints

35 endpoints across 1 groups. See references/api-spec.lap for full details.

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/projects/{project}/locations/{location}/apis | ListApis returns matching APIs. |
| POST | /v1/projects/{project}/locations/{location}/apis | CreateApi creates a specified API. |
| GET | /v1/projects/{project}/locations/{location}/apis/{api} | GetApi returns a specified API. |
| DELETE | /v1/projects/{project}/locations/{location}/apis/{api} | DeleteApi removes a specified API and all of the resources that it |
| PATCH | /v1/projects/{project}/locations/{location}/apis/{api} | UpdateApi can be used to modify a specified API. |
| GET | /v1/projects/{project}/locations/{location}/apis/{api}/deployments | ListApiDeployments returns matching deployments. |
| POST | /v1/projects/{project}/locations/{location}/apis/{api}/deployments | CreateApiDeployment creates a specified deployment. |
| GET | /v1/projects/{project}/locations/{location}/apis/{api}/deployments/{deployment} | GetApiDeployment returns a specified deployment. |
| DELETE | /v1/projects/{project}/locations/{location}/apis/{api}/deployments/{deployment} | DeleteApiDeployment removes a specified deployment, all revisions, and all |
| PATCH | /v1/projects/{project}/locations/{location}/apis/{api}/deployments/{deployment} | UpdateApiDeployment can be used to modify a specified deployment. |
| DELETE | /v1/projects/{project}/locations/{location}/apis/{api}/deployments/{deployment}:deleteRevision | DeleteApiDeploymentRevision deletes a revision of a deployment. |
| GET | /v1/projects/{project}/locations/{location}/apis/{api}/deployments/{deployment}:listRevisions | ListApiDeploymentRevisions lists all revisions of a deployment. |
| POST | /v1/projects/{project}/locations/{location}/apis/{api}/deployments/{deployment}:rollback | RollbackApiDeployment sets the current revision to a specified prior |
| POST | /v1/projects/{project}/locations/{location}/apis/{api}/deployments/{deployment}:tagRevision | TagApiDeploymentRevision adds a tag to a specified revision of a |
| GET | /v1/projects/{project}/locations/{location}/apis/{api}/versions | ListApiVersions returns matching versions. |
| POST | /v1/projects/{project}/locations/{location}/apis/{api}/versions | CreateApiVersion creates a specified version. |
| GET | /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version} | GetApiVersion returns a specified version. |
| DELETE | /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version} | DeleteApiVersion removes a specified version and all of the resources that |
| PATCH | /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version} | UpdateApiVersion can be used to modify a specified version. |
| GET | /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs | ListApiSpecs returns matching specs. |
| POST | /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs | CreateApiSpec creates a specified spec. |
| GET | /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs/{spec} | GetApiSpec returns a specified spec. |
| DELETE | /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs/{spec} | DeleteApiSpec removes a specified spec, all revisions, and all child |
| PATCH | /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs/{spec} | UpdateApiSpec can be used to modify a specified spec. |
| DELETE | /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs/{spec}:deleteRevision | DeleteApiSpecRevision deletes a revision of a spec. |
| GET | /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs/{spec}:getContents | GetApiSpecContents returns the contents of a specified spec. |
| GET | /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs/{spec}:listRevisions | ListApiSpecRevisions lists all revisions of a spec. |
| POST | /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs/{spec}:rollback | RollbackApiSpec sets the current revision to a specified prior revision. |
| POST | /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs/{spec}:tagRevision | TagApiSpecRevision adds a tag to a specified revision of a spec. |
| GET | /v1/projects/{project}/locations/{location}/artifacts | ListArtifacts returns matching artifacts. |
| POST | /v1/projects/{project}/locations/{location}/artifacts | CreateArtifact creates a specified artifact. |
| GET | /v1/projects/{project}/locations/{location}/artifacts/{artifact} | GetArtifact returns a specified artifact. |
| PUT | /v1/projects/{project}/locations/{location}/artifacts/{artifact} | ReplaceArtifact can be used to replace a specified artifact. |
| DELETE | /v1/projects/{project}/locations/{location}/artifacts/{artifact} | DeleteArtifact removes a specified artifact. |
| GET | /v1/projects/{project}/locations/{location}/artifacts/{artifact}:getContents | GetArtifactContents returns the contents of a specified artifact. |

## Enhanced Skill Content
## Question Mapping

- "What APIs are registered in my project?" -> GET /v1/projects/{project}/locations/{location}/apis
- "Show me details for a specific API" -> GET /v1/projects/{project}/locations/{location}/apis/{api}
- "How do I register a new API?" -> POST /v1/projects/{project}/locations/{location}/apis
- "What versions exist for this API?" -> GET /v1/projects/{project}/locations/{location}/apis/{api}/versions
- "Where is this API deployed?" -> GET /v1/projects/{project}/locations/{location}/apis/{api}/deployments
- "What specs are attached to this API version?" -> GET /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs
- "Download the raw spec content for a specific revision" -> GET /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs/{spec}:getContents
- "How do I roll back a deployment to a previous revision?" -> POST /v1/projects/{project}/locations/{location}/apis/{api}/deployments/{deployment}:rollback
- "What revision history does this spec have?" -> GET /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs/{spec}:listRevisions
- "How do I tag a deployment revision for release tracking?" -> POST /v1/projects/{project}/locations/{location}/apis/{api}/deployments/{deployment}:tagRevision
- "Delete an API and all its child resources" -> DELETE /v1/projects/{project}/locations/{location}/apis/{api} (with `force: true`)
- "Upload an OpenAPI spec to a specific API version" -> POST /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs
- "What artifacts are stored at the project level?" -> GET /v1/projects/{project}/locations/{location}/artifacts
- "Update only the description of an API without touching other fields" -> PATCH /v1/projects/{project}/locations/{location}/apis/{api} (with `updateMask: "description"`)
- "Remove a single spec revision without deleting the whole spec" -> DELETE /v1/projects/{project}/locations/{location}/apis/{api}/versions/{version}/specs/{spec}:deleteRevision

## Response Tips

- **List endpoints** (apis, versions, deployments, specs, artifacts): All return paginated arrays with `nextPageToken` -- loop until `nextPageToken` is absent or empty. Use `pageSize` to control batch size (default varies, max typically 1000).
- **Single resource GETs**: Return the full resource object directly (not wrapped in an array). A 404 means the resource name path is wrong -- double-check project, location, and resource IDs.
- **Create/Update (POST/PATCH)**: Return the created or updated resource. PATCH responses reflect only the fields included in `updateMask`; omitted fields remain unchanged.
- **Delete endpoints**: Return an empty 200 on success. The `force` flag on APIs, versions, and specs cascade-deletes all child resources -- without it, deletion fails if children exist.
- **Revision endpoints** (listRevisions, rollback, tagRevision, deleteRevision): Return deployment/spec objects with `revisionId` populated. `listRevisions` is paginated like other list endpoints.
- **Artifact contents** (getContents): Returns raw bytes, not JSON. Check `mimeType` on the artifact resource to know how to decode.
- **Spec contents**: The `contents` field is base64-encoded (`str(bytes)`). Decode before use. `sizeBytes` and `hash` refer to the decoded content.

## Anomaly Flags

- **Cascade deletion risk**: Surface a warning when `DELETE` is called with `force: true` on APIs, versions, or specs -- this permanently removes all child resources (versions, specs, deployments) with no undo.
- **Empty `updateMask` on PATCH**: If `updateMask` is omitted or empty, the API may replace all mutable fields. Flag when a PATCH request lacks an explicit field mask.
- **`allowMissing` upsert behavior**: When `allowMissing: true` is set on PATCH, the call silently creates the resource if it does not exist. Flag this as it can produce unintended resources.
- **Large spec uploads**: If `sizeBytes` exceeds typical thresholds (>10 MB), warn about potential timeout or quota issues.
- **Stale `recommendedVersion` or `recommendedDeployment`**: After deleting a version or deployment, check whether the parent API still points to the deleted resource in these fields. Surface if they reference a non-existent resource.
- **Revision accumulation**: When `listRevisions` returns a high page count, flag potential storage bloat and suggest pruning old revisions with `deleteRevision`.
- **Pagination truncation**: If a user fetches only the first page of results without following `nextPageToken`, warn that results are incomplete.

## Playbook

### 1. Register a new API with its first version and spec

1. `POST /v1/projects/{project}/locations/{location}/apis` with `apiId`, `displayName`, and `description` to create the API entry.
2. `POST /v1/projects/{project}/locations/{location}/apis/{api}/versions` with `apiVersionId` (e.g., `v1`), `displayName`, and `state` (e.g., `PRODUCTION`).
3. `POST /v1/projects/{project}/locations/{location}/apis/{api}/versions/v1/specs` with `apiSpecId`, `mimeType` (e.g., `application/x.openapi+gzip;version=3`), and base64-encoded `contents`.
4. Verify by calling `GET .../apis/{api}` and `GET .../versions/v1/specs/{spec}` to confirm the resources exist.
5. Optionally set `recommendedVersion` on the API via `PATCH .../apis/{api}` with `updateMask: "recommendedVersion"`.

### 2. Deploy an API and manage revisions

1. `POST /v1/projects/{project}/locations/{location}/apis/{api}/deployments` with `apiDeploymentId`, `endpointUri`, `apiSpecRevision` (linking to the spec revision), and `intendedAudience`.
2. When a new revision is deployed, `PATCH .../deployments/{deployment}` with updated `apiSpecRevision` and `endpointUri`. Each PATCH creates a new revision automatically.
3. List revision history with `GET .../deployments/{deployment}:listRevisions` to audit changes.
4. If a bad revision is deployed, roll back with `POST .../deployments/{deployment}:rollback` specifying the target `revisionId`.
5. Tag stable revisions with `POST .../deployments/{deployment}:tagRevision` using a meaningful `tag` (e.g., `stable`, `canary`).

### 3. Update a spec and track revision history

1. Fetch the current spec with `GET .../specs/{spec}` to confirm the existing `revisionId` and `hash`.
2. `PATCH .../specs/{spec}` with updated `contents` (base64-encoded) and `updateMask: "contents"`. This creates a new revision.
3. Verify the update with `GET .../specs/{spec}:getContents` to download and validate the raw content.
4. List all revisions with `GET .../specs/{spec}:listRevisions` to confirm the new revision appears.
5. If the update was incorrect, `POST .../specs/{spec}:rollback` to the previous `revisionId`.
6. Clean up obsolete revisions with `DELETE .../specs/{spec}:deleteRevision` for specific old revision IDs.

### 4. Audit all APIs and their deployment status

1. `GET /v1/projects/{project}/locations/{location}/apis` -- paginate through all APIs using `nextPageToken`.
2. For each API, check `recommendedVersion` and `recommendedDeployment` fields for staleness.
3. `GET .../apis/{api}/deployments` for each API to list active deployments.
4. For each deployment, inspect `apiSpecRevision` to verify it points to the latest spec revision.
5. Cross-reference by calling `GET .../versions/{version}/specs` to confirm the linked spec still exists and is current.

### 5. Store and retrieve project-level artifacts

1. `POST /v1/projects/{project}/locations/{location}/artifacts` with `artifactId`, `mimeType`, and base64-encoded `contents` (e.g., style guides, lint configs, governance policies).
2. List all artifacts with `GET .../artifacts` to discover what metadata is stored.
3. Retrieve a specific artifact's metadata with `GET .../artifacts/{artifact}`.
4. Download raw content with `GET .../artifacts/{artifact}:getContents`.
5. Replace an artifact entirely with `PUT .../artifacts/{artifact}` -- note this uses PUT (full replace), not PATCH.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
