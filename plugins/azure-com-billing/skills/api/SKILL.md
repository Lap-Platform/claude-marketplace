---
name: billingmanagementclient
description: "BillingManagementClient API skill. Use when working with BillingManagementClient for providers, subscriptions. Covers 119 endpoints."
version: 1.0.0
generator: lapsh
---

# BillingManagementClient
API version: 2019-10-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Billing/billingAccounts -- verify access
3. POST /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/listInvoiceSectionsWithCreateSubscriptionPermission -- create first listInvoiceSectionsWithCreateSubscriptionPermission

## Endpoints

119 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Billing/billingAccounts | Lists the billing accounts that a user has access to. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName} | Gets a billing account by its ID. |
| PATCH | /providers/Microsoft.Billing/billingAccounts/{billingAccountName} | Updates the properties of a billing account. Currently, displayName and address can be updated. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/listInvoiceSectionsWithCreateSubscriptionPermission | Lists the invoice sections for which the user has permission to create Azure subscriptions. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/paymentMethods | Lists the payment Methods for a billing account. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| POST | /providers/Microsoft.Billing/validateAddress | Validates an address. Use the operation to validate an address before using it as a billing account or a billing profile address. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/availableBalance/default | The available credit balance for a billing profile. This is the balance that can be used for pay now to settle due or past due invoices. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/instructions | Lists the instructions by billing profile id. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/instructions/{instructionName} | Get the instruction by name. These are custom billing instructions and are only applicable for certain customers. |
| PUT | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/instructions/{instructionName} | Creates or updates an instruction. These are custom billing instructions and are only applicable for certain customers. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/paymentMethods | Lists the payment Methods for a billing profile. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/validateDetachPaymentMethodEligibility | Validates if the default payment method can be detached from the billing profile. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles | Lists the billing profiles that a user has access to. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement or Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName} | Gets a billing profile by its ID. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement or Microsoft Partner Agreement. |
| PUT | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName} | Creates a billing profile. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement or Microsoft Partner Agreement. |
| PATCH | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName} | Updates the properties of a billing profile. Currently, displayName, poNumber, bill-to address and invoiceEmailOptIn can be updated. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement or Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/customers | Lists the customers that are billed to a billing profile. The operation is supported only for billing accounts with agreement type Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections | Lists the invoice sections that a user has access to. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName} | Gets an invoice section by its ID. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| PUT | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName} | Creates an invoice section. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| PATCH | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName} | Updates an invoice section. Currently, only displayName can be updated. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/customers | Lists the customers that are billed to a billing account. The operation is supported only for billing accounts with agreement type Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/customers/{customerName} | Gets a customer by its ID. The operation is supported only for billing accounts with agreement type Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/customers/{customerName}/billingPermissions | Lists the billing permissions the caller has for a customer. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/customers/{customerName}/billingSubscriptions | Lists the subscriptions for a customer. The operation is supported only for billing accounts with agreement type Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/customers/{customerName}/billingSubscriptions/{billingSubscriptionName} | Gets a subscription by its ID. The operation is supported only for billing accounts with agreement type Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/customers/{customerName}/products | Lists the products for a customer. These don't include products billed based on usage.The operation is supported only for billing accounts with agreement type Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/customers/{customerName}/products/{productName} | Gets a product by ID. The operation is supported only for billing accounts with agreement type Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/customers/{customerName}/transactions | Lists the billed and unbilled transactions by customer id for given start date and end date. Transactions include purchases, refunds and Azure usage charges. Unbilled transactions are listed under pending invoice Id and do not include tax. Tax is added to the amount once an invoice is generated. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/departments | Lists the departments that a user has access to. The operation is supported only for billing accounts with agreement type Enterprise Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/departments/{departmentName} | Gets a department by ID. The operation is supported only for billing accounts with agreement type Enterprise Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/enrollmentAccounts | Lists the enrollment accounts for a billing account. The operation is supported only for billing accounts with agreement type Enterprise Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/enrollmentAccounts/{enrollmentAccountName} | Gets an enrollment account by ID. The operation is supported only for billing accounts with agreement type Enterprise Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/invoices | Lists the invoices for a billing account for a given start date and end date. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement, Microsoft Customer Agreement or Enterprise Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/downloadDocuments | Gets a URL to download multiple invoice documents (invoice pdf, tax receipts, credit notes) as a zip file. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/invoices/{invoiceName} | Gets an invoice by billing account name and ID. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement, Microsoft Customer Agreement or Enterprise Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/default/billingSubscriptions/{subscriptionId}/downloadDocuments | Gets a URL to download multiple invoice documents (invoice pdf, tax receipts, credit notes) as a zip file. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoices/{invoiceName}/pricesheet/default/download | Gets a URL to download the pricesheet for an invoice. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement or Microsoft Customer Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/pricesheet/default/download | Gets a URL to download the current month's pricesheet for a billing profile. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement or Microsoft Customer Agreement.This API is hereby deprecated in favor of https://docs.microsoft.com/en-us/rest/api/cost-management/2022-02-01-preview/price-sheet/download-by-billing-profile. We highly recommend you move to the new preview version, as the csv file in the current preview version will have 500k max size that cannot scale with Azure product growth. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoices | Lists the invoices for a billing profile for a given start date and end date. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement or Microsoft Customer Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/downloadDocuments | Gets a URL to download multiple invoice documents (invoice pdf, tax receipts, credit notes) as a zip file. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoices/{invoiceName} | Gets an invoice by ID. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement or Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingSubscriptions | Lists the subscriptions for a billing account. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement or Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingSubscriptions/{billingSubscriptionName}/invoices | Lists the invoices for a subscription. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingSubscriptions/{billingSubscriptionName}/invoices/{invoiceName} | Gets an invoice by ID. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/billingSubscriptions | Lists the subscriptions that are billed to a billing profile. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement or Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/billingSubscriptions | Lists the subscriptions that are billed to an invoice section. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/billingSubscriptions/{billingSubscriptionName} | Gets a subscription by its ID. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/billingSubscriptions/{billingSubscriptionName}/transfer | Moves a subscription's charges to a new invoice section. The new invoice section must belong to the same billing profile as the existing invoice section. This operation is supported only for products that are purchased with a recurring charge and for billing accounts with agreement type Microsoft Customer Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/billingSubscriptions/{billingSubscriptionName}/validateTransferEligibility | Validates if a subscription's charges can be moved to a new invoice section. This operation is supported only for products that are purchased with a recurring charge and for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/products | Lists the products for a billing account. These don't include products billed based on usage. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement or Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/products | Lists the products for an invoice section. These don't include products billed based on usage. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/products/{productName} | Gets a product by ID. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/products/{productName}/transfer | Moves a product's charges to a new invoice section. The new invoice section must belong to the same billing profile as the existing invoice section. This operation is supported only for products that are purchased with a recurring charge and for billing accounts with agreement type Microsoft Customer Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/products/{productName}/validateTransferEligibility | Validates if a product's charges can be moved to a new invoice section. This operation is supported only for products that are purchased with a recurring charge and for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/transactions | Lists the billed and unbilled transactions by billing account name for given start and end date. Transactions include purchases, refunds and Azure usage charges. Unbilled transactions are listed under pending invoice ID and do not include tax. Tax is added to the amount once an invoice is generated. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/transactions | Lists the billed and unbilled transactions by billing profile name for given start date and end date. Transactions include purchases, refunds and Azure usage charges. Unbilled transactions are listed under pending invoice Id and do not include tax. Tax is added to the amount once an invoice is generated. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/transactions | Lists the billed and unbilled transactions by invoice section name for given start date and end date. Transactions include purchases, refunds and Azure usage charges. Unbilled transactions are listed under pending invoice Id and do not include tax. Tax is added to the amount once an invoice is generated. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoices/{invoiceName}/transactions | Lists the transactions for an invoice. Transactions include purchases, refunds and Azure usage charges. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/transactions/{transactionName} | Gets a transaction by ID. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement or Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/policies/default | Lists the policies for a billing profile. This operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| PUT | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/policies/default | Updates the policies for a billing profile. This operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/customers/{customerName}/policies/default | Lists the policies for a customer. This operation is supported only for billing accounts with agreement type Microsoft Partner Agreement. |
| PUT | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/customers/{customerName}/policies/default | Updates the policies for a customer. This operation is supported only for billing accounts with agreement type Microsoft Partner Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/products/{productName}/updateAutoRenew | Cancel auto renew for product by product id and invoice section name |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/elevate | Gives the caller permissions on an invoice section based on their billing profile access.  The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/initiateTransfer | Sends a request to a user in another billing account to transfer billing ownership of their subscriptions. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/transfers/{transferName} | Gets a transfer request by ID. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| DELETE | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/transfers/{transferName} | Cancels a transfer request. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/transfers | Lists the transfer requests for an invoice section. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/customers/{customerName}/initiateTransfer | Sends a request to a user in a customer's billing account to transfer billing ownership of their subscriptions. The operation is supported only for billing accounts with agreement type Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/customers/{customerName}/transfers/{transferName} | Gets a transfer request by ID. The operation is supported only for billing accounts with agreement type Microsoft Partner Agreement. |
| DELETE | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/customers/{customerName}/transfers/{transferName} | Cancels a transfer request. The operation is supported only for billing accounts with agreement type Microsoft Partner Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/customers/{customerName}/transfers | Lists the transfer requests sent to a customer. The operation is supported only for billing accounts with agreement type Microsoft Partner Agreement. |
| POST | /providers/Microsoft.Billing/transfers/{transferName}/acceptTransfer | Accepts a transfer request. |
| POST | /providers/Microsoft.Billing/transfers/{transferName}/validateTransfer | Validates if a subscription or a reservation can be transferred. Use this operation to validate your subscriptions or reservation before using the accept transfer operation. |
| POST | /providers/Microsoft.Billing/transfers/{transferName}/declineTransfer | Declines a transfer request. |
| GET | /providers/Microsoft.Billing/transfers/{transferName} | Gets a transfer request by ID. The caller must be the recipient of the transfer request. |
| GET | /providers/Microsoft.Billing/transfers | Lists the transfer requests received by the caller. |
| GET | /providers/Microsoft.Billing/operations | Lists the available billing REST API operations. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingPermissions | Lists the billing permissions the caller has on a billing account. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/billingPermissions | Lists the billing permissions the caller has on an invoice section. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/billingPermissions | Lists the billing permissions the caller has on a billing profile. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/departments/{departmentName}/billingPermissions | Lists the billing permissions the caller has on a department. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/enrollmentAccounts/{enrollmentAccountName}/billingPermissions | Lists the billing permissions the caller has on an enrollment account. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingRoleDefinitions/{billingRoleDefinitionName} | Gets the definition for a role on a billing account. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement or Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/billingRoleDefinitions/{billingRoleDefinitionName} | Gets the definition for a role on an invoice section. The operation is supported only for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/billingRoleDefinitions/{billingRoleDefinitionName} | Gets the definition for a role on a billing profile. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement or Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/departments/{departmentName}/billingRoleDefinitions/{billingRoleDefinitionName} | Gets the definition for a role on a department. The operation is supported only for billing accounts with agreement type Enterprise Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/enrollmentAccounts/{enrollmentAccountName}/billingRoleDefinitions/{billingRoleDefinitionName} | Gets the definition for a role on an enrollment account. The operation is supported only for billing accounts with agreement type Enterprise Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingRoleDefinitions | Lists the role definitions for a billing account. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement, Microsoft Customer Agreement or Enterprise Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/billingRoleDefinitions | Lists the role definitions for an invoice section. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement or Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/billingRoleDefinitions | Lists the role definitions for a billing profile. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement or Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/departments/{departmentName}/billingRoleDefinitions | Lists the role definitions for a department. The operation is supported only for billing accounts with agreement type Enterprise Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/enrollmentAccounts/{enrollmentAccountName}/billingRoleDefinitions | Lists the role definitions for a enrollmentAccount. The operation is supported only for billing accounts with agreement type Enterprise Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingRoleAssignments/{billingRoleAssignmentName} | Gets a role assignment for the caller on a billing account. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement, Microsoft Customer Agreement or Enterprise Agreement. |
| DELETE | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingRoleAssignments/{billingRoleAssignmentName} | Deletes a role assignment for the caller on a billing account. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement or Microsoft Customer Agreement. |
| PUT | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingRoleAssignments/{billingRoleAssignmentName} | Create or update a billing role assignment. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/billingRoleAssignments/{billingRoleAssignmentName} | Gets a role assignment for the caller on an invoice section. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement. |
| DELETE | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/billingRoleAssignments/{billingRoleAssignmentName} | Deletes a role assignment for the caller on an invoice section. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/billingRoleAssignments/{billingRoleAssignmentName} | Gets a role assignment for the caller on a billing profile. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement or Microsoft Customer Agreement. |
| DELETE | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/billingRoleAssignments/{billingRoleAssignmentName} | Deletes a role assignment for the caller on a billing profile. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement or Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/departments/{departmentName}/billingRoleAssignments/{billingRoleAssignmentName} | Gets a role assignment for the caller on a department. The operation is supported only for billing accounts with agreement type Enterprise Agreement. |
| DELETE | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/departments/{departmentName}/billingRoleAssignments/{billingRoleAssignmentName} | Deletes a role assignment for the caller on a department. The operation is supported only for billing accounts with agreement type Enterprise Agreement. |
| PUT | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/departments/{departmentName}/billingRoleAssignments/{billingRoleAssignmentName} | Create or update a billing role assignment. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/enrollmentAccounts/{enrollmentAccountName}/billingRoleAssignments/{billingRoleAssignmentName} | Gets a role assignment for the caller on a enrollment Account. The operation is supported only for billing accounts with agreement type Enterprise Agreement. |
| DELETE | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/enrollmentAccounts/{enrollmentAccountName}/billingRoleAssignments/{billingRoleAssignmentName} | Deletes a role assignment for the caller on a enrollment Account. The operation is supported only for billing accounts with agreement type Enterprise Agreement. |
| PUT | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/enrollmentAccounts/{enrollmentAccountName}/billingRoleAssignments/{billingRoleAssignmentName} | Create or update a billing role assignment. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingRoleAssignments | Lists the role assignments for the caller on a billing account. The operation is supported for billing accounts with agreement type Microsoft Partner Agreement, Microsoft Customer Agreement or Enterprise Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/createBillingRoleAssignment | Adds a role assignment on a billing account. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/billingRoleAssignments | Lists the role assignments for the caller on an invoice section. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/createBillingRoleAssignment | Adds a role assignment on an invoice section. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/billingRoleAssignments | Lists the role assignments for the caller on a billing profile. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement. |
| POST | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/createBillingRoleAssignment | Adds a role assignment on a billing profile. The operation is supported for billing accounts with agreement type Microsoft Customer Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/departments/{departmentName}/billingRoleAssignments | Lists the role assignments for the caller on a billing profile. The operation is supported for billing accounts of type Enterprise Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/enrollmentAccounts/{enrollmentAccountName}/billingRoleAssignments | Lists the role assignments for the caller on a billing profile. The operation is supported for billing accounts of type Enterprise Agreement. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/agreements | Lists the agreements for a billing account. |
| GET | /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/agreements/{agreementName} | Gets an agreement by ID. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Billing/billingProperty/default | Get the billing properties for a subscription. This operation is not supported for billing accounts with agreement type Enterprise Agreement. |

