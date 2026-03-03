---
name: account-management-overview
description: "Account Management Overview API skill. Use when working with Account Management Overview for resources. Covers 25 endpoints."
version: 1.0.0
generator: lapsh
---

# Account Management Overview

## Auth
Bearer bearer

## Base URL
https://api.frontegg.com/tenants

## Setup
1. Set Authorization header with your Bearer token
2. GET /resources/tenants/v2 -- verify access
3. POST /resources/tenants/v1 -- create first tenants

## Endpoints

25 endpoints across 1 groups. See references/api-spec.lap for full details.

### resources
| Method | Path | Description |
|--------|------|-------------|
| GET | /resources/tenants/v1/{tenantId} | Get account (tenant) by ID |
| PUT | /resources/tenants/v1/{tenantId} | Update account (tenant) |
| DELETE | /resources/tenants/v1/{tenantId} | Delete account (tenant) |
| POST | /resources/tenants/v1 | Create an account (tenant) |
| DELETE | /resources/tenants/v1 | Delete current account (tenant) |
| POST | /resources/tenants/v1/{tenantId}/metadata | Add account (tenant) metadata |
| DELETE | /resources/tenants/v1/{tenantId}/metadata/{key} | Delete account (tenant) metadata |
| GET | /resources/tenants/v2 | Get accounts (tenants) |
| GET | /resources/tenants/v2/alias/{alias} | Get account (tenant) by alias |
| GET | /resources/tenants/v2/{tenantId} | Get an account (tenant) |
| PUT | /resources/tenants/v2/{tenantId} | Update an account (tenant) |
| POST | /resources/sub-tenants/v1 | Create sub-account |
| PUT | /resources/sub-tenants/v1/{tenantId}/management | Update sub-account (tenant) management |
| PUT | /resources/sub-tenants/v1/{tenantId}/hierarchy-settings | Update sub-account hierarchy settings |
| DELETE | /resources/sub-tenants/v1/{tenantId} | Delete a sub-account by ID |
| GET | /resources/account-settings/v1 | Get account settings |
| PUT | /resources/account-settings/v1 | Update account settings |
| GET | /resources/account-settings/v1/public | Get public settings |
| POST | /resources/migrations/v1/tenants | Migrate accounts (tenants) |
| GET | /resources/migrations/v1/tenants/status/{migrationId} | Accounts (tenants) migration status |
| GET | /resources/hierarchy/v1 | Get sub-accounts (tenants) |
| POST | /resources/hierarchy/v1 | Create sub-account (tenant) |
| DELETE | /resources/hierarchy/v1 | Delete sub-account (tenant) |
| GET | /resources/hierarchy/v1/parents | Get parent accounts (tenants) |
| GET | /resources/hierarchy/v1/tree | Get sub-accounts (tenanants) hierarchy tree |

## Enhanced Skill Content
## Question Mapping

- "How do I get details for a specific tenant?" -> GET /resources/tenants/v1/{tenantId}
- "How do I list all tenants with pagination?" -> GET /resources/tenants/v2
- "How do I create a new tenant?" -> POST /resources/tenants/v1
- "How do I update a tenant's information?" -> PUT /resources/tenants/v1/{tenantId}
- "How do I delete a tenant?" -> DELETE /resources/tenants/v1/{tenantId}
- "How do I look up a tenant by its alias?" -> GET /resources/tenants/v2/alias/{alias}
- "How do I add custom metadata to a tenant?" -> POST /resources/tenants/v1/{tenantId}/metadata
- "How do I remove a metadata key from a tenant?" -> DELETE /resources/tenants/v1/{tenantId}/metadata/{key}
- "How do I create a sub-tenant under a parent tenant?" -> POST /resources/sub-tenants/v1
- "How do I delete a sub-tenant?" -> DELETE /resources/sub-tenants/v1/{tenantId}
- "How do I view the tenant hierarchy tree?" -> GET /resources/hierarchy/v1/tree
- "How do I get account settings for a tenant?" -> GET /resources/account-settings/v1
- "How do I migrate tenants in bulk?" -> POST /resources/migrations/v1/tenants
- "How do I check the status of a tenant migration?" -> GET /resources/migrations/v1/tenants/status/{migrationId}
- "How do I find all parent tenants in a hierarchy?" -> GET /resources/hierarchy/v1/parents

## Response Tips

