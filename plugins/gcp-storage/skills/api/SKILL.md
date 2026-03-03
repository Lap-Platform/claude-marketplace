---
name: cloud-storage-json-api
description: "Cloud Storage JSON API skill. Use when working with Cloud Storage JSON for b, channels, projects. Covers 52 endpoints."
version: 1.0.0
generator: lapsh
---

# Cloud Storage JSON API
API version: v1

## Auth
OAuth2 | OAuth2

## Base URL
https://storage.googleapis.com/storage/v1

## Setup
1. Configure auth: OAuth2 | OAuth2
2. GET /b -- verify access
3. POST /b -- create first b

## Endpoints

52 endpoints across 3 groups. See references/api-spec.lap for full details.

### b
| Method | Path | Description |
|--------|------|-------------|
| GET | /b | Retrieves a list of buckets for a given project. |
| POST | /b | Creates a new bucket. |
| DELETE | /b/{bucket} | Permanently deletes an empty bucket. |
| GET | /b/{bucket} | Returns metadata for the specified bucket. |
| PATCH | /b/{bucket} | Patches a bucket. Changes to the bucket will be readable immediately after writing, but configuration changes may take time to propagate. |
| PUT | /b/{bucket} | Updates a bucket. Changes to the bucket will be readable immediately after writing, but configuration changes may take time to propagate. |
| GET | /b/{bucket}/acl | Retrieves ACL entries on the specified bucket. |
| POST | /b/{bucket}/acl | Creates a new ACL entry on the specified bucket. |
| DELETE | /b/{bucket}/acl/{entity} | Permanently deletes the ACL entry for the specified entity on the specified bucket. |
| GET | /b/{bucket}/acl/{entity} | Returns the ACL entry for the specified entity on the specified bucket. |
| PATCH | /b/{bucket}/acl/{entity} | Patches an ACL entry on the specified bucket. |
| PUT | /b/{bucket}/acl/{entity} | Updates an ACL entry on the specified bucket. |
| GET | /b/{bucket}/defaultObjectAcl | Retrieves default object ACL entries on the specified bucket. |
| POST | /b/{bucket}/defaultObjectAcl | Creates a new default object ACL entry on the specified bucket. |
| DELETE | /b/{bucket}/defaultObjectAcl/{entity} | Permanently deletes the default object ACL entry for the specified entity on the specified bucket. |
| GET | /b/{bucket}/defaultObjectAcl/{entity} | Returns the default object ACL entry for the specified entity on the specified bucket. |
| PATCH | /b/{bucket}/defaultObjectAcl/{entity} | Patches a default object ACL entry on the specified bucket. |
| PUT | /b/{bucket}/defaultObjectAcl/{entity} | Updates a default object ACL entry on the specified bucket. |
| GET | /b/{bucket}/iam | Returns an IAM policy for the specified bucket. |
| PUT | /b/{bucket}/iam | Updates an IAM policy for the specified bucket. |
| GET | /b/{bucket}/iam/testPermissions | Tests a set of permissions on the given bucket to see which, if any, are held by the caller. |
| POST | /b/{bucket}/lockRetentionPolicy | Locks retention policy on a bucket. |
| GET | /b/{bucket}/notificationConfigs | Retrieves a list of notification subscriptions for a given bucket. |
| POST | /b/{bucket}/notificationConfigs | Creates a notification subscription for a given bucket. |
| DELETE | /b/{bucket}/notificationConfigs/{notification} | Permanently deletes a notification subscription. |
| GET | /b/{bucket}/notificationConfigs/{notification} | View a notification configuration. |
| GET | /b/{bucket}/o | Retrieves a list of objects matching the criteria. |
| POST | /b/{bucket}/o | Stores a new object and metadata. |
| POST | /b/{bucket}/o/watch | Watch for changes on all objects in a bucket. |
| DELETE | /b/{bucket}/o/{object} | Deletes an object and its metadata. Deletions are permanent if versioning is not enabled for the bucket, or if the generation parameter is used. |
| GET | /b/{bucket}/o/{object} | Retrieves an object or its metadata. |
| PATCH | /b/{bucket}/o/{object} | Patches an object's metadata. |
| PUT | /b/{bucket}/o/{object} | Updates an object's metadata. |
| GET | /b/{bucket}/o/{object}/acl | Retrieves ACL entries on the specified object. |
| POST | /b/{bucket}/o/{object}/acl | Creates a new ACL entry on the specified object. |
| DELETE | /b/{bucket}/o/{object}/acl/{entity} | Permanently deletes the ACL entry for the specified entity on the specified object. |
| GET | /b/{bucket}/o/{object}/acl/{entity} | Returns the ACL entry for the specified entity on the specified object. |
| PATCH | /b/{bucket}/o/{object}/acl/{entity} | Patches an ACL entry on the specified object. |
| PUT | /b/{bucket}/o/{object}/acl/{entity} | Updates an ACL entry on the specified object. |
| GET | /b/{bucket}/o/{object}/iam | Returns an IAM policy for the specified object. |
| PUT | /b/{bucket}/o/{object}/iam | Updates an IAM policy for the specified object. |
| GET | /b/{bucket}/o/{object}/iam/testPermissions | Tests a set of permissions on the given object to see which, if any, are held by the caller. |
| POST | /b/{destinationBucket}/o/{destinationObject}/compose | Concatenates a list of existing objects into a new object in the same bucket. |
| POST | /b/{sourceBucket}/o/{sourceObject}/copyTo/b/{destinationBucket}/o/{destinationObject} | Copies a source object to a destination object. Optionally overrides metadata. |
| POST | /b/{sourceBucket}/o/{sourceObject}/rewriteTo/b/{destinationBucket}/o/{destinationObject} | Rewrites a source object to a destination object. Optionally overrides metadata. |