## Enhanced Skill Content
## Question Mapping

- "What billing accounts do I have access to?" -> GET /providers/Microsoft.Billing/billingAccounts
- "Show me the details of a specific billing account" -> GET /providers/Microsoft.Billing/billingAccounts/{billingAccountName}
- "What invoices were generated this quarter?" -> GET /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/invoices
- "What is my available balance for a billing profile?" -> GET /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/availableBalance/default
- "List all subscriptions under a billing account" -> GET /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingSubscriptions
- "What products does a specific customer have?" -> GET /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/customers/{customerName}/products
- "Download invoices in bulk for a billing account" -> POST /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/downloadDocuments
- "Transfer a subscription to a different invoice section" -> POST /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/billingSubscriptions/{billingSubscriptionName}/transfer
- "Can this subscription be transferred?" -> POST /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/invoiceSections/{invoiceSectionName}/billingSubscriptions/{billingSubscriptionName}/validateTransferEligibility
- "Who has billing permissions on this account?" -> GET /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingPermissions
- "What role definitions exist for this billing profile?" -> GET /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/billingProfiles/{billingProfileName}/billingRoleDefinitions
- "Assign a billing role to a user at the account level" -> POST /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/createBillingRoleAssignment
- "What transactions occurred for a customer in the last month?" -> GET /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/customers/{customerName}/transactions
- "Validate a billing address before updating a profile" -> POST /providers/Microsoft.Billing/validateAddress
- "What agreements are associated with my billing account?" -> GET /providers/Microsoft.Billing/billingAccounts/{billingAccountName}/agreements