- **Tenant listing (v2):** Paginated via `_limit` and `_offset` params; use `_filter`, `_sortBy`, and `_order` for narrowing results. Always check if more pages remain by comparing result count to `_limit`.
- **Tenant CRUD (v1):** 400 errors indicate malformed input or missing required fields; 404 means the tenantId does not exist. DELETE on the collection endpoint (no tenantId) removes all tenants -- use with extreme caution.
- **Metadata:** Accepts arbitrary key-value via `metadata: any`. 404 on delete means either the tenant or the specific key was not found.
- **Sub-tenants:** Require both `tenantId` and `parentTenantId` on creation. Management and hierarchy-settings endpoints return 200 with no detailed error breakdown.
- **Account settings:** Requires `frontegg-tenant-id` as a header, not a path param. Public settings endpoint exposes a subset safe for unauthenticated contexts.
- **Migrations:** POST returns 202 (accepted, async). Poll the status endpoint with the returned `migrationId` until completion.
- **Hierarchy:** Tree and parents endpoints require `frontegg-tenant-id` header. 400 on tree typically means the tenant has no hierarchy configured.

## Anomaly Flags

- **Bulk delete warning:** `DELETE /resources/tenants/v1` (no tenantId) deletes all tenants. Surface a confirmation prompt before calling this endpoint -- there is no undo.
- **Async migration:** `POST /resources/migrations/v1/tenants` returns 202, not 200. Alert the user that the operation is asynchronous and they must poll `/status/{migrationId}`.
- **Header-based tenant context:** Several endpoints (`account-settings`, `hierarchy`) require `frontegg-tenant-id` as a request header rather than a path parameter. Flag if the header is missing from the request.
- **v1 vs v2 divergence:** Tenant GET/PUT exists in both v1 and v2. v2 adds pagination, filtering, and alias lookup. Surface a suggestion to prefer v2 for listing and search operations.
- **Sub-tenant hierarchy mutations:** `POST /resources/hierarchy/v1` and `DELETE /resources/hierarchy/v1` modify parent-child relationships. Warn before restructuring hierarchies as this affects access control and data isolation.
- **400 on hierarchy tree:** Indicates misconfigured or missing hierarchy. Suggest checking that the tenant actually participates in a hierarchy before retrying.

## Playbook

### 1. Provision a New Tenant with Metadata

1. Create the tenant: `POST /resources/tenants/v1` with name, status, and any optional fields (website, timezone, currency).
2. Note the returned `tenantId`.
3. Attach metadata: `POST /resources/tenants/v1/{tenantId}/metadata` with a `metadata` object containing custom key-value pairs.
4. Verify creation: `GET /resources/tenants/v2/{tenantId}` to confirm all fields and metadata are set.

### 2. Set Up a Multi-Level Tenant Hierarchy

1. Create the parent tenant: `POST /resources/tenants/v1` with desired parent details.
2. Create a sub-tenant: `POST /resources/sub-tenants/v1` with the parent's `tenantId` as `parentTenantId`.
3. Optionally link additional children: `POST /resources/hierarchy/v1` with `parentTenantId` and `childTenantId`.
4. Configure hierarchy settings: `PUT /resources/sub-tenants/v1/{tenantId}/hierarchy-settings`.
5. Verify the tree: `GET /resources/hierarchy/v1/tree` with the root tenant's `frontegg-tenant-id` header.

### 3. Bulk Migrate Tenants

1. Collect the list of tenant IDs to migrate.
2. Submit the migration: `POST /resources/migrations/v1/tenants` with `tenants` array.
3. Capture the `migrationId` from the 202 response.
4. Poll status: `GET /resources/migrations/v1/tenants/status/{migrationId}` until the migration reports completion.
5. Verify migrated tenants: `GET /resources/tenants/v2` with `_tenantIds` filter to confirm they appear correctly.

### 4. Search and Filter Tenants

1. List tenants with pagination: `GET /resources/tenants/v2` with `_limit=20` and `_offset=0`.
2. Apply a text filter: add `_filter=searchterm` to narrow results by name or other indexed fields.
3. Sort results: use `_sortBy=name` and `_order=asc` (or `desc`).
4. Look up a specific tenant by alias: `GET /resources/tenants/v2/alias/{alias}`.
5. Page through results by incrementing `_offset` by `_limit` until fewer results than `_limit` are returned.

### 5. Manage Account Settings for a Tenant

1. Retrieve current settings: `GET /resources/account-settings/v1` with `frontegg-tenant-id` header.
2. Review the response for configurable fields.
3. Update settings: `PUT /resources/account-settings/v1` with the `frontegg-tenant-id` header and modified fields in the body.
4. Confirm public-facing settings: `GET /resources/account-settings/v1/public` to verify what external users will see.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object
- Error responses use types: When

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
