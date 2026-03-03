---
name: credas-api
description: "Credas API skill. Use when working with Credas for api. Covers 37 endpoints."
version: 1.0.0
generator: lapsh
---

# Credas API
API version: v1

## Auth
ApiKey apikey in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /api/registrations/search -- verify access
3. POST /api/bank-accounts/verify -- create first verify

## Endpoints

37 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| POST | /api/bank-accounts/verify | Verifies bank account details. |
| POST | /api/companies | Searches for a company based on its Company Number and returns its details. |
| GET | /api/companies/{companyId} |  |
| POST | /api/credit-status/perform | Check includes identifying bankruptcy, insolvency, CCJ's or Company Directorship. |
| POST | /api/datachecks | Creates new data check against a specified registration. |
| GET | /api/images/selfie/{registrationId} | Retrieve the selfie image associated with a registration. |
| POST | /api/images/selfie | Add a selfie image to the registration. |
| GET | /api/images/liveness/{registrationId} | Retrieve the liveness action image (UAP) associated with a registration. |
| POST | /api/images/liveness | Add a liveness image (UAP) to the specified registration. |
| GET | /api/images/liveness-performed/{registrationId} | Retrieve the liveness performed image associated with a registration. |
| GET | /api/images/id-document/{registrationId} | Get all id document images associated with a registration. |
| POST | /api/images/id-document | Add an id document image to the specified registration. |
| GET | /api/images/scan-report-pdf/{scanId} | Returns a detailed report on the analysis that has taken place of a scanned document |
| POST | /api/property-register | Creates new property registry check against the registration. |
| GET | /api/property-register/{id} | Retrieves property registry check associated with the registration. |
| POST | /api/registrations/instant | Creates new registration record, adds an ID document and optional selfie image in one go. |
| POST | /api/registrations | Creates new registration. |
| GET | /api/registrations/{id}/check-submitted-id-documents | Checks if submitted documents are sufficient to complete registration. |
| GET | /api/registrations/referenceid/{referenceId}/summary | Finds registrations by the ReferenceId. |
| GET | /api/registrations/{id}/summary | Finds a registration by the Id. |
| GET | /api/registrations/regcode/{regCode}/summary | Finds a registration by the RegCode. |
| GET | /api/registrations/{id}/supported-id-documents | Get a list of supported id document for the specified registration id. |
| PUT | /api/registrations/{id}/status | Updates the status of the registration to one specified in the request. |
| GET | /api/registrations/{id}/pdf-export | Returns PDF export for a given registration. |
| GET | /api/registrations/{id}/pdf-export-sections | Returns a PDF report for a given registration containing specified sections |
| PUT | /api/registrations/{id}/override-check-status | Sets an override for a specific check on the registration. |
| POST | /api/registrations/{id}/resend-invitation | Resends any invitation for the specified registration. |
| GET | /api/registrations/{id}/settings | Gets registration settings or nothing if there are no settings associated with the registration. |
| PUT | /api/registrations/{id}/settings | Updates registration settings. |
| PUT | /api/registrations/{id}/contact-details | Updates a registration's contact details. |
| GET | /api/registrations/search | Gets paged registration list by search criteria or nothing if there are no matching fields. |
| GET | /api/registrations/{id}/pdf-settlement-status | Returns settlement status PDF (Share Code) for a given registration. |
| GET | /api/reg-types | Gets all available RegTypes. |
| POST | /api/report-view/by-referenceid | Retrieves secure links to registration details pages searching by the Reference Id. |
| POST | /api/report-view/by-registrationid | Retrieves secure link to registration details page searching by the Registration Id. |
| POST | /api/web-verifications/by-referenceid | Retrieves secure links to web verification pages searching by the Reference Id. |
| POST | /api/web-verifications/by-registrationid | Retrieves secure link to web verification page searching by the Registration Id. |

## Enhanced Skill Content
## Question Mapping

- "How do I verify a bank account?" -> POST /api/bank-accounts/verify
- "How do I look up a company by its ID?" -> GET /api/companies/{companyId}
- "How do I register a new company?" -> POST /api/companies
- "How do I run a credit check on someone?" -> POST /api/credit-status/perform
- "How do I create a new identity registration?" -> POST /api/registrations
- "How do I search for a registration by name or email?" -> GET /api/registrations/search
- "How do I get a summary of a registration?" -> GET /api/registrations/{id}/summary
- "How do I upload an ID document for verification?" -> POST /api/images/id-document
- "How do I check if liveness detection was performed?" -> GET /api/images/liveness-performed/{registrationId}
- "How do I export a registration as a PDF?" -> GET /api/registrations/{id}/pdf-export
- "How do I export only specific sections of a registration PDF?" -> GET /api/registrations/{id}/pdf-export-sections
- "How do I override the check status on a registration?" -> PUT /api/registrations/{id}/override-check-status
- "How do I resend an invitation to a registrant?" -> POST /api/registrations/{id}/resend-invitation
- "How do I update a registration's contact details?" -> PUT /api/registrations/{id}/contact-details
- "What registration types are available?" -> GET /api/reg-types

