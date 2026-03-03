---
name: legal-entity-management-api
description: "Legal Entity Management API skill. Use when working with Legal Entity Management for businessLines, documents, legalEntities. Covers 34 endpoints."
version: 1.0.0
generator: lapsh
---

# Legal Entity Management API
API version: 3

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://kyc-test.adyen.com/lem/v3

## Setup
1. Set Authorization header with your Bearer token
2. GET /themes -- verify access
3. POST /businessLines -- create first businessLines

## Endpoints

34 endpoints across 5 groups. See references/api-spec.lap for full details.

### businessLines
| Method | Path | Description |
|--------|------|-------------|
| POST | /businessLines | Create a business line |
| GET | /businessLines/{id} | Get a business line |
| DELETE | /businessLines/{id} | Delete a business line |
| PATCH | /businessLines/{id} | Update a business line |

### documents
| Method | Path | Description |
|--------|------|-------------|
| POST | /documents | Upload a document for verification checks |
| GET | /documents/{id} | Get a document |
| DELETE | /documents/{id} | Delete a document |
| PATCH | /documents/{id} | Update a document |

### legalEntities
| Method | Path | Description |
|--------|------|-------------|
| POST | /legalEntities | Create a legal entity |
| GET | /legalEntities/{id} | Get a legal entity |
| PATCH | /legalEntities/{id} | Update a legal entity |
| GET | /legalEntities/{id}/acceptedTermsOfServiceDocument/{termsofserviceacceptancereference} | Get accepted Terms of Service document |
| GET | /legalEntities/{id}/businessLines | Get all business lines under a legal entity |
| POST | /legalEntities/{id}/checkTaxElectronicDeliveryConsent | Check the status of consent for electronic delivery of tax forms |
| POST | /legalEntities/{id}/checkVerificationErrors | Check a legal entity's verification errors |
| POST | /legalEntities/{id}/confirmDataReview | Confirm data review |
| POST | /legalEntities/{id}/onboardingLinks | Get a link to an Adyen-hosted onboarding page |
| GET | /legalEntities/{id}/pciQuestionnaires | Get PCI questionnaire details |
| POST | /legalEntities/{id}/pciQuestionnaires/generatePciTemplates | Generate PCI questionnaire |
| POST | /legalEntities/{id}/pciQuestionnaires/signPciTemplates | Sign PCI questionnaire |
| POST | /legalEntities/{id}/pciQuestionnaires/signingRequired | Calculate PCI status of a legal entity |
| GET | /legalEntities/{id}/pciQuestionnaires/{pciid} | Get PCI questionnaire |
| POST | /legalEntities/{id}/setTaxElectronicDeliveryConsent | Set the consent status for electronic delivery of tax forms |
| POST | /legalEntities/{id}/termsOfService | Get Terms of Service document |
| PATCH | /legalEntities/{id}/termsOfService/{termsofservicedocumentid} | Accept Terms of Service |
| GET | /legalEntities/{id}/termsOfServiceAcceptanceInfos | Get Terms of Service information for a legal entity |
| GET | /legalEntities/{id}/termsOfServiceStatus | Get Terms of Service status |
| POST | /legalEntities/{id}/requestPeriodicReview | Request periodic data review. |

### themes
| Method | Path | Description |
|--------|------|-------------|
| GET | /themes | Get a list of hosted onboarding page themes |
| GET | /themes/{id} | Get an onboarding link theme |

