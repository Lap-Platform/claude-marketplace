---
name: management-api
description: "Management API skill. Use when working with Management for companies, me, merchants. Covers 130 endpoints."
version: 1.0.0
generator: lapsh
---

# Management API
API version: 1

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://management-test.adyen.com/v1

## Setup
1. Set Authorization header with your Bearer token
2. GET /companies -- verify access
3. POST /companies/{companyId}/apiCredentials -- create first apiCredentials

## Endpoints

130 endpoints across 5 groups. See references/api-spec.lap for full details.

### companies
| Method | Path | Description |
|--------|------|-------------|
| GET | /companies | Get a list of company accounts |
| GET | /companies/{companyId} | Get a company account |
| GET | /companies/{companyId}/androidApps | Get a list of Android apps |
| GET | /companies/{companyId}/androidApps/{id} | Get Android app |
| GET | /companies/{companyId}/androidCertificates | Get a list of Android certificates |
| GET | /companies/{companyId}/apiCredentials | Get a list of API credentials |
| POST | /companies/{companyId}/apiCredentials | Create an API credential. |
| GET | /companies/{companyId}/apiCredentials/{apiCredentialId} | Get an API credential |
| PATCH | /companies/{companyId}/apiCredentials/{apiCredentialId} | Update an API credential. |
| GET | /companies/{companyId}/apiCredentials/{apiCredentialId}/allowedOrigins | Get a list of allowed origins |
| POST | /companies/{companyId}/apiCredentials/{apiCredentialId}/allowedOrigins | Create an allowed origin |
| DELETE | /companies/{companyId}/apiCredentials/{apiCredentialId}/allowedOrigins/{originId} | Delete an allowed origin |
| GET | /companies/{companyId}/apiCredentials/{apiCredentialId}/allowedOrigins/{originId} | Get an allowed origin |
| POST | /companies/{companyId}/apiCredentials/{apiCredentialId}/generateApiKey | Generate new API key |
| POST | /companies/{companyId}/apiCredentials/{apiCredentialId}/generateClientKey | Generate new client key |
| GET | /companies/{companyId}/billingEntities | Get a list of billing entities |
| GET | /companies/{companyId}/merchants | Get a list of merchant accounts |
| GET | /companies/{companyId}/shippingLocations | Get a list of shipping locations |
| POST | /companies/{companyId}/shippingLocations | Create a shipping location |
| GET | /companies/{companyId}/terminalActions | Get a list of terminal actions |
| GET | /companies/{companyId}/terminalActions/{actionId} | Get terminal action |
| GET | /companies/{companyId}/terminalLogos | Get the terminal logo |
| PATCH | /companies/{companyId}/terminalLogos | Update the terminal logo |
| GET | /companies/{companyId}/terminalModels | Get a list of terminal models |
| GET | /companies/{companyId}/terminalOrders | Get a list of orders |
| POST | /companies/{companyId}/terminalOrders | Create an order |
| GET | /companies/{companyId}/terminalOrders/{orderId} | Get an order |
| PATCH | /companies/{companyId}/terminalOrders/{orderId} | Update an order |
| POST | /companies/{companyId}/terminalOrders/{orderId}/cancel | Cancel an order |
| GET | /companies/{companyId}/terminalProducts | Get a list of terminal products |
| GET | /companies/{companyId}/terminalSettings | Get terminal settings |
| PATCH | /companies/{companyId}/terminalSettings | Update terminal settings |
| GET | /companies/{companyId}/users | Get a list of users |
| POST | /companies/{companyId}/users | Create a new user |
| GET | /companies/{companyId}/users/{userId} | Get user details |
| PATCH | /companies/{companyId}/users/{userId} | Update user details |
| GET | /companies/{companyId}/webhooks | List all webhooks |
| POST | /companies/{companyId}/webhooks | Set up a webhook |
| DELETE | /companies/{companyId}/webhooks/{webhookId} | Remove a webhook |
| GET | /companies/{companyId}/webhooks/{webhookId} | Get a webhook |
| PATCH | /companies/{companyId}/webhooks/{webhookId} | Update a webhook |
| POST | /companies/{companyId}/webhooks/{webhookId}/generateHmac | Generate an HMAC key |
| POST | /companies/{companyId}/webhooks/{webhookId}/test | Test a webhook |

