---
name: configcat-public-management-api
description: "ConfigCat Public Management API skill. Use when working with ConfigCat Public Management for proxy-profiles, organizations, products. Covers 105 endpoints."
version: 1.0.0
generator: lapsh
---

# ConfigCat Public Management API
API version: v1

## Auth
Bearer basic

## Base URL
https://api.configcat.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/organizations -- verify access
3. POST /v1/organizations/{organizationId}/proxy-profiles -- create first proxy-profiles

## Endpoints

105 endpoints across 16 groups. See references/api-spec.lap for full details.

### proxy-profiles
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/proxy-profiles/{proxyProfileId} | Get Proxy Profile |
| PUT | /v1/proxy-profiles/{proxyProfileId} | Replace Proxy Profile |
| PATCH | /v1/proxy-profiles/{proxyProfileId} | Update Proxy Profile |
| DELETE | /v1/proxy-profiles/{proxyProfileId} | Delete Proxy Profile |
| GET | /v1/proxy-profiles/{proxyProfileId}/sdk-keys | Get selected SDK keys |
| POST | /v1/proxy-profiles/{proxyProfileId}/sdk-keys/deselect | Deselect SDK keys |
| POST | /v1/proxy-profiles/{proxyProfileId}/secret | Generate Secret |
| POST | /v1/proxy-profiles/{proxyProfileId}/sdk-keys/select | Select SDK keys |

### organizations
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/organizations | List Organizations |
| GET | /v1/organizations/{organizationId}/proxy-profiles | List Proxy Profiles |
| POST | /v1/organizations/{organizationId}/proxy-profiles | Create Proxy Profile |
| GET | /v1/organizations/{organizationId}/auditlogs | List Audit log items for Organization |
| GET | /v1/organizations/{organizationId}/organization-limitations | Get Organization limitations |
| GET | /v1/organizations/{organizationId}/members | List Organization Members |
| GET | /v2/organizations/{organizationId}/members | List Organization Members |
| GET | /v1/organizations/{organizationId}/invitations | List Pending Invitations in Organization |
| POST | /v1/organizations/{organizationId}/products | Create Product |
| POST | /v1/organizations/{organizationId}/members/{userId} | Update Member Permissions |
| DELETE | /v1/organizations/{organizationId}/members/{userId} | Delete Member from Organization |

### products
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/products | List Products |
| GET | /v1/products/{productId}/tags | List Tags |
| POST | /v1/products/{productId}/tags | Create Tag |
| GET | /v1/products/{productId}/webhooks | List Webhooks |
| GET | /v1/products/{productId}/configs | List Configs |
| POST | /v1/products/{productId}/configs | Create Config |
| GET | /v1/products/{productId}/environments | List Environments |
| POST | /v1/products/{productId}/environments | Create Environment |
| GET | /v1/products/{productId}/permissions | List Permission Groups |
| POST | /v1/products/{productId}/permissions | Create Permission Group |
| GET | /v1/products/{productId}/integrations | List Integrations |
| POST | /v1/products/{productId}/integrations | Create Integration |
| GET | /v1/products/{productId}/segments | List Segments |
| POST | /v1/products/{productId}/segments | Create Segment |
| GET | /v1/products/{productId}/auditlogs | List Audit log items for Product |
| GET | /v1/products/{productId}/staleflags | List Zombie (stale) flags for Product |
| GET | /v1/products/{productId}/invitations | List Pending Invitations in Product |
| GET | /v1/products/{productId} | Get Product |
| PUT | /v1/products/{productId} | Update Product |
| DELETE | /v1/products/{productId} | Delete Product |
| GET | /v1/products/{productId}/members | List Product Members |
| GET | /v1/products/{productId}/preferences | Get Product Preferences |
| POST | /v1/products/{productId}/preferences | Update Product Preferences |
| POST | /v1/products/{productId}/members/invite | Invite Member |
| DELETE | /v1/products/{productId}/members/{userId} | Delete Member from Product |

