---
name: drive-api
description: "Drive API skill. Use when working with Drive for about, changes, channels. Covers 48 endpoints."
version: 1.0.0
generator: lapsh
---

# Drive API
API version: v3

## Auth
OAuth2 | OAuth2

## Base URL
https://www.googleapis.com/drive/v3

## Setup
1. Configure auth: OAuth2 | OAuth2
2. GET /about -- verify access
3. POST /changes/watch -- create first watch

## Endpoints

48 endpoints across 6 groups. See references/api-spec.lap for full details.

### about
| Method | Path | Description |
|--------|------|-------------|
| GET | /about | Gets information about the user, the user's Drive, and system capabilities. |

### changes
| Method | Path | Description |
|--------|------|-------------|
| GET | /changes | Lists the changes for a user or shared drive. |
| GET | /changes/startPageToken | Gets the starting pageToken for listing future changes. |
| POST | /changes/watch | Subscribes to changes for a user. To use this method, you must include the pageToken query parameter. |

### channels
| Method | Path | Description |
|--------|------|-------------|
| POST | /channels/stop | Stop watching resources through this channel |

### drives
| Method | Path | Description |
|--------|------|-------------|
| GET | /drives | Lists the user's shared drives. |
| POST | /drives | Creates a shared drive. |
| DELETE | /drives/{driveId} | Permanently deletes a shared drive for which the user is an organizer. The shared drive cannot contain any untrashed items. |
| GET | /drives/{driveId} | Gets a shared drive's metadata by ID. |
| PATCH | /drives/{driveId} | Updates the metadata for a shared drive. |
| POST | /drives/{driveId}/hide | Hides a shared drive from the default view. |
| POST | /drives/{driveId}/unhide | Restores a shared drive to the default view. |

### files
| Method | Path | Description |
|--------|------|-------------|
| GET | /files | Lists or searches files. |
| POST | /files | Creates a file. |
| GET | /files/generateIds | Generates a set of file IDs which can be provided in create or copy requests. |
| DELETE | /files/trash | Permanently deletes all of the user's trashed files. |
| DELETE | /files/{fileId} | Permanently deletes a file owned by the user without moving it to the trash. If the file belongs to a shared drive the user must be an organizer on the parent. If the target is a folder, all descendants owned by the user are also deleted. |
| GET | /files/{fileId} | Gets a file's metadata or content by ID. |
| PATCH | /files/{fileId} | Updates a file's metadata and/or content. When calling this method, only populate fields in the request that you want to modify. When updating fields, some fields might change automatically, such as modifiedDate. This method supports patch semantics. |
| GET | /files/{fileId}/comments | Lists a file's comments. |
| POST | /files/{fileId}/comments | Creates a comment on a file. |
| DELETE | /files/{fileId}/comments/{commentId} | Deletes a comment. |
| GET | /files/{fileId}/comments/{commentId} | Gets a comment by ID. |
| PATCH | /files/{fileId}/comments/{commentId} | Updates a comment with patch semantics. |
| GET | /files/{fileId}/comments/{commentId}/replies | Lists a comment's replies. |
| POST | /files/{fileId}/comments/{commentId}/replies | Creates a reply to a comment. |
| DELETE | /files/{fileId}/comments/{commentId}/replies/{replyId} | Deletes a reply. |
| GET | /files/{fileId}/comments/{commentId}/replies/{replyId} | Gets a reply by ID. |
| PATCH | /files/{fileId}/comments/{commentId}/replies/{replyId} | Updates a reply with patch semantics. |
| POST | /files/{fileId}/copy | Creates a copy of a file and applies any requested updates with patch semantics. Folders cannot be copied. |
| GET | /files/{fileId}/export | Exports a Google Workspace document to the requested MIME type and returns exported byte content. Note that the exported content is limited to 10MB. |
| GET | /files/{fileId}/listLabels | Lists the labels on a file. |
| POST | /files/{fileId}/modifyLabels | Modifies the set of labels on a file. |
| GET | /files/{fileId}/permissions | Lists a file's or shared drive's permissions. |
| POST | /files/{fileId}/permissions | Creates a permission for a file or shared drive. For more information on creating permissions, see Share files, folders & drives. |
| DELETE | /files/{fileId}/permissions/{permissionId} | Deletes a permission. |
| GET | /files/{fileId}/permissions/{permissionId} | Gets a permission by ID. |
| PATCH | /files/{fileId}/permissions/{permissionId} | Updates a permission with patch semantics. |
| GET | /files/{fileId}/revisions | Lists a file's revisions. |
| DELETE | /files/{fileId}/revisions/{revisionId} | Permanently deletes a file version. You can only delete revisions for files with binary content in Google Drive, like images or videos. Revisions for other files, like Google Docs or Sheets, and the last remaining file version can't be deleted. |
| GET | /files/{fileId}/revisions/{revisionId} | Gets a revision's metadata or content by ID. |
| PATCH | /files/{fileId}/revisions/{revisionId} | Updates a revision with patch semantics. |
| POST | /files/{fileId}/watch | Subscribes to changes to a file. |

