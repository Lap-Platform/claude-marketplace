---
name: カラーミーショップアプリストア-api
description: "カラーミーショップアプリストア API skill. Use when working with カラーミーショップアプリストア for appstore, inline_script_tags.json, inline_script_tags. Covers 18 endpoints."
version: 1.0.0
generator: lapsh
---

# カラーミーショップアプリストア API
API version: 1.0.0

## Auth
OAuth2

## Base URL
https://api.shop-pro.jp

## Setup
1. Configure auth: OAuth2
2. GET /appstore/v1/script_tags.json -- verify access
3. POST /appstore/v1/script_tags.json -- create first script_tags.json

## Endpoints

18 endpoints across 5 groups. See references/api-spec.lap for full details.

### appstore
| Method | Path | Description |
|--------|------|-------------|
| GET | /appstore/v1/script_tags.json | スクリプトタグの取得 |
| POST | /appstore/v1/script_tags.json | スクリプトタグの作成 |
| GET | /appstore/v1/script_tags/{scriptTagId}.json | スクリプトタグの取得 |
| PUT | /appstore/v1/script_tags/{scriptTagId}.json | スクリプトタグの更新 |
| DELETE | /appstore/v1/script_tags/{scriptTagId}.json | スクリプトタグの削除 |
| POST | /appstore/v1/application_charges.json | アプリ内課金データの作成 |
| POST | /appstore/v1/recurring_application_charges/{recurringApplicationChargeId}/usage_charges.json | 従量課金データの作成 |
| DELETE | /appstore/v1/installation.json | アプリストアアプリのアンインストール |

### inline_script_tags.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/inline_script_tags.json | インラインスクリプトタグの取得 |
| POST | /v1/inline_script_tags.json | インラインスクリプトタグの登録 |

### inline_script_tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/inline_script_tags/{inlineScriptTagId}.json | インラインスクリプトタグの取得 |
| PUT | /v1/inline_script_tags/{inlineScriptTagId}.json | インラインスクリプトタグの更新 |
| DELETE | /v1/inline_script_tags/{inlineScriptTagId}.json | インラインスクリプトタグの削除 |

### script_tags.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/script_tags.json | スクリプトタグの取得 |
| POST | /v1/script_tags.json | スクリプトタグの作成 |

### script_tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/script_tags/{scriptTagId}.json | スクリプトタグの取得 |
| PUT | /v1/script_tags/{scriptTagId}.json | スクリプトタグの更新 |
| DELETE | /v1/script_tags/{scriptTagId}.json | スクリプトタグの削除 |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all script_tags.json?" -> GET /appstore/v1/script_tags.json
- "Create a script_tags.json?" -> POST /appstore/v1/script_tags.json
- "Get script_tag details?" -> GET /appstore/v1/script_tags/{scriptTagId}.json
- "Update a script_tag?" -> PUT /appstore/v1/script_tags/{scriptTagId}.json
- "Delete a script_tag?" -> DELETE /appstore/v1/script_tags/{scriptTagId}.json
- "List all inline_script_tags.json?" -> GET /v1/inline_script_tags.json
- "Create a inline_script_tags.json?" -> POST /v1/inline_script_tags.json
- "Get inline_script_tag details?" -> GET /v1/inline_script_tags/{inlineScriptTagId}.json
- "Update a inline_script_tag?" -> PUT /v1/inline_script_tags/{inlineScriptTagId}.json
- "Delete a inline_script_tag?" -> DELETE /v1/inline_script_tags/{inlineScriptTagId}.json
- "List all script_tags.json?" -> GET /v1/script_tags.json
- "Create a script_tags.json?" -> POST /v1/script_tags.json
- "Get script_tag details?" -> GET /v1/script_tags/{scriptTagId}.json
- "Update a script_tag?" -> PUT /v1/script_tags/{scriptTagId}.json
- "Delete a script_tag?" -> DELETE /v1/script_tags/{scriptTagId}.json
- "Create a application_charges.json?" -> POST /appstore/v1/application_charges.json
- "Create a usage_charges.json?" -> POST /appstore/v1/recurring_application_charges/{recurringApplicationChargeId}/usage_charges.json
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
