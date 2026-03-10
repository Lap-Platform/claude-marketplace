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

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Create a migrateToNewPricingModel?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/migrateToNewPricingModel
- "Create a rollbackToLegacyPricingModel?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/rollbackToLegacyPricingModel
- "Create a listMigrationdate?" -> POST /subscriptions/{subscriptionId}/providers/microsoft.insights/listMigrationdate
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