### teamdrives
| Method | Path | Description |
|--------|------|-------------|
| GET | /teamdrives | Deprecated use drives.list instead. |
| POST | /teamdrives | Deprecated use drives.create instead. |
| DELETE | /teamdrives/{teamDriveId} | Deprecated use drives.delete instead. |
| GET | /teamdrives/{teamDriveId} | Deprecated use drives.get instead. |
| PATCH | /teamdrives/{teamDriveId} | Deprecated use drives.update instead |

## Enhanced Skill Content
## Question Mapping

- "How much storage am I using?" -> GET /about
- "List all files in my Drive" -> GET /files
- "Find files named 'budget' in my Drive?" -> GET /files (use `q` parameter with `name contains 'budget'`)
- "What changed since my last sync?" -> GET /changes (requires `pageToken` from GET /changes/startPageToken)
- "Who has access to this file?" -> GET /files/{fileId}/permissions
- "Share a file with someone by email?" -> POST /files/{fileId}/permissions
- "How do I move a file to a different folder?" -> PATCH /files/{fileId} (use `addParents` and `removeParents`)
- "Download a Google Doc as PDF?" -> GET /files/{fileId}/export (set `mimeType=application/pdf`)
- "Delete a file permanently?" -> DELETE /files/{fileId}
- "Copy a file to a new location?" -> POST /files/{fileId}/copy
- "List all shared drives I have access to?" -> GET /drives
- "Get all comments on a document?" -> GET /files/{fileId}/comments
- "Watch a file for changes?" -> POST /files/{fileId}/watch
- "Stop receiving notifications for a channel?" -> POST /channels/stop
- "What are the revision history entries for a file?" -> GET /files/{fileId}/revisions

## Response Tips

- **Files & Drives lists**: Paginated via `nextPageToken` -- keep calling with `pageToken` until `nextPageToken` is absent or empty. Default `pageSize` is small (100 for files, 10 for drives); increase it to reduce round-trips.
- **Changes feed**: Returns `newStartPageToken` when you have consumed all changes (no more pages); store it for next poll. If `nextPageToken` is present instead, there are more pages to fetch.
- **File metadata**: The `capabilities` map is your permission truth -- check `canEdit`, `canShare`, `canDelete` before attempting write operations rather than guessing from `role`.
- **Comments & replies**: Nested structure -- comments contain `replies` arrays. Deleted items remain in responses with `deleted: true`; filter client-side unless `includeDeleted` is explicitly false.
- **Permissions**: The `type` field distinguishes `user`, `group`, `domain`, and `anyone` scopes. `permissionDetails` is an array showing inherited vs. direct grants.
- **Revisions**: `size` and numeric IDs are returned as strings (int64 format) -- parse them explicitly. `keepForever` defaults to false; old revisions get auto-purged.
- **Error responses**: Not in the 200 schema. Expect `{error: {code, message, errors[]}}` on 4xx/5xx. Common: 403 (insufficient permissions), 404 (file not found or no access), 429 (rate limited).

