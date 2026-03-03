---
name: amazon-workdocs
description: "Amazon WorkDocs API skill. Use when working with Amazon WorkDocs for api. Covers 44 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon WorkDocs
API version: 2016-05-01

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /api/v1/activities -- verify access
3. POST /api/v1/users/{UserId}/activation -- create first activation

## Endpoints

44 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /api/v1/documents/{DocumentId}/versions/{VersionId} | Aborts the upload of the specified document version that was previously initiated by InitiateDocumentVersionUpload. The client should make this call only when it no longer intends to upload the document version, or fails to do so. |
| POST | /api/v1/users/{UserId}/activation | Activates the specified user. Only active users can access Amazon WorkDocs. |
| POST | /api/v1/resources/{ResourceId}/permissions | Creates a set of permissions for the specified folder or document. The resource permissions are overwritten if the principals already have different permissions. |
| POST | /api/v1/documents/{DocumentId}/versions/{VersionId}/comment | Adds a new comment to the specified document version. |
| PUT | /api/v1/resources/{ResourceId}/customMetadata | Adds one or more custom properties to the specified resource (a folder, document, or version). |
| POST | /api/v1/folders | Creates a folder with the specified name and parent folder. |
| PUT | /api/v1/resources/{ResourceId}/labels | Adds the specified list of labels to the given resource (a document or folder) |
| POST | /api/v1/organizations/{OrganizationId}/subscriptions | Configure Amazon WorkDocs to use Amazon SNS notifications. The endpoint receives a confirmation message, and must confirm the subscription. For more information, see Setting up notifications for an IAM user or role in the Amazon WorkDocs Developer Guide. |
| POST | /api/v1/users | Creates a user in a Simple AD or Microsoft AD directory. The status of a newly created user is "ACTIVE". New users can access Amazon WorkDocs. |
| DELETE | /api/v1/users/{UserId}/activation | Deactivates the specified user, which revokes the user's access to Amazon WorkDocs. |
| DELETE | /api/v1/documents/{DocumentId}/versions/{VersionId}/comment/{CommentId} | Deletes the specified comment from the document version. |
| DELETE | /api/v1/resources/{ResourceId}/customMetadata | Deletes custom metadata from the specified resource. |
| DELETE | /api/v1/documents/{DocumentId} | Permanently deletes the specified document and its associated metadata. |
| DELETE | /api/v1/documentVersions/{DocumentId}/versions/{VersionId} | Deletes a specific version of a document. |
| DELETE | /api/v1/folders/{FolderId} | Permanently deletes the specified folder and its contents. |
| DELETE | /api/v1/folders/{FolderId}/contents | Deletes the contents of the specified folder. |
| DELETE | /api/v1/resources/{ResourceId}/labels | Deletes the specified list of labels from a resource. |
| DELETE | /api/v1/organizations/{OrganizationId}/subscriptions/{SubscriptionId} | Deletes the specified subscription from the specified organization. |
| DELETE | /api/v1/users/{UserId} | Deletes the specified user from a Simple AD or Microsoft AD directory.  Deleting a user immediately and permanently deletes all content in that user's folder structure. Site retention policies do NOT apply to this type of deletion. |
| GET | /api/v1/activities | Describes the user activities in a specified time period. |
| GET | /api/v1/documents/{DocumentId}/versions/{VersionId}/comments | List all the comments for the specified document version. |
| GET | /api/v1/documents/{DocumentId}/versions | Retrieves the document versions for the specified document. By default, only active versions are returned. |
| GET | /api/v1/folders/{FolderId}/contents | Describes the contents of the specified folder, including its documents and subfolders. By default, Amazon WorkDocs returns the first 100 active document and folder metadata items. If there are more results, the response includes a marker that you can use to request the next set of results. You can also request initialized documents. |
| GET | /api/v1/groups | Describes the groups specified by the query. Groups are defined by the underlying Active Directory. |
| GET | /api/v1/organizations/{OrganizationId}/subscriptions | Lists the specified notification subscriptions. |
| GET | /api/v1/resources/{ResourceId}/permissions | Describes the permissions of a specified resource. |
| GET | /api/v1/me/root | Describes the current user's special folders; the RootFolder and the RecycleBin. RootFolder is the root of user's files and folders and RecycleBin is the root of recycled items. This is not a valid action for SigV4 (administrative API) clients. This action requires an authentication token. To get an authentication token, register an application with Amazon WorkDocs. For more information, see Authentication and Access Control for User Applications in the Amazon WorkDocs Developer Guide. |
| GET | /api/v1/users | Describes the specified users. You can describe all users or filter the results (for example, by status or organization). By default, Amazon WorkDocs returns the first 24 active or pending users. If there are more results, the response includes a marker that you can use to request the next set of results. |
| GET | /api/v1/me | Retrieves details of the current user for whom the authentication token was generated. This is not a valid action for SigV4 (administrative API) clients. This action requires an authentication token. To get an authentication token, register an application with Amazon WorkDocs. For more information, see Authentication and Access Control for User Applications in the Amazon WorkDocs Developer Guide. |
| GET | /api/v1/documents/{DocumentId} | Retrieves details of a document. |
| GET | /api/v1/documents/{DocumentId}/path | Retrieves the path information (the hierarchy from the root folder) for the requested document. By default, Amazon WorkDocs returns a maximum of 100 levels upwards from the requested document and only includes the IDs of the parent folders in the path. You can limit the maximum number of levels. You can also request the names of the parent folders. |
| GET | /api/v1/documents/{DocumentId}/versions/{VersionId} | Retrieves version metadata for the specified document. |
| GET | /api/v1/folders/{FolderId} | Retrieves the metadata of the specified folder. |
| GET | /api/v1/folders/{FolderId}/path | Retrieves the path information (the hierarchy from the root folder) for the specified folder. By default, Amazon WorkDocs returns a maximum of 100 levels upwards from the requested folder and only includes the IDs of the parent folders in the path. You can limit the maximum number of levels. You can also request the parent folder names. |
| GET | /api/v1/resources | Retrieves a collection of resources, including folders and documents. The only CollectionType supported is SHARED_WITH_ME. |
| POST | /api/v1/documents | Creates a new document object and version object. The client specifies the parent folder ID and name of the document to upload. The ID is optionally specified when creating a new version of an existing document. This is the first step to upload a document. Next, upload the document to the URL returned from the call, and then call UpdateDocumentVersion. To cancel the document upload, call AbortDocumentVersionUpload. |
| DELETE | /api/v1/resources/{ResourceId}/permissions | Removes all the permissions from the specified resource. |
| DELETE | /api/v1/resources/{ResourceId}/permissions/{PrincipalId} | Removes the permission for the specified principal from the specified resource. |
| POST | /api/v1/documentVersions/restore/{DocumentId} | Recovers a deleted version of an Amazon WorkDocs document. |
| POST | /api/v1/search | Searches metadata and the content of folders, documents, document versions, and comments. |
| PATCH | /api/v1/documents/{DocumentId} | Updates the specified attributes of a document. The user must have access to both the document and its parent folder, if applicable. |
| PATCH | /api/v1/documents/{DocumentId}/versions/{VersionId} | Changes the status of the document version to ACTIVE.  Amazon WorkDocs also sets its document container to ACTIVE. This is the last step in a document upload, after the client uploads the document to an S3-presigned URL returned by InitiateDocumentVersionUpload. |
| PATCH | /api/v1/folders/{FolderId} | Updates the specified attributes of the specified folder. The user must have access to both the folder and its parent folder, if applicable. |
| PATCH | /api/v1/users/{UserId} | Updates the specified attributes of the specified user, and grants or revokes administrative privileges to the Amazon WorkDocs site. |

