---
name: service-accounts-api
description: "Service Accounts API skill. Use when working with Service Accounts for organizations, projects. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# Service Accounts API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /organizations/{organizationId}/service-accounts -- verify access
3. POST /organizations/{organizationId}/service-accounts -- create first service-accounts

## Endpoints

7 endpoints across 2 groups. See references/api-spec.lap for full details.

### organizations
| Method | Path | Description |
|--------|------|-------------|
| GET | /organizations/{organizationId}/service-accounts | List Service Accounts |
| POST | /organizations/{organizationId}/service-accounts | Create Service Account |
| GET | /organizations/{organizationId}/service-accounts/{serviceAccountId} | Get Service Account |
| DELETE | /organizations/{organizationId}/service-accounts/{serviceAccountId} | Delete Service Account |
| POST | /organizations/{organizationId}/service-accounts/add-to-project | Add Service Accounts To Projects |
| POST | /organizations/{organizationId}/service-accounts/remove-from-project | Remove Service Accounts From Projects |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects/{projectId}/service-accounts | List Service Accounts For Project |

## Enhanced Skill Content
## Question Mapping

- "List all service accounts in my organization?" -> GET /organizations/{organizationId}/service-accounts
- "Create a new service account?" -> POST /organizations/{organizationId}/service-accounts
- "Get details for a specific service account?" -> GET /organizations/{organizationId}/service-accounts/{serviceAccountId}
- "Delete a service account?" -> DELETE /organizations/{organizationId}/service-accounts/{serviceAccountId}
- "What service accounts are attached to a project?" -> GET /projects/{projectId}/service-accounts
- "Add a service account to one or more projects?" -> POST /organizations/{organizationId}/service-accounts/add-to-project
- "Remove a service account from a project?" -> POST /organizations/{organizationId}/service-accounts/remove-from-project
- "Create a service account with an expiration date?" -> POST /organizations/{organizationId}/service-accounts (use `expires` field)
- "Create a service account scoped to specific projects?" -> POST /organizations/{organizationId}/service-accounts (use `projects` field)
- "When was a service account last used?" -> GET /organizations/{organizationId}/service-accounts/{serviceAccountId} (check `last_used`)
- "Who created a specific service account?" -> GET /organizations/{organizationId}/service-accounts/{serviceAccountId} (check `creator`)
- "Assign multiple service accounts to a project at once?" -> POST /organizations/{organizationId}/service-accounts/add-to-project (pass multiple IDs in `service_account_ids`)
- "Remove multiple service accounts from different projects in one call?" -> POST /organizations/{organizationId}/service-accounts/remove-from-project (pass multiple project entries)

## Response Tips

- **Listing endpoints** (GET .../service-accounts): Returns `{results: [...], status: ...}`. Iterate over `results` array. No documented pagination -- assume full list unless response indicates otherwise.
- **Detail endpoint** (GET .../service-accounts/{id}): Returns flat object with `id`, `username`, `last_used`, `expires`, `creator`, `created`, `user`. Nullable datetime fields (`last_used`, `expires`) may be null if never used or non-expiring.
- **Create endpoint** (POST .../service-accounts): Returns 201 with `{results: ..., status: ...}`. Extract the created account from `results`.
- **Delete endpoint** (DELETE .../service-accounts/{id}): Returns 200 with no structured body. Treat success as confirmation of deletion.
- **Bulk project operations** (add-to-project, remove-from-project): Return `{status: ...}`. Check `status` value for confirmation. 400 errors typically indicate malformed project/role mappings.
- **Error responses**: 401 = missing or invalid auth, 403 = insufficient permissions for the org/project, 404 = org, project, or service account not found.

## Anomaly Flags

- **Expired service accounts**: When listing or fetching details, surface accounts where `expires` is in the past -- they may still appear but be non-functional.
- **Never-used accounts**: Flag service accounts where `last_used` is null or very old -- potential security hygiene issue.
- **Role mismatches**: When adding to projects, flag if the assigned role (`owner`, `admin`, `analyst`, `consumer`) differs significantly from the org-level role.
- **Bulk operation partial failures**: If `status` in add-to-project or remove-from-project responses indicates anything other than full success, surface which accounts or projects failed.
- **403 on org-scoped calls**: May indicate the caller's service account lacks org-level permissions -- suggest checking the caller's own role.
- **404 on valid-looking IDs**: Could mean the service account was recently deleted or the org/project ID is from a different environment (staging vs production).

## Playbook

### 1. Provision a New Service Account with Project Access

1. POST /organizations/{organizationId}/service-accounts with `username`, desired `role`, optional `expires`, and `projects` array
2. Note the returned service account ID from `results`
3. GET /organizations/{organizationId}/service-accounts/{serviceAccountId} to confirm creation and verify project assignments
4. Store the account credentials securely

### 2. Audit Service Account Usage Across an Organization

1. GET /organizations/{organizationId}/service-accounts to list all accounts
2. For each account in `results`, check `last_used` and `expires` fields via GET /organizations/{organizationId}/service-accounts/{serviceAccountId}
3. Flag accounts that have never been used (`last_used` is null) or have expired
4. Flag accounts with overly broad roles (`owner`, `admin`) that show no recent activity
5. Consider deleting stale accounts via DELETE /organizations/{organizationId}/service-accounts/{serviceAccountId}

### 3. Reassign Service Accounts Between Projects

1. GET /organizations/{organizationId}/service-accounts to identify the service account IDs to move
2. POST /organizations/{organizationId}/service-accounts/remove-from-project with the old project IDs and service account IDs
3. POST /organizations/{organizationId}/service-accounts/add-to-project with the new project IDs, desired roles, and the same service account IDs
4. GET /projects/{projectId}/service-accounts on both old and new projects to verify the change

### 4. Clean Up Expired or Unused Service Accounts

1. GET /organizations/{organizationId}/service-accounts to retrieve all accounts
2. For each account, GET /organizations/{organizationId}/service-accounts/{serviceAccountId} to inspect `expires` and `last_used`
3. Collect IDs where `expires` is past or `last_used` is null/stale
4. POST /organizations/{organizationId}/service-accounts/remove-from-project to detach them from all projects first
5. DELETE /organizations/{organizationId}/service-accounts/{serviceAccountId} for each account to remove


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