### configs
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/configs/{configId}/settings | List Flags |
| POST | /v1/configs/{configId}/settings | Create Flag |
| GET | /v1/configs/{configId} | Get Config |
| PUT | /v1/configs/{configId} | Update Config |
| DELETE | /v1/configs/{configId} | Delete Config |
| GET | /v1/configs/{configId}/deleted-settings | List Deleted Settings |
| GET | /v1/configs/{configId}/environments/{environmentId} | Get SDK Key |
| GET | /v1/configs/{configId}/environments/{environmentId}/values | Get values |
| POST | /v1/configs/{configId}/environments/{environmentId}/values | Post values |
| GET | /v2/configs/{configId}/environments/{environmentId}/values | Get values |
| POST | /v2/configs/{configId}/environments/{environmentId}/values | Post values |
| POST | /v1/configs/{configId}/environments/{environmentId}/webhooks | Create Webhook |

### settings
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/settings/{settingId}/code-references | Get References for Feature Flag or Setting |
| GET | /v1/settings/{settingId}/predefined-variations | Get predefined variations |
| PUT | /v1/settings/{settingId}/predefined-variations | Update predefined variations |
| GET | /v1/settings/{settingId} | Get Flag |
| PUT | /v1/settings/{settingId} | Replace Flag |
| PATCH | /v1/settings/{settingId} | Update Flag |
| DELETE | /v1/settings/{settingId} | Delete Flag |
| GET | /v1/settings/{settingKeyOrId}/value | Get value |
| PUT | /v1/settings/{settingKeyOrId}/value | Replace value |
| PATCH | /v1/settings/{settingKeyOrId}/value | Update value |
| GET | /v2/settings/{settingKeyOrId}/value | Get value |
| PUT | /v2/settings/{settingKeyOrId}/value | Replace value |
| PATCH | /v2/settings/{settingKeyOrId}/value | Update value |

### environments
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/environments/{environmentId} | Get Environment |
| PUT | /v1/environments/{environmentId} | Update Environment |
| DELETE | /v1/environments/{environmentId} | Delete Environment |
| GET | /v1/environments/{environmentId}/settings/{settingId}/value | Get value |
| PUT | /v1/environments/{environmentId}/settings/{settingId}/value | Replace value |
| PATCH | /v1/environments/{environmentId}/settings/{settingId}/value | Update value |
| GET | /v2/environments/{environmentId}/settings/{settingId}/value | Get value |
| PUT | /v2/environments/{environmentId}/settings/{settingId}/value | Replace value |
| PATCH | /v2/environments/{environmentId}/settings/{settingId}/value | Update value |
| POST | /v1/environments/{environmentId}/settings/{settingId}/integrationLinks/{integrationLinkType}/{key} | Add or update Integration link |
| DELETE | /v1/environments/{environmentId}/settings/{settingId}/integrationLinks/{integrationLinkType}/{key} | Delete Integration link |

### permissions
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/permissions/{permissionGroupId} | Get Permission Group |
| PUT | /v1/permissions/{permissionGroupId} | Update Permission Group |
| DELETE | /v1/permissions/{permissionGroupId} | Delete Permission Group |

### integrations
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/integrations/{integrationId} | Get Integration |
| PUT | /v1/integrations/{integrationId} | Update Integration |
| DELETE | /v1/integrations/{integrationId} | Delete Integration |

### integrationLink
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/integrationLink/{integrationLinkType}/{key}/details | Get Integration link |

### me
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/me | Get authenticated user details |

### segments
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/segments/{segmentId} | Get Segment |
| PUT | /v1/segments/{segmentId} | Update Segment |
| DELETE | /v1/segments/{segmentId} | Delete Segment |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/tags/{tagId}/settings | List Settings by Tag |
| GET | /v1/tags/{tagId} | Get Tag |
| PUT | /v1/tags/{tagId} | Update Tag |
| DELETE | /v1/tags/{tagId} | Delete Tag |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/webhooks/{webhookId} | Get Webhook |
| PUT | /v1/webhooks/{webhookId} | Replace Webhook |
| PATCH | /v1/webhooks/{webhookId} | Update Webhook |
| DELETE | /v1/webhooks/{webhookId} | Delete Webhook |
| GET | /v1/webhooks/{webhookId}/keys | Get Webhook Signing Keys |

