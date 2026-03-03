---
name: xero-assets-api
description: "Xero Assets API skill. Use when working with Xero Assets for Assets, AssetTypes, Settings. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Xero Assets API
API version: 11.1.0

## Auth
OAuth2

## Base URL
https://api.xero.com/assets.xro/1.0

## Setup
1. Configure auth: OAuth2
2. GET /Assets -- verify access
3. POST /Assets -- create first Assets

## Endpoints

6 endpoints across 3 groups. See references/api-spec.lap for full details.

### Assets
| Method | Path | Description |
|--------|------|-------------|
| GET | /Assets | searches fixed asset |
| POST | /Assets | adds a fixed asset |
| GET | /Assets/{id} | Retrieves fixed asset by id |

### AssetTypes
| Method | Path | Description |
|--------|------|-------------|
| GET | /AssetTypes | searches fixed asset types |
| POST | /AssetTypes | adds a fixed asset type |

### Settings
| Method | Path | Description |
|--------|------|-------------|
| GET | /Settings | searches fixed asset settings |

## Enhanced Skill Content
## Question Mapping

- "What assets do I have?" -> GET /Assets
- "Show me all registered assets" -> GET /Assets (status=Registered)
- "List disposed assets sorted by disposal date" -> GET /Assets (status=Disposed, orderBy=DisposalDate)
- "Get details for a specific asset" -> GET /Assets/{id}
- "Create a new asset" -> POST /Assets
- "Register a draft asset with purchase info" -> POST /Assets (assetStatus=Registered)
- "What asset types are available?" -> GET /AssetTypes
- "Create a new asset type with depreciation settings" -> POST /AssetTypes
- "What are my asset number settings?" -> GET /Settings
- "What is the last depreciation date?" -> GET /Settings
- "How many assets of a certain type exist?" -> GET /Assets (status=Registered, filterBy=type)
- "Show me page 2 of my draft assets" -> GET /Assets (status=Draft, page=2)
- "Can I roll back this asset?" -> GET /Assets/{id} (check canRollback field)
- "What is the book value of an asset?" -> GET /Assets/{id} (check accountingBookValue field)

## Response Tips

- **Assets list**: Response includes `pagination` object and `items` array. Use `page` and `pageSize` params to paginate; always check `pagination` for total count before iterating.
- **Single asset**: Flat object with depreciation nested in `bookDepreciationSetting` and `bookDepreciationDetail` -- inspect both for full depreciation picture.
- **Asset types**: Returns a flat array (no pagination wrapper). 409 on POST means a type with that name already exists.
- **Settings**: Single flat object. `assetNumberPrefix` + `assetNumberSequence` together determine next auto-assigned asset number.
- **All endpoints**: 400 errors carry validation detail -- surface the message body, not just the status code.

## Anomaly Flags

- **Depreciation gap**: If `Settings.lastDepreciationDate` is more than 30 days in the past, flag that depreciation may not have been run recently.
- **Rollback available**: When `canRollback` is true on a fetched asset, proactively mention the asset can be rolled back before the user makes further changes.
- **Draft accumulation**: If a filtered query for `status=Draft` returns a high item count, flag that many assets are sitting unregistered.
- **Missing depreciation accounts**: When creating an asset type, if `depreciationExpenseAccountId` or `accumulatedDepreciationAccountId` is omitted, warn that depreciation tracking will be incomplete.
- **Disposal without price**: If an asset has `assetStatus=Disposed` but `disposalPrice` is null or zero, flag a potentially incomplete disposal record.
- **409 Conflict on asset type creation**: Surface immediately -- the type name is already taken; suggest fetching existing types first.
- **Idempotency-Key missing on POST**: If the user retries a create without an `Idempotency-Key`, warn about potential duplicate creation.

## Playbook

### 1. Register a New Fixed Asset End-to-End

1. `GET /Settings` -- confirm asset numbering prefix and start date are configured.
2. `GET /AssetTypes` -- find the appropriate asset type ID, or create one with `POST /AssetTypes` if needed.
3. `POST /Assets` -- provide `assetName`, `assetTypeId`, `purchaseDate`, `purchasePrice`, and set `assetStatus` to `Registered`. Include an `Idempotency-Key`.
4. `GET /Assets/{id}` -- verify the asset was created correctly and check `bookDepreciationSetting`.

### 2. Audit All Disposed Assets

1. `GET /Assets` with `status=Disposed`, `orderBy=DisposalDate`, `sortDirection=desc`, `pageSize=50`.
2. Check `pagination` in the response for total count. Loop through pages if more exist.
3. For each asset, verify `disposalPrice` is populated. Flag any with missing disposal prices.
4. Cross-reference `disposalDate` against accounting periods to ensure disposals are recorded in the correct period.

### 3. Set Up a New Asset Type with Depreciation

1. `GET /AssetTypes` -- check that the desired type name does not already exist.
2. `POST /AssetTypes` -- provide `assetTypeName`, `fixedAssetAccountId`, `depreciationExpenseAccountId`, `accumulatedDepreciationAccountId`, and a complete `bookDepreciationSetting` object (method, rate, effective life).
3. Confirm the 200 response returns the new `assetTypeId`. If 409, the name is taken -- adjust and retry.

### 4. Paginate Through All Registered Assets

1. `GET /Assets` with `status=Registered`, `page=1`, `pageSize=100`.
2. Read `pagination` from the response to determine total pages.
3. Loop: increment `page` and repeat until all pages are fetched.
4. Aggregate `items` arrays across all pages for the complete asset list.

### 5. Review Depreciation Settings and Run Health Check

1. `GET /Settings` -- note `lastDepreciationDate` and `assetStartDate`.
2. If `lastDepreciationDate` is stale (more than a month old), flag for the user.
3. `GET /AssetTypes` -- for each type, inspect `bookDepreciationSetting` to confirm depreciation method and rates are reasonable.
4. `GET /Assets` with `status=Registered` -- spot-check a sample of assets to ensure `bookDepreciationDetail` is populated and `accountingBookValue` is decreasing over time.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
