---
name: configuration-api
description: "Configuration API skill. Use when working with Configuration for accountHolders, balanceAccounts, balancePlatforms. Covers 79 endpoints."
version: 1.0.0
generator: lapsh
---

# Configuration API
API version: 2

## Auth
ApiKey X-API-Key in header | Bearer basic | ApiKey clientKey in query

## Base URL
https://balanceplatform-api-test.adyen.com/bcl/v2

## Setup
1. Set Authorization header with your Bearer token
2. GET /cardorders -- verify access
3. POST /accountHolders -- create first accountHolders

## Endpoints

79 endpoints across 17 groups. See references/api-spec.lap for full details.

### accountHolders
| Method | Path | Description |
|--------|------|-------------|
| POST | /accountHolders | Create an account holder |
| GET | /accountHolders/{id} | Get an account holder |
| PATCH | /accountHolders/{id} | Update an account holder |
| GET | /accountHolders/{id}/balanceAccounts | Get all balance accounts of an account holder |
| GET | /accountHolders/{id}/taxForms | Get a tax form |
| GET | /accountHolders/{id}/transactionRules | Get all transaction rules for an account holder |
| GET | /accountHolders/{id}/taxFormSummary | Get summary of tax forms for an account holder |

### balanceAccounts
| Method | Path | Description |
|--------|------|-------------|
| POST | /balanceAccounts | Create a balance account |
| GET | /balanceAccounts/{balanceAccountId}/sweeps | Get all sweeps for a balance account |
| POST | /balanceAccounts/{balanceAccountId}/sweeps | Create a sweep |
| GET | /balanceAccounts/{balanceAccountId}/sweeps/{sweepId} | Get a sweep |
| DELETE | /balanceAccounts/{balanceAccountId}/sweeps/{sweepId} | Delete a sweep |
| PATCH | /balanceAccounts/{balanceAccountId}/sweeps/{sweepId} | Update a sweep |
| GET | /balanceAccounts/{id} | Get a balance account |
| PATCH | /balanceAccounts/{id} | Update a balance account |
| GET | /balanceAccounts/{id}/paymentInstruments | Get payment instruments linked to a balance account |
| GET | /balanceAccounts/{id}/transactionRules | Get all transaction rules for a balance account |
| POST | /balanceAccounts/{id}/transferLimits/approve | Approve pending transfer limits |
| GET | /balanceAccounts/{id}/transferLimits | Filter and view the transfer limits |
| POST | /balanceAccounts/{id}/transferLimits | Create a transfer limit |
| GET | /balanceAccounts/{id}/transferLimits/current | Get all current transfer limits |
| GET | /balanceAccounts/{id}/transferLimits/{transferLimitId} | Get the details of a transfer limit |
| DELETE | /balanceAccounts/{id}/transferLimits/{transferLimitId} | Delete a scheduled or pending transfer limit |

### balancePlatforms
| Method | Path | Description |
|--------|------|-------------|
| GET | /balancePlatforms/{id} | Get a balance platform |
| GET | /balancePlatforms/{id}/accountHolders | Get all account holders under a balance platform |
| GET | /balancePlatforms/{id}/transactionRules | Get all transaction rules for a balance platform |
| GET | /balancePlatforms/{balancePlatformId}/webhooks/{webhookId}/settings | Get all balance webhook settings |
| POST | /balancePlatforms/{balancePlatformId}/webhooks/{webhookId}/settings | Create a balance webhook setting |
| GET | /balancePlatforms/{balancePlatformId}/webhooks/{webhookId}/settings/{settingId} | Get a balance webhook setting by id |
| DELETE | /balancePlatforms/{balancePlatformId}/webhooks/{webhookId}/settings/{settingId} | Delete a balance webhook setting by id |
| PATCH | /balancePlatforms/{balancePlatformId}/webhooks/{webhookId}/settings/{settingId} | Update a balance webhook setting by id |
| GET | /balancePlatforms/{id}/transferLimits | Filter and view the transfer limits |
| POST | /balancePlatforms/{id}/transferLimits | Create a transfer limit |
| GET | /balancePlatforms/{id}/transferLimits/{transferLimitId} | Get the details of a transfer limit |
| DELETE | /balancePlatforms/{id}/transferLimits/{transferLimitId} | Delete a scheduled or pending transfer limit |