### me
| Method | Path | Description |
|--------|------|-------------|
| GET | /me | Get API credential details |
| GET | /me/allowedOrigins | Get allowed origins |
| POST | /me/allowedOrigins | Add allowed origin |
| DELETE | /me/allowedOrigins/{originId} | Remove allowed origin |
| GET | /me/allowedOrigins/{originId} | Get allowed origin details |
| POST | /me/generateClientKey | Generate a client key |

### merchants
| Method | Path | Description |
|--------|------|-------------|
| GET | /merchants | Get a list of merchant accounts |
| POST | /merchants | Create a merchant account |
| GET | /merchants/{merchantId} | Get a merchant account |
| POST | /merchants/{merchantId}/activate | Request to activate a merchant account |
| GET | /merchants/{merchantId}/apiCredentials | Get a list of API credentials |
| POST | /merchants/{merchantId}/apiCredentials | Create an API credential |
| GET | /merchants/{merchantId}/apiCredentials/{apiCredentialId} | Get an API credential |
| PATCH | /merchants/{merchantId}/apiCredentials/{apiCredentialId} | Update an API credential |
| GET | /merchants/{merchantId}/apiCredentials/{apiCredentialId}/allowedOrigins | Get a list of allowed origins |
| POST | /merchants/{merchantId}/apiCredentials/{apiCredentialId}/allowedOrigins | Create an allowed origin |
| DELETE | /merchants/{merchantId}/apiCredentials/{apiCredentialId}/allowedOrigins/{originId} | Delete an allowed origin |
| GET | /merchants/{merchantId}/apiCredentials/{apiCredentialId}/allowedOrigins/{originId} | Get an allowed origin |
| POST | /merchants/{merchantId}/apiCredentials/{apiCredentialId}/generateApiKey | Generate new API key |
| POST | /merchants/{merchantId}/apiCredentials/{apiCredentialId}/generateClientKey | Generate new client key |
| GET | /merchants/{merchantId}/billingEntities | Get a list of billing entities |
| GET | /merchants/{merchantId}/paymentMethodSettings | Get all payment methods |
| POST | /merchants/{merchantId}/paymentMethodSettings | Request a payment method |
| GET | /merchants/{merchantId}/paymentMethodSettings/{paymentMethodId} | Get payment method details |
| PATCH | /merchants/{merchantId}/paymentMethodSettings/{paymentMethodId} | Update a payment method |
| POST | /merchants/{merchantId}/paymentMethodSettings/{paymentMethodId}/addApplePayDomains | Add an Apple Pay domain |
| GET | /merchants/{merchantId}/paymentMethodSettings/{paymentMethodId}/getApplePayDomains | Get Apple Pay domains |
| GET | /merchants/{merchantId}/payoutSettings | Get a list of payout settings |
| POST | /merchants/{merchantId}/payoutSettings | Add a payout setting |
| DELETE | /merchants/{merchantId}/payoutSettings/{payoutSettingsId} | Delete a payout setting |
| GET | /merchants/{merchantId}/payoutSettings/{payoutSettingsId} | Get a payout setting |
| PATCH | /merchants/{merchantId}/payoutSettings/{payoutSettingsId} | Update a payout setting |
| GET | /merchants/{merchantId}/shippingLocations | Get a list of shipping locations |
| POST | /merchants/{merchantId}/shippingLocations | Create a shipping location |
| GET | /merchants/{merchantId}/splitConfigurations | Get a list of split configuration profiles |
| POST | /merchants/{merchantId}/splitConfigurations | Create a split configuration profile |
| DELETE | /merchants/{merchantId}/splitConfigurations/{splitConfigurationId} | Delete a split configuration profile |
| GET | /merchants/{merchantId}/splitConfigurations/{splitConfigurationId} | Get a split configuration profile |
| PATCH | /merchants/{merchantId}/splitConfigurations/{splitConfigurationId} | Update the description of the split configuration profile |
| POST | /merchants/{merchantId}/splitConfigurations/{splitConfigurationId} | Create a rule |
| DELETE | /merchants/{merchantId}/splitConfigurations/{splitConfigurationId}/rules/{ruleId} | Delete a rule |
| PATCH | /merchants/{merchantId}/splitConfigurations/{splitConfigurationId}/rules/{ruleId} | Update the split conditions |
| PATCH | /merchants/{merchantId}/splitConfigurations/{splitConfigurationId}/rules/{ruleId}/splitLogic/{splitLogicId} | Update the split logic |
| GET | /merchants/{merchantId}/stores | Get a list of stores |
| POST | /merchants/{merchantId}/stores | Create a store |
| GET | /merchants/{merchantId}/stores/{reference}/terminalLogos | Get the terminal logo |
| PATCH | /merchants/{merchantId}/stores/{reference}/terminalLogos | Update the terminal logo |
| GET | /merchants/{merchantId}/stores/{reference}/terminalSettings | Get terminal settings |
| PATCH | /merchants/{merchantId}/stores/{reference}/terminalSettings | Update terminal settings |
| GET | /merchants/{merchantId}/stores/{storeId} | Get a store |
| PATCH | /merchants/{merchantId}/stores/{storeId} | Update a store |
| GET | /merchants/{merchantId}/terminalLogos | Get the terminal logo |
| PATCH | /merchants/{merchantId}/terminalLogos | Update the terminal logo |
| GET | /merchants/{merchantId}/terminalModels | Get a list of terminal models |
| GET | /merchants/{merchantId}/terminalOrders | Get a list of orders |
| POST | /merchants/{merchantId}/terminalOrders | Create an order |
| GET | /merchants/{merchantId}/terminalOrders/{orderId} | Get an order |
| PATCH | /merchants/{merchantId}/terminalOrders/{orderId} | Update an order |
| POST | /merchants/{merchantId}/terminalOrders/{orderId}/cancel | Cancel an order |
| GET | /merchants/{merchantId}/terminalProducts | Get a list of terminal products |
| GET | /merchants/{merchantId}/terminalSettings | Get terminal settings |
| PATCH | /merchants/{merchantId}/terminalSettings | Update terminal settings |
| GET | /merchants/{merchantId}/users | Get a list of users |
| POST | /merchants/{merchantId}/users | Create a new user |
| GET | /merchants/{merchantId}/users/{userId} | Get user details |
| PATCH | /merchants/{merchantId}/users/{userId} | Update a user |
| GET | /merchants/{merchantId}/webhooks | List all webhooks |
| POST | /merchants/{merchantId}/webhooks | Set up a webhook |
| DELETE | /merchants/{merchantId}/webhooks/{webhookId} | Remove a webhook |
| GET | /merchants/{merchantId}/webhooks/{webhookId} | Get a webhook |
| PATCH | /merchants/{merchantId}/webhooks/{webhookId} | Update a webhook |
| POST | /merchants/{merchantId}/webhooks/{webhookId}/generateHmac | Generate an HMAC key |
| POST | /merchants/{merchantId}/webhooks/{webhookId}/test | Test a webhook |

