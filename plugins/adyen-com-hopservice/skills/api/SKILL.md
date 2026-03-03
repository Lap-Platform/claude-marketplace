---
name: hosted-onboarding-api
description: "Hosted onboarding API skill. Use when working with Hosted onboarding for getOnboardingUrl, getPciQuestionnaireUrl. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Hosted onboarding API
API version: 6

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://cal-test.adyen.com/cal/services/Hop/v6

## Setup
1. Set Authorization header with your Bearer token
3. POST /getOnboardingUrl -- create first getOnboardingUrl

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### getOnboardingUrl
| Method | Path | Description |
|--------|------|-------------|
| POST | /getOnboardingUrl | Get a link to a Adyen-hosted onboarding page |

### getPciQuestionnaireUrl
| Method | Path | Description |
|--------|------|-------------|
| POST | /getPciQuestionnaireUrl | Get a link to a PCI compliance questionnaire |

## Enhanced Skill Content
## Question Mapping

- "How do I get an onboarding URL for an account holder?" -> POST /getOnboardingUrl
- "How do I generate a PCI questionnaire link?" -> POST /getPciQuestionnaireUrl
- "How do I onboard a sub-merchant and collect their bank details?" -> POST /getOnboardingUrl (set collectInformation.bankDetails: true)
- "How do I let an account holder edit their previously submitted details?" -> POST /getOnboardingUrl (set editMode: true)
- "How do I collect shareholder information during onboarding?" -> POST /getOnboardingUrl (set collectInformation.shareholderDetails: true)
- "How do I skip the welcome page in the onboarding flow?" -> POST /getOnboardingUrl (set showPages.welcomePage: false)
- "How do I redirect the user back to my platform after onboarding?" -> POST /getOnboardingUrl (set returnUrl)
- "How do I localize the onboarding page to a specific language?" -> POST /getOnboardingUrl (set shopperLocale)
- "How do I collect business and legal arrangement details together?" -> POST /getOnboardingUrl (set collectInformation.businessDetails and legalArrangementDetails: true)
- "How do I show only the bank verification page during onboarding?" -> POST /getOnboardingUrl (set showPages with only bankVerificationPage: true)
- "How do I handle mobile OAuth callbacks during onboarding?" -> POST /getOnboardingUrl (set mobileOAuthCallbackUrl)
- "How do I brand the onboarding page with my platform name?" -> POST /getOnboardingUrl (set platformName)
- "How do I get a PCI questionnaire link that returns to a custom URL?" -> POST /getPciQuestionnaireUrl (set returnUrl)

## Response Tips

- **Onboarding/PCI responses**: Always check `resultCode` first -- "Success" means `redirectUrl` is ready to use. If `invalidFields` is non-empty, inspect each map entry for field-level validation errors before redirecting.
- **Error responses (400/422)**: Contain details about malformed requests or unprocessable entities -- parse the error body for `errorCode` and `message` fields to diagnose issues.
- **Auth errors (401/403)**: Indicate missing, invalid, or insufficiently scoped API key -- verify the `X-API-Key` header value and associated permissions.

## Anomaly Flags

- **Non-empty `invalidFields` on 200**: The call succeeded but some submitted data failed validation -- surface these to the user immediately as they may block onboarding completion.
- **`resultCode` != "Success"**: Even on a 200 response, a non-success result code signals a problem -- flag it and include the raw value.
- **422 Unprocessable Entity**: Likely means the `accountHolderCode` does not exist or is in an invalid state -- proactively suggest verifying the account holder exists in the Account API.
- **500 Internal Server Error**: Adyen-side failure -- recommend retry with exponential backoff and flag for manual review if persistent.
- **Missing `redirectUrl` in response**: If the response succeeds but `redirectUrl` is absent or empty, surface this as an anomaly -- the onboarding flow cannot proceed.

## Playbook

### 1. Generate a Full Onboarding Link for a New Sub-Merchant

1. Ensure the account holder exists (created via the Adyen Account API).
2. Call `POST /getOnboardingUrl` with `accountHolderCode` and set `collectInformation` to include `bankDetails`, `businessDetails`, `individualDetails`, and `shareholderDetails` as needed.
3. Set `returnUrl` to your platform's post-onboarding callback page.
4. Optionally set `platformName` and `shopperLocale` for branding and localization.
5. Check `resultCode` is "Success" and `invalidFields` is empty.
6. Redirect the user to `redirectUrl`.

### 2. Send an Account Holder to the PCI Questionnaire

1. Confirm the account holder's `accountHolderCode`.
2. Call `POST /getPciQuestionnaireUrl` with `accountHolderCode` and optionally `returnUrl`.
3. Verify `resultCode` is "Success".
4. Redirect the account holder to the returned `redirectUrl`.
5. Handle the callback at `returnUrl` to confirm questionnaire completion.

### 3. Let an Existing Account Holder Update Their Details

1. Call `POST /getOnboardingUrl` with the existing `accountHolderCode`.
2. Set `editMode: true` to allow modification of previously submitted data.
3. Use `showPages` to control which pages are visible (e.g., only `bankDetailsSummaryPage` and `individualDetailsSummaryPage`).
4. Set `returnUrl` to capture the result after editing.
5. Redirect the user to `redirectUrl`.

### 4. Collect Only PCI and Bank Details in a Targeted Flow

1. Call `POST /getOnboardingUrl` with `accountHolderCode`.
2. Set `collectInformation.pciQuestionnaire: true` and `collectInformation.bankDetails: true`; leave other fields false or omitted.
3. Use `showPages` to hide irrelevant pages (e.g., set `welcomePage: false`, `businessDetailsSummaryPage: false`).
4. Set `returnUrl` for post-completion redirect.
5. Check response for `invalidFields` and redirect to `redirectUrl`.

### 5. Handle Validation Errors and Retry

1. Call `POST /getOnboardingUrl` or `POST /getPciQuestionnaireUrl`.
2. If the response returns 200 but `invalidFields` is non-empty, iterate over each entry to identify the problematic fields.
3. Correct the input data based on field-level error messages.
4. Retry the call with corrected parameters.
5. If a 422 is returned, verify the `accountHolderCode` exists and is in a valid lifecycle state before retrying.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
