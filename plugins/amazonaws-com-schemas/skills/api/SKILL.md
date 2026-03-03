---
name: schemas
description: "Schemas API skill. Use when working with Schemas for discoverers, registries, policy. Covers 31 endpoints."
version: 1.0.0
generator: lapsh
---

# Schemas
API version: 2019-12-02

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /v1/policy -- verify access
3. POST /v1/discoverers -- create first discoverers

## Endpoints

31 endpoints across 5 groups. See references/api-spec.lap for full details.

### discoverers
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/discoverers | Creates a discoverer. |
| DELETE | /v1/discoverers/id/{discovererId} | Deletes a discoverer. |
| GET | /v1/discoverers/id/{discovererId} | Describes the discoverer. |
| GET | /v1/discoverers | List the discoverers. |
| POST | /v1/discoverers/id/{discovererId}/start | Starts the discoverer |
| POST | /v1/discoverers/id/{discovererId}/stop | Stops the discoverer |
| PUT | /v1/discoverers/id/{discovererId} | Updates the discoverer |

### registries
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/registries/name/{registryName} | Creates a registry. |
| POST | /v1/registries/name/{registryName}/schemas/name/{schemaName} | Creates a schema definition. Inactive schemas will be deleted after two years. |
| DELETE | /v1/registries/name/{registryName} | Deletes a Registry. |
| DELETE | /v1/registries/name/{registryName}/schemas/name/{schemaName} | Delete a schema definition. |
| DELETE | /v1/registries/name/{registryName}/schemas/name/{schemaName}/version/{schemaVersion} | Delete the schema version definition |
| GET | /v1/registries/name/{registryName}/schemas/name/{schemaName}/language/{language} | Describe the code binding URI. |
| GET | /v1/registries/name/{registryName} | Describes the registry. |
| GET | /v1/registries/name/{registryName}/schemas/name/{schemaName} | Retrieve the schema definition. |
| GET | /v1/registries/name/{registryName}/schemas/name/{schemaName}/export |  |
| GET | /v1/registries/name/{registryName}/schemas/name/{schemaName}/language/{language}/source | Get the code binding source URI. |
| GET | /v1/registries | List the registries. |
| GET | /v1/registries/name/{registryName}/schemas/name/{schemaName}/versions | Provides a list of the schema versions and related information. |
| GET | /v1/registries/name/{registryName}/schemas | List the schemas. |
| POST | /v1/registries/name/{registryName}/schemas/name/{schemaName}/language/{language} | Put code binding URI |
| GET | /v1/registries/name/{registryName}/schemas/search | Search the schemas |
| PUT | /v1/registries/name/{registryName} | Updates a registry. |
| PUT | /v1/registries/name/{registryName}/schemas/name/{schemaName} | Updates the schema definition Inactive schemas will be deleted after two years. |

### policy
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /v1/policy | Delete the resource-based policy attached to the specified registry. |
| GET | /v1/policy | Retrieves the resource-based policy attached to a given registry. |
| PUT | /v1/policy | The name of the policy. |

### discover
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/discover | Get the discovered schema that was generated based on sampled events. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{resource-arn} | Get tags for resource. |
| POST | /tags/{resource-arn} | Add tags to a resource. |
| DELETE | /tags/{resource-arn} | Removes tags from a resource. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new schema registry?" -> POST /v1/registries/name/{registryName}
- "How do I register a new schema?" -> POST /v1/registries/name/{registryName}/schemas/name/{schemaName}
- "What schemas exist in my registry?" -> GET /v1/registries/name/{registryName}/schemas
- "How do I search for a schema by keyword?" -> GET /v1/registries/name/{registryName}/schemas/search
- "How do I set up automatic schema discovery from an event source?" -> POST /v1/discoverers
- "How do I start or stop a discoverer?" -> POST /v1/discoverers/id/{discovererId}/start, POST /v1/discoverers/id/{discovererId}/stop
- "What versions does a schema have?" -> GET /v1/registries/name/{registryName}/schemas/name/{schemaName}/versions
- "How do I generate code bindings for a schema?" -> POST /v1/registries/name/{registryName}/schemas/name/{schemaName}/language/{language}
- "How do I download the generated source code?" -> GET /v1/registries/name/{registryName}/schemas/name/{schemaName}/language/{language}/source
- "How do I export a schema in a specific format?" -> GET /v1/registries/name/{registryName}/schemas/name/{schemaName}/export
- "How do I discover the schema from a raw event payload?" -> POST /v1/discover
- "How do I manage resource-based policies on a registry?" -> GET /v1/policy, PUT /v1/policy, DELETE /v1/policy
- "How do I tag or untag a schema or registry?" -> POST /tags/{resource-arn}, DELETE /tags/{resource-arn}
- "How do I delete a specific schema version without deleting the whole schema?" -> DELETE /v1/registries/name/{registryName}/schemas/name/{schemaName}/version/{schemaVersion}
- "How do I list all my discoverers or filter by source ARN?" -> GET /v1/discoverers

## Response Tips

