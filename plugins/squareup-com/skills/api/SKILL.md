---
name: square
description: "Square API skill. Use when working with Square for mobile, oauth2, {location_id}. Covers 327 endpoints."
version: 1.0.0
generator: lapsh
---

# Square
API version: 2.0

## Auth
OAuth2 | ApiKey Authorization in header

## Base URL
https://connect.squareup.com

## Setup
1. Set your API key in the appropriate header
2. GET /v2/bank-accounts -- verify access
3. POST /mobile/authorization-code -- create first authorization-code

## Endpoints

327 endpoints across 34 groups. See references/api-spec.lap for full details.

### mobile
| Method | Path | Description |
|--------|------|-------------|
| POST | /mobile/authorization-code | CreateMobileAuthorizationCode |

### oauth2
| Method | Path | Description |
|--------|------|-------------|
| POST | /oauth2/revoke | RevokeToken |
| POST | /oauth2/token | ObtainToken |
| POST | /oauth2/token/status | RetrieveTokenStatus |

### {location_id}
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/{location_id}/orders | V1ListOrders |
| GET | /v1/{location_id}/orders/{order_id} | V1RetrieveOrder |
| PUT | /v1/{location_id}/orders/{order_id} | V1UpdateOrder |

### apple-pay
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/apple-pay/domains | RegisterDomain |

### bank-accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/bank-accounts | ListBankAccounts |
| GET | /v2/bank-accounts/by-v1-id/{v1_bank_account_id} | GetBankAccountByV1Id |
| GET | /v2/bank-accounts/{bank_account_id} | GetBankAccount |

### bookings
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/bookings | ListBookings |
| POST | /v2/bookings | CreateBooking |
| POST | /v2/bookings/availability/search | SearchAvailability |
| POST | /v2/bookings/bulk-retrieve | BulkRetrieveBookings |
| GET | /v2/bookings/business-booking-profile | RetrieveBusinessBookingProfile |
| GET | /v2/bookings/custom-attribute-definitions | ListBookingCustomAttributeDefinitions |
| POST | /v2/bookings/custom-attribute-definitions | CreateBookingCustomAttributeDefinition |
| DELETE | /v2/bookings/custom-attribute-definitions/{key} | DeleteBookingCustomAttributeDefinition |
| GET | /v2/bookings/custom-attribute-definitions/{key} | RetrieveBookingCustomAttributeDefinition |
| PUT | /v2/bookings/custom-attribute-definitions/{key} | UpdateBookingCustomAttributeDefinition |
| POST | /v2/bookings/custom-attributes/bulk-delete | BulkDeleteBookingCustomAttributes |
| POST | /v2/bookings/custom-attributes/bulk-upsert | BulkUpsertBookingCustomAttributes |
| GET | /v2/bookings/location-booking-profiles | ListLocationBookingProfiles |
| GET | /v2/bookings/location-booking-profiles/{location_id} | RetrieveLocationBookingProfile |
| GET | /v2/bookings/team-member-booking-profiles | ListTeamMemberBookingProfiles |
| POST | /v2/bookings/team-member-booking-profiles/bulk-retrieve | BulkRetrieveTeamMemberBookingProfiles |
| GET | /v2/bookings/team-member-booking-profiles/{team_member_id} | RetrieveTeamMemberBookingProfile |
| GET | /v2/bookings/{booking_id} | RetrieveBooking |
| PUT | /v2/bookings/{booking_id} | UpdateBooking |
| POST | /v2/bookings/{booking_id}/cancel | CancelBooking |
| GET | /v2/bookings/{booking_id}/custom-attributes | ListBookingCustomAttributes |
| DELETE | /v2/bookings/{booking_id}/custom-attributes/{key} | DeleteBookingCustomAttribute |
| GET | /v2/bookings/{booking_id}/custom-attributes/{key} | RetrieveBookingCustomAttribute |
| PUT | /v2/bookings/{booking_id}/custom-attributes/{key} | UpsertBookingCustomAttribute |

### cards
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/cards | ListCards |
| POST | /v2/cards | CreateCard |
| GET | /v2/cards/{card_id} | RetrieveCard |
| POST | /v2/cards/{card_id}/disable | DisableCard |

### cash-drawers
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/cash-drawers/shifts | ListCashDrawerShifts |
| GET | /v2/cash-drawers/shifts/{shift_id} | RetrieveCashDrawerShift |
| GET | /v2/cash-drawers/shifts/{shift_id}/events | ListCashDrawerShiftEvents |

