---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# ApplicationInsightsManagementClient
API version: 2017-10-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
3. POST /subscriptions/{subscriptionId}/providers/microsoft.insights/migrateToNewPricingModel -- create first migrateToNewPricingModel

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /subscriptions/{subscriptionId}/providers/microsoft.insights/migrateToNewPricingModel | Enterprise Agreement Customer opted to use new pricing model. |
| POST | /subscriptions/{subscriptionId}/providers/microsoft.insights/rollbackToLegacyPricingModel | Enterprise Agreement Customer roll back to use legacy pricing model. |
| POST | /subscriptions/{subscriptionId}/providers/microsoft.insights/listMigrationdate | list date to migrate to new pricing model. |

## Enhanced Skill Content
## Question Mapping

- "How do I migrate to the new pricing model for Application Insights?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/migrateToNewPricingModel
- "How do I switch my subscription to the new Application Insights pricing?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/migrateToNewPricingModel
- "Can I roll back to the legacy pricing model?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/rollbackToLegacyPricingModel
- "How do I undo the pricing model migration?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/rollbackToLegacyPricingModel
- "How do I revert to the old Application Insights pricing?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/rollbackToLegacyPricingModel
- "When is my subscription scheduled to migrate?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/listMigrationdate
- "What is the migration date for my Application Insights pricing change?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/listMigrationdate
- "How do I check if my subscription has already migrated?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/listMigrationdate
- "Can I check the pricing migration status before deciding to roll back?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/listMigrationdate
- "What happens if I migrate and then want to go back to legacy pricing?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/rollbackToLegacyPricingModel
- "How do I confirm the migration completed successfully?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/listMigrationdate
- "Which subscription ID do I need for the pricing migration endpoints?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/listMigrationdate

## Response Tips

- **Migration and rollback endpoints (204):** A 204 No Content response means the operation succeeded -- there is no response body. Any non-204 status indicates failure; check the error object for `code` and `message` fields following Azure's standard error envelope (`{ "error": { "code": "...", "message": "..." } }`).
- **Migration date endpoint (200):** Returns a JSON body with migration date details. Parse the date fields carefully as they follow ISO 8601 format. A `null` or absent date may indicate the subscription has not yet been scheduled for migration.
- **Authentication errors (401/403):** Ensure the OAuth2 bearer token has the correct scope for the subscription. A 403 typically means the token lacks the `Microsoft.Insights` resource provider permissions.
- **Not found (404):** Usually means the `subscriptionId` is invalid or the subscription is not enrolled in Application Insights.

## Anomaly Flags

- **Double migration attempt:** If a user calls `migrateToNewPricingModel` on a subscription that has already migrated, surface the risk and suggest checking migration date first.
- **Rollback after extended period:** If the migration date is far in the past and the user requests a rollback, warn that data or billing differences may have accumulated.
- **Non-204 on migration/rollback:** Any response other than 204 is unexpected -- surface the full error body immediately, as these operations are not idempotent in their side effects.
- **Subscription scope mismatch:** If the user is working with multiple subscriptions, flag when the `subscriptionId` differs between calls in the same workflow to prevent accidental cross-subscription changes.
- **Deprecation risk:** This API version (2017-10-01) is old. Proactively note that Azure may deprecate legacy pricing migration endpoints and recommend checking for newer API versions.

## Playbook

### 1. Migrate a subscription to the new pricing model

1. Authenticate with OAuth2 and obtain a bearer token scoped to the target subscription.
2. Call `POST /subscriptions/{subscriptionId}/providers/microsoft.insights/listMigrationdate` to check current migration status and scheduled date.
3. Review the response -- confirm the subscription has not already migrated.
4. Call `POST /subscriptions/{subscriptionId}/providers/microsoft.insights/migrateToNewPricingModel`.
5. Verify the response is 204 No Content, confirming successful migration.
6. Optionally call `listMigrationdate` again to confirm the updated status.

### 2. Roll back to legacy pricing after a migration

1. Call `POST /subscriptions/{subscriptionId}/providers/microsoft.insights/listMigrationdate` to confirm the subscription is currently on the new pricing model.
2. Call `POST /subscriptions/{subscriptionId}/providers/microsoft.insights/rollbackToLegacyPricingModel`.
3. Verify the response is 204 No Content.
4. Call `listMigrationdate` once more to confirm the rollback took effect.

### 3. Audit migration status across multiple subscriptions

1. Gather all relevant `subscriptionId` values from your Azure account.
2. For each subscription, call `POST /subscriptions/{subscriptionId}/providers/microsoft.insights/listMigrationdate`.
3. Collect and compare the migration dates and statuses.
4. Identify subscriptions that are still on legacy pricing versus those already migrated.
5. Decide per-subscription whether to migrate, roll back, or leave as-is.

### 4. Safe migration with rollback contingency

1. Call `listMigrationdate` to record the pre-migration state.
2. Call `migrateToNewPricingModel` and confirm 204.
3. Monitor Application Insights billing and behavior over a validation period.
4. If issues arise, call `rollbackToLegacyPricingModel` and confirm 204.
5. Call `listMigrationdate` to verify the subscription is back on legacy pricing.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
