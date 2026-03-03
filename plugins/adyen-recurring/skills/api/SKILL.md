---
name: adyen-recurring-api
description: "Adyen Recurring API skill. Use when working with Adyen Recurring for createPermit, disable, disablePermit. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Adyen Recurring API
API version: 68

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://paltokenization-test.adyen.com/paltokenization/servlet/Recurring/v68

## Setup
1. Set Authorization header with your Bearer token
3. POST /createPermit -- create first createPermit

## Endpoints

6 endpoints across 6 groups. See references/api-spec.lap for full details.

### createPermit
| Method | Path | Description |
|--------|------|-------------|
| POST | /createPermit | Create new permits linked to a recurring contract. |

### disable
| Method | Path | Description |
|--------|------|-------------|
| POST | /disable | Disable stored payment details |

### disablePermit
| Method | Path | Description |
|--------|------|-------------|
| POST | /disablePermit | Disable an existing permit. |

### listRecurringDetails
| Method | Path | Description |
|--------|------|-------------|
| POST | /listRecurringDetails | Get stored payment details |

### notifyShopper
| Method | Path | Description |
|--------|------|-------------|
| POST | /notifyShopper | Ask issuer to notify the shopper |

### scheduleAccountUpdater
| Method | Path | Description |
|--------|------|-------------|
| POST | /scheduleAccountUpdater | Schedule running the Account Updater |

## Enhanced Skill Content
## Question Mapping

- "How do I store a recurring payment method for a shopper?" -> POST /listRecurringDetails (retrieve first), then POST /createPermit
- "How do I list all saved payment methods for a customer?" -> POST /listRecurringDetails
- "How do I delete a stored payment method?" -> POST /disable
- "How do I revoke a specific recurring detail by reference?" -> POST /disable (with recurringDetailReference)
- "How do I disable all recurring details for a shopper at once?" -> POST /disable (shopperReference only, omit recurringDetailReference)
- "How do I create a permit for a partner to charge a shopper?" -> POST /createPermit
- "How do I cancel an active permit?" -> POST /disablePermit
- "How do I notify a shopper about an upcoming recurring charge?" -> POST /notifyShopper
- "How do I update expired card details automatically?" -> POST /scheduleAccountUpdater
- "How do I check if a shopper has any active recurring contracts?" -> POST /listRecurringDetails (inspect returned details array)
- "How do I restrict a permit to a single use?" -> POST /createPermit (set restriction.singleUse: true)
- "How do I set a maximum amount on a recurring permit?" -> POST /createPermit (set restriction.maxAmount)
- "How do I send a pre-debit notification with the billing amount?" -> POST /notifyShopper (with amount, billingDate, billingSequenceNumber)
- "How do I schedule a card update for a specific card number?" -> POST /scheduleAccountUpdater (with card object)

## Response Tips

- **createPermit / disablePermit / scheduleAccountUpdater**: Key on `pspReference` -- this is your transaction tracking ID; store it for reconciliation and support inquiries.
- **disable**: Returns a simple `{response: str}` -- expect `"[detail-successfully-disabled]"` on success; any other value indicates partial or failed disablement.
- **listRecurringDetails**: The `details` array contains nested maps with card info, contract types, and creation dates; iterate and filter by `recurringDetailReference` or `variant` (e.g., `"visa"`, `"sepadirectdebit"`).
- **notifyShopper**: Check `resultCode` for success/failure; `displayedReference` and `shopperNotificationReference` are useful for audit trails.
- **All endpoints**: Error responses (400-500) return a JSON body with `status`, `errorCode`, `message`, and `errorType` -- always parse these for actionable diagnostics.

## Anomaly Flags

- **401 responses**: API key is invalid or expired -- surface immediately, all subsequent calls will also fail.
- **422 responses**: Validation error, often caused by malformed `shopperReference` or missing `merchantAccount` -- flag the specific field from the error body.
- **Empty `details` array** from listRecurringDetails: Shopper has no stored methods; flag before attempting disable or permit creation.
- **`result` field in scheduleAccountUpdater** returning anything other than success: Card update was not scheduled, likely due to unsupported card network or issuer.
- **`resultCode` in notifyShopper** not indicating success: Notification was not delivered; the shopper may not receive the pre-debit notice (compliance risk).
- **Permit with past `validTillDate`**: If createPermit is called with an expiry in the past, flag it -- the permit will be immediately invalid.
- **500 errors**: Adyen platform issue; suggest retry with exponential backoff, and flag if it persists across 3+ attempts.

## Playbook

### 1. Set Up a New Recurring Payment Permit

1. Call POST /listRecurringDetails with `shopperReference` to confirm the shopper has stored payment methods.
2. Pick the desired `recurringDetailReference` from the returned `details` array.
3. Call POST /createPermit with the `recurringDetailReference`, `shopperReference`, desired `permits` array (including partner ID, restrictions, and validity date).
4. Store the returned `pspReference` and any `resultKey` values from `permitResultList` for future reference.

### 2. Disable a Specific Stored Payment Method

1. Call POST /listRecurringDetails with `shopperReference` to get all stored methods.
2. Identify the target `recurringDetailReference` from the `details` array.
3. Call POST /disable with both `shopperReference` and `recurringDetailReference`.
4. Verify the response contains `"[detail-successfully-disabled]"`.

### 3. Send Pre-Debit Notification and Process Recurring Charge

1. Call POST /listRecurringDetails to confirm the shopper's stored method is still active.
2. Call POST /notifyShopper with the `shopperReference`, `amount` (currency + value in minor units), `reference`, and `billingDate`.
3. Check `resultCode` for successful delivery.
4. Store `shopperNotificationReference` for compliance audit trail.
5. Proceed with the actual payment via the Adyen Payments API (separate service).

### 4. Bulk Disable All Recurring Details for a Shopper

1. Call POST /disable with only `shopperReference` (omit `recurringDetailReference` and `contract`).
2. This disables all stored payment methods and contracts for that shopper.
3. Verify the response confirms disablement.
4. Optionally call POST /listRecurringDetails to confirm the `details` array is now empty.

### 5. Schedule Automatic Card Updates

1. Call POST /scheduleAccountUpdater with a unique `reference` and either a `shopperReference` + `selectedRecurringDetailReference` (for stored methods) or a `card` object (for raw card data).
2. Check the `result` field in the response for confirmation.
3. Store the `pspReference` for tracking the update status.
4. Card networks will asynchronously provide updated details -- monitor via Adyen webhooks (separate configuration).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