## Response Tips

- **List endpoints** (billingAccounts, billingProfiles, invoiceSections, customers, products): Responses return `value` arrays with `nextLink` for pagination; follow `nextLink` until null. Use `$skiptoken` from the URL when present, and `$filter` for server-side narrowing.
- **Single resource GETs** (billingAccount by name, invoice by name, customer by name): Return a flat object with `id`, `name`, `type`, and a `properties` nested object containing all domain fields -- always drill into `properties` for useful data.
- **PUT/PATCH mutations** (billingProfiles, invoiceSections, instructions): Return 200 for synchronous completion or 202 with a `Location` header for long-running operations -- poll the Location URL until the operation completes.
- **Document downloads** (downloadDocuments, pricesheet download): Return 202 with an async operation; the final 200 contains a `url` field with a time-limited SAS link to the actual file.
- **Transfer operations** (initiateTransfer, acceptTransfer, declineTransfer): Return a transfer object with `transferStatus` -- check for `Completed`, `InProgress`, `Failed`, or `CompletedWithErrors`.
- **Validation endpoints** (validateAddress, validateTransferEligibility): Return a `status` of `Valid` or `Invalid` with a `validationMessage` array describing each issue.
- **Role assignments/definitions**: Scoped hierarchically (account > profile > invoiceSection > department > enrollmentAccount) -- ensure you query at the correct scope level or you will get empty results.