### catalog
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/catalog/batch-delete | BatchDeleteCatalogObjects |
| POST | /v2/catalog/batch-retrieve | BatchRetrieveCatalogObjects |
| POST | /v2/catalog/batch-upsert | BatchUpsertCatalogObjects |
| POST | /v2/catalog/images | CreateCatalogImage |
| PUT | /v2/catalog/images/{image_id} | UpdateCatalogImage |
| GET | /v2/catalog/info | CatalogInfo |
| GET | /v2/catalog/list | ListCatalog |
| POST | /v2/catalog/object | UpsertCatalogObject |
| DELETE | /v2/catalog/object/{object_id} | DeleteCatalogObject |
| GET | /v2/catalog/object/{object_id} | RetrieveCatalogObject |
| POST | /v2/catalog/search | SearchCatalogObjects |
| POST | /v2/catalog/search-catalog-items | SearchCatalogItems |
| POST | /v2/catalog/update-item-modifier-lists | UpdateItemModifierLists |
| POST | /v2/catalog/update-item-taxes | UpdateItemTaxes |

### channels
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/channels | ListChannels |
| POST | /v2/channels/bulk-retrieve | BulkRetrieveChannels |
| GET | /v2/channels/{channel_id} | RetrieveChannel |

### customers
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/customers | ListCustomers |
| POST | /v2/customers | CreateCustomer |
| POST | /v2/customers/bulk-create | BulkCreateCustomers |
| POST | /v2/customers/bulk-delete | BulkDeleteCustomers |
| POST | /v2/customers/bulk-retrieve | BulkRetrieveCustomers |
| POST | /v2/customers/bulk-update | BulkUpdateCustomers |
| GET | /v2/customers/custom-attribute-definitions | ListCustomerCustomAttributeDefinitions |
| POST | /v2/customers/custom-attribute-definitions | CreateCustomerCustomAttributeDefinition |
| DELETE | /v2/customers/custom-attribute-definitions/{key} | DeleteCustomerCustomAttributeDefinition |
| GET | /v2/customers/custom-attribute-definitions/{key} | RetrieveCustomerCustomAttributeDefinition |
| PUT | /v2/customers/custom-attribute-definitions/{key} | UpdateCustomerCustomAttributeDefinition |
| POST | /v2/customers/custom-attributes/bulk-upsert | BulkUpsertCustomerCustomAttributes |
| GET | /v2/customers/groups | ListCustomerGroups |
| POST | /v2/customers/groups | CreateCustomerGroup |
| DELETE | /v2/customers/groups/{group_id} | DeleteCustomerGroup |
| GET | /v2/customers/groups/{group_id} | RetrieveCustomerGroup |
| PUT | /v2/customers/groups/{group_id} | UpdateCustomerGroup |
| POST | /v2/customers/search | SearchCustomers |
| GET | /v2/customers/segments | ListCustomerSegments |
| GET | /v2/customers/segments/{segment_id} | RetrieveCustomerSegment |
| DELETE | /v2/customers/{customer_id} | DeleteCustomer |
| GET | /v2/customers/{customer_id} | RetrieveCustomer |
| PUT | /v2/customers/{customer_id} | UpdateCustomer |
| POST | /v2/customers/{customer_id}/cards | CreateCustomerCard |
| DELETE | /v2/customers/{customer_id}/cards/{card_id} | DeleteCustomerCard |
| GET | /v2/customers/{customer_id}/custom-attributes | ListCustomerCustomAttributes |
| DELETE | /v2/customers/{customer_id}/custom-attributes/{key} | DeleteCustomerCustomAttribute |
| GET | /v2/customers/{customer_id}/custom-attributes/{key} | RetrieveCustomerCustomAttribute |
| POST | /v2/customers/{customer_id}/custom-attributes/{key} | UpsertCustomerCustomAttribute |
| DELETE | /v2/customers/{customer_id}/groups/{group_id} | RemoveGroupFromCustomer |
| PUT | /v2/customers/{customer_id}/groups/{group_id} | AddGroupToCustomer |

### devices
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/devices | ListDevices |
| GET | /v2/devices/codes | ListDeviceCodes |
| POST | /v2/devices/codes | CreateDeviceCode |
| GET | /v2/devices/codes/{id} | GetDeviceCode |
| GET | /v2/devices/{device_id} | GetDevice |

