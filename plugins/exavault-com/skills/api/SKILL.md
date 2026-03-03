---
name: exavault-api
description: "ExaVault API skill. Use when working with ExaVault for email-lists, forms, activity. Covers 59 endpoints."
version: 1.0.0
generator: lapsh
---

# ExaVault API
API version: 2.0

## Auth
ApiKey ev-api-key in header

## Base URL
https://accountname.exavault.com/api/v2

## Setup
1. Set your API key in the appropriate header
2. GET /email-lists -- verify access
3. POST /email-lists -- create first email-lists

## Endpoints

59 endpoints across 12 groups. See references/api-spec.lap for full details.

### email-lists
| Method | Path | Description |
|--------|------|-------------|
| GET | /email-lists | Get all email groups |
| POST | /email-lists | Create new email list |
| GET | /email-lists/{id} | Get individual email group |
| PATCH | /email-lists/{id} | Update an email group |
| DELETE | /email-lists/{id} | Delete an email group with given id |

### forms
| Method | Path | Description |
|--------|------|-------------|
| GET | /forms | Get receive folder form settings |
| GET | /forms/{id} | Get receive folder form by Id |
| PATCH | /forms/{id} | Updates a form with given parameters |
| GET | /forms/entries/{id} | Get form data entries for a receive |
| DELETE | /forms/entries/{id} | Delete a receive form submission |

### activity
| Method | Path | Description |
|--------|------|-------------|
| GET | /activity/session | Get activity logs |
| GET | /activity/webhooks | Get webhook logs |

### notifications
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /notifications/{id} | Update a notification |
| GET | /notifications/{id} | Get notification details |
| DELETE | /notifications/{id} | Delete a notification |
| POST | /notifications | Create a new notification |
| GET | /notifications | Get a list of notifications |

### users
| Method | Path | Description |
|--------|------|-------------|
| POST | /users | Create a user |
| GET | /users | Get a list of users |
| GET | /users/{id} | Get info for a user |
| DELETE | /users/{id} | Delete a user |
| PATCH | /users/{id} | Update a user |

### resources
| Method | Path | Description |
|--------|------|-------------|
| GET | /resources/list | Get a list of all resources |
| GET | /resources/{id} | Get resource metadata |
| PATCH | /resources/{id} | Rename a resource. |
| DELETE | /resources/{id} | Delete a Resource |
| DELETE | /resources | Delete Resources |
| POST | /resources | Create a folder |
| GET | /resources | Get Resource Properties |
| GET | /resources/list/{id} | List contents of folder |
| POST | /resources/compress | Compress resources |
| POST | /resources/extract | Extract resources |
| POST | /resources/copy | Copy resources |
| POST | /resources/move | Move resources |
| GET | /resources/preview | Preview a file |
| POST | /resources/upload | Upload a file |
| GET | /resources/download | Download a file |

### account
| Method | Path | Description |
|--------|------|-------------|
| GET | /account | Get account settings |
| PATCH | /account | Update account settings |

### email
| Method | Path | Description |
|--------|------|-------------|
| POST | /email/welcome/{username} | Resend welcome email to specific user |
| POST | /email/referral | Send referral email to a given address |

### shares
| Method | Path | Description |
|--------|------|-------------|
| POST | /shares | Creates a share |
| GET | /shares | Get a list of shares |
| GET | /shares/{id} | Get a share |
| PATCH | /shares/{id} | Update a share |
| DELETE | /shares/{id} | Deactivate a share |
| POST | /shares/complete-send/{id} | Complete send files |

### recipients
| Method | Path | Description |
|--------|------|-------------|
| POST | /recipients/shares/invites/{shareId} | Resend invitations to share recipients |

### ssh-keys
| Method | Path | Description |
|--------|------|-------------|
| GET | /ssh-keys | Get metadata for a list of SSH Keys |
| POST | /ssh-keys | Create a new SSH Key |
| GET | /ssh-keys/{id} | Get metadata for an SSH Key |
| DELETE | /ssh-keys/{id} | Delete an SSH Key |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /webhooks | Get Webhooks List |
| POST | /webhooks | Add A New Webhook |
| GET | /webhooks/{id} | Get info for a webhook |
| PATCH | /webhooks/{id} | Update a webhook |
| DELETE | /webhooks/{id} | Delete a webhook |
| POST | /webhooks/resend/{activityId} | Resend a webhook message |
| POST | /webhooks/regenerate-token/{id} | Regenerate security token |

## Enhanced Skill Content
## Question Mapping

- "How much storage space is left on my account?" -> GET /account
- "List all files in a folder" -> GET /resources/list
- "Upload a file to a specific path" -> POST /resources/upload
- "Who are the users on this account?" -> GET /users
- "Create a new user with limited permissions" -> POST /users
- "Share a folder with someone via email" -> POST /shares
- "What activity happened on the account today?" -> GET /activity/session
- "Download multiple files as a zip" -> GET /resources/download
- "Set up a webhook for upload events" -> POST /webhooks
- "Move files from one folder to another" -> POST /resources/move
- "Check if a share link has expired" -> GET /shares/{id}
- "Add an SSH key for a user" -> POST /ssh-keys
- "Get a thumbnail preview of a document" -> GET /resources/preview
- "Create a notification when someone uploads to a folder" -> POST /notifications
- "Resend a failed webhook delivery" -> POST /webhooks/resend/{activityId}

