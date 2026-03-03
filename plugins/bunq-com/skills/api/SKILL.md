---
name: bunq-api
description: "bunq API skill. Use when working with bunq for user, attachment-public, avatar. Covers 480 endpoints."
version: 1.0.0
generator: lapsh
---

# bunq API
API version: 1.0

## Auth
ApiKey X-Bunq-Client-Authentication in header

## Base URL
https://public-api.sandbox.bunq.com/{basePath}

## Setup
1. Set your API key in the appropriate header
2. GET /device -- verify access
3. POST /user/{userID}/additional-transaction-information-category-user-defined -- create first additional-transaction-information-category-user-defined

## Endpoints

480 endpoints across 16 groups. See references/api-spec.lap for full details.

### user
| Method | Path | Description |
|--------|------|-------------|
| GET | /user/{userID}/additional-transaction-information-category | Get the available categories. |
| POST | /user/{userID}/additional-transaction-information-category-user-defined | Manage user-defined categories. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/attachment | Create a new monetary account attachment. Create a POST request with a payload that contains the binary representation of the file, without any JSON wrapping. Make sure you define the MIME type (i.e. image/jpeg) in the Content-Type header. You are required to provide a description of the attachment using the X-Bunq-Attachment-Description header. |
| GET | /user/{userID}/attachment/{itemId} | Get a specific attachment. The header of the response contains the content-type of the attachment. |
| GET | /user/{userID}/billing-contract-subscription | Get all subscription billing contract for the authenticated user. |
| GET | /user/{userID}/bunqme-fundraiser-profile/{itemId} | bunq.me public profile of the user. |
| GET | /user/{userID}/bunqme-fundraiser-profile | bunq.me public profile of the user. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-fundraiser-result/{itemId} | bunq.me fundraiser result containing all payments. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-tab | bunq.me tabs allows you to create a payment request and share the link through e-mail, chat, etc. Multiple persons are able to respond to the payment request and pay through bunq, iDeal or SOFORT. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-tab | bunq.me tabs allows you to create a payment request and share the link through e-mail, chat, etc. Multiple persons are able to respond to the payment request and pay through bunq, iDeal or SOFORT. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-tab/{itemId} | bunq.me tabs allows you to create a payment request and share the link through e-mail, chat, etc. Multiple persons are able to respond to the payment request and pay through bunq, iDeal or SOFORT. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-tab/{itemId} | bunq.me tabs allows you to create a payment request and share the link through e-mail, chat, etc. Multiple persons are able to respond to the payment request and pay through bunq, iDeal or SOFORT. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-tab-result-response/{itemId} | Used to view bunq.me TabResultResponse objects belonging to a tab. A TabResultResponse is an object that holds details on a tab which has been paid from the provided monetary account. |
| GET | /user/{userID}/oauth-client/{oauth-clientID}/callback-url/{itemId} | Used for managing OAuth Client Callback URLs. |
| PUT | /user/{userID}/oauth-client/{oauth-clientID}/callback-url/{itemId} | Used for managing OAuth Client Callback URLs. |
| DELETE | /user/{userID}/oauth-client/{oauth-clientID}/callback-url/{itemId} | Used for managing OAuth Client Callback URLs. |
| POST | /user/{userID}/oauth-client/{oauth-clientID}/callback-url | Used for managing OAuth Client Callback URLs. |
| GET | /user/{userID}/oauth-client/{oauth-clientID}/callback-url | Used for managing OAuth Client Callback URLs. |
| PUT | /user/{userID}/card/{itemId} | Update the card details. Allow to change pin code, status, limits, country permissions and the monetary account connected to the card. When the card has been received, it can be also activated through this endpoint. |
| GET | /user/{userID}/card/{itemId} | Return the details of a specific card. |
| GET | /user/{userID}/card | Return all the cards available to the user. |
| POST | /user/{userID}/card-batch | Used to update multiple cards in a batch. |
| POST | /user/{userID}/card-batch-replace | Used to replace multiple cards in a batch. |
| POST | /user/{userID}/card-credit | Create a new credit card request. |
| POST | /user/{userID}/card-debit | Create a new debit card request. |
| GET | /user/{userID}/card-name | Return all the accepted card names for a specific user. |
| POST | /user/{userID}/certificate-pinned | Pin the certificate chain. |
| GET | /user/{userID}/certificate-pinned | List all the pinned certificate chain for the given user. |
| DELETE | /user/{userID}/certificate-pinned/{itemId} | Remove the pinned certificate chain with the specific ID. |
| GET | /user/{userID}/certificate-pinned/{itemId} | Get the pinned certificate chain with the specified ID. |
| GET | /user/{userID}/challenge-request/{itemId} | Endpoint for apps to fetch a challenge request. |
| PUT | /user/{userID}/challenge-request/{itemId} | Endpoint for apps to fetch a challenge request. |
| POST | /user/{userID}/company | Create and manage companies. |
| GET | /user/{userID}/company | Create and manage companies. |
| GET | /user/{userID}/company/{itemId} | Create and manage companies. |
| PUT | /user/{userID}/company/{itemId} | Create and manage companies. |
| POST | /user/{userID}/confirmation-of-funds | Used to confirm availability of funds on an account. |
| GET | /user/{userID}/chat-conversation/{chat-conversationID}/attachment/{attachmentID}/content | Get the raw content of a specific attachment. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/attachment/{attachmentID}/content | Get the raw content of a specific attachment. |
| GET | /user/{userID}/attachment/{attachmentID}/content | Get the raw content of a specific attachment. |
| GET | /user/{userID}/export-annual-overview/{export-annual-overviewID}/content | Used to retrieve the raw content of an annual overview. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/export-rib/{export-ribID}/content | Used to retrieve the raw content of an RIB. |
| GET | /user/{userID}/card/{cardID}/export-statement-card/{export-statement-cardID}/content | Fetch the raw content of a card statement export. The returned file format could be CSV or PDF depending on the statement format specified during the statement creation. The doc won't display the response of a request to get the content of a statement export. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/customer-statement/{customer-statementID}/content | Fetch the raw content of a statement export. The returned file format could be MT940, CSV or PDF depending on the statement format specified during the statement creation. The doc won't display the response of a request to get the content of a statement export. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/event/{eventID}/statement/{statementID}/content | Fetch the raw content of a payment statement export. |
| GET | /user/{userID}/credential-password-ip/{itemId} | Create a credential of a user for server authentication, or delete the credential of a user for server authentication. |
| GET | /user/{userID}/credential-password-ip | Create a credential of a user for server authentication, or delete the credential of a user for server authentication. |
| POST | /user/{userID}/currency-cloud-beneficiary | Endpoint to manage CurrencyCloud beneficiaries. |
| GET | /user/{userID}/currency-cloud-beneficiary | Endpoint to manage CurrencyCloud beneficiaries. |
| GET | /user/{userID}/currency-cloud-beneficiary/{itemId} | Endpoint to manage CurrencyCloud beneficiaries. |
| GET | /user/{userID}/currency-cloud-beneficiary-requirement | Endpoint to list requirements for CurrencyCloud beneficiaries. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/currency-cloud-payment-quote | Endpoint for managing currency conversions. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/currency-conversion | Endpoint for managing currency conversions. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/currency-conversion/{itemId} | Endpoint for managing currency conversions. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/currency-conversion-quote | Endpoint to create a quote for currency conversions. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/currency-conversion-quote/{itemId} | Endpoint to create a quote for currency conversions. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/currency-conversion-quote/{itemId} | Endpoint to create a quote for currency conversions. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/customer-statement | Used to create new and read existing statement exports. Statement exports can be created in either CSV, MT940 or PDF file format. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/customer-statement | Used to create new and read existing statement exports. Statement exports can be created in either CSV, MT940 or PDF file format. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/customer-statement/{itemId} | Used to create new and read existing statement exports. Statement exports can be created in either CSV, MT940 or PDF file format. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/customer-statement/{itemId} | Used to create new and read existing statement exports. Statement exports can be created in either CSV, MT940 or PDF file format. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-auto-allocate/{payment-auto-allocateID}/definition | List all the definitions in a payment auto allocate. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment | Create a new DraftPayment. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment | Get a listing of all DraftPayments from a given MonetaryAccount. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment/{itemId} | Update a DraftPayment. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment/{itemId} | Get a specific DraftPayment. |
| GET | /user/{userID}/event/{itemId} | Get a specific event for a given user. |
| GET | /user/{userID}/event | Get a collection of events for a given user. You can add query the parameters monetary_account_id, status and/or display_user_event to filter the response. When monetary_account_id={id,id} is provided only events that relate to these monetary account ids are returned. When status={AWAITING_REPLY/FINALIZED} is provided the response only contains events with the status AWAITING_REPLY or FINALIZED. When display_user_event={true/false} is set to false user events are excluded from the response, when not provided user events are displayed. User events are events that are not related to a monetary account (for example: connect invites). |
| POST | /user/{userID}/export-annual-overview | Create a new annual overview for a specific year. An overview can be generated only for a past year. |
| GET | /user/{userID}/export-annual-overview | List all the annual overviews for a user. |
| GET | /user/{userID}/export-annual-overview/{itemId} | Get an annual overview for a user by its id. |
| DELETE | /user/{userID}/export-annual-overview/{itemId} | Used to create new and read existing annual overviews of all the user's monetary accounts. Once created, annual overviews can be downloaded in PDF format via the 'export-annual-overview/{id}/content' endpoint. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/export-rib | Create a new RIB. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/export-rib | List all the RIBs for a monetary account. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/export-rib/{itemId} | Get a RIB for a monetary account by its id. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/export-rib/{itemId} | Used to create new and read existing RIBs of a monetary account |
| GET | /user/{userID}/card/{cardID}/export-statement-card/{itemId} | Used to create new and read existing card statement exports. Statement exports can be created in either CSV or PDF file format. |
| GET | /user/{userID}/card/{cardID}/export-statement-card | Used to create new and read existing card statement exports. Statement exports can be created in either CSV or PDF file format. |
| POST | /user/{userID}/card/{cardID}/export-statement-card-csv | Used to serialize ExportStatementCardCsv |
| GET | /user/{userID}/card/{cardID}/export-statement-card-csv | Used to serialize ExportStatementCardCsv |
| GET | /user/{userID}/card/{cardID}/export-statement-card-csv/{itemId} | Used to serialize ExportStatementCardCsv |
| DELETE | /user/{userID}/card/{cardID}/export-statement-card-csv/{itemId} | Used to serialize ExportStatementCardCsv |
| POST | /user/{userID}/card/{cardID}/export-statement-card-pdf | Used to serialize ExportStatementCardPdf |
| GET | /user/{userID}/card/{cardID}/export-statement-card-pdf | Used to serialize ExportStatementCardPdf |
| GET | /user/{userID}/card/{cardID}/export-statement-card-pdf/{itemId} | Used to serialize ExportStatementCardPdf |
| DELETE | /user/{userID}/card/{cardID}/export-statement-card-pdf/{itemId} | Used to serialize ExportStatementCardPdf |
| GET | /user/{userID}/feature-announcement/{itemId} | view for updating the feature display. |
| POST | /user/{userID}/card/{cardID}/generated-cvc2 | Generate a new CVC2 code for a card. |
| GET | /user/{userID}/card/{cardID}/generated-cvc2 | Get all generated CVC2 codes for a card. |
| GET | /user/{userID}/card/{cardID}/generated-cvc2/{itemId} | Get the details for a specific generated CVC2 code. |
| PUT | /user/{userID}/card/{cardID}/generated-cvc2/{itemId} | Endpoint for generating and retrieving a new CVC2 code. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/ideal-merchant-transaction | View for requesting iDEAL transactions and polling their status. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/ideal-merchant-transaction | View for requesting iDEAL transactions and polling their status. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/ideal-merchant-transaction/{itemId} | View for requesting iDEAL transactions and polling their status. |
| GET | /user/{userID}/insight-preference-date | Used to allow users to set insight/budget preferences. |
| GET | /user/{userID}/insights | Used to get insights about transactions between given time range. |
| GET | /user/{userID}/insights-search | Used to get events based on time and insight category. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-auto-allocate/{payment-auto-allocateID}/instance | List all the times a users payment was automatically allocated. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-auto-allocate/{payment-auto-allocateID}/instance/{itemId} | List all the times a users payment was automatically allocated. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/invoice | Used to view a bunq invoice. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/invoice/{itemId} | Used to view a bunq invoice. |
| GET | /user/{userID}/invoice | Used to list bunq invoices by user. |
| GET | /user/{userID}/invoice/{itemId} | Used to list bunq invoices by user. |
| GET | /user/{userID}/invoice/{invoiceID}/invoice-export/{itemId} | Get a PDF export of an invoice. |
| PUT | /user/{userID}/invoice/{invoiceID}/invoice-export/{itemId} | Get a PDF export of an invoice. |
| DELETE | /user/{userID}/invoice/{invoiceID}/invoice-export/{itemId} | Get a PDF export of an invoice. |
| POST | /user/{userID}/invoice/{invoiceID}/invoice-export | Get a PDF export of an invoice. |
| GET | /user/{userID}/credential-password-ip/{credential-password-ipID}/ip/{itemId} | Manage the IPs which may be used for a credential of a user for server authentication. |
| PUT | /user/{userID}/credential-password-ip/{credential-password-ipID}/ip/{itemId} | Manage the IPs which may be used for a credential of a user for server authentication. |
| POST | /user/{userID}/credential-password-ip/{credential-password-ipID}/ip | Manage the IPs which may be used for a credential of a user for server authentication. |
| GET | /user/{userID}/credential-password-ip/{credential-password-ipID}/ip | Manage the IPs which may be used for a credential of a user for server authentication. |
| GET | /user/{userID}/legal-name | Endpoint for getting available legal names that can be used by the user. |
| GET | /user/{userID}/limit | Get all limits for the authenticated user. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/mastercard-action/{itemId} | MasterCard transaction view. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/mastercard-action | MasterCard transaction view. |
| GET | /user/{userID}/monetary-account/{itemId} | Get a specific MonetaryAccount. |
| GET | /user/{userID}/monetary-account | Get a collection of all your MonetaryAccounts. |
| POST | /user/{userID}/monetary-account-bank | Create new MonetaryAccountBank. |
| GET | /user/{userID}/monetary-account-bank | Gets a listing of all MonetaryAccountBanks of a given user. |
| GET | /user/{userID}/monetary-account-bank/{itemId} | Get a specific MonetaryAccountBank. |
| PUT | /user/{userID}/monetary-account-bank/{itemId} | Update a specific existing MonetaryAccountBank. |
| GET | /user/{userID}/monetary-account-card/{itemId} | Get a specific MonetaryAccountCard. |
| PUT | /user/{userID}/monetary-account-card/{itemId} | Update a specific existing MonetaryAccountCard. |
| GET | /user/{userID}/monetary-account-card | Gets a listing of all MonetaryAccountCard of a given user. |
| POST | /user/{userID}/monetary-account-external | Endpoint for managing monetary accounts which are connected to external services. |
| GET | /user/{userID}/monetary-account-external | Endpoint for managing monetary accounts which are connected to external services. |
| GET | /user/{userID}/monetary-account-external/{itemId} | Endpoint for managing monetary accounts which are connected to external services. |
| PUT | /user/{userID}/monetary-account-external/{itemId} | Endpoint for managing monetary accounts which are connected to external services. |
| POST | /user/{userID}/monetary-account-external-savings | Endpoint for managing monetary account savings which are connected to external services. |
| GET | /user/{userID}/monetary-account-external-savings | Endpoint for managing monetary account savings which are connected to external services. |
| GET | /user/{userID}/monetary-account-external-savings/{itemId} | Endpoint for managing monetary account savings which are connected to external services. |
| PUT | /user/{userID}/monetary-account-external-savings/{itemId} | Endpoint for managing monetary account savings which are connected to external services. |
| POST | /user/{userID}/monetary-account-joint | The endpoint for joint monetary accounts. |
| GET | /user/{userID}/monetary-account-joint | The endpoint for joint monetary accounts. |
| GET | /user/{userID}/monetary-account-joint/{itemId} | The endpoint for joint monetary accounts. |
| PUT | /user/{userID}/monetary-account-joint/{itemId} | The endpoint for joint monetary accounts. |
| POST | /user/{userID}/monetary-account-savings | Create new MonetaryAccountSavings. |
| GET | /user/{userID}/monetary-account-savings | Gets a listing of all MonetaryAccountSavingss of a given user. |
| GET | /user/{userID}/monetary-account-savings/{itemId} | Get a specific MonetaryAccountSavings. |
| PUT | /user/{userID}/monetary-account-savings/{itemId} | Update a specific existing MonetaryAccountSavings. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/adyen-card-transaction/{adyen-card-transactionID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/adyen-card-transaction/{adyen-card-transactionID}/note-attachment | Used to manage attachment notes. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/adyen-card-transaction/{adyen-card-transactionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/adyen-card-transaction/{adyen-card-transactionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/adyen-card-transaction/{adyen-card-transactionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/switch-service-payment/{switch-service-paymentID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/switch-service-payment/{switch-service-paymentID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/switch-service-payment/{switch-service-paymentID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/switch-service-payment/{switch-service-paymentID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/switch-service-payment/{switch-service-paymentID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-fundraiser-result/{bunqme-fundraiser-resultID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-fundraiser-result/{bunqme-fundraiser-resultID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-fundraiser-result/{bunqme-fundraiser-resultID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-fundraiser-result/{bunqme-fundraiser-resultID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-fundraiser-result/{bunqme-fundraiser-resultID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment/{draft-paymentID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment/{draft-paymentID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment/{draft-paymentID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment/{draft-paymentID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment/{draft-paymentID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/ideal-merchant-transaction/{ideal-merchant-transactionID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/ideal-merchant-transaction/{ideal-merchant-transactionID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/ideal-merchant-transaction/{ideal-merchant-transactionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/ideal-merchant-transaction/{ideal-merchant-transactionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/ideal-merchant-transaction/{ideal-merchant-transactionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/mastercard-action/{mastercard-actionID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/mastercard-action/{mastercard-actionID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/mastercard-action/{mastercard-actionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/mastercard-action/{mastercard-actionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/mastercard-action/{mastercard-actionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/open-banking-merchant-transaction/{open-banking-merchant-transactionID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/open-banking-merchant-transaction/{open-banking-merchant-transactionID}/note-attachment | Used to manage attachment notes. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/open-banking-merchant-transaction/{open-banking-merchant-transactionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/open-banking-merchant-transaction/{open-banking-merchant-transactionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/open-banking-merchant-transaction/{open-banking-merchant-transactionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch/{payment-batchID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch/{payment-batchID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch/{payment-batchID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch/{payment-batchID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch/{payment-batchID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/payment-delayed/{payment-delayedID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-delayed/{payment-delayedID}/note-attachment | Used to manage attachment notes. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/payment-delayed/{payment-delayedID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/payment-delayed/{payment-delayedID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-delayed/{payment-delayedID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/payment/{paymentID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment/{paymentID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/payment/{paymentID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/payment/{paymentID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment/{paymentID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch/{request-inquiry-batchID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch/{request-inquiry-batchID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch/{request-inquiry-batchID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch/{request-inquiry-batchID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch/{request-inquiry-batchID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry/{request-inquiryID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry/{request-inquiryID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry/{request-inquiryID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry/{request-inquiryID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry/{request-inquiryID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/request-response/{request-responseID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-response/{request-responseID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/request-response/{request-responseID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/request-response/{request-responseID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-response/{request-responseID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{scheduleID}/schedule-instance/{schedule-instanceID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{scheduleID}/schedule-instance/{schedule-instanceID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{scheduleID}/schedule-instance/{schedule-instanceID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{scheduleID}/schedule-instance/{schedule-instanceID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{scheduleID}/schedule-instance/{schedule-instanceID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch/{schedule-payment-batchID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch/{schedule-payment-batchID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch/{schedule-payment-batchID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch/{schedule-payment-batchID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch/{schedule-payment-batchID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment/{schedule-paymentID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment/{schedule-paymentID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment/{schedule-paymentID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment/{schedule-paymentID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment/{schedule-paymentID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry-batch/{schedule-request-inquiry-batchID}/note-attachment | Used to manage attachment notes for a scheduled request. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry-batch/{schedule-request-inquiry-batchID}/note-attachment | Manage the notes for a scheduled request. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry-batch/{schedule-request-inquiry-batchID}/note-attachment/{itemId} | Used to manage attachment notes for a scheduled request. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry-batch/{schedule-request-inquiry-batchID}/note-attachment/{itemId} | Used to manage attachment notes for a scheduled request. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry-batch/{schedule-request-inquiry-batchID}/note-attachment/{itemId} | Used to manage attachment notes for a scheduled request. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry/{schedule-request-inquiryID}/note-attachment | Used to manage attachment notes for a scheduled request. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry/{schedule-request-inquiryID}/note-attachment | Manage the notes for a scheduled request. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry/{schedule-request-inquiryID}/note-attachment/{itemId} | Used to manage attachment notes for a scheduled request. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry/{schedule-request-inquiryID}/note-attachment/{itemId} | Used to manage attachment notes for a scheduled request. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry/{schedule-request-inquiryID}/note-attachment/{itemId} | Used to manage attachment notes for a scheduled request. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/sofort-merchant-transaction/{sofort-merchant-transactionID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/sofort-merchant-transaction/{sofort-merchant-transactionID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/sofort-merchant-transaction/{sofort-merchant-transactionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/sofort-merchant-transaction/{sofort-merchant-transactionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/sofort-merchant-transaction/{sofort-merchant-transactionID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/whitelist/{whitelistID}/whitelist-result/{whitelist-resultID}/note-attachment | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/whitelist/{whitelistID}/whitelist-result/{whitelist-resultID}/note-attachment | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/whitelist/{whitelistID}/whitelist-result/{whitelist-resultID}/note-attachment/{itemId} | Used to manage attachment notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/whitelist/{whitelistID}/whitelist-result/{whitelist-resultID}/note-attachment/{itemId} | Used to manage attachment notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/whitelist/{whitelistID}/whitelist-result/{whitelist-resultID}/note-attachment/{itemId} | Used to manage attachment notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/adyen-card-transaction/{adyen-card-transactionID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/adyen-card-transaction/{adyen-card-transactionID}/note-text | Used to manage text notes. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/adyen-card-transaction/{adyen-card-transactionID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/adyen-card-transaction/{adyen-card-transactionID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/adyen-card-transaction/{adyen-card-transactionID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/switch-service-payment/{switch-service-paymentID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/switch-service-payment/{switch-service-paymentID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/switch-service-payment/{switch-service-paymentID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/switch-service-payment/{switch-service-paymentID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/switch-service-payment/{switch-service-paymentID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-fundraiser-result/{bunqme-fundraiser-resultID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-fundraiser-result/{bunqme-fundraiser-resultID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-fundraiser-result/{bunqme-fundraiser-resultID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-fundraiser-result/{bunqme-fundraiser-resultID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/bunqme-fundraiser-result/{bunqme-fundraiser-resultID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment/{draft-paymentID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment/{draft-paymentID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment/{draft-paymentID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment/{draft-paymentID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/draft-payment/{draft-paymentID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/ideal-merchant-transaction/{ideal-merchant-transactionID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/ideal-merchant-transaction/{ideal-merchant-transactionID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/ideal-merchant-transaction/{ideal-merchant-transactionID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/ideal-merchant-transaction/{ideal-merchant-transactionID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/ideal-merchant-transaction/{ideal-merchant-transactionID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/mastercard-action/{mastercard-actionID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/mastercard-action/{mastercard-actionID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/mastercard-action/{mastercard-actionID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/mastercard-action/{mastercard-actionID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/mastercard-action/{mastercard-actionID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/open-banking-merchant-transaction/{open-banking-merchant-transactionID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/open-banking-merchant-transaction/{open-banking-merchant-transactionID}/note-text | Used to manage text notes. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/open-banking-merchant-transaction/{open-banking-merchant-transactionID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/open-banking-merchant-transaction/{open-banking-merchant-transactionID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/open-banking-merchant-transaction/{open-banking-merchant-transactionID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch/{payment-batchID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch/{payment-batchID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch/{payment-batchID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch/{payment-batchID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch/{payment-batchID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/payment-delayed/{payment-delayedID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-delayed/{payment-delayedID}/note-text | Used to manage text notes. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/payment-delayed/{payment-delayedID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/payment-delayed/{payment-delayedID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-delayed/{payment-delayedID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/payment/{paymentID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment/{paymentID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/payment/{paymentID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/payment/{paymentID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment/{paymentID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch/{request-inquiry-batchID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch/{request-inquiry-batchID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch/{request-inquiry-batchID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch/{request-inquiry-batchID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch/{request-inquiry-batchID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry/{request-inquiryID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry/{request-inquiryID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry/{request-inquiryID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry/{request-inquiryID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry/{request-inquiryID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/request-response/{request-responseID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-response/{request-responseID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/request-response/{request-responseID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/request-response/{request-responseID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-response/{request-responseID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{scheduleID}/schedule-instance/{schedule-instanceID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{scheduleID}/schedule-instance/{schedule-instanceID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{scheduleID}/schedule-instance/{schedule-instanceID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{scheduleID}/schedule-instance/{schedule-instanceID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{scheduleID}/schedule-instance/{schedule-instanceID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch/{schedule-payment-batchID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch/{schedule-payment-batchID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch/{schedule-payment-batchID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch/{schedule-payment-batchID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch/{schedule-payment-batchID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment/{schedule-paymentID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment/{schedule-paymentID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment/{schedule-paymentID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment/{schedule-paymentID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment/{schedule-paymentID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry-batch/{schedule-request-inquiry-batchID}/note-text | Used to manage text notes for a scheduled request. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry-batch/{schedule-request-inquiry-batchID}/note-text | Manage the notes for a given schedule request. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry-batch/{schedule-request-inquiry-batchID}/note-text/{itemId} | Used to manage text notes for a scheduled request. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry-batch/{schedule-request-inquiry-batchID}/note-text/{itemId} | Used to manage text notes for a scheduled request. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry-batch/{schedule-request-inquiry-batchID}/note-text/{itemId} | Used to manage text notes for a scheduled request. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry/{schedule-request-inquiryID}/note-text | Used to manage text notes for a scheduled request. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry/{schedule-request-inquiryID}/note-text | Manage the notes for a given schedule request. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry/{schedule-request-inquiryID}/note-text/{itemId} | Used to manage text notes for a scheduled request. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry/{schedule-request-inquiryID}/note-text/{itemId} | Used to manage text notes for a scheduled request. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-request-inquiry/{schedule-request-inquiryID}/note-text/{itemId} | Used to manage text notes for a scheduled request. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/sofort-merchant-transaction/{sofort-merchant-transactionID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/sofort-merchant-transaction/{sofort-merchant-transactionID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/sofort-merchant-transaction/{sofort-merchant-transactionID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/sofort-merchant-transaction/{sofort-merchant-transactionID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/sofort-merchant-transaction/{sofort-merchant-transactionID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/whitelist/{whitelistID}/whitelist-result/{whitelist-resultID}/note-text | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/whitelist/{whitelistID}/whitelist-result/{whitelist-resultID}/note-text | Manage the notes for a given user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/whitelist/{whitelistID}/whitelist-result/{whitelist-resultID}/note-text/{itemId} | Used to manage text notes. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/whitelist/{whitelistID}/whitelist-result/{whitelist-resultID}/note-text/{itemId} | Used to manage text notes. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/whitelist/{whitelistID}/whitelist-result/{whitelist-resultID}/note-text/{itemId} | Used to manage text notes. |
| POST | /user/{userID}/notification-filter-email | Manage the email notification filters for a user. |
| GET | /user/{userID}/notification-filter-email | Manage the email notification filters for a user. |
| POST | /user/{userID}/notification-filter-failure | Manage the url notification filters for a user. |
| GET | /user/{userID}/notification-filter-failure | Manage the url notification filters for a user. |
| POST | /user/{userID}/notification-filter-push | Manage the push notification filters for a user. |
| GET | /user/{userID}/notification-filter-push | Manage the push notification filters for a user. |
| POST | /user/{userID}/notification-filter-url | Manage the url notification filters for a user. |
| GET | /user/{userID}/notification-filter-url | Manage the url notification filters for a user. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/notification-filter-url | Manage the url notification filters for a user. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/notification-filter-url | Manage the url notification filters for a user. |
| GET | /user/{userID}/oauth-client/{itemId} | Used for managing OAuth Clients. |
| PUT | /user/{userID}/oauth-client/{itemId} | Used for managing OAuth Clients. |
| POST | /user/{userID}/oauth-client | Used for managing OAuth Clients. |
| GET | /user/{userID}/oauth-client | Used for managing OAuth Clients. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/payment | Create a new Payment. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment | Get a listing of all Payments performed on a given MonetaryAccount (incoming and outgoing). |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment/{itemId} | Get a specific previous Payment. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/mastercard-action/{mastercard-actionID}/payment | MasterCard transaction view. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/payment-auto-allocate | Manage a users automatic payment auto allocated settings. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-auto-allocate | Manage a users automatic payment auto allocated settings. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-auto-allocate/{itemId} | Manage a users automatic payment auto allocated settings. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/payment-auto-allocate/{itemId} | Manage a users automatic payment auto allocated settings. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/payment-auto-allocate/{itemId} | Manage a users automatic payment auto allocated settings. |
| GET | /user/{userID}/payment-auto-allocate | List a users automatic payment auto allocated settings. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch | Create a payment batch by sending an array of single payment objects, that will become part of the batch. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch | Return all the payment batches for a monetary account. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch/{itemId} | Revoke a bunq.to payment batch. The status of all the payments will be set to REVOKED. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/payment-batch/{itemId} | Return the details of a specific payment batch. |
| POST | /user/{userID}/payment-service-provider-draft-payment | Manage the PaymentServiceProviderDraftPayment's for a PISP. |
| GET | /user/{userID}/payment-service-provider-draft-payment | Manage the PaymentServiceProviderDraftPayment's for a PISP. |
| PUT | /user/{userID}/payment-service-provider-draft-payment/{itemId} | Manage the PaymentServiceProviderDraftPayment's for a PISP. |
| GET | /user/{userID}/payment-service-provider-draft-payment/{itemId} | Manage the PaymentServiceProviderDraftPayment's for a PISP. |
| POST | /user/{userID}/payment-service-provider-issuer-transaction | The endpoint for payment service provider issuer transactions |
| GET | /user/{userID}/payment-service-provider-issuer-transaction | The endpoint for payment service provider issuer transactions |
| GET | /user/{userID}/payment-service-provider-issuer-transaction/{itemId} | The endpoint for payment service provider issuer transactions |
| PUT | /user/{userID}/payment-service-provider-issuer-transaction/{itemId} | The endpoint for payment service provider issuer transactions |
| GET | /user/{userID}/invoice/{invoiceID}/pdf-content | Get a PDF export of an invoice. |
| POST | /user/{userID}/card/{cardID}/replace | Request a card replacement. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry | Create a new payment request. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry | Get all payment requests for a user's monetary account. bunqme_share_url is always null if the counterparty is a bunq user. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry/{itemId} | Revoke a request for payment, by updating the status to REVOKED. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry/{itemId} | Get the details of a specific payment request, including its status. bunqme_share_url is always null if the counterparty is a bunq user. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch | Create a request batch by sending an array of single request objects, that will become part of the batch. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch | Return all the request batches for a monetary account. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch/{itemId} | Revoke a request batch. The status of all the requests will be set to REVOKED. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch/{itemId} | Return the details of a specific request batch. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/request-response/{itemId} | Update the status to accept or reject the RequestResponse. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-response/{itemId} | Get the details for a specific existing RequestResponse. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/request-response | Get all RequestResponses for a MonetaryAccount. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{itemId} | Get a specific schedule definition for a given monetary account. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule | Get a collection of scheduled definition for a given monetary account. You can add the parameter type to filter the response. When type={SCHEDULE_DEFINITION_PAYMENT,SCHEDULE_DEFINITION_PAYMENT_BATCH} is provided only schedule definition object that relate to these definitions are returned. |
| GET | /user/{userID}/schedule | Get a collection of scheduled definition for all accessible monetary accounts of the user. You can add the parameter type to filter the response. When type={SCHEDULE_DEFINITION_PAYMENT,SCHEDULE_DEFINITION_PAYMENT_BATCH} is provided only schedule definition object that relate to these definitions are returned. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{scheduleID}/schedule-instance/{itemId} | view for reading, updating and listing the scheduled instance. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{scheduleID}/schedule-instance/{itemId} | view for reading, updating and listing the scheduled instance. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule/{scheduleID}/schedule-instance | view for reading, updating and listing the scheduled instance. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment | Endpoint for schedule payments. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment | Endpoint for schedule payments. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment/{itemId} | Endpoint for schedule payments. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment/{itemId} | Endpoint for schedule payments. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment/{itemId} | Endpoint for schedule payments. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch/{itemId} | Endpoint for schedule payment batches. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch/{itemId} | Endpoint for schedule payment batches. |
| DELETE | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch/{itemId} | Endpoint for schedule payment batches. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment-batch | Endpoint for schedule payment batches. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/share-invite-monetary-account-inquiry | [DEPRECATED - use /share-invite-monetary-account-response] Create a new share inquiry for a monetary account, specifying the permission the other bunq user will have on it. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/share-invite-monetary-account-inquiry | [DEPRECATED - use /share-invite-monetary-account-response] Get a list with all the share inquiries for a monetary account, only if the requesting user has permission to change the details of the various ones. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/share-invite-monetary-account-inquiry/{itemId} | [DEPRECATED - use /share-invite-monetary-account-response] Get the details of a specific share inquiry. |
| PUT | /user/{userID}/monetary-account/{monetary-accountID}/share-invite-monetary-account-inquiry/{itemId} | [DEPRECATED - use /share-invite-monetary-account-response] Update the details of a share. This includes updating status (revoking or cancelling it), granted permission and validity period of this share. |
| GET | /user/{userID}/share-invite-monetary-account-response/{itemId} | Return the details of a specific share a user was invited to. |
| PUT | /user/{userID}/share-invite-monetary-account-response/{itemId} | Accept or reject a share a user was invited to. |
| GET | /user/{userID}/share-invite-monetary-account-response | Return all the shares a user was invited to. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/sofort-merchant-transaction/{itemId} | View for requesting Sofort transactions and polling their status. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/sofort-merchant-transaction | View for requesting Sofort transactions and polling their status. |
| POST | /user/{userID}/monetary-account/{monetary-accountID}/event/{eventID}/statement | Used to create a statement export of a single payment. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/event/{eventID}/statement/{itemId} | Used to create a statement export of a single payment. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/switch-service-payment/{itemId} | An incoming payment made towards an account of an external bank and redirected to a bunq account via switch service. |
| POST | /user/{userID}/token-qr-request-ideal | Create a request from an ideal transaction. |
| POST | /user/{userID}/token-qr-request-sofort | Create a request from an SOFORT transaction. |
| GET | /user/{userID}/transferwise-currency | Used to get a list of supported currencies for Transferwise. |
| POST | /user/{userID}/transferwise-quote | Used to get quotes from Transferwise. These can be used to initiate payments. |
| GET | /user/{userID}/transferwise-quote/{itemId} | Used to get quotes from Transferwise. These can be used to initiate payments. |
| POST | /user/{userID}/transferwise-quote-temporary | Used to get temporary quotes from Transferwise. These cannot be used to initiate payments |
| GET | /user/{userID}/transferwise-quote-temporary/{itemId} | Used to get temporary quotes from Transferwise. These cannot be used to initiate payments |
| POST | /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-recipient | Used to manage recipient accounts with Transferwise. |
| GET | /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-recipient | Used to manage recipient accounts with Transferwise. |
| GET | /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-recipient/{itemId} | Used to manage recipient accounts with Transferwise. |
| DELETE | /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-recipient/{itemId} | Used to manage recipient accounts with Transferwise. |
| POST | /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-recipient-requirement | Used to determine the recipient account requirements for Transferwise transfers. |
| GET | /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-recipient-requirement | Used to determine the recipient account requirements for Transferwise transfers. |
| POST | /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-transfer | Used to create Transferwise payments. |
| GET | /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-transfer | Used to create Transferwise payments. |
| GET | /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-transfer/{itemId} | Used to create Transferwise payments. |
| POST | /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-transfer-requirement | Used to determine the account requirements for Transferwise transfers. |
| POST | /user/{userID}/transferwise-user | Used to manage Transferwise users. |
| GET | /user/{userID}/transferwise-user | Used to manage Transferwise users. |
| GET | /user/{userID}/tree-progress | See how many trees this user has planted. |
| GET | /user/{itemId} | Get a specific user. |
| GET | /user | Get a collection of all available users. |
| GET | /user/{userID}/whitelist-sdd/{itemId} | Get a specific recurring SDD whitelist entry. |
| GET | /user/{userID}/whitelist-sdd | Get a listing of all recurring SDD whitelist entries for a target monetary account. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/whitelist-sdd/{itemId} | Get a specific SDD whitelist entry. |
| GET | /user/{userID}/monetary-account/{monetary-accountID}/whitelist-sdd | Get a listing of all SDD whitelist entries for a target monetary account. |
| GET | /user/{userID}/whitelist-sdd-one-off/{itemId} | Get a specific one off SDD whitelist entry. |
| PUT | /user/{userID}/whitelist-sdd-one-off/{itemId} | Whitelist an one off SDD so that when another one off SDD from the creditor comes in, it is automatically accepted. |
| DELETE | /user/{userID}/whitelist-sdd-one-off/{itemId} | Whitelist an one off SDD so that when another one off SDD from the creditor comes in, it is automatically accepted. |
| POST | /user/{userID}/whitelist-sdd-one-off | Create a new one off SDD whitelist entry. |
| GET | /user/{userID}/whitelist-sdd-one-off | Get a listing of all one off SDD whitelist entries for a target monetary account. |
| GET | /user/{userID}/whitelist-sdd-recurring/{itemId} | Get a specific recurring SDD whitelist entry. |
| PUT | /user/{userID}/whitelist-sdd-recurring/{itemId} | Whitelist a recurring SDD so that when another recurrence comes in, it is automatically accepted. |
| DELETE | /user/{userID}/whitelist-sdd-recurring/{itemId} | Whitelist a recurring SDD so that when another recurrence comes in, it is automatically accepted. |
| POST | /user/{userID}/whitelist-sdd-recurring | Create a new recurring SDD whitelist entry. |
| GET | /user/{userID}/whitelist-sdd-recurring | Get a listing of all recurring SDD whitelist entries for a target monetary account. |

### attachment-public
| Method | Path | Description |
|--------|------|-------------|
| POST | /attachment-public | Create a new public attachment. Create a POST request with a payload that contains a binary representation of the file, without any JSON wrapping. Make sure you define the MIME type (i.e. image/jpeg, or image/png) in the Content-Type header. You are required to provide a description of the attachment using the X-Bunq-Attachment-Description header. |
| GET | /attachment-public/{itemId} | Get a specific attachment's metadata through its UUID. The Content-Type header of the response will describe the MIME type of the attachment file. |
| GET | /attachment-public/{attachment-publicUUID}/content | Get the raw content of a specific attachment. |

### avatar
| Method | Path | Description |
|--------|------|-------------|
| POST | /avatar | Avatars are public images used to represent you or your company. Avatars are used to represent users, monetary accounts and cash registers. Avatars cannot be deleted, only replaced. Avatars can be updated after uploading the image you would like to use through AttachmentPublic. Using the attachment_public_uuid which is returned you can update your Avatar. Avatars used for cash registers and company accounts will be reviewed by bunq. |
| GET | /avatar/{itemId} | Avatars are public images used to represent you or your company. Avatars are used to represent users, monetary accounts and cash registers. Avatars cannot be deleted, only replaced. Avatars can be updated after uploading the image you would like to use through AttachmentPublic. Using the attachment_public_uuid which is returned you can update your Avatar. Avatars used for cash registers and company accounts will be reviewed by bunq. |

### device
| Method | Path | Description |
|--------|------|-------------|
| GET | /device/{itemId} | Get a single Device. A Device is either a DevicePhone or a DeviceServer. |
| GET | /device | Get a collection of Devices. A Device is either a DevicePhone or a DeviceServer. |

### device-server
| Method | Path | Description |
|--------|------|-------------|
| POST | /device-server | Create a new DeviceServer providing the installation token in the header and signing the request with the private part of the key you used to create the installation. The API Key that you are using will be bound to the IP address of the DeviceServer which you have created.<br/><br/>Using a Wildcard API Key gives you the freedom to make API calls even if the IP address has changed after the POST device-server.<br/><br/>Find out more at this link <a href="https:/bunq.com/en/apikey-dynamic-ip" target="_blank">https:/bunq.com/en/apikey-dynamic-ip</a>. |
| GET | /device-server | Get a collection of all the DeviceServers you have created. |
| GET | /device-server/{itemId} | Get one of your DeviceServers. |

### health-check
| Method | Path | Description |
|--------|------|-------------|
| GET | /health-check | Basic health check for uptime and instance health monitoring. |

### installation
| Method | Path | Description |
|--------|------|-------------|
| POST | /installation | This is the only API call that does not require you to use the "X-Bunq-Client-Authentication" and "X-Bunq-Client-Signature" headers. |
| GET | /installation | You must have an active session to make this call. This call returns the Id of the the Installation you are using in your session. |
| GET | /installation/{itemId} | You must have an active session to make this call. This call is used to check whether the Id you provide is the Id of your current installation or not. |
| GET | /installation/{installationID}/server-public-key | Show the ServerPublicKey for this Installation. |

### user-company
| Method | Path | Description |
|--------|------|-------------|
| GET | /user-company/{user-companyID}/name | Return all the known (trade) names for a specific user company. |
| GET | /user-company/{itemId} | Get a specific company. |
| PUT | /user-company/{itemId} | Modify a specific company's data. |

### payment-service-provider-credential
| Method | Path | Description |
|--------|------|-------------|
| GET | /payment-service-provider-credential/{itemId} | Register a Payment Service Provider and provide credentials |
| POST | /payment-service-provider-credential | Register a Payment Service Provider and provide credentials |

### sandbox-user-company
| Method | Path | Description |
|--------|------|-------------|
| POST | /sandbox-user-company | Used to create a sandbox userCompany. |

### sandbox-user-person
| Method | Path | Description |
|--------|------|-------------|
| POST | /sandbox-user-person | Used to create a sandbox userPerson. |

### server-error
| Method | Path | Description |
|--------|------|-------------|
| POST | /server-error | An endpoint that will always throw an error. |

### session
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /session/{itemId} | Deletes the current session. |

### session-server
| Method | Path | Description |
|--------|------|-------------|
| POST | /session-server | Create a new session for a DeviceServer. Provide the Installation token in the "X-Bunq-Client-Authentication" header. And don't forget to create the "X-Bunq-Client-Signature" header. The response contains a Session token that should be used for as the "X-Bunq-Client-Authentication" header for all future API calls. The ip address making this call needs to match the ip address bound to your API key. |

### user-payment-service-provider
| Method | Path | Description |
|--------|------|-------------|
| GET | /user-payment-service-provider/{itemId} | Used to view UserPaymentServiceProvider for session creation. |

### user-person
| Method | Path | Description |
|--------|------|-------------|
| GET | /user-person/{itemId} | Get a specific person. |
| PUT | /user-person/{itemId} | Modify a specific person object's data. |

## Enhanced Skill Content
## Question Mapping

- "How do I set up a new API session?" -> POST /installation then POST /device-server then POST /session-server
- "What bank accounts do I have?" -> GET /user/{userID}/monetary-account
- "How do I send money to someone?" -> POST /user/{userID}/monetary-account/{monetary-accountID}/payment
- "What is my account balance?" -> GET /user/{userID}/monetary-account-bank/{itemId}
- "How do I request money from someone?" -> POST /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry
- "What cards are linked to my account?" -> GET /user/{userID}/card
- "How do I freeze or cancel a card?" -> PUT /user/{userID}/card/{itemId} (set status)
- "How do I create a bunq.me payment link?" -> POST /user/{userID}/monetary-account/{monetary-accountID}/bunqme-tab
- "What happened on my account recently?" -> GET /user/{userID}/event
- "How do I schedule a recurring payment?" -> POST /user/{userID}/monetary-account/{monetary-accountID}/schedule-payment
- "How do I send money internationally via TransferWise?" -> POST /user/{userID}/transferwise-quote then POST .../transferwise-transfer
- "How do I get a bank statement?" -> POST /user/{userID}/monetary-account/{monetary-accountID}/customer-statement
- "How do I share account access with someone?" -> POST /user/{userID}/monetary-account/{monetary-accountID}/share-invite-monetary-account-inquiry
- "How do I convert currencies?" -> POST /user/{userID}/monetary-account/{monetary-accountID}/currency-conversion-quote then PUT to accept
- "How do I add a note to a transaction?" -> POST /user/{userID}/monetary-account/{monetary-accountID}/payment/{paymentID}/note-text

## Response Tips

- **Payments & transactions**: Amounts are always nested as `{value: str, currency: str}` -- parse both fields. The `balance_after_mutation` field shows the running balance. Check `type` and `sub_type` to distinguish incoming vs outgoing.
- **Monetary accounts**: Responses are polymorphic -- the top-level key (`MonetaryAccountBank`, `MonetaryAccountSavings`, `MonetaryAccountJoint`, etc.) indicates the account type. Always check which variant is returned.
- **List endpoints**: Most GET list endpoints return bare `@returns(200)` with no schema -- expect an array of the same object type as the single-item GET. Pagination uses `older_id` and `newer_id` query parameters (not in spec but standard bunq pattern).
- **Events**: The `object` field in events is a union type -- exactly one key will be populated (e.g., `Payment`, `MasterCardAction`, `RequestInquiry`). Switch on the key name.
- **Cards**: Card details include deeply nested `monetary_account` with all account subtypes inlined. Extract only the fields you need.
- **Errors**: All endpoints return `{400}` uniformly -- the actual error body contains `error_description` and `error_description_translated` in a nested array.
- **Notes (text/attachment)**: Both follow identical CRUD patterns. The `label_user_creator` field identifies who authored the note.
- **Identity**: `alias` and `counterparty_alias` contain IBAN, display name, avatar, and bunq.me pointer. The `label_user` sub-object has the user UUID.

## Anomaly Flags

- **Card status changes**: Surface when `card.status` is `DEACTIVATED`, `LOST`, `STOLEN`, or `order_status` is `CARD_REQUEST_PENDING` -- the user may not realize a card is inactive.
- **Payment suspended outgoing**: Flag `payment_suspended_outgoing` with non-null `status` -- indicates a payment is being held and may need action.
- **Session timeout approaching**: The `session_timeout` value from session-server response indicates seconds until expiry. Warn when nearing the limit; a new session-server call is needed.
- **Challenge requests pending**: When `challenge-request` returns status `PENDING`, the user must approve or deny -- surface this as an action item.
- **bunqto expiry**: Payments with `bunqto_status` of `WAITING_FOR_PAYMENT` and `bunqto_expiry` approaching should be flagged -- the recipient link will expire.
- **Scheduled payment errors**: `schedule-instance` responses with `error_message` populated indicate a failed execution -- surface with the translated description.
- **Card limit thresholds**: Compare `card_limit` and `card_limit_atm` values against spending patterns. Flag when `spent_amount_monthly` approaches `limit_amount_monthly` in company accounts.
- **Currency conversion quote expiry**: `time_expiry` on currency-conversion-quote responses -- warn before quote expires so the user can accept in time.
- **Account sub_status changes**: Flag when `sub_status` shifts to values like `REDEMPTION_INVOLUNTARY` or `UNDER_REVIEW` on any monetary account.

## Playbook

### 1. Initial API Setup (Installation + Device + Session)

1. Generate an RSA key pair locally.
2. Call `POST /installation` with `client_public_key` -- save the returned `Token.token` (installation token) and `ServerPublicKey.server_public_key`.
3. Call `POST /device-server` with your API key as `secret`, a `description`, and optionally `permitted_ips`. Use the installation token for auth.
4. Call `POST /session-server` with your API key as `secret` -- save the returned `Token.token` (session token) and the `UserPerson` or `UserCompany` object for your `userID`.
5. Use the session token as `X-Bunq-Client-Authentication` for all subsequent requests.

### 2. Making a Payment

1. Call `GET /user/{userID}/monetary-account` to list accounts and pick the source `monetary-accountID`.
2. Call `POST /user/{userID}/monetary-account/{monetary-accountID}/payment` with `amount` (`{value, currency}`), `counterparty_alias` (IBAN + name), and `description`.
3. The response returns the payment `id`. Call `GET .../payment/{id}` to verify `type`, `sub_type`, and `balance_after_mutation`.
4. Optionally add a note via `POST .../payment/{id}/note-text` with `content`.

### 3. International Transfer via TransferWise

1. Call `GET /user/{userID}/transferwise-currency` to check supported currencies.
2. Call `POST /user/{userID}/transferwise-quote` with `currency_source`, `currency_target`, and either `amount_source` or `amount_target` -- save the quote `id`.
3. Call `GET .../transferwise-quote/{id}/transferwise-recipient-requirement` to learn required recipient fields.
4. Call `POST .../transferwise-quote/{id}/transferwise-recipient` with `name_account_holder`, `type`, `country`, and `detail` (key-value pairs from requirements).
5. Call `POST .../transferwise-quote/{id}/transferwise-transfer` with `monetary_account_id` and `recipient_id` to execute the transfer.
6. Monitor status via `GET .../transferwise-transfer/{id}` -- watch `status_transferwise` for completion or issues.

### 4. Splitting a Bill

1. Call `POST /user/{userID}/monetary-account/{monetary-accountID}/request-inquiry-batch` with an array of `request_inquiries`, each containing `amount_inquired`, `counterparty_alias`, `description`, and `allow_bunqme: true`.
2. The batch returns an `id`. Monitor via `GET .../request-inquiry-batch/{id}` -- check each inquiry's `status` (ACCEPTED, REJECTED, EXPIRED).
3. The `total_amount_inquired` field gives the aggregate. Individual `amount_responded` fields show what each person actually paid.
4. Attach a receipt as context via `POST .../request-inquiry-batch/{id}/note-attachment` with the `attachment_id`.

### 5. Generating an Account Statement

1. Call `GET /user/{userID}/monetary-account` to find the target `monetary-accountID`.
2. Call `POST /user/{userID}/monetary-account/{monetary-accountID}/customer-statement` with `statement_format` (CSV, MT940, PDF), `date_start`, and `date_end`.
3. Poll `GET .../customer-statement/{id}` until `status` is `STATEMENT_AVAILABLE`.
4. Download the file via `GET .../customer-statement/{id}/content` -- this returns the raw file bytes.
5. To clean up, call `DELETE .../customer-statement/{id}` after downloading.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