### cardorders
| Method | Path | Description |
|--------|------|-------------|
| GET | /cardorders | Get a list of card orders |
| GET | /cardorders/{id}/items | Get card order items |

### grantAccounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /grantAccounts/{id} | Get a grant account |

### grantOffers
| Method | Path | Description |
|--------|------|-------------|
| GET | /grantOffers | Get all available grant offers |
| GET | /grantOffers/{grantOfferId} | Get a grant offer |

### networkTokens
| Method | Path | Description |
|--------|------|-------------|
| GET | /networkTokens/{networkTokenId} | Get a network token |
| PATCH | /networkTokens/{networkTokenId} | Update a network token |

### paymentInstrumentGroups
| Method | Path | Description |
|--------|------|-------------|
| POST | /paymentInstrumentGroups | Create a payment instrument group |
| GET | /paymentInstrumentGroups/{id} | Get a payment instrument group |
| GET | /paymentInstrumentGroups/{id}/transactionRules | Get all transaction rules for a payment instrument group |

### paymentInstruments
| Method | Path | Description |
|--------|------|-------------|
| POST | /paymentInstruments | Create a payment instrument |
| POST | /paymentInstruments/reveal | Reveal the data of a payment instrument |
| GET | /paymentInstruments/{id} | Get a payment instrument |
| PATCH | /paymentInstruments/{id} | Update a payment instrument |
| GET | /paymentInstruments/{id}/networkTokenActivationData | Get network token activation data |
| POST | /paymentInstruments/{id}/networkTokenActivationData | Create network token provisioning data |
| GET | /paymentInstruments/{id}/networkTokens | List network tokens |
| GET | /paymentInstruments/{id}/reveal | Get the PAN of a payment instrument |
| GET | /paymentInstruments/{id}/transactionRules | Get all transaction rules for a payment instrument |
| GET | /paymentInstruments/{paymentInstrumentId}/authorisedCardUsers | Get authorized users for a card. |
| POST | /paymentInstruments/{paymentInstrumentId}/authorisedCardUsers | Create authorized users for a card. |
| DELETE | /paymentInstruments/{paymentInstrumentId}/authorisedCardUsers | Delete the authorized users for a card. |
| PATCH | /paymentInstruments/{paymentInstrumentId}/authorisedCardUsers | Update the authorized users for a card. |

### pins
| Method | Path | Description |
|--------|------|-------------|
| POST | /pins/change | Change a card PIN |
| POST | /pins/reveal | Reveal a card PIN |

### publicKey
| Method | Path | Description |
|--------|------|-------------|
| GET | /publicKey | Get an RSA public key |

### registeredDevices
| Method | Path | Description |
|--------|------|-------------|
| GET | /registeredDevices | Get a list of registered SCA devices |
| POST | /registeredDevices | Initiate the registration of an SCA device |
| POST | /registeredDevices/{deviceId}/associations | Initiate an association between an SCA device and a resource |
| PATCH | /registeredDevices/{deviceId}/associations | Complete an association between an SCA device and a resource |
| DELETE | /registeredDevices/{id} | Delete a registration of an SCA device |
| PATCH | /registeredDevices/{id} | Complete the registration of an SCA device |

### transactionRules
| Method | Path | Description |
|--------|------|-------------|
| POST | /transactionRules | Create a transaction rule |
| GET | /transactionRules/{transactionRuleId} | Get a transaction rule |
| DELETE | /transactionRules/{transactionRuleId} | Delete a transaction rule |
| PATCH | /transactionRules/{transactionRuleId} | Update a transaction rule |

### transferRoutes
| Method | Path | Description |
|--------|------|-------------|
| POST | /transferRoutes/calculate | Calculate transfer routes |

