---
name: file-storage-api
description: "File storage API skill. Use when working with File storage for file-storage. Covers 33 endpoints."
version: 1.0.0
generator: lapsh
---

# File storage API
API version: 10.24.0

## Auth
ApiKey Authorization in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /file-storage/files -- verify access
3. POST /file-storage/files -- create first files

## Endpoints

33 endpoints across 1 groups. See references/api-spec.lap for full details.

### file-storage
| Method | Path | Description |
|--------|------|-------------|
| GET | /file-storage/files | List Files |
| POST | /file-storage/files | Upload file |
| POST | /file-storage/files/search | Search Files |
| GET | /file-storage/files/{id} | Get File |
| PATCH | /file-storage/files/{id} | Rename or move File |
| DELETE | /file-storage/files/{id} | Delete File |
| GET | /file-storage/files/{id}/download | Download File |
| GET | /file-storage/files/{id}/export | Export File |
| POST | /file-storage/folders | Create Folder |
| GET | /file-storage/folders/{id} | Get Folder |
| PATCH | /file-storage/folders/{id} | Rename or move Folder |
| DELETE | /file-storage/folders/{id} | Delete Folder |
| POST | /file-storage/folders/{id}/copy | Copy Folder |
| GET | /file-storage/shared-links | List Shared Links |
| POST | /file-storage/shared-links | Create Shared Link |
| GET | /file-storage/shared-links/{id} | Get Shared Link |
| PATCH | /file-storage/shared-links/{id} | Update Shared Link |
| DELETE | /file-storage/shared-links/{id} | Delete Shared Link |
| POST | /file-storage/upload-sessions | Start Upload Session |
| GET | /file-storage/upload-sessions/{id} | Get Upload Session |
| PUT | /file-storage/upload-sessions/{id} | Upload part of File to Upload Session |
| DELETE | /file-storage/upload-sessions/{id} | Abort Upload Session |
| POST | /file-storage/upload-sessions/{id}/finish | Finish Upload Session |
| GET | /file-storage/drives | List Drives |
| POST | /file-storage/drives | Create Drive |
| GET | /file-storage/drives/{id} | Get Drive |
| PATCH | /file-storage/drives/{id} | Update Drive |
| DELETE | /file-storage/drives/{id} | Delete Drive |
| GET | /file-storage/drive-groups | List DriveGroups |
| POST | /file-storage/drive-groups | Create DriveGroup |
| GET | /file-storage/drive-groups/{id} | Get DriveGroup |
| PATCH | /file-storage/drive-groups/{id} | Update DriveGroup |
| DELETE | /file-storage/drive-groups/{id} | Delete DriveGroup |

## Enhanced Skill Content
## Question Mapping

- "List all files in my storage?" -> GET /file-storage/files
- "Search for a file by name?" -> POST /file-storage/files/search
- "Get details about a specific file?" -> GET /file-storage/files/{id}
- "Upload a new file?" -> POST /file-storage/files
- "Download a file?" -> GET /file-storage/files/{id}/download
- "Export a file to a different format?" -> GET /file-storage/files/{id}/export
- "Rename or move a file to another folder?" -> PATCH /file-storage/files/{id}
- "Delete a file?" -> DELETE /file-storage/files/{id}
- "Create a new folder?" -> POST /file-storage/folders
- "Copy a folder to another location?" -> POST /file-storage/folders/{id}/copy
- "Share a file with a public link?" -> POST /file-storage/shared-links
- "Upload a large file in chunks?" -> POST /file-storage/upload-sessions
- "List all available drives?" -> GET /file-storage/drives
- "What drive groups exist?" -> GET /file-storage/drive-groups
- "Check the status of a chunked upload?" -> GET /file-storage/upload-sessions/{id}

## Response Tips

