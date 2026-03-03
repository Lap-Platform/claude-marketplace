---
name: beezup-merchant-api
description: "BeezUP Merchant API skill. Use when working with BeezUP Merchant for public, user, orders. Covers 249 endpoints."
version: 1.0.0
generator: lapsh
---

# BeezUP Merchant API
API version: 2.0

## Auth
ApiKey Ocp-Apim-Subscription-Key in header

## Base URL
https://api.beezup.com

## Setup
1. Set your API key in the appropriate header
2. GET /v2/public/channels/ -- verify access
3. POST /v2/public/security/login -- create first login

## Endpoints

249 endpoints across 3 groups. See references/api-spec.lap for full details.

### public
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/public/security/login | Login |
| POST | /v2/public/security/login/mfa | Login |
| POST | /v2/public/security/register | User Registration |
| POST | /v2/public/security/lostpassword | Lost password |
| GET | /v2/public/channels/ | Get public channel index |
| GET | /v2/public/channels/{countryIsoCode} | The channel list for one country |
| GET | /v2/public/lov/ | Get all list names |
| GET | /v2/public/lov/{listName} | Get the list of values related to this list name |

### user
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/user/lov/ | Get all list names |
| GET | /v2/user/lov/{listName} | Get the list of values related to this list name |
| GET | /v2/user/customer/ | The index of all operations and LOV |
| GET | /v2/user/customer/account | Get user account information |
| POST | /v2/user/customer/account/resendEmailActivation | Resend email activation |
| POST | /v2/user/customer/account/activate | Activate the user account |
| PUT | /v2/user/customer/account/personalInfo | Save user personal information |
| PUT | /v2/user/customer/account/companyInfo | Change company information |
| GET | /v2/user/customer/account/profilePictureInfo | Get profile picture information |
| PUT | /v2/user/customer/account/profilePictureInfo | Change user picture information |
| GET | /v2/user/customer/account/creditCardInfo | Get credit card information |
| PUT | /v2/user/customer/account/creditCardInfo | Save user credit card info |
| POST | /v2/user/customer/account/changeEmail | Change user email |
| POST | /v2/user/customer/account/changePassword | Change user password |
| POST | /v2/user/customer/security/logout | Log out the current user from go2 |
| GET | /v2/user/customer/zendeskToken | Zendesk token |
| GET | /v2/user/customer/stores | Get store list |
| POST | /v2/user/customer/stores | Create a new store |
| GET | /v2/user/customer/stores/{storeId} | Get store's information |
| PATCH | /v2/user/customer/stores/{storeId} | Update some store's information. |
| DELETE | /v2/user/customer/stores/{storeId} | Delete a store |
| GET | /v2/user/customer/stores/{storeId}/rights | Get store's rights |
| GET | /v2/user/customer/stores/{storeId}/alerts | Get store's alerts |
| POST | /v2/user/customer/stores/{storeId}/alerts | Save store alerts |
| GET | /v2/user/customer/stores/{storeId}/shares | Get shares related to this store |
| POST | /v2/user/customer/stores/{storeId}/shares | Share a store to another user |
| DELETE | /v2/user/customer/stores/{storeId}/shares/{userId} | Delete a share of a store to another user |
| GET | /v2/user/customer/friends/{userId} | Get friend information |
| GET | /v2/user/customer/billingPeriods | Get billing periods conditions |
| GET | /v2/user/customer/offers | Get all standard offers |
| POST | /v2/user/customer/offers | Get offer pricing |
| GET | /v2/user/customer/contracts | Get contract list |
| POST | /v2/user/customer/contracts | Create a new contract |
| POST | /v2/user/customer/contracts/current/disableAutoRenewal | Schedule termination of your current contract at the end of the commitment. |
| POST | /v2/user/customer/contracts/current/reenableAutoRenewal | Reactivate your terminated contract. |
| DELETE | /v2/user/customer/contracts/next | Delete your next contract |
| GET | /v2/user/customer/invoices | Get all your invoices |
| GET | /v2/user/catalogs/ | Get the index of the catalog API |
| GET | /v2/user/catalogs/beezupColumns | Get the BeezUP columns |
| GET | /v2/user/catalogs/{storeId} | Get the index of the catalog API for this store |
| GET | /v2/user/catalogs/{storeId}/inputConfiguration | Get the last input configuration |
| GET | /v2/user/catalogs/{storeId}/catalogColumns | Get catalog column list |
| POST | /v2/user/catalogs/{storeId}/catalogColumns/{columnId}/rename | Change Catalog Column User Name |
| GET | /v2/user/catalogs/{storeId}/customColumns | Get custom column list |
| PUT | /v2/user/catalogs/{storeId}/customColumns/{columnId} | Create or replace a custom column |
| DELETE | /v2/user/catalogs/{storeId}/customColumns/{columnId} | Delete custom column |
| POST | /v2/user/catalogs/{storeId}/customColumns/{columnId}/rename | Change Custom Column User Name |
| GET | /v2/user/catalogs/{storeId}/customColumns/{columnId}/expression | Get the encrypted custom column expression |
| PUT | /v2/user/catalogs/{storeId}/customColumns/{columnId}/expression | Change custom column expression |
| POST | /v2/user/catalogs/{storeId}/customColumns/computeExpression | Compute the expression for this catalog. |
| GET | /v2/user/catalogs/{storeId}/categories | Get category list |
| POST | /v2/user/catalogs/{storeId}/products/list | Get product list |
| GET | /v2/user/catalogs/{storeId}/products/random | Get random product list |
| GET | /v2/user/catalogs/{storeId}/products/{productId} | Get product by ProductId |
| GET | /v2/user/catalogs/{storeId}/products | Get product by Sku |
| POST | /v2/user/catalogs/{storeId}/products/batches/{actionType} | Push product batches |
| GET | /v2/user/catalogs/{storeId}/importations/{batchId}/getReportUrl | Get Reporting By BatchId |
| GET | /v2/user/catalogs/{storeId}/beezUPColumns | Get the BeezUPColumns' Mapping of a Store |
| PATCH | /v2/user/catalogs/{storeId}/beezUPColumns | Patch the BeezUPColumns' Mapping of a Store. |
| PUT | /v2/user/catalogs/{storeId}/beezUPColumns | Replace the BeezUPColumns' Mapping of a Store. |
| PUT | /v2/user/catalogs/{storeId}/beezUPColumns/{beezUPColumnName} | Replace the BeezUPColumns' Mapping of a Store. |
| DELETE | /v2/user/catalogs/{storeId}/beezUPColumns/{beezUPColumnName} | Delete the BeezUPColumn' Mapping of a Store. |
| GET | /v2/user/catalogs/importations | Get the latest catalog importation reporting for all your stores |
| GET | /v2/user/catalogs/{storeId}/importations | Get the latest catalog importation reporting |
| POST | /v2/user/catalogs/{storeId}/importations/start | Start Manual Import |
| GET | /v2/user/catalogs/{storeId}/importations/{executionId} | Get the importation status |
| POST | /v2/user/catalogs/{storeId}/importations/{executionId}/cancel | Cancel importation |
| GET | /v2/user/catalogs/{storeId}/importations/{executionId}/technicalProgression | Get technical progression |
| POST | /v2/user/catalogs/{storeId}/importations/{executionId}/configureRemainingCatalogColumns | Configure remaining catalog columns |
| POST | /v2/user/catalogs/{storeId}/importations/{executionId}/commitColumns | Commit columns |
| POST | /v2/user/catalogs/{storeId}/importations/{executionId}/commit | Commit Importation |
| GET | /v2/user/catalogs/{storeId}/importations/{executionId}/productSamples/{productSampleIndex} | Get the product sample related to this importation with all columns (catalog and custom) |
| GET | /v2/user/catalogs/{storeId}/importations/{executionId}/productSamples/{productSampleIndex}/customColumns/{columnId} | Get product sample custom column value related to this importation. |
| GET | /v2/user/catalogs/{storeId}/importations/{executionId}/catalogColumns | Get detected catalog columns during this importation. |
| POST | /v2/user/catalogs/{storeId}/importations/{executionId}/catalogColumns/{columnId} | Configure catalog column |
| POST | /v2/user/catalogs/{storeId}/importations/{executionId}/catalogColumns/{columnId}/ignore | Ignore Column |
| POST | /v2/user/catalogs/{storeId}/importations/{executionId}/catalogColumns/{columnId}/reattend | Reattend Column |
| POST | /v2/user/catalogs/{storeId}/importations/{executionId}/catalogColumns/{columnId}/map | Map catalog column to a BeezUP column |
| POST | /v2/user/catalogs/{storeId}/importations/{executionId}/catalogColumns/{columnId}/unmap | Unmap catalog column |
| GET | /v2/user/catalogs/{storeId}/importations/{executionId}/customColumns | Get custom columns currently place in this importation |
| GET | /v2/user/catalogs/{storeId}/importations/{executionId}/customColumns/{columnId}/expression | Get the encrypted custom column expression in this importation |
| PUT | /v2/user/catalogs/{storeId}/importations/{executionId}/customColumns/{columnId} | Create or replace a custom column |
| DELETE | /v2/user/catalogs/{storeId}/importations/{executionId}/customColumns/{columnId} | Delete Custom Column |
| POST | /v2/user/catalogs/{storeId}/importations/{executionId}/customColumns/{columnId}/map | Map custom column to a BeezUP column |
| POST | /v2/user/catalogs/{storeId}/importations/{executionId}/customColumns/{columnId}/unmap | Unmap custom column |
| POST | /v2/user/catalogs/{storeId}/importations/{executionId}/products/list | Importation Get Products Report |
| GET | /v2/user/catalogs/{storeId}/importations/{executionId}/report | Importation Get Report |
| POST | /v2/user/catalogs/{storeId}/autoImport/activate | Activate the auto importation of the last successful manual catalog importation. |
| GET | /v2/user/catalogs/{storeId}/autoImport | Get the auto import configuration |
| DELETE | /v2/user/catalogs/{storeId}/autoImport | Delete Auto Import |
| POST | /v2/user/catalogs/{storeId}/autoImport/start | Start Auto Import Manually |
| POST | /v2/user/catalogs/{storeId}/autoImport/pause | Pause Auto Import |
| POST | /v2/user/catalogs/{storeId}/autoImport/resume | Resume Auto Import |
| POST | /v2/user/catalogs/{storeId}/autoImport/scheduling/interval | Configure Auto Import Interval |
| POST | /v2/user/catalogs/{storeId}/autoImport/scheduling/schedules | Configure Auto Import Schedules |
| GET | /v2/user/catalogs/{storeId}/replication/to | [PREVIEW] [Mocked] Get Store's Replicated To Configuration |
| PUT | /v2/user/catalogs/{storeId}/replication/to | [PREVIEW] [Mocked] Put Store's Replicated To Configuration |
| PATCH | /v2/user/catalogs/{storeId}/replication/to | [PREVIEW] [Mocked] Patch Store's Replicated To Configuration |
| GET | /v2/user/catalogs/{storeId}/replication/from | [PREVIEW] [Mocked] Get Store's Replicated From Configuration |
| GET | /v2/user/catalogs/{storeId}/replication/logs | [PREVIEW] [Mocked] Get Replication Logs - Can be filtered by ExecutionId |
| GET | /v2/user/channels/ | List all available channel for this store |
| GET | /v2/user/channels/{channelId} | Get channel information |
| GET | /v2/user/channels/{channelId}/categories | Get channel categories |
| POST | /v2/user/channels/{channelId}/columns | Get channel columns |
| GET | /v2/user/channelCatalogs/ | List all your current channel catalogs |
| POST | /v2/user/channelCatalogs/ | Add a new channel catalog |
| GET | /v2/user/channelCatalogs/{channelCatalogId} | Get the channel catalog information |
| DELETE | /v2/user/channelCatalogs/{channelCatalogId} | Delete the channel catalog |
| GET | /v2/user/channelCatalogs/filterOperators | Get channel catalog filter operators |
| POST | /v2/user/channelCatalogs/{channelCatalogId}/enable | Enable a channel catalog |
| POST | /v2/user/channelCatalogs/{channelCatalogId}/disable | Disable a channel catalog |
| PUT | /v2/user/channelCatalogs/{channelCatalogId}/settings/general | Configure channel catalog general settings |
| PUT | /v2/user/channelCatalogs/{channelCatalogId}/settings/cost | Configure channel catalog cost settings |
| PUT | /v2/user/channelCatalogs/{channelCatalogId}/columnMappings | Configure channel catalog column mappings |
| GET | /v2/user/channelCatalogs/{channelCatalogId}/categories | Get channel catalog categories |
| POST | /v2/user/channelCatalogs/{channelCatalogId}/categories/disableMapping | Disable a channel catalog category mapping |
| POST | /v2/user/channelCatalogs/{channelCatalogId}/categories/reenableMapping | Reenable a channel catalog category mapping |
| POST | /v2/user/channelCatalogs/{channelCatalogId}/categories/configure | Configure channel catalog category |
| GET | /v2/user/channelCatalogs/{channelCatalogId}/exclusionFilters | Get channel catalog exclusion filters |
| PUT | /v2/user/channelCatalogs/{channelCatalogId}/exclusionFilters | Configure channel catalog exclusion filters |
| POST | /v2/user/channelCatalogs/{channelCatalogId}/products | Get channel catalog product information list |
| POST | /v2/user/channelCatalogs/{channelCatalogId}/products/export | Export channel catalog product information list |
| GET | /v2/user/channelCatalogs/{channelCatalogId}/products/counters | Get channel catalog products' counters |
| POST | /v2/user/channelCatalogs/products | Get channel catalog products related to these channel catalogs |
| GET | /v2/user/channelCatalogs/{channelCatalogId}/products/{productId} | Get channel catalog product information |
| PUT | /v2/user/channelCatalogs/{channelCatalogId}/products/{productId}/overrides | Override channel catalog product values |
| DELETE | /v2/user/channelCatalogs/{channelCatalogId}/products/{productId}/overrides/{channelColumnId} | Delete a specific channel catalog product value override |
| GET | /v2/user/channelCatalogs/{channelCatalogId}/products/{productId}/overrides/copy | Get channel catalog product value override compatibilities status |
| POST | /v2/user/channelCatalogs/{channelCatalogId}/products/{productId}/overrides/copy | Copy channel catalog product value override |
| POST | /v2/user/channelCatalogs/{channelCatalogId}/products/{productId}/disable | Disable channel catalog product |
| POST | /v2/user/channelCatalogs/{channelCatalogId}/products/{productId}/reenable | Reenable channel catalog product |
| GET | /v2/user/channelCatalogs/{channelCatalogId}/exportations/cache | Get the exportation cache information |
| POST | /v2/user/channelCatalogs/{channelCatalogId}/exportations/cache/clear | Clear the exportation cache |
| GET | /v2/user/channelCatalogs/{channelCatalogId}/exportations/history | Get the exportation history |
| GET | /v2/user/channelCatalogs/{channelCatalogId}/attributes | Get the Concerned Channel Catalog Attributes |
| GET | /v2/user/channelCatalogs/{channelCatalogId}/attributes/counters | Get Attributes Value Mapping Counters |
| GET | /v2/user/channelCatalogs/{channelCatalogId}/attributes/{channelAttributeId}/mapping | Get the Channel Catalog Attribute Value Mapping |
| POST | /v2/user/channelCatalogs/{channelCatalogId}/attributes/{channelAttributeId}/mapping | Set the Channel Catalog Attribute Value Mapping |
| GET | /v2/user/channelCatalogs/{channelCatalogId}/replication/to | [PREVIEW] [Mocked] Get ChannelCatalog's Replicated To Configuration |
| PUT | /v2/user/channelCatalogs/{channelCatalogId}/replication/to | [PREVIEW] [Mocked] Put ChannelCatalog's Replicated To Configuration |
| PATCH | /v2/user/channelCatalogs/{channelCatalogId}/replication/to | [PREVIEW] [Mocked] Patch ChannelCatalog's Replicated To Configuration |
| GET | /v2/user/channelCatalogs/{channelCatalogId}/replication/from | [PREVIEW] [Mocked] Get ChannelCatalog's Replicated From Configuration |
| GET | /v2/user/channelCatalogs/{channelCatalogId}/replication/logs | [PREVIEW] [Mocked] Get Replication Logs - Can be filtered by ExecutionId. |
| GET | /v2/user/marketplaces/channelcatalogs/ | Get your marketplace channel catalog list |
| POST | /v2/user/marketplaces/channelcatalogs/publications/{marketplaceTechnicalCode}/{accountId}/publish | Launch a publication of the catalog to the marketplace |
| GET | /v2/user/marketplaces/channelcatalogs/publications/{marketplaceTechnicalCode}/{accountId}/history | Fetch the publication history for an account, sorted by descending start date |
| GET | /v2/user/marketplaces/channelcatalogs/{channelCatalogId}/properties | Get the marketplace properties for a channel catalog |
| GET | /v2/user/marketplaces/channelcatalogs/{channelCatalogId}/settings | Get the marketplace settings for a channel catalog |
| POST | /v2/user/marketplaces/channelcatalogs/{channelCatalogId}/settings | Save new marketplace settings for a channel catalog |
| GET | /v2/user/marketplaces/orders/ | [DEPRECATED] Get all actions you can do on the order API |
| GET | /v2/user/marketplaces/orders/status | [DEPRECATED] Get current synchronization status between your marketplaces and BeezUP accounts |
| POST | /v2/user/marketplaces/orders/harvest | [DEPRECATED] Send harvest request to all your marketplaces |
| GET | /v2/user/marketplaces/orders/automaticTransitions | Get list of configured automatic Order status transitions |
| POST | /v2/user/marketplaces/orders/automaticTransitions | Configure new or existing automatic Order status transition |
| POST | /v2/user/marketplaces/orders/list/full | [DEPRECATED] Get a paginated list of all Orders with all Order and Order Item(s) properties |
| POST | /v2/user/marketplaces/orders/list/light | [DEPRECATED] Get a paginated list of all Orders without details |
| GET | /v2/user/marketplaces/orders/exportations | Get a paginated list of Order report exportations |
| POST | /v2/user/marketplaces/orders/exportations | Request a new Order report exportation to be generated |
| POST | /v2/user/marketplaces/orders/batches/setMerchantOrderInfos | [DEPRECATED] Send a batch of operations to set an Order's merchant information  (max 100 items per call) |
| POST | /v2/user/marketplaces/orders/batches/clearMerchantOrderInfos | [DEPRECATED] Send a batch of operations to clear an Order's merchant information (max 100 items per call) |
| POST | /v2/user/marketplaces/orders/batches/changeOrders/{changeOrderType} | [DEPRECATED] Send a batch of operations to change your marketplace Order information: accept, ship, etc.  (max 100 items per call) |
| HEAD | /v2/user/marketplaces/orders/{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId} | [DEPRECATED] DEPRECATED - Get the meta information about the order (ETag, Last-Modified) |
| GET | /v2/user/marketplaces/orders/{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId} | [DEPRECATED] DEPRECATED - Get full Order and Order Item(s) properties |
| GET | /v2/user/marketplaces/orders/{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/history | [DEPRECATED] Get an Order's harvest and change history |
| POST | /v2/user/marketplaces/orders/{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/harvest | [DEPRECATED] Send harvest request for a single Order |
| POST | /v2/user/marketplaces/orders/{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/setMerchantOrderInfo | [DEPRECATED] Set an Order's merchant information |
| POST | /v2/user/marketplaces/orders/{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/clearMerchantOrderInfo | [DEPRECATED] Clear an Order's merchant information |
| POST | /v2/user/marketplaces/orders/{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/{changeOrderType} | [DEPRECATED] Change your marketplace Order Information (accept, ship, etc.) |
| GET | /v2/user/marketplaces/orders/subscriptions/ | Get the subscription list |
| POST | /v2/user/marketplaces/orders/subscriptions/{id} | Creates a subscription to the orders |
| GET | /v2/user/marketplaces/orders/subscriptions/{id} | Get a subscription to the orders |
| DELETE | /v2/user/marketplaces/orders/subscriptions/{id} | Delete a subscription to the orders |
| GET | /v2/user/marketplaces/orders/subscriptions/{id}/reporting | Get the push reporting related to this subscription |
| POST | /v2/user/marketplaces/orders/subscriptions/{id}/activate | Activate a subscription to the orders |
| POST | /v2/user/marketplaces/orders/subscriptions/{id}/deactivate | Deactivate a subscription to the orders |
| POST | /v2/user/marketplaces/orders/subscriptions/{id}/retry | Force retry push orders immediatly |
| GET | /v2/user/analytics/ | Get the Analytics API operation index |
| GET | /v2/user/analytics/{storeId} | Get the Analytics API operation index for one store |
| GET | /v2/user/analytics/tracking/status | Get the global synchronization status of clicks and orders |
| GET | /v2/user/analytics/{storeId}/tracking/status | Get the synchronization status of clicks and orders of a store |
| GET | /v2/user/analytics/{storeId}/tracking/clicks | Get the latest tracked clicks |
| GET | /v2/user/analytics/{storeId}/tracking/orders | Get the latest tracked orders |
| GET | /v2/user/analytics/{storeId}/tracking/externalorders | Get the latest tracked external orders |
| POST | /v2/user/analytics/reports/byday | Get the report by day for a StoreId |
| POST | /v2/user/analytics/{storeId}/reports/byday | Get the report by day for a StoreId |
| POST | /v2/user/analytics/{storeId}/reports/bychannel | Get the report by channel |
| POST | /v2/user/analytics/{storeId}/reports/bycategory | Get the report by category |
| POST | /v2/user/analytics/{storeId}/reports/byproduct | Get the report by product |
| POST | /v2/user/analytics/{storeId}/optimisations/all/{actionName} | Optimise all products |
| POST | /v2/user/analytics/{storeId}/optimisations/{actionName} | Optimise products by page |
| POST | /v2/user/analytics/{storeId}/optimisations/bychannel/{channelId}/{actionName} | Optimise products by channel |
| POST | /v2/user/analytics/{storeId}/optimisations/bycategory/{catalogCategoryId}/{actionName} | Optimise products by category |
| POST | /v2/user/analytics/{storeId}/optimisations/byproduct/{productId}/{actionName} | Optimise product |
| POST | /v2/user/analytics/{storeId}/optimisations/copy | Copy product optimisations between 2 channels |
| GET | /v2/user/analytics/{storeId}/reports/filters | Get report filter list for the given store |
| GET | /v2/user/analytics/{storeId}/reports/filters/{reportFilterId} | Get the report filter description |
| PUT | /v2/user/analytics/{storeId}/reports/filters/{reportFilterId} | Save the report filter |
| DELETE | /v2/user/analytics/{storeId}/reports/filters/{reportFilterId} | Delete the report filter |
| GET | /v2/user/analytics/{storeId}/rules | Gets the list of rules for a given store |
| POST | /v2/user/analytics/{storeId}/rules | Rule creation |
| GET | /v2/user/analytics/{storeId}/rules/{ruleId} | Gets the rule |
| PATCH | /v2/user/analytics/{storeId}/rules/{ruleId} | Update Rule |
| DELETE | /v2/user/analytics/{storeId}/rules/{ruleId} | Delete Rule |
| POST | /v2/user/analytics/{storeId}/rules/{ruleId}/moveup | Move the rule up |
| POST | /v2/user/analytics/{storeId}/rules/{ruleId}/movedown | Move the rule down |
| POST | /v2/user/analytics/{storeId}/rules/{ruleId}/enable | Enable rule |
| POST | /v2/user/analytics/{storeId}/rules/{ruleId}/disable | Disable rule |
| POST | /v2/user/analytics/{storeId}/rules/run | Run all rules for this store |
| POST | /v2/user/analytics/{storeId}/rules/{ruleId}/run | Run rule |
| GET | /v2/user/analytics/{storeId}/rules/executions | Get the rules execution history |
| GET | /v2/user/legacyTracking/channelCatalogs/ | List all your current channel catalogs configured to use legacy tracking format |
| GET | /v2/user/legacyTracking/channelCatalogs/{channelCatalogId} | Get the channel catalog configured to use legacy tracking format information |
| POST | /v2/user/legacyTracking/channelCatalogs/{channelCatalogId}/migrate | Migrate a channel catalog to current tracking format |
| PUT | /v2/user/marketplaces/orders/invoices/settings/general | Save Order Invoice general settings |
| GET | /v2/user/marketplaces/orders/invoices/settings/general | Get Order Invoice general settings |
| PUT | /v2/user/marketplaces/orders/invoices/settings/design | Save Order Invoice design settings |
| GET | /v2/user/marketplaces/orders/invoices/settings/design | Get Order Invoice design settings |
| POST | /v2/user/marketplaces/orders/invoices/settings/design/preview | View a preview an Order Invoice using custom design settings |
| POST | /v2/user/marketplaces/orders/invoices/{marketplaceTechnicalCode}/{accountId}/{beezUPOrderUUID}/generate | Generate an Order Invoice |
| POST | /v2/user/marketplaces/orders/invoices/generate | Generate an Order Invoice batch |
| POST | /v2/user/marketplaces/orders/invoices/{marketplaceTechnicalCode}/{accountId}/{beezUPOrderUUID}/preview | View a preview an Order Invoice |
| POST | /v2/user/marketplaces/orders/invoices/getPdfInvoice | Returns the PDF version of the invoice |

### orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /orders/v3//lov/orderManagementReadyMarketplaceBusinessCode | Get the list of MarketplaceBusinessCode ready for Order Management |
| GET | /orders/v3//status | Get current synchronization status between your marketplaces and BeezUP accounts |
| POST | /orders/v3//harvest | Send harvest request to all your marketplaces |
| POST | /orders/v3//list/full | Get a paginated list of all Orders with all Order and Order Item(s) properties |
| POST | /orders/v3//list/light | Get a paginated list of all Orders without details |
| HEAD | /orders/v3//{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId} | Get the meta information about the order (ETag, Last-Modified) |
| GET | /orders/v3//{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId} | Get full Order and Order Item(s) properties |
| POST | /orders/v3//{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/{changeOrderType} | Change your marketplace Order Information (accept, ship, etc.) |
| POST | /orders/v3//{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/closeIncident | Mark an order incident as resolved |
| GET | /orders/v3//{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/history | Get an Order's harvest and change history |
| POST | /orders/v3//{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/harvest | Send harvest request for a single Order |
| POST | /orders/v3//{marketplaceTechnicalCode}/{accountId}/harvest | Send harvest request for an Account |
| GET | /orders/v3//{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/history/{orderChangeExecutionUUID} | Get the order change reporting |
| POST | /orders/v3//{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/setMerchantOrderInfo | Set an Order's merchant information |
| POST | /orders/v3//{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/clearMerchantOrderInfo | Clear an Order's merchant information |
| POST | /orders/v3//batches/setMerchantOrderInfos | Send a batch of operations to set an Order's merchant information  (max 100 items per call) |
| POST | /orders/v3//batches/clearMerchantOrderInfos | Send a batch of operations to clear an Order's merchant information (max 100 items per call) |
| POST | /orders/v3//batches/changeOrders/{changeOrderType} | Send a batch of operations to change your marketplace Order information: accept, ship, etc.  (max 100 items per call) |
| POST | /orders/v3//batches/changeOrders | Send a batch of operations to change your marketplace Order information: accept, ship, etc.  (max 100 items per call) |

## Enhanced Skill Content
## Question Mapping

- "How do I log in to BeezUP?" -> POST /v2/public/security/login
- "How do I handle two-factor authentication?" -> POST /v2/public/security/login/mfa
- "How do I create a new BeezUP account?" -> POST /v2/public/security/register
- "What sales channels are available in my country?" -> GET /v2/public/channels/{countryIsoCode}
- "How do I list all my stores?" -> GET /v2/user/customer/stores
- "How do I import a product catalog?" -> POST /v2/user/catalogs/{storeId}/importations/start
- "How do I check the status of a catalog import?" -> GET /v2/user/catalogs/{storeId}/importations/{executionId}
- "How do I list my marketplace orders?" -> POST /v2/user/marketplaces/orders/list/full
- "How do I ship or change an order status?" -> POST /v2/user/marketplaces/orders/{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/{changeOrderType}
- "How do I publish products to a marketplace?" -> POST /v2/user/marketplaces/channelcatalogs/publications/{marketplaceTechnicalCode}/{accountId}/publish
- "How do I get analytics reports by day?" -> POST /v2/user/analytics/{storeId}/reports/byday
- "How do I set up auto-import for my catalog?" -> POST /v2/user/catalogs/{storeId}/autoImport/activate
- "How do I generate an invoice for an order?" -> POST /v2/user/marketplaces/orders/invoices/{marketplaceTechnicalCode}/{accountId}/{beezUPOrderUUID}/generate
- "How do I configure channel catalog column mappings?" -> PUT /v2/user/channelCatalogs/{channelCatalogId}/columnMappings
- "How do I harvest latest orders from marketplaces?" -> POST /orders/v3//harvest

## Response Tips

- **Authentication endpoints**: Login returns a session token on 200; MFA may return 202 (accepted, awaiting second factor). Always check for 403 (account locked/disabled).
- **Public channels/LOV**: Support `If-None-Match` for caching; 304 means data unchanged. Channel lists may be large -- use `Accept-Encoding: gzip`.
- **Store and account endpoints**: 204 means success with no body. Customer/store objects are nested maps with links. Always check for 404 when using storeId paths.
- **Catalog importation**: Start returns 202 (async). Poll the executionId endpoint for progress. The technical progression endpoint gives step-by-step status. 409 means another import is already running.
- **Order list endpoints**: Full and light variants exist. Full requires `Accept-Encoding`. Both use POST with a request body for filtering. Results contain nested order objects with marketplace-specific fields.
- **Order change operations**: Require `If-Match` (ETag) for optimistic concurrency on single-order changes. 412 means the order was modified since last read. 409 means the transition is not valid for current state.
- **Analytics reports**: POST-based with request body filters (date ranges, channels). Reports return nested data structures grouped by the requested dimension (day, channel, category, product).
- **Batch operations**: Return 202 (queued). There is no synchronous result -- check status via order list or history endpoints afterward.
- **Exportation history**: Paginated via `pageNumber` and `pageSize` query params. Always pass both.
- **Invoices**: Generate returns 202 (async generation). Preview returns 200 with PDF-like content. 429 means invoice rate limit hit.

## Anomaly Flags

- **429 on email activation or invoice generation**: Rate limit reached. Surface this immediately and advise waiting before retrying. These endpoints explicitly enforce throttling.
- **409 on catalog importation**: Another import is already in progress. Alert the user and suggest checking the current importation status before retrying.
- **409 on order change**: The order state does not allow the requested transition. Surface the current order status and valid transitions.
- **412 on order operations**: ETag mismatch indicates the order was modified by another process. Refetch the order to get the current ETag before retrying.
- **402 on store creation or channel enable**: Payment required. The user's subscription plan may not cover additional stores or channels. Surface billing info.
- **503 on marketplace endpoints**: The external marketplace is temporarily unavailable. Flag this as a third-party outage, not a BeezUP issue.
- **304 on cached resources**: Not an error, but agents should recognize this means the client's cached copy is still valid. Do not treat as a failure.
- **400 with body on batch order changes**: The batch partially failed. Parse the response body for per-order error details and surface individual failures.
- **Deprecated `v2/user/legacyTracking` endpoints**: These exist for migration only. Flag any usage and recommend migrating via the `/migrate` endpoint.

## Playbook

### 1. First-Time Setup: Register, Login, and Create a Store

1. POST /v2/public/security/register with email, password, and account details
2. Check email for activation link, then POST /v2/user/customer/account/activate with the `emailActivationId`
3. POST /v2/public/security/login with credentials to get a session token
4. If MFA is enabled, POST /v2/public/security/login/mfa with the verification code
5. Set the `Ocp-Apim-Subscription-Key` header for all subsequent requests
6. PUT /v2/user/customer/account/personalInfo and /companyInfo to complete profile
7. POST /v2/user/customer/stores with store name and country to create your first store

### 2. Import a Product Catalog

1. GET /v2/user/catalogs/{storeId}/inputConfiguration to check current feed settings
2. POST /v2/user/catalogs/{storeId}/importations/start with the feed URL and configuration
3. Note the `executionId` from the 202 response
4. GET /v2/user/catalogs/{storeId}/importations/{executionId}/technicalProgression to monitor progress
5. GET /v2/user/catalogs/{storeId}/importations/{executionId}/catalogColumns to review detected columns
6. POST .../catalogColumns/{columnId}/map to map any unmapped columns to BeezUP columns
7. POST /v2/user/catalogs/{storeId}/importations/{executionId}/commit to finalize the import
8. Optionally POST /v2/user/catalogs/{storeId}/autoImport/activate then configure scheduling via /scheduling/interval or /scheduling/schedules

### 3. Connect a Channel and Publish Products

1. GET /v2/user/channels/ with your storeId to list available channels
2. POST /v2/user/channelCatalogs/ with storeId and channelId to create a channel catalog
3. PUT /v2/user/channelCatalogs/{channelCatalogId}/columnMappings to map product fields to channel fields
4. POST /v2/user/channelCatalogs/{channelCatalogId}/categories/configure to set category mappings
5. PUT /v2/user/channelCatalogs/{channelCatalogId}/exclusionFilters to exclude unwanted products
6. POST /v2/user/channelCatalogs/{channelCatalogId}/enable to activate the channel
7. POST /v2/user/marketplaces/channelcatalogs/publications/{marketplaceTechnicalCode}/{accountId}/publish to push products live
8. GET .../publications/{marketplaceTechnicalCode}/{accountId}/history to verify publication status

### 4. Process Marketplace Orders

1. POST /orders/v3//harvest (or /v2/user/marketplaces/orders/harvest) to pull latest orders from all marketplaces
2. POST /orders/v3//list/full with date range and status filters to retrieve order details
3. GET /orders/v3//{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId} to view a specific order (note the ETag in the response)
4. POST /orders/v3//{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/setMerchantOrderInfo to attach your internal order reference
5. POST /orders/v3//{marketplaceTechnicalCode}/{accountId}/{beezUPOrderId}/{changeOrderType} with `userName`, the ETag as `If-Match`, and shipping details to ship the order
6. GET .../history to confirm the status change was applied

### 5. Monitor Performance with Analytics

1. GET /v2/user/analytics/{storeId} to see available analytics dimensions
2. POST /v2/user/analytics/{storeId}/reports/byday with date range to get daily revenue and click data
3. POST /v2/user/analytics/{storeId}/reports/bychannel to compare channel performance
4. POST /v2/user/analytics/{storeId}/reports/byproduct to identify top and underperforming products
5. GET /v2/user/analytics/{storeId}/rules to review existing optimization rules
6. POST /v2/user/analytics/{storeId}/rules to create a new rule (e.g., disable products with zero clicks after 30 days)
7. POST /v2/user/analytics/{storeId}/rules/run to execute all rules immediately


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