### disputes
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/disputes | ListDisputes |
| GET | /v2/disputes/{dispute_id} | RetrieveDispute |
| POST | /v2/disputes/{dispute_id}/accept | AcceptDispute |
| GET | /v2/disputes/{dispute_id}/evidence | ListDisputeEvidence |
| POST | /v2/disputes/{dispute_id}/evidence-files | CreateDisputeEvidenceFile |
| POST | /v2/disputes/{dispute_id}/evidence-text | CreateDisputeEvidenceText |
| DELETE | /v2/disputes/{dispute_id}/evidence/{evidence_id} | DeleteDisputeEvidence |
| GET | /v2/disputes/{dispute_id}/evidence/{evidence_id} | RetrieveDisputeEvidence |
| POST | /v2/disputes/{dispute_id}/submit-evidence | SubmitEvidence |

### employees
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/employees | ListEmployees |
| GET | /v2/employees/{id} | RetrieveEmployee |

### events
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/events | SearchEvents |
| PUT | /v2/events/disable | DisableEvents |
| PUT | /v2/events/enable | EnableEvents |
| GET | /v2/events/types | ListEventTypes |

### gift-cards
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/gift-cards | ListGiftCards |
| POST | /v2/gift-cards | CreateGiftCard |
| GET | /v2/gift-cards/activities | ListGiftCardActivities |
| POST | /v2/gift-cards/activities | CreateGiftCardActivity |
| POST | /v2/gift-cards/from-gan | RetrieveGiftCardFromGAN |
| POST | /v2/gift-cards/from-nonce | RetrieveGiftCardFromNonce |
| POST | /v2/gift-cards/{gift_card_id}/link-customer | LinkCustomerToGiftCard |
| POST | /v2/gift-cards/{gift_card_id}/unlink-customer | UnlinkCustomerFromGiftCard |
| GET | /v2/gift-cards/{id} | RetrieveGiftCard |

### inventory
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/inventory/adjustment/{adjustment_id} | DeprecatedRetrieveInventoryAdjustment |
| GET | /v2/inventory/adjustments/{adjustment_id} | RetrieveInventoryAdjustment |
| POST | /v2/inventory/batch-change | DeprecatedBatchChangeInventory |
| POST | /v2/inventory/batch-retrieve-changes | DeprecatedBatchRetrieveInventoryChanges |
| POST | /v2/inventory/batch-retrieve-counts | DeprecatedBatchRetrieveInventoryCounts |
| POST | /v2/inventory/changes/batch-create | BatchChangeInventory |
| POST | /v2/inventory/changes/batch-retrieve | BatchRetrieveInventoryChanges |
| POST | /v2/inventory/counts/batch-retrieve | BatchRetrieveInventoryCounts |
| GET | /v2/inventory/physical-count/{physical_count_id} | DeprecatedRetrieveInventoryPhysicalCount |
| GET | /v2/inventory/physical-counts/{physical_count_id} | RetrieveInventoryPhysicalCount |
| GET | /v2/inventory/transfers/{transfer_id} | RetrieveInventoryTransfer |
| GET | /v2/inventory/{catalog_object_id} | RetrieveInventoryCount |
| GET | /v2/inventory/{catalog_object_id}/changes | RetrieveInventoryChanges |

### invoices
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/invoices | ListInvoices |
| POST | /v2/invoices | CreateInvoice |
| POST | /v2/invoices/search | SearchInvoices |
| DELETE | /v2/invoices/{invoice_id} | DeleteInvoice |
| GET | /v2/invoices/{invoice_id} | GetInvoice |
| PUT | /v2/invoices/{invoice_id} | UpdateInvoice |
| POST | /v2/invoices/{invoice_id}/attachments | CreateInvoiceAttachment |
| DELETE | /v2/invoices/{invoice_id}/attachments/{attachment_id} | DeleteInvoiceAttachment |
| POST | /v2/invoices/{invoice_id}/cancel | CancelInvoice |
| POST | /v2/invoices/{invoice_id}/publish | PublishInvoice |