## Anomaly Flags

- **Rate limit proximity**: Surface HTTP 429 responses or `userRateLimitExceeded` / `rateLimitExceeded` error reasons immediately -- back off exponentially before retrying.
- **Storage quota near limit**: After GET /about, flag when `storageQuota.usage` approaches `storageQuota.limit` (e.g., >90% used).
- **Deprecated Team Drives usage**: Any use of `/teamdrives` endpoints or `supportsTeamDrives`/`teamDriveId` parameters -- these are legacy; recommend migrating to `/drives` and `supportsAllDrives`/`driveId`.
- **Trashed file operations**: Flag when `trashed: true` or `explicitlyTrashed: true` appears on a file the user is trying to work with -- they may not realize the file is in trash.
- **Incomplete search results**: When `incompleteSearch: true` appears in GET /files response, the result set is partial and the user should narrow their query.
- **Expiring permissions**: When `expirationTime` is present on a permission and is approaching, alert the user that access will be revoked soon.
- **Missing capabilities**: Before destructive or sharing operations, check the file's `capabilities` map and warn if the required capability (e.g., `canShare`, `canDelete`) is false.

## Playbook

### 1. Poll for Recent Changes (Incremental Sync)

1. Call GET /changes/startPageToken to get an initial `startPageToken` (first run only; store it persistently).
2. Call GET /changes with `pageToken` set to the stored token and `includeItemsFromAllDrives: true`, `supportsAllDrives: true`.
3. Process each entry in the `changes` array (file metadata, removal flags).
4. If `nextPageToken` is present, repeat step 2 with that token.
5. When `newStartPageToken` appears instead, store it for the next poll cycle.

### 2. Share a File and Notify the Recipient

1. Call GET /files/{fileId} to confirm the file exists and check `capabilities.canShare`.
2. Call POST /files/{fileId}/permissions with body `{type: "user", role: "writer", emailAddress: "user@example.com"}` and query `sendNotificationEmail=true`, optionally with `emailMessage`.
3. Verify the returned permission object has the expected `role` and `emailAddress`.
4. Optionally call GET /files/{fileId}/permissions to confirm the full permission list.

### 3. Export a Google Workspace Document

1. Call GET /files/{fileId} to retrieve the file's `mimeType` and confirm it is a Google Workspace type (e.g., `application/vnd.google-apps.document`).
2. Call GET /about and inspect `exportFormats` to find supported export MIME types for that source type.
3. Call GET /files/{fileId}/export with `mimeType` set to the desired format (e.g., `application/pdf`).
4. The response body is the binary file content -- stream it directly to disk or the client.

### 4. Organize Files into a Shared Drive Folder

1. Call GET /drives to list available shared drives; identify the target `driveId`.
2. Call GET /files with `q: "'<folderId>' in parents"`, `driveId`, `supportsAllDrives: true`, `includeItemsFromAllDrives: true` to see current contents.
3. To move a file in, call PATCH /files/{fileId} with `addParents=<targetFolderId>`, `removeParents=<currentParentId>`, and `supportsAllDrives: true`.
4. To upload a new file, call POST /files with the file metadata including `parents: ["<targetFolderId>"]` and `supportsAllDrives: true`.

### 5. Set Up Push Notifications for a File

1. Call POST /files/{fileId}/watch with body `{id: "<unique-channel-id>", type: "web_hook", address: "https://your-server.com/webhook"}`.
2. Store the returned `resourceId` and `id` -- you will need both to stop the channel later.
3. Note the `expiration` timestamp; channels expire automatically (max ~24 hours). Set a timer to renew before expiry by repeating step 1.
4. To stop notifications early, call POST /channels/stop with `{id: "<channel-id>", resourceId: "<resource-id>"}`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