### stores
| Method | Path | Description |
|--------|------|-------------|
| GET | /stores | Get a list of stores |
| POST | /stores | Create a store |
| GET | /stores/{storeId} | Get a store |
| PATCH | /stores/{storeId} | Update a store |
| GET | /stores/{storeId}/terminalLogos | Get the terminal logo |
| PATCH | /stores/{storeId}/terminalLogos | Update the terminal logo |
| GET | /stores/{storeId}/terminalSettings | Get terminal settings |
| PATCH | /stores/{storeId}/terminalSettings | Update terminal settings |

### terminals
| Method | Path | Description |
|--------|------|-------------|
| GET | /terminals | Get a list of terminals |
| POST | /terminals/scheduleActions | Create a terminal action |
| GET | /terminals/{terminalId}/terminalLogos | Get the terminal logo |
| PATCH | /terminals/{terminalId}/terminalLogos | Update the logo |
| GET | /terminals/{terminalId}/terminalSettings | Get terminal settings |
| PATCH | /terminals/{terminalId}/terminalSettings | Update terminal settings |

## Enhanced Skill Content
## Question Mapping

- "What companies do I have access to?" -> GET /companies
- "Show me details for a specific company" -> GET /companies/{companyId}
- "Who are the users under this merchant account?" -> GET /merchants/{merchantId}/users
- "What API credentials exist for my company?" -> GET /companies/{companyId}/apiCredentials
- "How do I rotate an API key for a credential?" -> POST /companies/{companyId}/apiCredentials/{apiCredentialId}/generateApiKey
- "What payment methods are configured for this merchant?" -> GET /merchants/{merchantId}/paymentMethodSettings
- "How do I enable Apple Pay on a merchant?" -> POST /merchants/{merchantId}/paymentMethodSettings (type: "applepay", with domains)
- "What terminals do I have and where are they?" -> GET /terminals
- "How do I order new terminals for a merchant?" -> POST /merchants/{merchantId}/terminalOrders
- "What webhooks are configured and are any failing?" -> GET /companies/{companyId}/webhooks
- "How do I test if a webhook endpoint is reachable?" -> POST /companies/{companyId}/webhooks/{webhookId}/test
- "What stores belong to this merchant?" -> GET /merchants/{merchantId}/stores
- "How do I create a new merchant account under my company?" -> POST /merchants
- "What are the current terminal settings at the store level?" -> GET /merchants/{merchantId}/stores/{reference}/terminalSettings
- "Who am I authenticated as right now?" -> GET /me

