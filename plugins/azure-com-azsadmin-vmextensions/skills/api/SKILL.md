---
name: compute-admin-client
description: "Compute Admin Client API skill. Use when working with Compute Admin Client for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Compute Admin Client
API version: 2015-12-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension/publishers/{publisher}/types/{type}/versions/{version} | Returns requested Virtual Machine Extension Image. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension/publishers/{publisher}/types/{type}/versions/{version} | Create a Virtual Machine Extension Image. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension/publishers/{publisher}/types/{type}/versions/{version} | Deletes a Virtual Machine Extension Image. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension | Returns a list of all Virtual Machine Extension Images. |

## Enhanced Skill Content
## Question Mapping

- "What VM extensions are available in my location?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension
- "Get details for a specific VM extension version" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension/publishers/{publisher}/types/{type}/versions/{version}
- "How do I register a new VM extension?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension/publishers/{publisher}/types/{type}/versions/{version}
- "Update an existing VM extension version" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension/publishers/{publisher}/types/{type}/versions/{version}
- "Remove a VM extension from the marketplace" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension/publishers/{publisher}/types/{type}/versions/{version}
- "List all extensions published by a specific publisher" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension
- "Does a specific VM extension version exist?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension/publishers/{publisher}/types/{type}/versions/{version}
- "How do I replace a VM extension with a newer version?" -> PUT (new version) then DELETE (old version)
- "What publishers offer VM extensions in my region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension
- "How do I clean up unused VM extension versions?" -> GET (list all) then DELETE (each unused version)
- "Create a VM extension with custom metadata" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/artifactTypes/VMExtension/publishers/{publisher}/types/{type}/versions/{version}
- "Verify a VM extension was deleted successfully" -> DELETE then GET to confirm 404

## Response Tips

- **List endpoint (GET .../VMExtension):** Returns an array of extension objects; filter client-side by publisher or type since no query parameters are exposed.
- **Detail endpoint (GET .../versions/{version}):** Returns a single extension object with full metadata; a 404 means the publisher/type/version combination does not exist.
- **Create/Update (PUT):** Returns 200 for updates to existing resources and 201 for newly created resources; inspect the status code to distinguish between create and update.
- **Delete (DELETE):** Returns 200 on success; repeat calls to an already-deleted resource may return 404 -- this is idempotent and safe.

## Anomaly Flags

- **201 vs 200 on PUT:** Surface when a PUT returns 201 (new resource created) versus 200 (existing resource updated) so the caller knows whether they overwrote something.
- **Missing extension field on PUT:** The `extension` map body is required; flag immediately if the request payload is empty or missing required nested properties.
- **Unexpected 4xx/5xx on DELETE:** A 404 on delete may indicate the resource was already removed or the path segments (publisher/type/version) are wrong -- surface both possibilities.
- **OAuth2 token expiry:** Proactively warn when the OAuth2 token is near expiration before making multi-step workflows that depend on sequential calls.
- **Long path parameter chains:** Flag if any of the six path parameters (subscriptionId, location, publisher, type, version) appear empty or malformed, since the deeply nested URL makes typos likely.
- **Deprecated API version:** This spec uses `2015-12-01-preview` -- surface a warning that this is a preview version and may be superseded by a stable release.

## Playbook

### 1. Register a New VM Extension

1. Determine the target `subscriptionId`, `location`, `publisher`, `type`, and `version` values.
2. Build the extension metadata map with required properties (source blob URI, compute role, handler schema, etc.).
3. Call PUT `.../publishers/{publisher}/types/{type}/versions/{version}` with the extension map in the body.
4. Confirm the response is 201 (created). If 200, the version already existed and was updated.
5. Verify by calling GET on the same path and inspecting the returned metadata.

### 2. List and Inspect Available Extensions

1. Call GET `.../artifactTypes/VMExtension` to retrieve all registered extensions for the location.
2. Parse the response array and group by publisher or type as needed.
3. For any extension of interest, call GET `.../publishers/{publisher}/types/{type}/versions/{version}` to get full details.
4. Compare version numbers to identify the latest available release.

### 3. Upgrade a VM Extension to a New Version

1. Call GET on the existing version to capture its current metadata and configuration.
2. Modify the extension map with updated properties (new blob URI, updated schema, etc.).
3. Call PUT with the new version number in the path and the updated extension map in the body.
4. Confirm 201 response for the new version.
5. Optionally call DELETE on the old version to remove it from the marketplace.
6. Verify the old version returns 404 on GET and the new version returns 200.

### 4. Clean Up Unused Extension Versions

1. Call GET `.../artifactTypes/VMExtension` to list all registered extensions.
2. Identify versions that are outdated or no longer in use (compare against active deployments).
3. For each unused version, call DELETE `.../publishers/{publisher}/types/{type}/versions/{version}`.
4. Confirm each DELETE returns 200.
5. Re-run the list GET to verify only desired versions remain.

### 5. Verify Extension Existence Before Deployment

1. Call GET `.../publishers/{publisher}/types/{type}/versions/{version}` for the target extension.
2. If 200, the extension is available -- proceed with VM deployment referencing this extension.
3. If 404, the extension must be registered first -- follow the "Register a New VM Extension" playbook.
4. Inspect the returned metadata to confirm compatibility with the target VM compute role.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
