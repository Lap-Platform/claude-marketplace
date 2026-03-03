---
name: sync-for-commerce
description: "Sync for Commerce API skill. Use when working with Sync for Commerce for config, companies, sync. Covers 22 endpoints."
version: 1.0.0
generator: lapsh
---

# Sync for Commerce
API version: 1.1

## Auth
ApiKey Authorization in header

## Base URL
https://api.codat.io

## Setup
1. Set your API key in the appropriate header
2. GET /companies -- verify access
3. POST /companies -- create first companies

## Endpoints

22 endpoints across 5 groups. See references/api-spec.lap for full details.

### config
| Method | Path | Description |
|--------|------|-------------|
| GET | /config/sync/commerce/{commerceKey}/{accountingKey}/start | Start new sync flow |
| GET | /config/companies/{companyId}/sync/commerce | Get company configuration |
| POST | /config/companies/{companyId}/sync/commerce | Set configuration |
| GET | /config/integrations | List integrations |
| GET | /config/integrations/{platformKey}/branding | Get branding for an integration |

### companies
| Method | Path | Description |
|--------|------|-------------|
| GET | /companies | List companies |
| POST | /companies | Create company |
| GET | /companies/{companyId}/connections | List connections |
| POST | /companies/{companyId}/connections | Create connection |
| PATCH | /companies/{companyId}/connections/{connectionId} | Update connection |
| PUT | /companies/{companyId}/connections/{connectionId}/authorization | Update authorization |
| POST | /companies/{companyId}/sync/commerce/latest | Initiate new sync |
| GET | /companies/{companyId}/sync/commerce/syncs/lastSuccessful/status | Last successful sync |
| GET | /companies/{companyId}/sync/commerce/syncs/latest/status | Latest sync status |
| GET | /companies/{companyId}/sync/commerce/syncs/{syncId}/status | Get sync status |
| GET | /companies/{companyId}/sync/commerce/syncs/list/status | List sync statuses |

### sync
| Method | Path | Description |
|--------|------|-------------|
| GET | /sync/commerce/config/ui/text | Get preferences for text fields |
| PATCH | /sync/commerce/config/ui/text | Update preferences for text fields |
| POST | /sync/commerce/config/ui/accounts/platform/{platformKey} | Update visible accounts |

### clients
| Method | Path | Description |
|--------|------|-------------|
| GET | /clients/{clientId}/config/ui/accounts/platform/{platformKey} | List visible accounts |

### meta
| Method | Path | Description |
|--------|------|-------------|
| POST | /meta/companies/{companyId}/sync/commerce/historic | Initiate sync for specific range |
| GET | /meta/companies/{companyId}/sync/commerce/status | Get sync status |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my companies?" -> GET /companies
- "How do I create a new company?" -> POST /companies
- "How do I connect a company to a commerce platform?" -> POST /companies/{companyId}/connections
- "How do I check the sync status for a company?" -> GET /companies/{companyId}/sync/commerce/syncs/latest/status
- "How do I trigger a sync for a company?" -> POST /companies/{companyId}/sync/commerce/latest
- "How do I run a historic sync for a specific date range?" -> POST /meta/companies/{companyId}/sync/commerce/historic
- "How do I view or update the sync configuration for a company?" -> GET /config/companies/{companyId}/sync/commerce + POST /config/companies/{companyId}/sync/commerce
- "How do I disconnect or deauthorize a connection?" -> PATCH /companies/{companyId}/connections/{connectionId} (set status to Deauthorized)
- "How do I get the start URL for the commerce sync flow?" -> GET /config/sync/commerce/{commerceKey}/{accountingKey}/start
- "How do I list available integrations?" -> GET /config/integrations
- "How do I get branding assets for an integration?" -> GET /config/integrations/{platformKey}/branding
- "When was the last successful sync for a company?" -> GET /companies/{companyId}/sync/commerce/syncs/lastSuccessful/status
- "How do I check the status of a specific sync?" -> GET /companies/{companyId}/sync/commerce/syncs/{syncId}/status
- "How do I customize the UI text for a locale?" -> PATCH /sync/commerce/config/ui/text
- "How do I control which accounts are visible for a platform?" -> POST /sync/commerce/config/ui/accounts/platform/{platformKey}

## Response Tips