## Response Tips

- **Paginated lists** (companies, merchants, users, credentials, webhooks, stores, terminals): Check `pagesTotal` and `itemsTotal`; follow `_links.next.href` to page forward. An empty `data` array or 204 means no results.
- **Entity details** (company, merchant, store, user): The `_links` object contains HATEOAS URLs for related resources (credentials, webhooks, users) -- use these instead of constructing URLs manually.
- **Terminal settings**: Deeply nested object with 20+ top-level config sections. PATCH merges at the section level -- only send the sections you want to change.
- **Payment method settings**: Response contains config blocks for every supported method (visa, mc, klarna, etc.) but only the one matching `type` is populated. Check `enabled`, `allowed`, and `verificationStatus` to understand actual state.
- **Webhooks**: `hasError: true` signals delivery failures; `hasPassword: true` confirms auth is set without exposing the value. The HMAC key is only returned from the `/generateHmac` endpoint.
- **Terminal orders**: `status` tracks order lifecycle; `trackingUrl` is only populated after shipment. 204 responses on merchant-scoped endpoints indicate the merchant exists but has no matching data.
- **Error responses** (400/401/403/422/500): All endpoints share the same error code set. 422 typically means valid JSON but failed business validation (e.g., duplicate domain, invalid role).

## Anomaly Flags

