---
name: xero-files-api
description: "Xero Files API skill. Use when working with Xero Files for Files, Associations, Folders. Covers 18 endpoints."
version: 1.0.0
generator: lapsh
---

# Xero Files API
API version: 11.1.0

## Auth
OAuth2

## Base URL
https://api.xero.com/files.xro/1.0/

## Setup
1. Configure auth: OAuth2
2. GET /Files -- verify access
3. POST /Files -- create first Files

## Endpoints

18 endpoints across 4 groups. See references/api-spec.lap for full details.

### Files
| Method | Path | Description |
|--------|------|-------------|
| GET | /Files | Retrieves files |
| POST | /Files | Uploads a File to the inbox |
| GET | /Files/{FileId} | Retrieves a file by a unique file ID |
| PUT | /Files/{FileId} | Update a file |
| DELETE | /Files/{FileId} | Deletes a specific file |
| POST | /Files/{FolderId} | Uploads a File to a specific folder |
| GET | /Files/{FileId}/Content | Retrieves the content of a specific file |
| GET | /Files/{FileId}/Associations | Retrieves a specific file associations |
| POST | /Files/{FileId}/Associations | Creates a new file association |
| DELETE | /Files/{FileId}/Associations/{ObjectId} | Deletes an existing file association |

### Associations
| Method | Path | Description |
|--------|------|-------------|
| GET | /Associations/{ObjectId} | Retrieves an association object using a unique object ID |
| GET | /Associations/Count | Retrieves a count of associations for a list of objects. |

### Folders
| Method | Path | Description |
|--------|------|-------------|
| GET | /Folders | Retrieves folders |
| POST | /Folders | Creates a new folder |
| GET | /Folders/{FolderId} | Retrieves specific folder by using a unique folder ID |
| PUT | /Folders/{FolderId} | Updates an existing folder |
| DELETE | /Folders/{FolderId} | Deletes a folder |

### Inbox
| Method | Path | Description |
|--------|------|-------------|
| GET | /Inbox | Retrieves inbox folder |

## Enhanced Skill Content
## Question Mapping

- "How do I list all files in my Xero account?" -> GET /Files
- "How do I upload a file to Xero?" -> POST /Files
- "How do I upload a file to a specific folder?" -> POST /Files/{FolderId}
- "How do I get details about a specific file?" -> GET /Files/{FileId}
- "How do I download a file's content?" -> GET /Files/{FileId}/Content
- "How do I rename or update a file?" -> PUT /Files/{FileId}
- "How do I delete a file?" -> DELETE /Files/{FileId}
- "How do I associate a file with an invoice or contact?" -> POST /Files/{FileId}/Associations
- "What Xero objects is a file linked to?" -> GET /Files/{FileId}/Associations
- "What files are associated with a specific invoice or contact?" -> GET /Associations/{ObjectId}
- "How many files are associated with a set of objects?" -> GET /Associations/Count
- "How do I remove a file association from an object?" -> DELETE /Files/{FileId}/Associations/{ObjectId}
- "How do I list all folders?" -> GET /Folders
- "How do I create a new folder?" -> POST /Folders
- "How do I check my inbox for incoming files?" -> GET /Inbox

## Response Tips

- **Files (list):** Paginated via `TotalCount`, `Page`, and `PerPage` fields. Items array contains file objects. Default page size applies if `pagesize` is omitted -- always check `TotalCount` against returned items to know if more pages exist.
- **Files (single/create/update):** Returns the full file object with nested `User` map. `User.Id` is a UUID; `FolderId` tells you which folder the file lives in.
- **File content:** Returns raw binary data (the actual file), not JSON. Handle the response as a blob/stream based on the file's `MimeType`.
- **Associations:** Creating an association returns the association object with `ObjectGroup` and `ObjectType` indicating the linked Xero entity. GET on associations may return a flat list without pagination wrapper -- check response shape.
- **Associations/Count:** Accepts an array of `ObjectIds` and returns counts per object. Useful for batch checking before fetching full association lists.
- **Folders:** No pagination -- returns all folders in a flat list. Each folder includes `FileCount` for quick size checks without listing files.
- **Inbox:** Returns a single folder object (not an array). The inbox is a system folder with `IsInbox: true`.
- **Errors (400):** Returned on validation failures for POST/PUT operations. Check the response body for field-level error details.
- **Deletes (204):** Return no body. A successful delete is confirmed solely by the 204 status code.