### jira
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/jira/environments/{environmentId}/settings/{settingId}/integrationLinks/{key} |  |
| POST | /v1/jira/connect |  |

### code-references
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/code-references/delete-reports | Delete Reference reports |
| POST | /v1/code-references | Upload References |

### invitations
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /v1/invitations/{invitationId} | Delete Invitation |

## Enhanced Skill Content
## Question Mapping

- "What organizations do I have access to?" -> GET /v1/organizations
- "List all products in my account" -> GET /v1/products
- "Who am I authenticated as?" -> GET /v1/me
- "What feature flags exist in this config?" -> GET /v1/configs/{configId}/settings
- "What is the current value of a feature flag?" -> GET /v2/settings/{settingKeyOrId}/value
- "How do I toggle a boolean feature flag on or off?" -> PUT /v2/settings/{settingKeyOrId}/value
- "What environments does this product have?" -> GET /v1/products/{productId}/environments
- "Show me all setting values for a specific config and environment" -> GET /v2/configs/{configId}/environments/{environmentId}/values
- "What are the members of my organization?" -> GET /v2/organizations/{organizationId}/members
- "How do I create a new feature flag?" -> POST /v1/configs/{configId}/settings
- "What stale flags need cleanup?" -> GET /v1/products/{productId}/staleflags
- "Show the audit log for recent changes" -> GET /v1/products/{productId}/auditlogs
- "How do I set up a percentage rollout for a flag?" -> PUT /v2/settings/{settingKeyOrId}/value (with targetingRules containing percentageOptions)
- "What webhooks are configured for this product?" -> GET /v1/products/{productId}/webhooks
- "How do I invite a team member to a product?" -> POST /v1/products/{productId}/members/invite

## Response Tips

- **Listing endpoints** (organizations, products, members, settings): Return flat arrays at the top level; iterate directly without unwrapping a `data` or `items` key.
- **Setting value endpoints** (v1 and v2): Responses are deeply nested -- the actual flag value is in `.value` (v1) or `.defaultValue` (v2), with targeting rules, rollout percentages, config, and environment metadata all inline. Extract what you need.
- **v2 members endpoint**: Returns members grouped by role (`admins`, `billingManagers`, `members`) rather than a flat list; merge or filter as needed.
- **Delete endpoints**: Return 204 with no body on success; treat any non-204 as failure.
- **Bulk value endpoints** (`/configs/{id}/environments/{id}/values`): Wrap all setting values in a `settingValues` (v1) or `settingFormulas` (v2) array alongside config/environment metadata.
- **Error responses**: 400 (validation), 404 (resource not found), 429 (rate limited) are universal; parse the response body for error details on 400.
- **v1 vs v2 setting values**: v1 uses `rolloutRules`/`rolloutPercentageItems` at the top level; v2 uses structured `targetingRules` with nested `conditions` and `percentageOptions`. Prefer v2 for new integrations.

## Anomaly Flags