- **Webhook `hasError: true`**: Proactively warn when any webhook shows delivery errors -- this means notifications are being dropped.
- **API credential `active: false`**: Flag inactive credentials that may be blocking integrations, especially if recently changed via PATCH.
- **Payment method `verificationStatus` not verified**: Surface when a configured payment method has a pending or failed verification -- it will not process live transactions.
- **Payment method `allowed: false` but `enabled: true`**: Contradictory state indicating Adyen has disallowed a method the merchant tried to enable. Requires Adyen support.
- **Store `status: closed` or `inactive`**: Alert when operating on a store that is not active, as terminal settings and orders may not apply.
- **Terminal order `status` unchanged**: If an order stays in the same status across checks, flag potential fulfillment delays.
- **Webhook SSL settings**: Flag `acceptsExpiredCertificate`, `acceptsSelfSignedCertificate`, or `acceptsUntrustedRootCertificate` set to true -- these weaken security.
- **429 on payment method endpoints**: This group uniquely returns 429 (rate limit). Surface immediately and advise backing off.
- **Empty `data` arrays with 200 status**: Distinguish from 204 (no content) -- 200 with empty data means the parent entity exists but has no children of that type.

## Playbook

### 1. Onboard a new merchant with a store and terminals

1. `POST /merchants` with `companyId` and optional `description`, `pricingPlan`
2. Note the returned `id` as `merchantId`
3. `POST /merchants/{merchantId}/stores` with address, phone, shopperStatement
4. `POST /merchants/{merchantId}/paymentMethodSettings` for each payment method (e.g., visa, mc, applepay)
5. `GET /merchants/{merchantId}/terminalProducts?country=XX` to find available terminal models
6. `POST /merchants/{merchantId}/shippingLocations` to set delivery address
7. `GET /merchants/{merchantId}/billingEntities` to find billing entity ID
8. `POST /merchants/{merchantId}/terminalOrders` with items, shippingLocationId, billingEntityId

### 2. Set up webhook notifications for a company

1. `POST /companies/{companyId}/webhooks` with `url`, `type`, `communicationFormat: "json"`, `active: true`, `filterMerchantAccountType`, and `filterMerchantAccounts`
2. Note the returned webhook `id`
3. `POST /companies/{companyId}/webhooks/{webhookId}/generateHmac` to get the HMAC key for signature verification
4. `POST /companies/{companyId}/webhooks/{webhookId}/test` with a sample notification to verify delivery
5. Check the test response `data` array for success/failure per merchant

### 3. Rotate API credentials safely

1. `GET /companies/{companyId}/apiCredentials` to list all credentials
2. Identify the target credential by `description` or `username`
3. `POST /companies/{companyId}/apiCredentials/{apiCredentialId}/generateApiKey` to get a new API key (old key is immediately invalidated)
4. Update the consuming application with the new `apiKey` value
5. `POST /companies/{companyId}/apiCredentials/{apiCredentialId}/generateClientKey` if a client-side key is also needed
6. Optionally `PATCH /companies/{companyId}/apiCredentials/{apiCredentialId}` to update `allowedOrigins` or `roles`

### 4. Configure terminal settings across the hierarchy

1. `PATCH /companies/{companyId}/terminalSettings` to set company-wide defaults (localization, receipt printing, refund policy)
2. `PATCH /merchants/{merchantId}/terminalSettings` to override at the merchant level (e.g., different gratuity config)
3. `PATCH /merchants/{merchantId}/stores/{reference}/terminalSettings` for store-specific overrides (e.g., pay-at-table, standalone mode)
4. `PATCH /terminals/{terminalId}/terminalSettings` for individual terminal exceptions
5. Settings inherit downward: company -> merchant -> store -> terminal. Only send the sections you want to override at each level.

### 5. Manage user access for a merchant

1. `GET /merchants/{merchantId}/users` to list current users (use `pageSize` and `pageNumber` for large lists)
2. `POST /merchants/{merchantId}/users` with `email`, `username`, `name`, and `roles` to invite a new user
3. `PATCH /merchants/{merchantId}/users/{userId}` to change roles, deactivate (`active: false`), or update email
4. To audit a specific user: `GET /merchants/{merchantId}/users/{userId}` and review `roles`, `accountGroups`, and `active` status
5. Repeat at company level via `/companies/{companyId}/users` for broader access -- company users can have `associatedMerchantAccounts` to scope their access


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