- **Companies & Connections**: Paginated with `page` and `pageSize` defaults (1 and 100). Filter with `query` and sort with `orderBy`. Connection objects nest `dataConnectionErrors` and `connectionInfo` as optional maps.
- **Sync Status**: Check `syncStatusCode` (integer) and `syncStatus` (string) together. `errorMessage` and `syncExceptionMessage` are nullable -- only populated on failure. `dataPushed` indicates whether data actually reached the accounting platform.
- **Config**: The sync configuration response is deeply nested (configuration > sales/payments/fees > accounts/taxRates/grouping). Walk each level carefully; many inner fields are optional maps.
- **Branding**: Logo and button assets are nested two levels deep (e.g., `logo.full.image.src`). All image URLs are URIs.
- **Errors**: All endpoints share a common error set (401/402/403/429/500/503). A 402 typically means a billing issue on the Codat account. A 409 on config POST means a conflicting update.

## Anomaly Flags

- **429 Too Many Requests**: Surface immediately with retry guidance. All 22 endpoints can return this.
- **402 Payment Required**: Indicates a Codat billing or plan limitation. Alert the user that their subscription may need attention.
- **syncStatusCode non-zero with empty errorMessage**: The sync failed but no error detail was provided. Flag for manual investigation.
- **syncExceptionMessage populated**: An unexpected internal error occurred. Surface the full message as it often contains actionable detail.
- **dataPushed: false after a completed sync**: Data was processed but not pushed to the accounting platform. Likely a configuration or connection issue.
- **Connection status Deauthorized**: If a connection silently transitions to Deauthorized, flag it -- syncs will fail until re-authorized.
- **dataConnectionErrors array non-empty**: Surface these errors immediately; they indicate broken or degraded connections.
- **configured: false on sync config**: The company's sync has not been fully configured yet. Warn before attempting to trigger a sync.

## Playbook

### 1. Set Up a New Company and Start Syncing

1. Create a company: `POST /companies` with a `name`.
2. Create a connection: `POST /companies/{companyId}/connections` with the desired `platformKey`.
3. Direct the user to the `linkUrl` from the connection response to authorize the platform.
4. Retrieve and review sync config: `GET /config/companies/{companyId}/sync/commerce`.
5. Update config as needed: `POST /config/companies/{companyId}/sync/commerce` (enable sync, set schedule, map accounts).
6. Trigger initial sync: `POST /companies/{companyId}/sync/commerce/latest`.
7. Monitor: `GET /companies/{companyId}/sync/commerce/syncs/latest/status` until `syncStatus` shows completion.

### 2. Diagnose a Failed Sync

1. Check latest sync status: `GET /companies/{companyId}/sync/commerce/syncs/latest/status`.
2. If `syncStatusCode` indicates failure, read `errorMessage` and `syncExceptionMessage`.
3. Check connection health: `GET /companies/{companyId}/connections` and inspect `status` and `dataConnectionErrors`.
4. If connection is Deauthorized, re-authorize: `PUT /companies/{companyId}/connections/{connectionId}/authorization`.
5. If connection looks healthy, review config: `GET /config/companies/{companyId}/sync/commerce` for misconfigured mappings.
6. Retry the sync: `POST /companies/{companyId}/sync/commerce/latest`.

### 3. Run a Historic Backfill

1. Confirm the company and connection are active: `GET /companies/{companyId}/connections`.
2. Trigger historic sync: `POST /meta/companies/{companyId}/sync/commerce/historic` with `dateRange` containing `start` and `finish`.
3. Poll status: `GET /meta/companies/{companyId}/sync/commerce/status` until complete.
4. Verify data was pushed: check `dataPushed: true` in the status response.
5. Compare with last successful sync: `GET /companies/{companyId}/sync/commerce/syncs/lastSuccessful/status` to confirm the new sync is reflected.

### 4. Customize the Sync UI for White-Labeling

1. Retrieve current UI text: `GET /sync/commerce/config/ui/text` with the target `locale` (en-us or fr-fr).
2. Modify text strings as needed: `PATCH /sync/commerce/config/ui/text` with the same `locale`.
3. Get integration branding: `GET /config/integrations/{platformKey}/branding` for logo and button assets.
4. Control visible accounts: `POST /sync/commerce/config/ui/accounts/platform/{platformKey}` with the desired `visibleAccounts` list.
5. Verify client-facing view: `GET /clients/{clientId}/config/ui/accounts/platform/{platformKey}` to confirm visible accounts match expectations.

### 5. Manage Connections Across Multiple Companies

1. List all companies: `GET /companies` (paginate with `page` and `pageSize` if many).
2. For each company, list connections: `GET /companies/{companyId}/connections`.
3. Identify stale or errored connections by checking `status` and `dataConnectionErrors`.
4. Unlink unused connections: `PATCH /companies/{companyId}/connections/{connectionId}` with `status: Unlinked`.
5. Bulk-check sync health: for each active company, `GET /companies/{companyId}/sync/commerce/syncs/latest/status` and flag any with errors or `dataPushed: false`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