- **List endpoints** (GET /v1/registries, /v1/discoverers, /v1/.../schemas, /v1/.../versions, /v1/.../schemas/search): All return a `NextToken` field -- pass it back as a query parameter to paginate. A missing or null `NextToken` means you have reached the last page. Use `limit` to control page size.
- **Create/Update endpoints** (POST/PUT on registries, schemas, discoverers): Return the full resource representation on success (200). Check `SchemaVersion` after schema creates/updates to confirm which version was written.
- **Code generation** (POST .../language/{language}): Returns `Status` which may be `CREATE_IN_PROGRESS` -- poll the GET endpoint until status changes to `CREATE_COMPLETE` before downloading source.
- **Source download** (GET .../language/{language}/source): Returns raw `Body` as bytes (a zip archive), not JSON. Handle the response as binary.
- **Policy endpoints**: `Policy` is returned as a JSON-encoded string inside the response -- parse it separately. `RevisionId` is required for safe concurrent updates via PUT.
- **Error responses**: Expect structured error bodies with `Code` and `Message` fields. Common codes: `NotFoundException` (404), `ConflictException` (409 on duplicate creates), `ServiceUnavailableException` (503).

## Anomaly Flags

- **Code generation stuck**: If `PUT/POST .../language/{language}` returns `Status: CREATE_IN_PROGRESS` for more than 60 seconds on repeated polls, surface a warning that generation may have failed silently.
- **Discoverer state mismatch**: If `start` is called but a subsequent `describe` still shows `State: STOPPED`, flag that the event source ARN may be invalid or permissions are missing.
- **NextToken loop**: If the same `NextToken` is returned across consecutive list calls, flag a potential pagination bug and stop iterating to avoid infinite loops.
- **Schema version proliferation**: When listing versions returns a high count (50+), proactively note that old versions can be pruned with the version-specific DELETE endpoint.
- **Cross-account discoverer**: When `CrossAccount: true` is set on a discoverer, flag that the caller needs cross-account EventBridge permissions or discovery will silently produce no results.
- **Missing Content on schema GET**: If `Content` is null on a describe-schema call, the schema may have been created as a placeholder -- surface this so the user does not assume it is fully defined.
- **Policy RevisionId conflicts**: If a PUT /v1/policy call fails with a conflict, alert the user that another process modified the policy and they should re-fetch before retrying.

## Playbook

### 1. Set Up Automatic Schema Discovery for an Event Bus

1. Create a discoverer: `POST /v1/discoverers` with `SourceArn` set to the EventBridge event bus ARN.
2. Start the discoverer: `POST /v1/discoverers/id/{discovererId}/start`.
3. Send test events to the event bus so the discoverer can infer schemas.
4. List registries to find the `aws.events` discovered-schemas registry: `GET /v1/registries?registryNamePrefix=aws.events`.
5. List schemas in that registry: `GET /v1/registries/name/aws.events/schemas` to see newly discovered schemas.
6. When done capturing, stop the discoverer: `POST /v1/discoverers/id/{discovererId}/stop`.

### 2. Create a Custom Registry, Publish a Schema, and Generate Code

1. Create a registry: `POST /v1/registries/name/{registryName}` with a description.
2. Publish a schema: `POST /v1/registries/name/{registryName}/schemas/name/{schemaName}` with `Content` (JSON Schema or OpenAPI) and `Type` ("OpenApi3" or "JSONSchemaDraft4").
3. Kick off code generation: `POST /v1/registries/name/{registryName}/schemas/name/{schemaName}/language/{language}` (e.g., language = "Python3").
4. Poll generation status: `GET /v1/registries/name/{registryName}/schemas/name/{schemaName}/language/{language}` until `Status` is `CREATE_COMPLETE`.
5. Download the source archive: `GET /v1/registries/name/{registryName}/schemas/name/{schemaName}/language/{language}/source` and save the binary response as a zip file.

### 3. Search and Export a Schema

1. Search by keyword: `GET /v1/registries/name/{registryName}/schemas/search?keywords=OrderPlaced`.
2. Paginate results using `NextToken` if the result set is large.
3. Describe the matching schema: `GET /v1/registries/name/{registryName}/schemas/name/{schemaName}` to inspect full content and version info.
4. Export in a specific format: `GET /v1/registries/name/{registryName}/schemas/name/{schemaName}/export?type=OpenApi3`.

### 4. Manage Cross-Account Access with Resource Policies

1. Fetch the current policy: `GET /v1/policy?registryName={registryName}`.
2. Note the `RevisionId` from the response (needed for safe updates).
3. Construct a new policy JSON string granting cross-account access.
4. Apply it: `PUT /v1/policy` with `Policy`, `registryName`, and `RevisionId`.
5. Verify by re-fetching: `GET /v1/policy?registryName={registryName}`.

### 5. Infer a Schema from a Raw Event Payload

1. Collect one or more sample event JSON payloads.
2. Call `POST /v1/discover` with `Events` (array of JSON strings) and `Type` ("OpenApi3" or "JSONSchemaDraft4").
3. Inspect the returned `Content` -- this is the inferred schema definition.
4. Optionally publish it to a registry using `POST /v1/registries/name/{registryName}/schemas/name/{schemaName}` with the inferred content.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