## Enhanced Skill Content
## Question Mapping

- "How do I upload a new document to a folder?" -> POST /api/v1/documents
- "What files and folders are inside a specific folder?" -> GET /api/v1/folders/{FolderId}/contents
- "Who has access to this document?" -> GET /api/v1/resources/{ResourceId}/permissions
- "How do I share a document with another user?" -> POST /api/v1/resources/{ResourceId}/permissions
- "How do I search for a document by name or content?" -> POST /api/v1/search
- "What is the current user's root folder?" -> GET /api/v1/me/root
- "How do I move a document to a different folder?" -> PATCH /api/v1/documents/{DocumentId}
- "How do I add a comment to a document?" -> POST /api/v1/documents/{DocumentId}/versions/{VersionId}/comment
- "How do I see the version history of a document?" -> GET /api/v1/documents/{DocumentId}/versions
- "How do I delete a folder and everything in it?" -> DELETE /api/v1/folders/{FolderId}/contents then DELETE /api/v1/folders/{FolderId}
- "How do I create a new user account?" -> POST /api/v1/users
- "How do I deactivate a user?" -> DELETE /api/v1/users/{UserId}/activation
- "What activity has happened on a resource recently?" -> GET /api/v1/activities
- "How do I restore a deleted document?" -> POST /api/v1/documentVersions/restore/{DocumentId}
- "How do I tag a resource with labels?" -> PUT /api/v1/resources/{ResourceId}/labels

## Response Tips