### channels
| Method | Path | Description |
|--------|------|-------------|
| POST | /channels/stop | Stop watching resources through this channel |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects/{projectId}/hmacKeys | Retrieves a list of HMAC keys matching the criteria. |
| POST | /projects/{projectId}/hmacKeys | Creates a new HMAC key for the specified service account. |
| DELETE | /projects/{projectId}/hmacKeys/{accessId} | Deletes an HMAC key. |
| GET | /projects/{projectId}/hmacKeys/{accessId} | Retrieves an HMAC key's metadata |
| PUT | /projects/{projectId}/hmacKeys/{accessId} | Updates the state of an HMAC key. See the HMAC Key resource descriptor for valid states. |
| GET | /projects/{projectId}/serviceAccount | Get the email address of this project's Google Cloud Storage service account. |

## Enhanced Skill Content
## Question Mapping

- "What buckets exist in my project?" -> GET /b
- "How do I create a new storage bucket?" -> POST /b
- "What are the details of a specific bucket?" -> GET /b/{bucket}
- "How do I delete a bucket?" -> DELETE /b/{bucket}
- "How do I update bucket settings like versioning or lifecycle rules?" -> PATCH /b/{bucket}
- "What objects are in a bucket?" -> GET /b/{bucket}/o
- "How do I upload a file to a bucket?" -> POST /b/{bucket}/o
- "How do I download or get metadata for a specific object?" -> GET /b/{bucket}/o/{object}
- "How do I copy an object to another bucket?" -> POST /b/{sourceBucket}/o/{sourceObject}/copyTo/b/{destinationBucket}/o/{destinationObject}
- "How do I compose multiple objects into one?" -> POST /b/{destinationBucket}/o/{destinationObject}/compose
- "Who has access to this bucket?" -> GET /b/{bucket}/iam
- "How do I set permissions on a bucket?" -> PUT /b/{bucket}/iam
- "How do I move a large object across buckets with resumable rewrite?" -> POST /b/{sourceBucket}/o/{sourceObject}/rewriteTo/b/{destinationBucket}/o/{destinationObject}
- "How do I manage HMAC keys for service accounts?" -> GET /projects/{projectId}/hmacKeys
- "How do I stop receiving change notifications?" -> POST /channels/stop

## Response Tips

- **Bucket/Object listings** (`GET /b`, `GET /b/{bucket}/o`): Paginated via `nextPageToken` -- keep calling with `pageToken` until `nextPageToken` is absent. Items live in the `items` array; `prefixes` array appears on object lists when using `delimiter`.
- **Bucket/Object metadata** (`GET /b/{bucket}`, `GET /b/{bucket}/o/{object}`): Deeply nested -- check `iamConfiguration.uniformBucketLevelAccess.enabled` for access model, `lifecycle.rule` for retention rules, `retentionPolicy.isLocked` before attempting changes.
- **ACL endpoints** (`/acl`, `/defaultObjectAcl`): Return flat objects with `entity` as the principal identifier (e.g., `user-email`, `project-team-READERS`). `role` is one of READER, WRITER, OWNER.
- **IAM endpoints** (`/iam`): Return `bindings` array with `role` + `members` pairs. Always include `etag` on PUT to avoid conflicts.
- **Rewrite responses**: Check `done: bool` -- if false, re-send with the returned `rewriteToken` to continue. `totalBytesRewritten` and `objectSize` track progress.
- **HMAC key creation**: The `secret` field is only returned on POST (creation) -- store it immediately, it cannot be retrieved again.