### labor
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/labor/break-types | ListBreakTypes |
| POST | /v2/labor/break-types | CreateBreakType |
| DELETE | /v2/labor/break-types/{id} | DeleteBreakType |
| GET | /v2/labor/break-types/{id} | GetBreakType |
| PUT | /v2/labor/break-types/{id} | UpdateBreakType |
| GET | /v2/labor/employee-wages | ListEmployeeWages |
| GET | /v2/labor/employee-wages/{id} | GetEmployeeWage |
| POST | /v2/labor/scheduled-shifts | CreateScheduledShift |
| POST | /v2/labor/scheduled-shifts/bulk-publish | BulkPublishScheduledShifts |
| POST | /v2/labor/scheduled-shifts/search | SearchScheduledShifts |
| GET | /v2/labor/scheduled-shifts/{id} | RetrieveScheduledShift |
| PUT | /v2/labor/scheduled-shifts/{id} | UpdateScheduledShift |
| POST | /v2/labor/scheduled-shifts/{id}/publish | PublishScheduledShift |
| POST | /v2/labor/shifts | CreateShift |
| POST | /v2/labor/shifts/search | SearchShifts |
| DELETE | /v2/labor/shifts/{id} | DeleteShift |
| GET | /v2/labor/shifts/{id} | GetShift |
| PUT | /v2/labor/shifts/{id} | UpdateShift |
| GET | /v2/labor/team-member-wages | ListTeamMemberWages |
| GET | /v2/labor/team-member-wages/{id} | GetTeamMemberWage |
| POST | /v2/labor/timecards | CreateTimecard |
| POST | /v2/labor/timecards/search | SearchTimecards |
| DELETE | /v2/labor/timecards/{id} | DeleteTimecard |
| GET | /v2/labor/timecards/{id} | RetrieveTimecard |
| PUT | /v2/labor/timecards/{id} | UpdateTimecard |
| GET | /v2/labor/workweek-configs | ListWorkweekConfigs |
| PUT | /v2/labor/workweek-configs/{id} | UpdateWorkweekConfig |

### locations
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/locations | ListLocations |
| POST | /v2/locations | CreateLocation |
| GET | /v2/locations/custom-attribute-definitions | ListLocationCustomAttributeDefinitions |
| POST | /v2/locations/custom-attribute-definitions | CreateLocationCustomAttributeDefinition |
| DELETE | /v2/locations/custom-attribute-definitions/{key} | DeleteLocationCustomAttributeDefinition |
| GET | /v2/locations/custom-attribute-definitions/{key} | RetrieveLocationCustomAttributeDefinition |
| PUT | /v2/locations/custom-attribute-definitions/{key} | UpdateLocationCustomAttributeDefinition |
| POST | /v2/locations/custom-attributes/bulk-delete | BulkDeleteLocationCustomAttributes |
| POST | /v2/locations/custom-attributes/bulk-upsert | BulkUpsertLocationCustomAttributes |
| GET | /v2/locations/{location_id} | RetrieveLocation |
| PUT | /v2/locations/{location_id} | UpdateLocation |
| POST | /v2/locations/{location_id}/checkouts | CreateCheckout |
| GET | /v2/locations/{location_id}/custom-attributes | ListLocationCustomAttributes |
| DELETE | /v2/locations/{location_id}/custom-attributes/{key} | DeleteLocationCustomAttribute |
| GET | /v2/locations/{location_id}/custom-attributes/{key} | RetrieveLocationCustomAttribute |
| POST | /v2/locations/{location_id}/custom-attributes/{key} | UpsertLocationCustomAttribute |
| GET | /v2/locations/{location_id}/transactions | ListTransactions |
| GET | /v2/locations/{location_id}/transactions/{transaction_id} | RetrieveTransaction |
| POST | /v2/locations/{location_id}/transactions/{transaction_id}/capture | CaptureTransaction |
| POST | /v2/locations/{location_id}/transactions/{transaction_id}/void | VoidTransaction |

### loyalty
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/loyalty/accounts | CreateLoyaltyAccount |
| POST | /v2/loyalty/accounts/search | SearchLoyaltyAccounts |
| GET | /v2/loyalty/accounts/{account_id} | RetrieveLoyaltyAccount |
| POST | /v2/loyalty/accounts/{account_id}/accumulate | AccumulateLoyaltyPoints |
| POST | /v2/loyalty/accounts/{account_id}/adjust | AdjustLoyaltyPoints |
| POST | /v2/loyalty/events/search | SearchLoyaltyEvents |
| GET | /v2/loyalty/programs | ListLoyaltyPrograms |
| GET | /v2/loyalty/programs/{program_id} | RetrieveLoyaltyProgram |
| POST | /v2/loyalty/programs/{program_id}/calculate | CalculateLoyaltyPoints |
| GET | /v2/loyalty/programs/{program_id}/promotions | ListLoyaltyPromotions |
| POST | /v2/loyalty/programs/{program_id}/promotions | CreateLoyaltyPromotion |
| GET | /v2/loyalty/programs/{program_id}/promotions/{promotion_id} | RetrieveLoyaltyPromotion |
| POST | /v2/loyalty/programs/{program_id}/promotions/{promotion_id}/cancel | CancelLoyaltyPromotion |
| POST | /v2/loyalty/rewards | CreateLoyaltyReward |
| POST | /v2/loyalty/rewards/search | SearchLoyaltyRewards |
| DELETE | /v2/loyalty/rewards/{reward_id} | DeleteLoyaltyReward |
| GET | /v2/loyalty/rewards/{reward_id} | RetrieveLoyaltyReward |
| POST | /v2/loyalty/rewards/{reward_id}/redeem | RedeemLoyaltyReward |