- **429 Too Many Requests**: Every endpoint can return 429. Surface rate limit hits immediately and back off before retrying. Monitor frequency -- repeated 429s indicate the integration is too aggressive.
- **readOnly: true on setting values**: Indicates the environment or setting cannot be modified (locked or restricted). Surface this before attempting any PUT/PATCH to avoid confusing 400 errors.
- **reasonRequired: true on products/environments**: When present, all value updates MUST include a `reason` field or the request will fail. Detect this from the product/environment metadata and prompt accordingly.
- **evaluationVersion mismatch**: Configs can be v1 or v2. Using v2 endpoints on a v1 config (or vice versa) may produce unexpected behavior. Check `evaluationVersion` on the config object.
- **Empty targeting rules with percentage rollout**: If `rolloutPercentageItems` (v1) or `percentageOptions` (v2) do not sum to 100%, flag this as a misconfiguration.
- **Stale flags detected**: When `GET /v1/products/{productId}/staleflags` returns results, proactively surface them as cleanup candidates.
- **403 on proxy SDK key select/deselect**: Unlike most endpoints (400/404/429 only), these can return 403 indicating insufficient permissions -- surface this distinctly from other auth failures.
- **Deleted settings**: The `GET /v1/configs/{configId}/deleted-settings` endpoint exists. If a setting lookup returns 404, check deleted settings to determine if it was removed rather than never existing.

## Playbook

### 1. Create and Configure a New Feature Flag

1. List products: `GET /v1/products` and pick the target product
2. List configs for the product: `GET /v1/products/{productId}/configs`
3. Create the feature flag: `POST /v1/configs/{configId}/settings` with `key`, `name`, `settingType` (boolean/string/int/double), and optionally `initialValues` to set per-environment defaults
4. Verify creation: `GET /v1/settings/{settingId}` to confirm the flag exists
5. Optionally tag it: create a tag with `POST /v1/products/{productId}/tags`, then update the setting with the tag ID via `PUT /v1/settings/{settingId}`

### 2. Roll Out a Feature Flag to a Percentage of Users

1. Get the current flag value and targeting rules: `GET /v2/settings/{settingKeyOrId}/value` (pass the SDK key header for the target environment)
2. Check `readOnly` and `featureFlagLimitations.maxPercentageOptionCount` to confirm changes are allowed
3. Update with percentage targeting: `PUT /v2/settings/{settingKeyOrId}/value` with `targetingRules` containing `percentageOptions` (e.g., 10% true, 90% false)
4. Verify the update: `GET /v2/settings/{settingKeyOrId}/value` again and confirm `targetingRules` reflect the new percentages
5. Monitor via audit log: `GET /v1/products/{productId}/auditlogs` filtered by `configId` and time range

### 3. Set Up a Webhook for Flag Change Notifications

1. Identify the config and environment: `GET /v1/products/{productId}/configs` and `GET /v1/products/{productId}/environments`
2. Create the webhook: `POST /v1/configs/{configId}/environments/{environmentId}/webhooks` with `url` and optional `httpMethod`, `content` template, and `webHookHeaders`
3. Verify creation: `GET /v1/products/{productId}/webhooks` to see it listed
4. Retrieve signing keys: `GET /v1/webhooks/{webhookId}/keys` to get `key1`/`key2` for signature verification on your server

### 4. Audit and Clean Up Stale Feature Flags

1. Detect stale flags: `GET /v1/products/{productId}/staleflags` with `staleFlagAgeDays` set to your threshold (e.g., 90)
2. Review each stale flag: `GET /v1/settings/{settingId}` for metadata, then `GET /v1/settings/{settingId}/code-references` to check if the flag is still referenced in code
3. For flags with no code references: confirm with the team, then delete via `DELETE /v1/settings/{settingId}`
4. Check deleted settings: `GET /v1/configs/{configId}/deleted-settings` to verify cleanup

### 5. Invite a User and Configure Their Permissions

1. List existing permission groups: `GET /v1/products/{productId}/permissions` to find or create the right group
2. If no suitable group exists, create one: `POST /v1/products/{productId}/permissions` with the desired capability flags (e.g., `canCreateOrUpdateSetting`, `canViewSdkKey`)
3. Invite the user: `POST /v1/products/{productId}/members/invite` with `emails` array and `permissionGroupId`
4. Verify pending invitations: `GET /v1/products/{productId}/invitations`
5. To revoke later: `DELETE /v1/invitations/{invitationId}` (pending) or `DELETE /v1/products/{productId}/members/{userId}` (accepted)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
