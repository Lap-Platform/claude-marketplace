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

- "How do I list all saved payment methods for a shopper?" -> POST /listRecurringDetails
- "How do I delete a stored payment method?" -> POST /disable
- "How do I disable all recurring details for a shopper?" -> POST /disable (omit recurringDetailReference)
- "How do I create a permit for a recurring payment?" -> POST /createPermit
- "How do I revoke a specific permit?" -> POST /disablePermit
- "How do I notify a shopper about an upcoming recurring charge?" -> POST /notifyShopper
- "How do I update expired card details automatically?" -> POST /scheduleAccountUpdater
- "How do I check what contract types a shopper has?" -> POST /listRecurringDetails (inspect recurring.contract in response)
- "How do I disable a specific recurring detail by reference?" -> POST /disable (include recurringDetailReference)
- "How do I set up a permit with date restrictions?" -> POST /createPermit (use restriction and validTillDate in permits)
- "How do I find the last known email for a shopper?" -> POST /listRecurringDetails (read lastKnownShopperEmail from response)
- "How do I send a billing notification with a custom display reference?" -> POST /notifyShopper (set displayedReference)
- "How do I schedule a card update with full card details instead of a stored reference?" -> POST /scheduleAccountUpdater (pass card object instead of selectedRecurringDetailReference)

## Response Tips

- **Listing (listRecurringDetails):** Response `details` is an array of mixed-type objects; each entry's shape varies by payment method type (card, SEPA, etc.). Always check `creationDate` for staleness.
- **Disable/DisablePermit:** `disable` returns a simple `{response: str}` where `"[detail-successfully-disabled]"` is the success value. `disablePermit` returns a `status` field instead.
- **Permits (createPermit):** `permitResultList` is an array of maps -- iterate it to check individual permit outcomes even if pspReference indicates overall acceptance.
- **Notifications (notifyShopper):** Check `resultCode` for success/failure; `shopperNotificationReference` is your correlation ID for tracking notification delivery.
- **Account Updater (scheduleAccountUpdater):** `result` indicates scheduling status, not the update outcome itself -- actual card updates arrive asynchronously via webhooks.
- **Errors (all endpoints):** 422 indicates validation failure with detailed field-level messages. 401/403 distinguish between missing credentials and insufficient permissions.

## Anomaly Flags

- **422 validation errors on disable:** May indicate the recurringDetailReference is already disabled or does not exist -- surface this explicitly rather than retrying.
- **Empty `details` array from listRecurringDetails:** Shopper may have no stored methods or the contract filter may be too restrictive -- flag if the shopper was expected to have saved methods.
- **`resultCode` other than success on notifyShopper:** Surface immediately; failed notifications may mean the shopper won't be aware of an upcoming charge, creating compliance risk.
- **`result` value on scheduleAccountUpdater:** If not a clear success indicator, flag that the card update was not scheduled and manual intervention may be needed.
- **401/403 on any endpoint:** API key may be expired or lack the required recurring role -- surface with a recommendation to check Adyen Customer Area permissions.
- **Permit `validTillDate` in the past:** If creating permits with expired dates, flag before sending the request to avoid a guaranteed 422.
- **Missing `merchantAccount` in any request:** Common field required by all endpoints -- surface early since every call will fail without it.

## Playbook

### 1. Remove a Specific Saved Payment Method

1. Call `POST /listRecurringDetails` with `shopperReference` to retrieve all stored methods
2. Identify the target entry in the `details` array and note its `recurringDetailReference`
3. Call `POST /disable` with `shopperReference` and the `recurringDetailReference`
4. Confirm the response contains `"[detail-successfully-disabled]"`

### 2. Set Up a Recurring Permit with Restrictions

1. Call `POST /listRecurringDetails` with `shopperReference` to get the `recurringDetailReference` for the stored payment method
2. Call `POST /createPermit` with the `recurringDetailReference`, `shopperReference`, and a `permits` array specifying `restriction`, `validTillDate`, and `partnerId`
3. Check `permitResultList` to confirm each permit was created successfully
4. Store the returned `pspReference` for future reference or revocation

### 3. Notify Shopper Before a Recurring Charge

1. Call `POST /listRecurringDetails` to verify the shopper still has an active stored payment method
2. Call `POST /notifyShopper` with `shopperReference`, `amount` (currency + value in minor units), and `reference`
3. Optionally set `billingDate` and `displayedReference` for clearer shopper communication
4. Check `resultCode` in the response to confirm the notification was accepted
5. Log `shopperNotificationReference` for tracking and compliance auditing

### 4. Refresh Expired Card Details via Account Updater

1. Call `POST /listRecurringDetails` to find stored cards with upcoming or past expiry dates
2. For each expired card, call `POST /scheduleAccountUpdater` with either `selectedRecurringDetailReference` (preferred) or full `card` details
3. Check the `result` field to confirm the update was scheduled
4. Monitor Adyen webhooks for the actual card update result (new expiry, new number, or card closed)

### 5. Fully Remove a Shopper's Recurring Profile

1. Call `POST /listRecurringDetails` with `shopperReference` to enumerate all stored methods
2. For each entry in `details`, call `POST /disable` with the corresponding `recurringDetailReference`
3. Alternatively, call `POST /disable` with only `shopperReference` (no `recurringDetailReference`) to disable all at once
4. If any permits exist, call `POST /disablePermit` with each permit `token`
5. Verify by calling `POST /listRecurringDetails` again -- `details` should be empty


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