## Response Tips

- **Resources**: All resource responses use `int64` IDs; `size` is in bytes. Bulk operations (copy, move, delete) may return `207` with per-item results in `responses[]` -- check each entry individually.
- **Lists** (users, shares, notifications, email-lists, activity): Paginated via `offset`/`limit` with `totalResults` and `returnedResults` in the envelope -- loop until `offset + returnedResults >= totalResults`.
- **Relationships**: Nested under `data.relationships` as reference objects (`{data: {id, type}}`); use `?include=` to inline the full related objects in `included[]`.
- **Shares**: The `expired` boolean is computed server-side; do not rely solely on comparing `expiration` to current time. `status` field indicates active/deactivated state separately from expiration.
- **Uploads**: Returns the created resource metadata on `201`; supports resumable uploads via `offsetBytes` + `resume=true`.
- **Webhooks**: Activity log responses (GET /activity/webhooks) are separate from webhook config (GET /webhooks) -- use the activity endpoint for delivery history.

## Anomaly Flags

- **Quota approaching limit**: Surface when `quota.diskUsed / quota.diskLimit > 0.9` or `quota.bandwidthUsed / quota.bandwidthLimit > 0.9` from GET /account. Alert user before uploads fail silently.
- **Expired shares still active**: Flag any share where `expired: true` but `status` is not deactivated -- recipients may still have cached access.
- **207 Multi-Status on bulk operations**: Never treat copy/move/delete bulk responses as success without inspecting each item in `responses[]`. Surface individual failures to the user.
- **User expiration imminent**: Flag users where `expiration` is within 7 days and `locked: false` -- they will lose access without warning.
- **Webhook delivery failures**: When GET /activity/webhooks shows repeated non-2xx `statusCode` values for the same endpoint, surface the failing URL and suggest checking the receiver.
- **Locked users with active shares**: If a user is `locked: true` but owns active shares, flag the orphaned shares that may need reassignment.
- **SSH key with no recent login**: Flag SSH keys where `lastLogin` is null or older than 90 days as potential security cleanup candidates.

## Playbook

### 1. Set up a secure file drop for external clients

1. Create a destination folder: `POST /resources` with desired `path`
2. Create a receive share: `POST /shares` with `type: "receive"`, target `resources: ["/path"]`, `requireEmail: true`, `password: "..."`, and `fileDropCreateFolders: true`
3. Add notification: `POST /notifications` with `type: "folder"`, `resource: "/path"`, `action: "upload"`, `sendEmail: true`, and recipient emails
4. Optionally set up a webhook: `POST /webhooks` with `triggers.resources.upload: true` and `resource: "/path"` for real-time integration
5. Send the share link to the client: note the `hash` from the share response for the public URL

### 2. Onboard a new team member with scoped access

1. Create the user's home folder: `POST /resources` with `path: "/users/jdoe"`
2. Create the user: `POST /users` with `homeResource: "/users/jdoe"`, appropriate `role` and `permissions` (disable `delete` and `share` for restricted users), set `welcomeEmail: true`
3. Add their SSH key if SFTP access is needed: `POST /ssh-keys` with `userId` and `publicKey`
4. Create a shared folder for collaboration: `POST /shares` with `type: "shared_folder"`, `resources: ["/team/shared"]`, and the new user as a recipient
5. Verify the setup: `GET /users/{id}?include=homeResource` to confirm home directory and permissions

### 3. Monitor account activity and audit file operations

1. Pull session activity for the date range: `GET /activity/session` with `startDate` and `endDate`, paginate with `offset`/`limit`
2. Filter for specific users or actions: add `username` or `type` (e.g., `type: "DELE"` for deletions) query parameters
3. Check webhook delivery health: `GET /activity/webhooks` filtered by `statusCode` to find failures
4. Review account-level stats: `GET /account` to check quota usage, user count vs. max, and bandwidth consumption
5. Export results by collecting all paginated data until `returnedResults` is 0

### 4. Bulk migrate files between folders

1. List source folder contents: `GET /resources/list` with `resource: "/old-folder"`, paginate to collect all resource paths
2. Create the destination folder if needed: `POST /resources` with `path: "/new-folder"`
3. Move in batches: `POST /resources/move` with `resources: ["/old-folder/file1", ...]` and `parentResource: "/new-folder"` -- keep batches under 50 items
4. Check for partial failures: inspect any `207` responses and retry failed items individually
5. Verify destination: `GET /resources/list` with `resource: "/new-folder"` to confirm all files arrived, compare counts with source

### 5. Create and manage email distribution for share notifications

1. Create an email list: `POST /email-lists` with `name: "Engineering Team"` and `emails: ["a@co.com", "b@co.com"]`
2. Create or update a share with notification: `POST /shares` with `hasNotification: true` and `notificationEmails` referencing the list members
3. Update the list as team changes: `PATCH /email-lists/{id}` with the revised `emails` array (this is a full replacement, not append)
4. Send a referral or welcome: `POST /email/referral` with `emails` from the list and a custom `message`
5. Clean up unused lists: `GET /email-lists` to audit, then `DELETE /email-lists/{id}` for stale entries


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