### merchants
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/merchants | ListMerchants |
| GET | /v2/merchants/custom-attribute-definitions | ListMerchantCustomAttributeDefinitions |
| POST | /v2/merchants/custom-attribute-definitions | CreateMerchantCustomAttributeDefinition |
| DELETE | /v2/merchants/custom-attribute-definitions/{key} | DeleteMerchantCustomAttributeDefinition |
| GET | /v2/merchants/custom-attribute-definitions/{key} | RetrieveMerchantCustomAttributeDefinition |
| PUT | /v2/merchants/custom-attribute-definitions/{key} | UpdateMerchantCustomAttributeDefinition |
| POST | /v2/merchants/custom-attributes/bulk-delete | BulkDeleteMerchantCustomAttributes |
| POST | /v2/merchants/custom-attributes/bulk-upsert | BulkUpsertMerchantCustomAttributes |
| GET | /v2/merchants/{merchant_id} | RetrieveMerchant |
| GET | /v2/merchants/{merchant_id}/custom-attributes | ListMerchantCustomAttributes |
| DELETE | /v2/merchants/{merchant_id}/custom-attributes/{key} | DeleteMerchantCustomAttribute |
| GET | /v2/merchants/{merchant_id}/custom-attributes/{key} | RetrieveMerchantCustomAttribute |
| POST | /v2/merchants/{merchant_id}/custom-attributes/{key} | UpsertMerchantCustomAttribute |

### online-checkout
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/online-checkout/location-settings/{location_id} | RetrieveLocationSettings |
| PUT | /v2/online-checkout/location-settings/{location_id} | UpdateLocationSettings |
| GET | /v2/online-checkout/merchant-settings | RetrieveMerchantSettings |
| PUT | /v2/online-checkout/merchant-settings | UpdateMerchantSettings |
| GET | /v2/online-checkout/payment-links | ListPaymentLinks |
| POST | /v2/online-checkout/payment-links | CreatePaymentLink |
| DELETE | /v2/online-checkout/payment-links/{id} | DeletePaymentLink |
| GET | /v2/online-checkout/payment-links/{id} | RetrievePaymentLink |
| PUT | /v2/online-checkout/payment-links/{id} | UpdatePaymentLink |

### orders
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/orders | CreateOrder |
| POST | /v2/orders/batch-retrieve | BatchRetrieveOrders |
| POST | /v2/orders/calculate | CalculateOrder |
| POST | /v2/orders/clone | CloneOrder |
| GET | /v2/orders/custom-attribute-definitions | ListOrderCustomAttributeDefinitions |
| POST | /v2/orders/custom-attribute-definitions | CreateOrderCustomAttributeDefinition |
| DELETE | /v2/orders/custom-attribute-definitions/{key} | DeleteOrderCustomAttributeDefinition |
| GET | /v2/orders/custom-attribute-definitions/{key} | RetrieveOrderCustomAttributeDefinition |
| PUT | /v2/orders/custom-attribute-definitions/{key} | UpdateOrderCustomAttributeDefinition |
| POST | /v2/orders/custom-attributes/bulk-delete | BulkDeleteOrderCustomAttributes |
| POST | /v2/orders/custom-attributes/bulk-upsert | BulkUpsertOrderCustomAttributes |
| POST | /v2/orders/search | SearchOrders |
| GET | /v2/orders/{order_id} | RetrieveOrder |
| PUT | /v2/orders/{order_id} | UpdateOrder |
| GET | /v2/orders/{order_id}/custom-attributes | ListOrderCustomAttributes |
| DELETE | /v2/orders/{order_id}/custom-attributes/{custom_attribute_key} | DeleteOrderCustomAttribute |
| GET | /v2/orders/{order_id}/custom-attributes/{custom_attribute_key} | RetrieveOrderCustomAttribute |
| POST | /v2/orders/{order_id}/custom-attributes/{custom_attribute_key} | UpsertOrderCustomAttribute |
| POST | /v2/orders/{order_id}/pay | PayOrder |