## Anomaly Flags

- **Rewrite not completing in one call**: When `done: false` is returned from rewrite, surface that the operation requires multiple rounds and provide the `rewriteToken` for continuation.
- **Retention policy lock warning**: `POST /b/{bucket}/lockRetentionPolicy` is irreversible -- flag any attempt to lock retention and confirm the `ifMetagenerationMatch` value is current.
- **Uniform bucket-level access enabled**: When `iamConfiguration.uniformBucketLevelAccess.enabled` is true, ACL endpoints will fail -- surface this before attempting ACL operations.
- **Object versioning active**: When `versioning.enabled` is true on a bucket, deletes create archived versions rather than permanently removing -- flag the storage cost implication.
- **Missing nextPageToken assumption**: If a list call returns fewer items than expected but no `nextPageToken`, the result set is complete -- surface this to avoid infinite pagination loops.
- **HMAC key in DELETED state**: If `showDeletedKeys` returns keys with `state: DELETED`, surface that these are non-recoverable and only visible for audit purposes.
- **Requester-pays bucket**: When `billing.requesterPays` is true, all requests must include `userProject` or they will fail with 400 -- flag this on bucket metadata retrieval.

## Playbook

### 1. Upload and Verify an Object

1. List existing objects to check for conflicts: `GET /b/{bucket}/o?prefix={name}`
2. Upload the object: `POST /b/{bucket}/o` with `name` and content
3. Retrieve metadata to verify: `GET /b/{bucket}/o/{object}`
4. Confirm `md5Hash` and `size` match your source file
5. Optionally set ACL: `PATCH /b/{bucket}/o/{object}` with `predefinedAcl`

### 2. Move an Object Across Buckets (Large Files)

1. Initiate rewrite: `POST /b/{src}/o/{obj}/rewriteTo/b/{dst}/o/{obj}`
2. Check response for `done: true` -- if false, re-send with `rewriteToken`
3. Repeat step 2 until `done: true` (track progress via `totalBytesRewritten / objectSize`)
4. Verify destination object: `GET /b/{dst}/o/{obj}`
5. Delete source object: `DELETE /b/{src}/o/{obj}`

### 3. Configure a Bucket with Lifecycle and Versioning

1. Get current bucket config: `GET /b/{bucket}?projection=full`
2. Enable versioning: `PATCH /b/{bucket}` with `versioning: {enabled: true}`
3. Add lifecycle rules: `PATCH /b/{bucket}` with `lifecycle: {rule: [{action: {type: "Delete"}, condition: {age: 30}}]}`
4. Verify applied settings: `GET /b/{bucket}` and confirm `versioning` and `lifecycle` fields

### 4. Set Up Bucket Change Notifications

1. Create a notification config: `POST /b/{bucket}/notificationConfigs` with `topic` (Pub/Sub topic) and optional `event_types` filter
2. List active notifications: `GET /b/{bucket}/notificationConfigs`
3. Verify the new config appears with correct `topic` and `payload_format`
4. To stop a watch channel: `POST /channels/stop` with `id` and `resourceId` from the watch response
5. To clean up: `DELETE /b/{bucket}/notificationConfigs/{notification}`

### 5. Manage HMAC Keys for Service Account Auth

1. Get the project service account: `GET /projects/{projectId}/serviceAccount`
2. Create an HMAC key: `POST /projects/{projectId}/hmacKeys?serviceAccountEmail={email}`
3. Immediately store the `secret` from the response (shown only once)
4. List keys to verify: `GET /projects/{projectId}/hmacKeys`
5. To rotate: create a new key (step 2), update your application, then deactivate the old key via `PUT /projects/{projectId}/hmacKeys/{accessId}` with `state: INACTIVE`, and finally delete with `DELETE /projects/{projectId}/hmacKeys/{accessId}`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
