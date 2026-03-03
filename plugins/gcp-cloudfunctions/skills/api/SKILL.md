---
name: cloud-functions-api
description: "Cloud Functions API skill. Use when working with Cloud Functions for {name}, {name}:generateDownloadUrl, {parent}. Covers 13 endpoints."
version: 1.0.0
generator: lapsh
---

# Cloud Functions API
API version: v2

## Auth
OAuth2 | OAuth2

## Base URL
https://cloudfunctions.googleapis.com/

## Setup
1. Configure auth: OAuth2 | OAuth2
2. GET /v2/{name}/locations -- verify access
3. POST /v2/{name}:generateDownloadUrl -- create first resource

## Endpoints

13 endpoints across 6 groups. See references/api-spec.lap for full details.

### {name}
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /v2/{name} | Deletes a function with the given name from the specified project. If the given function is used by some trigger, the trigger will be updated to remove this function. |
| GET | /v2/{name} | Gets the latest state of a long-running operation. Clients can use this method to poll the operation result at intervals as recommended by the API service. |
| PATCH | /v2/{name} | Updates existing function. |
| GET | /v2/{name}/locations | Lists information about the supported locations for this service. |
| GET | /v2/{name}/operations | Lists operations that match the specified filter in the request. If the server doesn't support this method, it returns `UNIMPLEMENTED`. |

### {name}:generateDownloadUrl
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/{name}:generateDownloadUrl | Returns a signed URL for downloading deployed function source code. The URL is only valid for a limited period and should be used within 30 minutes of generation. For more information about the signed URL usage see: https://cloud.google.com/storage/docs/access-control/signed-urls |

### {parent}
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/{parent}/functions | Returns a list of functions that belong to the requested project. |
| POST | /v2/{parent}/functions | Creates a new function. If a function with the given name already exists in the specified project, the long running operation will return `ALREADY_EXISTS` error. |
| POST | /v2/{parent}/functions:generateUploadUrl | Returns a signed URL for uploading a function source code. For more information about the signed URL usage see: https://cloud.google.com/storage/docs/access-control/signed-urls. Once the function source code upload is complete, the used signed URL should be provided in CreateFunction or UpdateFunction request as a reference to the function source code. When uploading source code to the generated signed URL, please follow these restrictions: * Source file type should be a zip file. * No credentials should be attached - the signed URLs provide access to the target bucket using internal service identity; if credentials were attached, the identity from the credentials would be used, but that identity does not have permissions to upload files to the URL. When making a HTTP PUT request, these two headers need to be specified: * `content-type: application/zip` And this header SHOULD NOT be specified: * `Authorization: Bearer YOUR_TOKEN` |
| GET | /v2/{parent}/runtimes | Returns a list of runtimes that are supported for the requested project. |

### {resource}:getIamPolicy
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/{resource}:getIamPolicy | Gets the access control policy for a resource. Returns an empty policy if the resource exists and does not have a policy set. |

### {resource}:setIamPolicy
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/{resource}:setIamPolicy | Sets the access control policy on the specified resource. Replaces any existing policy. Can return `NOT_FOUND`, `INVALID_ARGUMENT`, and `PERMISSION_DENIED` errors. |

### {resource}:testIamPermissions
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/{resource}:testIamPermissions | Returns permissions that a caller has on the specified resource. If the resource does not exist, this will return an empty set of permissions, not a `NOT_FOUND` error. Note: This operation is designed to be used for building permission-aware UIs and command-line tools, not for authorization checking. This operation may "fail open" without warning. |

## Enhanced Skill Content
## Question Mapping

- "List all my Cloud Functions in a project and region?" -> GET /v2/{parent}/functions
- "Get details about a specific Cloud Function?" -> GET /v2/{name}
- "Create a new Cloud Function?" -> POST /v2/{parent}/functions
- "Update a Cloud Function's configuration or source code?" -> PATCH /v2/{name}
- "Delete a Cloud Function?" -> DELETE /v2/{name}
- "Download the source code of a deployed function?" -> POST /v2/{name}:generateDownloadUrl
- "Upload new source code for a function deployment?" -> POST /v2/{parent}/functions:generateUploadUrl
- "What runtimes are available in my project?" -> GET /v2/{parent}/runtimes
- "Who has access to a specific Cloud Function?" -> GET /v2/{resource}:getIamPolicy
- "Grant a user or service account permission to invoke a function?" -> POST /v2/{resource}:setIamPolicy
- "Check if a service account has permission to call a function?" -> POST /v2/{resource}:testIamPermissions
- "List available locations/regions for Cloud Functions?" -> GET /v2/{name}/locations
- "Check the status of a long-running deploy or delete operation?" -> GET /v2/{name}/operations
- "Find all functions with a specific label?" -> GET /v2/{parent}/functions (use `filter` param)
- "Scale a function to zero minimum instances?" -> PATCH /v2/{name} (set `serviceConfig.minInstanceCount: 0`)