### payments
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/payments | ListPayments |
| POST | /v2/payments | CreatePayment |
| POST | /v2/payments/cancel | CancelPaymentByIdempotencyKey |
| GET | /v2/payments/{payment_id} | GetPayment |
| PUT | /v2/payments/{payment_id} | UpdatePayment |
| POST | /v2/payments/{payment_id}/cancel | CancelPayment |
| POST | /v2/payments/{payment_id}/complete | CompletePayment |

### payouts
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/payouts | ListPayouts |
| GET | /v2/payouts/{payout_id} | GetPayout |
| GET | /v2/payouts/{payout_id}/payout-entries | ListPayoutEntries |

### refunds
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/refunds | ListPaymentRefunds |
| POST | /v2/refunds | RefundPayment |
| GET | /v2/refunds/{refund_id} | GetPaymentRefund |

### sites
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/sites | ListSites |
| DELETE | /v2/sites/{site_id}/snippet | DeleteSnippet |
| GET | /v2/sites/{site_id}/snippet | RetrieveSnippet |
| POST | /v2/sites/{site_id}/snippet | UpsertSnippet |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/subscriptions | CreateSubscription |
| POST | /v2/subscriptions/bulk-swap-plan | BulkSwapPlan |
| POST | /v2/subscriptions/search | SearchSubscriptions |
| GET | /v2/subscriptions/{subscription_id} | RetrieveSubscription |
| PUT | /v2/subscriptions/{subscription_id} | UpdateSubscription |
| DELETE | /v2/subscriptions/{subscription_id}/actions/{action_id} | DeleteSubscriptionAction |
| POST | /v2/subscriptions/{subscription_id}/billing-anchor | ChangeBillingAnchorDate |
| POST | /v2/subscriptions/{subscription_id}/cancel | CancelSubscription |
| GET | /v2/subscriptions/{subscription_id}/events | ListSubscriptionEvents |
| POST | /v2/subscriptions/{subscription_id}/pause | PauseSubscription |
| POST | /v2/subscriptions/{subscription_id}/resume | ResumeSubscription |
| POST | /v2/subscriptions/{subscription_id}/swap-plan | SwapPlan |

### team-members
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/team-members | CreateTeamMember |
| POST | /v2/team-members/bulk-create | BulkCreateTeamMembers |
| POST | /v2/team-members/bulk-update | BulkUpdateTeamMembers |
| GET | /v2/team-members/jobs | ListJobs |
| POST | /v2/team-members/jobs | CreateJob |
| GET | /v2/team-members/jobs/{job_id} | RetrieveJob |
| PUT | /v2/team-members/jobs/{job_id} | UpdateJob |
| POST | /v2/team-members/search | SearchTeamMembers |
| GET | /v2/team-members/{team_member_id} | RetrieveTeamMember |
| PUT | /v2/team-members/{team_member_id} | UpdateTeamMember |
| GET | /v2/team-members/{team_member_id}/wage-setting | RetrieveWageSetting |
| PUT | /v2/team-members/{team_member_id}/wage-setting | UpdateWageSetting |

### terminals
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/terminals/actions | CreateTerminalAction |
| POST | /v2/terminals/actions/search | SearchTerminalActions |
| GET | /v2/terminals/actions/{action_id} | GetTerminalAction |
| POST | /v2/terminals/actions/{action_id}/cancel | CancelTerminalAction |
| POST | /v2/terminals/actions/{action_id}/dismiss | DismissTerminalAction |
| POST | /v2/terminals/checkouts | CreateTerminalCheckout |
| POST | /v2/terminals/checkouts/search | SearchTerminalCheckouts |
| GET | /v2/terminals/checkouts/{checkout_id} | GetTerminalCheckout |
| POST | /v2/terminals/checkouts/{checkout_id}/cancel | CancelTerminalCheckout |
| POST | /v2/terminals/checkouts/{checkout_id}/dismiss | DismissTerminalCheckout |
| POST | /v2/terminals/refunds | CreateTerminalRefund |
| POST | /v2/terminals/refunds/search | SearchTerminalRefunds |
| GET | /v2/terminals/refunds/{terminal_refund_id} | GetTerminalRefund |
| POST | /v2/terminals/refunds/{terminal_refund_id}/cancel | CancelTerminalRefund |
| POST | /v2/terminals/refunds/{terminal_refund_id}/dismiss | DismissTerminalRefund |