### validateBankAccountIdentification
| Method | Path | Description |
|--------|------|-------------|
| POST | /validateBankAccountIdentification | Validate a bank account |

### scaAssociations
| Method | Path | Description |
|--------|------|-------------|
| GET | /scaAssociations | Get a list of devices associated with an entity |
| DELETE | /scaAssociations | Delete association to devices |
| PATCH | /scaAssociations | Approve a pending approval association |

### scaDevices
| Method | Path | Description |
|--------|------|-------------|
| POST | /scaDevices | Begin SCA device registration |
| PATCH | /scaDevices/{deviceId} | Finish registration process for a SCA device |
| POST | /scaDevices/{deviceId}/scaAssociations | Create a new SCA association for a device |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new account holder?" -> POST /accountHolders
- "What are the details of a specific account holder?" -> GET /accountHolders/{id}
- "How do I update an account holder's contact details or status?" -> PATCH /accountHolders/{id}
- "What balance accounts belong to this account holder?" -> GET /accountHolders/{id}/balanceAccounts
- "How do I issue a new card or bank account payment instrument?" -> POST /paymentInstruments
- "How do I suspend or close a payment instrument?" -> PATCH /paymentInstruments/{id}
- "How do I reveal the full PAN and CVC of a card?" -> GET /paymentInstruments/{id}/reveal
- "How do I set up an automatic sweep on a balance account?" -> POST /balanceAccounts/{balanceAccountId}/sweeps
- "How do I create a transaction rule to block certain MCCs or countries?" -> POST /transactionRules
- "What transaction rules apply to a specific payment instrument?" -> GET /paymentInstruments/{id}/transactionRules
- "How do I validate a bank account number before creating a transfer?" -> POST /validateBankAccountIdentification
- "How do I download a US tax form (1099-K) for an account holder?" -> GET /accountHolders/{id}/taxForms
- "What grant offers are available for an account holder?" -> GET /grantOffers
- "How do I set a daily transfer limit on a balance account?" -> POST /balanceAccounts/{id}/transferLimits
- "How do I calculate available transfer routes for a payout?" -> POST /transferRoutes/calculate

## Response Tips

- **Paginated lists** (balanceAccounts, sweeps, cardorders, accountHolders, registeredDevices): Check `hasNext`/`hasPrevious` booleans and pass `offset`+`limit` to page forward; registeredDevices uses `pageNumber`/`pageSize` with `pagesTotal` and `itemsTotal` instead.
- **Account holders & balance accounts**: The `status` field (`active`, `suspended`, `closed`) and `capabilities` map are critical -- capabilities contain per-capability verification statuses that determine what the entity can do.
- **Payment instruments**: Responses vary significantly by `type` (`card` vs `bankAccount`) -- only one of the `card` or `bankAccount` nested objects will be populated; card responses include deeply nested `configuration`, `deliveryContact`, and `expiration` objects.
- **Transaction rules**: The response wraps the rule in a `transactionRule` key on GET but returns it flat on POST/PATCH/DELETE -- normalize accordingly.
- **Sweeps**: The `reason` field contains machine-readable failure codes (e.g., `notEnoughBalance`, `counterpartyAccountBlocked`) -- always surface this when a sweep is not in `active` status.
- **Error responses** (400, 401, 403, 422, 500): 422 typically carries field-level validation details; 401 means the API key is invalid or missing; 403 means the key lacks permission for the specific resource.

## Anomaly Flags

- **Account holder `verificationDeadlines`**: Surface any upcoming deadlines -- missing them can result in capabilities being disabled or the account being suspended.
- **Sweep `reason` not `approved`**: If a sweep exists but its reason is `notEnoughBalance`, `counterpartyAccountBlocked`, or `error`, flag it immediately as the sweep is failing silently.
- **Payment instrument `status` = `suspended` or `inactive`**: Proactively warn when a card or bank account is not active, especially if the user is trying to transact with it.
- **`replacedById` on payment instruments**: Indicates the card has been replaced (lost/stolen/expired) -- flag if the user is referencing a superseded instrument.
- **Transfer limit `limitStatus` changes**: Surface when a limit moves out of active state or when SCA approval is pending (`scaInformation.status`).
- **422 errors on POST /transactionRules**: These usually indicate conflicting rule restrictions or invalid interval configurations -- surface the specific field validation errors.
- **Network token `status` = `suspended` or `closed`**: Flag tokenized cards that are no longer functional for wallet payments.
- **`statusReason` = `suspectedFraud` or `stolen`**: Escalate immediately when payment instruments carry fraud-related status reasons.