### transferInstruments
| Method | Path | Description |
|--------|------|-------------|
| POST | /transferInstruments | Create a transfer instrument |
| GET | /transferInstruments/{id} | Get a transfer instrument |
| DELETE | /transferInstruments/{id} | Delete a transfer instrument |
| PATCH | /transferInstruments/{id} | Update a transfer instrument |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new legal entity for an organization?" -> POST /legalEntities
- "How do I look up a legal entity by its ID?" -> GET /legalEntities/{id}
- "How do I update an individual's address or name?" -> PATCH /legalEntities/{id}
- "How do I upload a passport or ID document for KYC?" -> POST /documents
- "How do I check if a legal entity has verification errors?" -> POST /legalEntities/{id}/checkVerificationErrors
- "How do I create an onboarding link for a merchant?" -> POST /legalEntities/{id}/onboardingLinks
- "How do I add a bank account to a legal entity?" -> POST /transferInstruments
- "How do I set up a business line for payment processing?" -> POST /businessLines
- "How do I accept the terms of service for a legal entity?" -> PATCH /legalEntities/{id}/termsOfService/{termsofservicedocumentid}
- "How do I check which terms of service still need to be accepted?" -> GET /legalEntities/{id}/termsOfServiceStatus
- "How do I get all business lines for a legal entity?" -> GET /legalEntities/{id}/businessLines
- "How do I check if PCI questionnaire signing is required?" -> POST /legalEntities/{id}/pciQuestionnaires/signingRequired
- "How do I delete a document that was uploaded by mistake?" -> DELETE /documents/{id}
- "How do I retrieve a document without downloading its content?" -> GET /documents/{id} (with skipContent=true)
- "How do I list available hosted onboarding themes?" -> GET /themes

## Response Tips

- **Legal entities**: Response includes a type-specific sub-object (`individual`, `organization`, `soleProprietorship`, `trust`, `unincorporatedPartnership`) -- only the one matching the entity type is populated; ignore the rest. Check `problems` array for actionable verification issues. `entityAssociations` links shareholders/signatories to sub-entities.
- **Business lines**: The `problems` array on create/update indicates missing data blocking activation. `capability` and `service` determine what the business line enables. The `id` returned is needed for all subsequent operations.
- **Documents**: The `attachment.content` field is base64-encoded binary -- omit it in read calls using `skipContent=true` to reduce payload size. `owner.id` and `owner.type` tie the document to a legal entity or transfer instrument.
- **Transfer instruments**: `bankAccount.accountIdentification` is a polymorphic `any` type -- its shape varies by country (IBAN vs. US routing/account number vs. others). Always check `problems` for bank account validation issues.
- **Terms of service**: `GET .../termsOfServiceStatus` returns an array of required ToS types. `POST .../termsOfService` fetches the document; `PATCH .../termsOfService/{id}` records acceptance. The document content is base64-encoded.
- **Themes**: `GET /themes` supports cursor-based pagination via `next` and `previous` URL fields -- follow these until both are null.
- **Errors**: All endpoints share the same error codes (400, 401, 403, 422, 500). 422 typically means validation failure with details in the response body. 403 can mean insufficient API credential scope, not just authentication failure.

## Anomaly Flags

- **`problems` array is non-empty**: Surface immediately after any create/update on legal entities, business lines, or transfer instruments. These indicate verification blockers or missing required data that will prevent activation.
- **`verificationDeadlines` approaching**: Legal entity responses include deadline dates for required verification actions. Flag any deadline within 7 days as urgent.
- **422 on entity updates**: Often means a required nested field is missing (e.g., `registeredAddress` on an organization). Surface the full error body -- it usually contains field-level detail.
- **Document expiry dates**: When retrieving documents, flag any where `expiryDate` is in the past or within 30 days. Expired identity documents block verification.
- **Missing capabilities**: If `capabilities` map on a legal entity or transfer instrument shows any capability not in `allowed` state, surface which capabilities are blocked and why.
- **Terms of service not accepted**: If `termsOfServiceStatus` returns non-empty `termsOfServiceTypes`, the entity cannot transact until these are accepted. Flag proactively after entity creation.
- **PCI signing required**: After creating business lines with ecommerce sales channels, proactively check `signingRequired` -- unresolved PCI obligations block payment processing.
- **`x-requested-verification-code` header usage**: This header triggers re-verification. Flag when it appears in requests, as it resets verification state and may cause temporary processing disruption.