## Response Tips

- **Functions list** (`GET /v2/{parent}/functions`): Paginated via `nextPageToken`; also returns `unreachable` array listing regions that failed to respond -- always check this field for partial results.
- **Mutating operations** (CREATE/PATCH/DELETE): Return a long-running `Operation` object, not the final resource. Poll `GET /v2/{name}/operations` or the operation `name` until `done: true`, then inspect `response` for success or `error` for failure.
- **IAM responses**: The `etag` field is opaque and required for safe read-modify-write on policies. Always fetch the current policy before setting a new one.
- **Locations/Operations lists**: Standard pagination with `nextPageToken` and `pageSize`. Pass `pageToken` from previous response to get the next page.
- **Runtimes**: Flat list, no pagination. Each entry includes lifecycle stage (e.g., GA, deprecated, decommissioned).
- **Upload/Download URLs**: Return pre-signed URLs that are time-limited. Use them immediately; do not store for later reuse.

## Anomaly Flags

- **Operation errors**: Surface any operation where `done: true` and `error` is present -- the deploy/delete failed. Show `error.message` and `error.code` prominently.
- **Function state drift**: Flag functions in `FAILED`, `DEPLOYING`, or `UNKNOWN` state -- these require attention.
- **Unreachable regions**: When `unreachable` is non-empty in a list response, warn that results are incomplete and name the missing regions.
- **Deprecated runtimes**: Cross-reference function `buildConfig.runtime` against the runtimes list; flag any function running on a deprecated or decommissioned runtime.
- **Missing IAM bindings**: If `getIamPolicy` returns an empty `bindings` array, flag that the function has no explicit access grants (may be relying on project-level defaults).
- **High instance counts**: Flag functions where `maxInstanceCount` exceeds 100 or `minInstanceCount` exceeds 10 as potential cost concerns.
- **No VPC connector**: For functions accessing private resources, flag when `vpcConnector` is unset.

## Playbook

### Deploy a New Cloud Function from Source

1. Call `POST /v2/{parent}/functions:generateUploadUrl` to get a pre-signed `uploadUrl` and `storageSource`.
2. Upload your source archive (zip) to the `uploadUrl` via HTTP PUT with `Content-Type: application/zip`.
3. Call `POST /v2/{parent}/functions` with `buildConfig.source.storageSource` set to the returned `storageSource`, plus your desired `runtime`, `entryPoint`, and `serviceConfig`.
4. Capture the operation `name` from the response.
5. Poll `GET /v2/{operationName}` until `done: true`. Check `error` for failures or `response` for the created function.

### Update a Function's Environment Variables

1. Call `GET /v2/{name}` to retrieve the current function configuration.
2. Modify the `serviceConfig.environmentVariables` map as needed.
3. Call `PATCH /v2/{name}` with the updated body and `updateMask` set to `serviceConfig.environmentVariables`.
4. Poll the returned operation until `done: true` to confirm the update succeeded.

### Grant Invoke Permission to a Service Account

1. Call `GET /v2/{resource}:getIamPolicy` to fetch the current IAM policy. Save the `etag`.
2. Add a new entry to `bindings` with `role: "roles/cloudfunctions.invoker"` and `members: ["serviceAccount:your-sa@project.iam.gserviceaccount.com"]`.
3. Call `POST /v2/{resource}:setIamPolicy` with the modified `policy` including the original `etag`.
4. Verify the response contains your new binding.

### Audit All Functions Across Regions

1. Call `GET /v2/{name}/locations` to list all available regions.
2. For each location, call `GET /v2/{parent}/functions` with `parent` set to `projects/{project}/locations/{location}`.
3. Page through results using `nextPageToken` until exhausted.
4. Check the `unreachable` field in each response to identify regions that failed to respond.
5. Aggregate results and flag any functions in `FAILED` or `UNKNOWN` state, or running deprecated runtimes.

### Download Function Source Code

1. Call `GET /v2/{name}` to confirm the function exists and note its current state.
2. Call `POST /v2/{name}:generateDownloadUrl` to get a time-limited `downloadUrl`.
3. Immediately download the source archive from `downloadUrl` via HTTP GET.
4. Extract the archive to inspect or modify the source locally.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
