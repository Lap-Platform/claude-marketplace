---
name: adyen-data-protection-api
description: "Adyen Data Protection API skill. Use when working with Adyen Data Protection for requestSubjectErasure. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Adyen Data Protection API
API version: 1

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://ca-test.adyen.com/ca/services/DataProtectionService/v1

## Setup
1. Set Authorization header with your Bearer token
3. POST /requestSubjectErasure -- create first requestSubjectErasure

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### requestSubjectErasure
| Method | Path | Description |
|--------|------|-------------|
| POST | /requestSubjectErasure | Submit a Subject Erasure Request. |

## Enhanced Skill Content
## Question Mapping

- "How do I delete a customer's personal data?" -> POST /requestSubjectErasure
- "How do I submit a GDPR erasure request?" -> POST /requestSubjectErasure
- "How do I erase data for a specific payment reference?" -> POST /requestSubjectErasure
- "Can I force-delete shopper data even if there are pending transactions?" -> POST /requestSubjectErasure (with forceErasure: true)
- "How do I handle a data subject access erasure request for a specific merchant account?" -> POST /requestSubjectErasure
- "What happens if I request erasure without specifying a PSP reference?" -> POST /requestSubjectErasure (pspReference is optional)
- "How do I comply with right-to-be-forgotten requests through Adyen?" -> POST /requestSubjectErasure
- "Can I erase data across multiple merchant accounts?" -> POST /requestSubjectErasure (call once per merchantAccount)
- "What authentication do I need for data protection requests?" -> Use X-API-Key header or Basic auth
- "How do I verify an erasure request was processed successfully?" -> POST /requestSubjectErasure, check result field in 200 response
- "What if an erasure request fails validation?" -> POST /requestSubjectErasure returns 422 for unprocessable requests
- "How do I retry a failed erasure request?" -> POST /requestSubjectErasure with same parameters

## Response Tips

- **200 Success**: Response contains a single `result` field (string) indicating erasure outcome -- check this value to confirm processing status rather than assuming success from the status code alone.
- **400 Bad Request**: Malformed request body; verify JSON structure and field types (forceErasure must be boolean, not string).
- **401 Unauthorized**: API key missing or invalid; confirm X-API-Key header or Basic auth credentials are set correctly.
- **403 Forbidden**: API key lacks Data Protection permissions; check role assignments in the Adyen Customer Area.
- **422 Unprocessable Entity**: Valid JSON but business logic rejection -- typically the pspReference does not exist or the merchant account is not eligible for erasure.
- **500 Internal Server Error**: Retry with exponential backoff; if persistent, escalate to Adyen support.

## Anomaly Flags

- **forceErasure used**: Surface a warning when `forceErasure: true` is set, as this bypasses safety checks and may erase data tied to open disputes or chargebacks.
- **Repeated 422 responses**: Flag if multiple erasure requests return 422 -- may indicate incorrect merchant account configuration or invalid PSP references being submitted systematically.
- **401/403 clusters**: Alert if auth errors spike, as this may signal a rotated or revoked API key.
- **Missing merchantAccount**: Warn if merchantAccount is omitted, as the request may not target the intended account scope.
- **500 errors**: Proactively surface any 500 responses -- data protection operations are compliance-sensitive and failures should not go unnoticed.
- **No result confirmation**: Flag if the `result` field in a 200 response contains an unexpected or empty value, as the erasure may not have completed.

## Playbook

### 1. Submit a Standard GDPR Erasure Request

1. Identify the `pspReference` for the shopper whose data should be erased.
2. Determine the correct `merchantAccount` identifier.
3. Call `POST /requestSubjectErasure` with `{ merchantAccount, pspReference }`.
4. Check the response status is 200 and read the `result` field.
5. Log the result for compliance audit trail.

### 2. Force-Erase Data with Pending Transactions

1. Confirm with the data controller that forced erasure is authorized despite open transactions.
2. Call `POST /requestSubjectErasure` with `{ merchantAccount, pspReference, forceErasure: true }`.
3. Verify the 200 response and `result` value.
4. Document the forced erasure decision and outcome for regulatory records.

### 3. Bulk Erasure Across Multiple Merchant Accounts

1. Collect all merchant account identifiers and associated PSP references for the data subject.
2. For each merchant account, call `POST /requestSubjectErasure` with the corresponding `{ merchantAccount, pspReference }`.
3. Track each response -- log successes (200) and failures (422/500) separately.
4. Retry any failed requests after investigating the error.
5. Confirm all accounts processed before marking the erasure request as complete.

### 4. Troubleshoot a Rejected Erasure Request

1. Attempt `POST /requestSubjectErasure` with the target parameters.
2. If 422 is returned, verify the `pspReference` exists in the specified `merchantAccount`.
3. If 403, check that the API key has the DataProtection role in Adyen Customer Area.
4. If the PSP reference is valid but erasure is blocked, retry with `forceErasure: true` (after authorization).
5. If 500, wait 30 seconds and retry; escalate to Adyen support if the error persists after 3 attempts.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