### transfer-orders
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/transfer-orders | CreateTransferOrder |
| POST | /v2/transfer-orders/search | SearchTransferOrders |
| DELETE | /v2/transfer-orders/{transfer_order_id} | DeleteTransferOrder |
| GET | /v2/transfer-orders/{transfer_order_id} | RetrieveTransferOrder |
| PUT | /v2/transfer-orders/{transfer_order_id} | UpdateTransferOrder |
| POST | /v2/transfer-orders/{transfer_order_id}/cancel | CancelTransferOrder |
| POST | /v2/transfer-orders/{transfer_order_id}/receive | ReceiveTransferOrder |
| POST | /v2/transfer-orders/{transfer_order_id}/start | StartTransferOrder |

### vendors
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/vendors/bulk-create | BulkCreateVendors |
| POST | /v2/vendors/bulk-retrieve | BulkRetrieveVendors |
| PUT | /v2/vendors/bulk-update | BulkUpdateVendors |
| POST | /v2/vendors/create | CreateVendor |
| POST | /v2/vendors/search | SearchVendors |
| GET | /v2/vendors/{vendor_id} | RetrieveVendor |
| PUT | /v2/vendors/{vendor_id} | UpdateVendor |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/webhooks/event-types | ListWebhookEventTypes |
| GET | /v2/webhooks/subscriptions | ListWebhookSubscriptions |
| POST | /v2/webhooks/subscriptions | CreateWebhookSubscription |
| DELETE | /v2/webhooks/subscriptions/{subscription_id} | DeleteWebhookSubscription |
| GET | /v2/webhooks/subscriptions/{subscription_id} | RetrieveWebhookSubscription |
| PUT | /v2/webhooks/subscriptions/{subscription_id} | UpdateWebhookSubscription |
| POST | /v2/webhooks/subscriptions/{subscription_id}/signature-key | UpdateWebhookSubscriptionSignatureKey |
| POST | /v2/webhooks/subscriptions/{subscription_id}/test | TestWebhookSubscription |

## Enhanced Skill Content
## Question Mapping

- "How do I accept a payment?" -> POST /v2/payments
- "How do I refund a customer?" -> POST /v2/refunds
- "How do I look up a customer by email or phone?" -> POST /v2/customers/search
- "What locations does my business have?" -> GET /v2/locations
- "How do I create a catalog item?" -> POST /v2/catalog/object
- "What is the inventory count for a product?" -> GET /v2/inventory/{catalog_object_id}
- "How do I create an invoice and send it?" -> POST /v2/invoices then POST /v2/invoices/{invoice_id}/publish
- "How do I schedule a booking for a customer?" -> POST /v2/bookings
- "How do I check available appointment slots?" -> POST /v2/bookings/availability/search
- "How do I set up a webhook to listen for payment events?" -> POST /v2/webhooks/subscriptions
- "How do I create a payment link for online checkout?" -> POST /v2/online-checkout/payment-links
- "How do I check a loyalty account balance?" -> GET /v2/loyalty/accounts/{account_id}
- "How do I transfer inventory between locations?" -> POST /v2/transfer-orders
- "How do I clock in an employee?" -> POST /v2/labor/shifts
- "How do I cancel a subscription?" -> POST /v2/subscriptions/{subscription_id}/cancel

## Response Tips

- **Payments/Orders/Refunds**: Money fields use `{amount, currency}` where amount is in the smallest currency unit (cents). A `status` field tracks lifecycle state. Check `processing_fee` array for fee breakdowns.
- **Catalog**: Objects are polymorphic -- the `type` field determines which `*_data` sub-object is populated (e.g., `item_data`, `item_variation_data`). Use `include_related_objects` to pull linked items in one call.
- **Customers/Team Members**: Paginate with `cursor` (opaque string returned in response). The `version` field is required for safe concurrent updates (optimistic locking).
- **Inventory**: Quantities are strings (not numbers) to support decimal units. State transitions (`from_state` -> `to_state`) track the full audit trail.
- **Bookings/Labor**: Timestamps use ISO 8601 with timezone. Shifts and bookings carry a `version` field -- always pass the latest version on updates to avoid conflicts.
- **Subscriptions/Invoices**: Both return `actions` arrays representing pending scheduled changes. Invoice `version` must be passed to publish, cancel, or update.
- **All endpoints**: Every response includes an `errors` array. An HTTP 200 with a non-empty `errors` array is a partial failure -- always check it.