- **Files & Folders**: All list endpoints return `data` as an array of maps; single-resource endpoints return `data` as a flat map with `id`, `name`, `path`, `mime_type`, `owner`, and `parent_folders`. Check `parent_folders_complete` to know if the full ancestry is included.
- **Pagination**: Uses cursor-based pagination via `meta.cursors.next` and `links.next`. Default page size is 20 (`limit`). Pass the `cursor` value from `meta.cursors.next` into the next request to advance. A `null` next cursor means you have reached the last page.
- **Mutations (POST/PATCH/DELETE)**: Write responses return only `data.id` -- re-fetch the resource if you need the full object after mutation.
- **Upload Sessions**: `GET /upload-sessions/{id}` returns `part_size`, `parallel_upload_supported`, and `uploaded_byte_range` -- use these to coordinate chunked PUT requests before calling `/finish`.
- **Shared Links**: The `scope` field is an enum (`public` or `company`); `password_protected` and `expires_at` indicate link restrictions.
- **Errors**: All endpoints share the same error codes (400, 401, 402, 404, 422). A 402 indicates a payment/plan restriction on the connected service. A 422 means the request body failed validation -- check the error detail for the offending field.

## Anomaly Flags

- **402 Payment Required**: Surface immediately -- the user's connected service plan may not support this operation or has exceeded its quota.
- **401 on previously working calls**: The API key or consumer/app/service headers may have been rotated or revoked; prompt the user to verify credentials.
- **`parent_folders_complete: false`**: The full folder ancestry was truncated by the downstream service -- warn the user that path reconstruction may be incomplete.
- **`exportable: false` with export attempt**: If a file's metadata shows `exportable: false` or empty `export_formats`, flag this before the user tries `GET /export` to avoid a wasted call.
- **Upload session `expires_at` approaching**: When checking upload session status, compare `expires_at` against the current time and warn if less than 10 minutes remain.
- **`downstream_id` differs from `id`**: The downstream service uses a different identifier; surface this when the user needs to cross-reference with the native storage provider.
- **Shared link with no expiry and public scope**: Flag shared links that are `scope: public` with no `expires_at` as a potential security concern.

## Playbook

### 1. Upload a Small File

1. Call `POST /file-storage/files` with the file content in the body and metadata in the `x-apideck-metadata` header (JSON with `name` and `parent_folder_id`).
2. Capture the returned `data.id`.
3. Verify the upload by calling `GET /file-storage/files/{id}` with the new ID.
4. Confirm `name`, `size`, and `parent_folders` match expectations.

### 2. Upload a Large File via Chunked Sessions

1. Call `POST /file-storage/upload-sessions` with `name`, `parent_folder_id`, and total `size` in bytes.
2. Capture the session `data.id`.
3. Call `GET /file-storage/upload-sessions/{id}` to retrieve `part_size` and check `parallel_upload_supported`.
4. Split the file into chunks of `part_size` bytes. For each chunk, call `PUT /file-storage/upload-sessions/{id}` with the `part_number` and optionally a `digest` header.
5. After all parts are uploaded, call `POST /file-storage/upload-sessions/{id}/finish` (include `digest` if the service requires it).
6. The response returns the full file metadata -- verify `size` and `name`.

### 3. Search, Download, and Share a File

1. Call `POST /file-storage/files/search` with `query` set to the filename or keyword.
2. Iterate `data` results to find the target file; note its `id`.
3. Download it via `GET /file-storage/files/{id}/download`.
4. To share it, call `POST /file-storage/shared-links` with `target_id` set to the file ID, `scope` as `public` or `company`, and optionally `password` and `expires_at`.
5. Return the shared link `id` to the user; retrieve the full URL via `GET /file-storage/shared-links/{id}`.

### 4. Organize Files into a New Folder Structure

1. Call `POST /file-storage/folders` with the desired `name` and `parent_folder_id` (use root or an existing folder ID).
2. Capture the new folder `data.id`.
3. For each file to move, call `PATCH /file-storage/files/{id}` with `parent_folder_id` set to the new folder ID.
4. Verify by calling `GET /file-storage/folders/{id}` on the new folder, then list files with `GET /file-storage/files` filtered to that folder.

### 5. Manage Drives and Drive Groups

1. List available drives with `GET /file-storage/drives`.
2. To create a new drive, call `POST /file-storage/drives` with `id` and `name`.
3. Group drives by calling `POST /file-storage/drive-groups` with `id`, `name`, and optionally `display_name`.
4. Assign context by passing `drive_id` when creating folders or upload sessions to target a specific drive.
5. Clean up unused drives with `DELETE /file-storage/drives/{id}` after confirming no active files reference them.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