- **Listings (folders, users, groups, subscriptions):** All return a `Marker` field for cursor-based pagination. Pass the returned `Marker` as the `marker` query param in the next request. Stop when `Marker` is null or absent.
- **Document creation:** `POST /documents` returns both `Metadata` and `UploadMetadata` with a pre-signed `UploadUrl`. You must PUT file bytes to that URL using the `SignedHeaders` to complete the upload.
- **User objects:** Nested `Storage.StorageRule` contains allocation and type; `Storage.StorageUtilizedInBytes` shows current usage. Both can be null.
- **Comments:** The `Comment` response nests a full `Contributor` (User) object. Use `CommentId` for deletes, `ThreadId`/`ParentId` for threading.
- **Permissions:** The `ShareResults` array from POST may contain per-principal success/failure statuses -- always iterate to confirm each share succeeded.
- **Custom metadata:** Returned as a flat `map<str,str>` alongside `Metadata`. Only present when `includeCustomMetadata=true` on GET requests.
- **Search results:** `Items` is an array of `ResponseItem` objects, not raw document metadata. Use `AdditionalResponseFields` to control which fields are included.
- **Errors:** AWS-style errors return HTTP 4xx/5xx with an error type string (e.g., `EntityNotExistsException`, `UnauthorizedResourceAccessException`). Match on the error type, not the message.

## Anomaly Flags

- **Storage quota near limit:** When `StorageUtilizedInBytes` approaches `StorageAllocatedInBytes` on a user, warn before upload attempts will fail.
- **Deactivated users:** If a user's `Status` is not `ACTIVE`, flag that operations on their behalf will likely fail with authorization errors.
- **Empty upload URL:** If `POST /documents` returns `Metadata` but `UploadMetadata.UploadUrl` is null, the document was created but content cannot be uploaded -- surface immediately.
- **ResourceState changes:** When `ResourceState` is `RECYCLING` or `RECYCLED` on a document or folder, flag that the resource is in the trash and may be permanently deleted.
- **Pagination loops:** If the same `Marker` value is returned twice in succession, flag a potential infinite pagination loop and stop.
- **Missing permissions on share:** If any entry in `ShareResults` indicates failure (e.g., status is not success), surface which principals could not be added and the reason.
- **Deprecated version status:** When a `DocumentVersionMetadata.Status` is not `ACTIVE`, flag that the version may be a draft or otherwise unavailable for download.
- **Large folder contents:** If `GET /folders/{id}/contents` returns a `Marker` on the first page, warn the user the folder has many items and full enumeration may require multiple requests.

## Playbook

### 1. Upload a Document to a Folder

1. Identify the target folder ID (use `GET /api/v1/me/root` for the current user's root, or `GET /api/v1/folders/{FolderId}/contents` to browse).
2. Call `POST /api/v1/documents` with `ParentFolderId`, `Name`, `ContentType`, and `DocumentSizeInBytes`.
3. Extract `UploadMetadata.UploadUrl` and `UploadMetadata.SignedHeaders` from the response.
4. PUT the raw file bytes to the `UploadUrl`, including all `SignedHeaders` in the request.
5. Verify upload by calling `GET /api/v1/documents/{DocumentId}` and checking `LatestVersionMetadata.Status` is `ACTIVE`.

### 2. Share a Document and Notify Collaborators

1. Get the document's `ResourceId` (same as `DocumentId`).
2. Build a `Principals` array with each `SharePrincipal` specifying user/group ID, role, and type.
3. Call `POST /api/v1/resources/{ResourceId}/permissions` with the principals and `NotificationOptions` to send email.
4. Inspect `ShareResults` in the response to confirm each principal was added successfully.
5. Verify final permissions with `GET /api/v1/resources/{ResourceId}/permissions`.

### 3. Review and Comment on a Document Version

1. Call `GET /api/v1/documents/{DocumentId}/versions` to list all versions.
2. Pick the target `VersionId` (usually the latest).
3. Call `GET /api/v1/documents/{DocumentId}/versions/{VersionId}/comments` to see existing discussion.
4. Add your comment with `POST /api/v1/documents/{DocumentId}/versions/{VersionId}/comment`, providing `Text` and optionally `ThreadId` to reply in-thread.
5. Set `Visibility` to `PUBLIC` or `PRIVATE` depending on audience.

### 4. Organize Documents with Folders and Labels

1. Create a folder with `POST /api/v1/folders`, passing the `ParentFolderId` and `Name`.
2. Move documents into it with `PATCH /api/v1/documents/{DocumentId}`, setting `ParentFolderId` to the new folder ID.
3. Apply labels with `PUT /api/v1/resources/{ResourceId}/labels`, passing an array of label strings.
4. Add custom metadata with `PUT /api/v1/resources/{ResourceId}/customMetadata` for key-value tagging.
5. Browse the organized structure with `GET /api/v1/folders/{FolderId}/contents`, using `sort` and `order` params.

### 5. Audit Recent Activity Across the Organization

1. Call `GET /api/v1/activities` with `organizationId` and a `startTime`/`endTime` window.
2. Optionally filter by `activityTypes` (e.g., document uploads, permission changes) or `userId`.
3. Set `includeIndirectActivities=true` to capture actions triggered by shares or automation.
4. Page through results using `Marker` until it is absent.
5. For each activity referencing a resource, call `GET /api/v1/documents/{DocumentId}` or `GET /api/v1/folders/{FolderId}` to get current state and confirm no anomalies.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