## Playbook

### 1. Onboard a New Account Holder with a Balance Account and Card

1. Create the account holder: `POST /accountHolders` with `legalEntityId` and `contactDetails`.
2. Note the returned `id` and check `verificationDeadlines` for any pending KYC requirements.
3. Create a balance account: `POST /balanceAccounts` with `accountHolderId` set to the new holder's ID and desired `defaultCurrencyCode`.
4. Issue a card: `POST /paymentInstruments` with `balanceAccountId`, `issuingCountryCode`, `type: "card"`, and the `card` object (brand, brandVariant, cardholderName, formFactor, configurationProfileId).
5. Verify the card status is `active` in the response; if `inactive`, check if activation is required via `card.configuration.activation`.

### 2. Set Up Automated Sweeps for Payouts

1. Identify the balance account: `GET /balanceAccounts/{id}` to confirm it exists and is `active`.
2. Create the sweep: `POST /balanceAccounts/{balanceAccountId}/sweeps` with `counterparty` (target balance account or transfer instrument), `currency`, `schedule` (cron or daily), and either `triggerAmount` or `targetAmount`.
3. Verify the sweep was created with `status: "active"` in the response.
4. Monitor sweep health: `GET /balanceAccounts/{balanceAccountId}/sweeps` periodically and check the `reason` field -- anything other than `approved` indicates a problem.
5. To pause a sweep: `PATCH /balanceAccounts/{balanceAccountId}/sweeps/{sweepId}` with `status: "inactive"`.

### 3. Create a Transaction Rule to Block High-Risk Countries

1. Identify the entity to protect: note the `entityReference` (account holder ID, balance account ID, or payment instrument ID) and `entityType`.
2. Create the block rule: `POST /transactionRules` with `type: "blockList"`, `ruleRestrictions.countries` set to `{ operation: "anyOf", value: ["XX", "YY"] }`, and `interval.type` appropriate to your use case.
3. Set `outcomeType: "hardBlock"` to reject transactions outright, or `"enforceSCA"` to require additional authentication instead.
4. Confirm the rule is `active` in the response and note the returned `id`.
5. To verify it's applied: `GET /accountHolders/{id}/transactionRules` (or the relevant entity's transaction rules endpoint) and confirm your rule appears.

### 4. Reveal Card Details for Customer Display

1. Fetch the public key: `GET /publicKey` with `purpose` and `format` to get the RSA encryption key.
2. Encrypt your client-side key using the returned `publicKey`.
3. Call `POST /paymentInstruments/reveal` with `encryptedKey` and `paymentInstrumentId` to get `encryptedData` containing PAN, CVC, and expiry.
4. Alternatively, for server-side use: `GET /paymentInstruments/{id}/reveal` returns `pan`, `cvc`, and `expiration` directly -- ensure this is only called in PCI-compliant environments.

### 5. Manage Transfer Limits with SCA Approval

1. Review current limits: `GET /balanceAccounts/{id}/transferLimits/current` to see what's active now.
2. Create a new limit: `POST /balanceAccounts/{id}/transferLimits` with `amount`, `scope` (`perDay` or `perTransaction`), and `transferType` (`instant` or `all`).
3. Check the response `limitStatus` and `scaInformation.status` -- if SCA is required, the limit will be pending until approved.
4. Approve pending limits: `POST /balanceAccounts/{id}/transferLimits/approve` with the `transferLimitIds` array and provide the `WWW-Authenticate` header with the SCA token.
5. To remove a limit: `DELETE /balanceAccounts/{id}/transferLimits/{transferLimitId}`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