## Anomaly Flags

- **Non-empty `errors` array on 200 responses**: Square returns errors inline even on success status codes. Always surface these to the user -- they indicate partial failures or warnings.
- **`version` mismatch on updates**: If a PUT or state-change call fails with a version conflict, alert that another process modified the resource. Re-fetch and retry.
- **Deprecated v1 endpoints**: The `/v1/{location_id}/orders` endpoints are legacy. Flag when these are used and suggest the `/v2/orders` equivalents.
- **`delay_action` on payments**: When a payment has `delayed_until` set, it will auto-complete or auto-cancel. Surface the deadline so the user can act before it fires.
- **`expiring_point_deadlines` on loyalty accounts**: Proactively warn when loyalty points are about to expire so the merchant can notify customers.
- **`issuer_alert` on cards**: When present, this signals the card issuer has flagged the card (e.g., fraud concern). Surface immediately.
- **Subscription `actions` array**: Pending plan changes (swap, pause, cancel) scheduled for the future. Flag so the user is aware of upcoming billing changes.
- **`risk_evaluation` on payments**: When `risk_level` is elevated, surface the risk assessment so the merchant can review before fulfilling.
- **Invoice `status` stuck in DRAFT**: If an invoice was created but never published, flag it as potentially forgotten.

## Playbook

### 1. Process a Payment and Issue a Receipt

1. Create the order: `POST /v2/orders` with `location_id` and `line_items`
2. Take payment: `POST /v2/payments` with `source_id` (card nonce), `amount_money`, and `order_id` from step 1
3. Verify `payment.status` is `COMPLETED` and `errors` is empty
4. Retrieve receipt URL from `payment.receipt_url` to share with the customer
5. If autocomplete is disabled, explicitly complete: `POST /v2/payments/{payment_id}/complete`

### 2. Create and Send an Invoice

1. Create the order: `POST /v2/orders` with line items and `location_id`
2. Create the invoice: `POST /v2/invoices` with `order_id`, `primary_recipient` (customer info), and `payment_requests` (due date, amount)
3. Optionally attach files: `POST /v2/invoices/{invoice_id}/attachments`
4. Publish and send: `POST /v2/invoices/{invoice_id}/publish` with the invoice `version`
5. Monitor status via `GET /v2/invoices/{invoice_id}` -- status progresses through DRAFT -> UNPAID -> PAID

### 3. Set Up a Loyalty Program Reward Flow

1. Retrieve the program: `GET /v2/loyalty/programs` to get `program_id` and reward tiers
2. Find or create the loyalty account: `POST /v2/loyalty/accounts/search` by `customer_id`, or `POST /v2/loyalty/accounts` to enroll
3. Accumulate points after a purchase: `POST /v2/loyalty/accounts/{account_id}/accumulate` with `order_id` and `location_id`
4. When enough points, create a reward: `POST /v2/loyalty/rewards` with `reward_tier_id` and `loyalty_account_id`
5. Redeem at checkout: `POST /v2/loyalty/rewards/{reward_id}/redeem` with `location_id`

### 4. Manage Inventory Across Locations

1. List locations: `GET /v2/locations` to get all `location_id` values
2. Check current counts: `POST /v2/inventory/counts/batch-retrieve` with `catalog_object_ids` and `location_ids`
3. Adjust stock (receiving shipment): `POST /v2/inventory/changes/batch-create` with adjustment entries (`from_state: NONE`, `to_state: IN_STOCK`)
4. Transfer between locations: `POST /v2/transfer-orders` with source/destination location IDs and line items
5. Start the transfer: `POST /v2/transfer-orders/{id}/start`, then confirm receipt: `POST /v2/transfer-orders/{id}/receive`

### 5. Onboard a Customer with a Saved Card

1. Create the customer: `POST /v2/customers` with name, email, and phone
2. Save a card on file: `POST /v2/cards` with `source_id` (card nonce from Web Payments SDK), `customer_id`, and `idempotency_key`
3. Verify the card was saved: check `card.enabled` is `true` in the response
4. For future payments, use `POST /v2/payments` with `source_id` set to the saved `card.id` and `customer_id`
5. To remove the card later: `POST /v2/cards/{card_id}/disable`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