## Anomaly Flags

- **202 Accepted without polling**: If a PUT/PATCH/POST returns 202, the agent should surface the `Location` or `Retry-After` header and remind the user the operation is still in progress -- do not treat 202 as a completed success.
- **Preview API version**: This API uses `2019-10-01-preview` -- surface a warning that this is a preview version; behavior and schemas may change without notice, and production reliance carries risk.
- **Empty `value` arrays on list endpoints**: If a list returns 200 with an empty `value` array, flag that the caller may lack permissions at the queried scope rather than there being no resources.
- **Transfer eligibility failures**: When `validateTransferEligibility` returns issues, proactively surface the specific `errorCode` and `message` from each validation result before attempting the actual transfer.
- **Role assignment deletions**: Deleting a billingRoleAssignment is irreversible -- flag this before executing, especially at the account level where blast radius is highest.
- **Missing `$expand` on profile/account GETs**: Several endpoints support `$expand` (e.g., for invoice sections, billing profiles) -- if the user asks about nested entities and gets sparse results, suggest re-fetching with `$expand`.
- **Date range required on invoices/transactions**: These endpoints require `periodStartDate` and `periodEndDate` -- if the user does not specify, the agent should ask rather than guess, since overly broad ranges can return very large datasets.

## Playbook

### 1. Audit billing permissions across all scopes