## Playbook

### Onboard a New Organization

1. Create the legal entity: `POST /legalEntities` with `type: "organization"`, providing `legalName`, `registeredAddress`, and `registrationNumber` in the `organization` object.
2. Note the returned `id` -- this is the `legalEntityId` for all subsequent steps.
3. Create entity associations for shareholders/signatories: `PATCH /legalEntities/{id}` with `entityAssociations` linking to individual legal entities (create those first via separate `POST /legalEntities` with `type: "individual"`).
4. Upload required documents: `POST /documents` with `owner.id` set to the legal entity ID, `owner.type` set to `"organization"`, and appropriate `type` (e.g., `registrationDocument`, `proofOfAddress`).
5. Create a business line: `POST /businessLines` with the `legalEntityId`, `industryCode`, and `service`.
6. Check for verification errors: `POST /legalEntities/{id}/checkVerificationErrors` and resolve any items in the `problems` array.
7. Check terms of service status: `GET /legalEntities/{id}/termsOfServiceStatus`, then for each required type, fetch with `POST /legalEntities/{id}/termsOfService` and accept with `PATCH /legalEntities/{id}/termsOfService/{docId}`.

### Add a Bank Account to an Existing Entity

1. Retrieve the legal entity: `GET /legalEntities/{id}` to confirm it exists and note its type.
2. Create the transfer instrument: `POST /transferInstruments` with `legalEntityId`, `type: "bankAccount"`, and the `bankAccount` object containing `accountIdentification`, `countryCode`, and `accountType`.
3. Check the response `problems` array for validation issues (wrong IBAN format, unsupported country, etc.).
4. If problems exist, correct the data and update: `PATCH /transferInstruments/{id}`.
5. Optionally upload a bank statement: `POST /documents` with `type: "bankStatement"` and `owner` pointing to the transfer instrument ID.

### Complete PCI Compliance

1. Check if signing is required: `POST /legalEntities/{id}/pciQuestionnaires/signingRequired`, optionally passing `additionalSalesChannels`.
2. If `signingRequired` is true, generate PCI templates: `POST /legalEntities/{id}/pciQuestionnaires/generatePciTemplates` with the desired `language`.
3. Note the `pciTemplateReferences` in the response -- these identify the templates to sign.
4. Sign the templates: `POST /legalEntities/{id}/pciQuestionnaires/signPciTemplates` with the `pciTemplateReferences` array and `signedBy` (name of the signer).
5. Verify completion: `GET /legalEntities/{id}/pciQuestionnaires` to confirm questionnaires are on file.

### Generate a Hosted Onboarding Link

1. Ensure the legal entity exists: `GET /legalEntities/{id}`.
2. Optionally select a theme: `GET /themes` to list available themes, note the desired `themeId`.
3. Generate the link: `POST /legalEntities/{id}/onboardingLinks` with `redirectUrl` (where the user returns after onboarding), optional `locale` for language, optional `themeId`, and any `settings` overrides (e.g., `acceptedCountries`, `instantBankVerification`).
4. Use the returned `url` to redirect the merchant to the hosted onboarding page.
5. After onboarding completes, confirm data review: `POST /legalEntities/{id}/confirmDataReview`.

### Update Entity Details and Trigger Re-verification

1. Retrieve current entity state: `GET /legalEntities/{id}`.
2. Update the entity: `PATCH /legalEntities/{id}` with the changed fields. Include the `x-requested-verification-code` header if you need to trigger re-verification of already-verified data.
3. Check verification errors: `POST /legalEntities/{id}/checkVerificationErrors` to see if the update introduced new issues.
4. Upload any newly required documents flagged in the `problems` array: `POST /documents`.
5. If needed, request a periodic review: `POST /legalEntities/{id}/requestPeriodicReview` (returns 204 on success).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