## Response Tips

- **Registrations:** Summaries can be fetched by internal ID, reference ID, or reg code -- all return the same structure. Use the lookup that matches the identifier you have on hand.
- **Search:** `GET /api/registrations/search` supports `pageNum` and `pageSize` for pagination. Always check if more pages exist by comparing result count to `pageSize`.
- **Images:** GET endpoints for selfie, liveness, and id-document return binary image data tied to a `registrationId`. A 403 means the registration exists but you lack access; a 404 (liveness-performed) means the check has not been run yet.
- **PDF exports:** `/pdf-export` returns the full report. `/pdf-export-sections` accepts boolean flags (Comments, StandardChecks, PepSanctionChecks, etc.) to include or exclude specific sections.
- **Errors:** All endpoints share a common error pattern -- 400 (bad input), 401 (missing or invalid API key), 402 (insufficient credits/billing issue), 403 (access denied to resource), 500 (server error). A 402 specifically signals a billing or quota problem.

## Anomaly Flags

- **402 Payment Required:** Surface immediately -- indicates the account has run out of credits or the billing plan does not cover this operation. The user needs to top up before retrying.
- **401 on previously working calls:** API key may have been rotated or revoked. Prompt the user to verify their `apikey` header value.
- **404 on registration lookups:** Could mean the ID/referenceId/regCode is wrong, or the registration was deleted. Confirm the identifier before retrying.
- **403 on image retrieval:** The registration exists but the caller lacks permission. This may indicate a multi-tenant access boundary issue.
- **Liveness not performed (404 on /liveness-performed):** The registrant has not completed the liveness step yet. Flag this when it blocks downstream workflows like PDF export or summary review.
- **Repeated 500 errors:** Likely a transient backend issue. Surface after two consecutive failures on the same endpoint and suggest waiting before retry.

## Playbook

### 1. Full Identity Verification (KYC Flow)

1. Create a registration: `POST /api/registrations` with the applicant's details.
2. Note the returned registration `id`.
3. Upload a selfie: `POST /api/images/selfie` with the registration ID.
4. Upload an ID document: `POST /api/images/id-document` with the registration ID.
5. Submit liveness check: `POST /api/images/liveness` with the registration ID.
6. Run a data check: `POST /api/datachecks` referencing the registration.
7. Retrieve the full summary: `GET /api/registrations/{id}/summary`.
8. Export the PDF report: `GET /api/registrations/{id}/pdf-export`.

### 2. Company Due Diligence with Credit Check

1. Register the company: `POST /api/companies` with the company number.
2. Retrieve full company details: `GET /api/companies/{companyId}`.
3. Run a credit status check: `POST /api/credit-status/perform` with the company reference.
4. Optionally verify a bank account: `POST /api/bank-accounts/verify`.
5. Review results and flag any 402 errors indicating billing limits.

### 3. Search and Review Existing Registrations

1. Search for registrations: `GET /api/registrations/search?forename=Jane&surname=Doe&pageSize=20`.
2. Pick the matching result and note its `id`.
3. Get the summary: `GET /api/registrations/{id}/summary`.
4. Check submitted documents: `GET /api/registrations/{id}/check-submitted-id-documents`.
5. If needed, export a sectioned PDF: `GET /api/registrations/{id}/pdf-export-sections?StandardChecks=true&PepSanctionChecks=true`.

### 4. Resend Invitation and Update Contact Details

1. Look up the registration summary by reference ID: `GET /api/registrations/referenceid/{referenceId}/summary`.
2. Update contact details if they have changed: `PUT /api/registrations/{id}/contact-details` with the corrected info.
3. Resend the invitation: `POST /api/registrations/{id}/resend-invitation`.
4. Confirm settings are correct: `GET /api/registrations/{id}/settings`.

### 5. Generate Report Views for External Stakeholders

1. Generate a report view by reference ID: `POST /api/report-view/by-referenceid` with the reference.
2. Alternatively, use the registration ID: `POST /api/report-view/by-registrationid`.
3. For web-based verification links, use `POST /api/web-verifications/by-referenceid` or `POST /api/web-verifications/by-registrationid`.
4. Share the resulting report or verification URL with the stakeholder.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
