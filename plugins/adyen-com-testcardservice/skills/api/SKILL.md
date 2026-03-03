---
name: adyen-test-cards-api
description: "Adyen Test Cards API skill. Use when working with Adyen Test Cards for createTestCardRanges. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Adyen Test Cards API
API version: 1

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://pal-test.adyen.com/pal/services/TestCard/v1

## Setup
1. Set Authorization header with your Bearer token
3. POST /createTestCardRanges -- create first createTestCardRanges

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### createTestCardRanges
| Method | Path | Description |
|--------|------|-------------|
| POST | /createTestCardRanges | Creates one or more test card ranges. |

## Enhanced Skill Content
## Question Mapping

- "How do I create test card ranges for an account?" -> POST /createTestCardRanges
- "How do I set up test cards for a merchant account?" -> POST /createTestCardRanges
- "Can I create multiple test card ranges at once?" -> POST /createTestCardRanges (pass multiple items in `testCardRanges` array)
- "How do I provision test cards for a specific account type?" -> POST /createTestCardRanges (set `accountTypeCode`)
- "What fields are required to create test card ranges?" -> POST /createTestCardRanges (requires `accountCode`, `accountTypeCode`, `testCardRanges`)
- "How do I check if my test card range creation succeeded?" -> POST /createTestCardRanges (inspect `rangeCreationResults` in response)
- "How do I add test cards for a Company account?" -> POST /createTestCardRanges with `accountTypeCode: "Company"`
- "How do I add test cards for a MerchantAccount?" -> POST /createTestCardRanges with `accountTypeCode: "MerchantAccount"`
- "What happens if I submit an invalid test card range?" -> POST /createTestCardRanges (returns 422 for validation errors)
- "How do I authenticate with the Test Cards API?" -> Use `X-API-Key` header or HTTP Basic auth
- "Can I create test card ranges in bulk?" -> POST /createTestCardRanges (batch via `testCardRanges` array)
- "What account types support test card ranges?" -> POST /createTestCardRanges (determined by `accountTypeCode` values accepted)

## Response Tips

- **createTestCardRanges**: Response contains `rangeCreationResults` array -- each element maps to an input range with its own success/failure status. Always iterate the full array; partial failures are possible where some ranges succeed and others fail within a single request.
- **Error responses (400/422)**: Typically include field-level validation details. A 422 means the request was well-formed but semantically invalid (e.g., overlapping ranges, invalid card numbers).
- **Auth errors (401/403)**: A 401 means missing or invalid API key; a 403 means the key lacks permission for the target account. Verify `accountCode` matches your credential scope.

## Anomaly Flags

- **Partial failures in batch**: If `rangeCreationResults` contains a mix of success and failure statuses, surface which ranges failed and why -- callers often assume all-or-nothing behavior.
- **403 on valid credentials**: May indicate the API key does not have access to the specified `accountCode` -- flag as a permission/scope issue rather than a credential issue.
- **422 validation errors**: Surface the specific field or range that failed validation; these often indicate overlapping or duplicate card ranges.
- **500 errors**: Adyen platform issue -- recommend retry with exponential backoff. Surface if repeated 500s occur, as this may indicate a service outage.
- **Empty rangeCreationResults**: If the response returns 200 but `rangeCreationResults` is empty, flag as unexpected -- it may indicate the `testCardRanges` input was silently ignored.

## Playbook

### 1. Create Test Card Ranges for a Merchant Account

1. Obtain your test API key from the Adyen Customer Area (Test environment).
2. Identify the `accountCode` for the target merchant account.
3. Call `POST /createTestCardRanges` with `accountCode`, `accountTypeCode: "MerchantAccount"`, and your desired `testCardRanges` array.
4. Inspect each entry in `rangeCreationResults` to confirm all ranges were created successfully.
5. If any range failed, check the error detail and correct the input (e.g., adjust range boundaries to avoid overlaps).

### 2. Bulk-Provision Test Cards Across Multiple Ranges

1. Prepare a `testCardRanges` array with all desired ranges (card number prefixes, lengths, etc.).
2. Send a single `POST /createTestCardRanges` request with the full batch.
3. Parse `rangeCreationResults` and separate successes from failures.
4. For any failed ranges, fix validation issues and resubmit only the failed ranges in a follow-up request.

### 3. Troubleshoot Failed Test Card Range Creation

1. Check the HTTP status code: 400 (malformed request), 422 (validation failure), 401/403 (auth issue).
2. For 422 errors, read the response body for field-level details -- common causes are overlapping ranges or invalid card number formats.
3. For 403 errors, verify that your API key has access to the `accountCode` specified.
4. For 500 errors, wait and retry. If persistent, check Adyen's status page for outages.
5. Confirm `accountTypeCode` matches the actual account type in the Adyen platform.

### 4. Validate API Credentials Before Provisioning

1. Set the `X-API-Key` header with your test environment API key (or use Basic auth).
2. Send a minimal `POST /createTestCardRanges` request with a known-valid `accountCode` and a single test range.
3. A 200 response confirms credentials and permissions are correct.
4. A 401 indicates an invalid key; a 403 indicates insufficient permissions for that account.
5. Once validated, proceed with full provisioning requests.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