1. GET `/providers/Microsoft.Billing/billingAccounts` to list all accessible accounts
2. For each account, GET `.../billingPermissions` to see account-level permissions
3. GET `.../billingProfiles` for each account, then GET `.../billingProfiles/{name}/billingPermissions` per profile
4. GET `.../invoiceSections` per profile, then GET `.../invoiceSections/{name}/billingPermissions` per section
5. Compile results into a scope-to-permission matrix for the caller

### 2. Transfer a subscription between invoice sections

1. GET `.../billingSubscriptions/{name}` to confirm the subscription exists and note its current invoice section
2. POST `.../invoiceSections/{sourceSectionName}/billingSubscriptions/{name}/validateTransferEligibility` with the target invoice section in the body
3. Review validation response -- if `status` is not `Valid`, stop and surface issues
4. POST `.../invoiceSections/{sourceSectionName}/billingSubscriptions/{name}/transfer` with the destination details
5. If 202 returned, poll the `Location` header until the transfer completes; surface `transferStatus` to the user

### 3. Download invoices for a date range

1. GET `.../billingAccounts/{name}/invoices?periodStartDate=YYYY-MM-DD&periodEndDate=YYYY-MM-DD` to list invoices
2. Collect the `downloadUrl` values from each invoice in the response
3. POST `.../billingAccounts/{name}/downloadDocuments` with the `downloadUrls` array
4. Poll the 202 operation until 200 is returned with the final SAS download link
5. Present the download URL to the user (note: link is time-limited)

### 4. Set up a new billing profile with invoice section and role assignment

1. PUT `.../billingProfiles/{newProfileName}` with display name, bill-to address, and payment method -- handle 202 by polling
2. Once the profile is created, PUT `.../billingProfiles/{newProfileName}/invoiceSections/{newSectionName}` with the section display name
3. POST `.../billingProfiles/{newProfileName}/createBillingRoleAssignment` to grant a user the appropriate billing role
4. GET `.../billingProfiles/{newProfileName}/policies/default` to review default policies
5. PUT `.../billingProfiles/{newProfileName}/policies/default` to adjust policies (e.g., marketplace purchases, reservation purchases) as needed

### 5. Investigate a customer's billing activity

1. GET `.../customers/{customerName}` with `$expand` to load full customer details
2. GET `.../customers/{customerName}/billingSubscriptions` to list all subscriptions
3. GET `.../customers/{customerName}/products` to list purchased products
4. GET `.../customers/{customerName}/transactions?periodStartDate=...&periodEndDate=...` for transaction history in the target window
5. Cross-reference subscription and product IDs with transactions to identify billing anomalies or unexpected charges


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