## Anomaly Flags

- **Large file counts with no pagination:** If `TotalCount` is significantly larger than `PerPage`, warn that multiple pages need fetching to get all results.
- **Orphaned files:** Files not in any folder (missing or null `FolderId`) may indicate upload issues -- surface these when listing files.
- **Inbox accumulation:** If `GET /Inbox` shows a high `FileCount`, flag that the inbox has unprocessed files that should be moved to folders.
- **Association ObjectType mismatch:** If an association's `ObjectType` doesn't align logically with the `ObjectGroup` (e.g., `ObjectGroup: Invoice` but `ObjectType: Contact`), flag the inconsistency.
- **Idempotency-Key absence on retries:** If a POST or PUT is retried without an `Idempotency-Key` header, warn about potential duplicate creation.
- **OAuth2 token expiry:** Since the API uses OAuth2, surface warnings when tokens are near expiration to prevent mid-workflow auth failures.
- **Empty folder cleanup:** Flag folders with `FileCount: 0` that may be candidates for cleanup.
- **Deprecated or unknown ObjectType values:** If an association uses `ObjectType: Unknown`, surface this as it may indicate a data quality issue.

## Playbook

### 1. Upload a File and Associate It with an Invoice

1. Create or identify the target folder: `GET /Folders` to list existing folders, or `POST /Folders` with `{"Name": "Invoice Attachments"}` to create one.
2. Upload the file to the folder: `POST /Files/{FolderId}` with the file content as multipart form data. Include an `Idempotency-Key` header to prevent duplicates. Note the returned `Id` (FileId).
3. Associate the file with the invoice: `POST /Files/{FileId}/Associations` with `ObjectId` set to the invoice UUID, `ObjectGroup: "Invoice"`, and `ObjectType: "AccRec"` (for accounts receivable invoices) or `"Accpay"` (for bills).
4. Verify the association: `GET /Files/{FileId}/Associations` to confirm the link was created.

### 2. Organize Inbox Files into Folders

1. Check the inbox: `GET /Inbox` to see how many files are waiting (`FileCount`).
2. List inbox files: `GET /Files` with sorting by `CreatedDateUTC` and filter for files in the inbox folder (use the inbox `Id` from step 1).
3. Create destination folders if needed: `POST /Folders` with descriptive names.
4. Move each file: `PUT /Files/{FileId}` with the new `FolderId` set to the destination folder's UUID.
5. Verify the inbox is cleared: `GET /Inbox` again and confirm `FileCount` has decreased.

### 3. Audit All Associations for a Contact or Invoice

1. Get the association count: `GET /Associations/Count` with the target `ObjectIds` array to see how many files are linked.
2. Retrieve full association list: `GET /Associations/{ObjectId}` with pagination parameters (`page`, `pagesize`) to get all linked files.
3. For each associated file, fetch details: `GET /Files/{FileId}` to get metadata (name, size, upload date, uploader).
4. Optionally download files for review: `GET /Files/{FileId}/Content` for each file that needs inspection.

### 4. Bulk Clean Up Unused Files

1. List all folders: `GET /Folders` and note each folder's `Id` and `FileCount`.
2. For each folder, list files: `GET /Files` with pagination, sorted by `CreatedDateUTC` in `ASC` order to find oldest files first.
3. Check each file's associations: `GET /Files/{FileId}/Associations`. Files with no associations are candidates for deletion.
4. Delete unassociated files: `DELETE /Files/{FileId}` for each orphaned file. No response body is returned -- 204 confirms success.
5. Delete empty folders: After cleanup, `DELETE /Folders/{FolderId}` for any folders with `FileCount: 0`.

### 5. Duplicate-Safe File Upload with Idempotency

1. Generate a unique `Idempotency-Key` (e.g., UUID v4) before starting the upload.
2. Attempt the upload: `POST /Files/{FolderId}` with the `Idempotency-Key` header and file content.
3. If the request times out or returns a network error, retry with the same `Idempotency-Key`. The API will return the original response rather than creating a duplicate.
4. On success (201), store the returned `Id` for subsequent association or reference.
5. If you receive a 400 error, inspect the error body for validation details (file size limits, unsupported MIME type) before retrying with corrected data.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
