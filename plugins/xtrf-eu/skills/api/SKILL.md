---
name: xtrf-home-portal-api
description: "XTRF Home Portal API skill. Use when working with XTRF Home Portal for browser, accounting, customers. Covers 341 endpoints."
version: 1.0.0
generator: lapsh
---

# XTRF Home Portal API
API version: 2.0

## Auth
ApiKey X-AUTH-ACCESS-TOKEN in header

## Base URL
https://presentation.s.xtrf.eu/home-api

## Setup
1. Set your API key in the appropriate header
2. GET /browser/csv -- verify access
3. POST /browser/views/for/{className} -- create first for

## Endpoints

341 endpoints across 20 groups. See references/api-spec.lap for full details.

### browser
| Method | Path | Description |
|--------|------|-------------|
| GET | /browser/csv | Searches for data (ie. customer, task, etc) and returns it in a CSV form. |
| GET | /browser | Searches for data (ie. customer, task, etc) and returns it in a tabular form. |
| GET | /browser/views/for/{className} | Returns views' brief. |
| POST | /browser/views/for/{className} | Creates view for given class. |
| GET | /browser/views/{viewId} | Returns all view's information. |
| PUT | /browser/views/{viewId} | Updates all view's information. |
| DELETE | /browser/views/{viewId} | Removes a view. |
| DELETE | /browser/views/{viewId}/columns/{columnName} | Deletes a single column from view. |
| GET | /browser/views/{viewId}/columns/{columnName}/settings | Returns column's specific settings. |
| PUT | /browser/views/{viewId}/columns/{columnName}/settings | Updates column's specific settings. |
| GET | /browser/views/{viewId}/columns | Returns columns defined in view. |
| PUT | /browser/views/{viewId}/columns | Updates columns in view. |
| GET | /browser/views/details/for/{className} | Returns current view's detailed information, suitable for browser. |
| GET | /browser/views/{viewId}/filter | Returns view's filter. |
| PUT | /browser/views/{viewId}/filter | Updates view's filter. |
| GET | /browser/views/{viewId}/settings/local | Returns view's local settings (for current user). |
| PUT | /browser/views/{viewId}/settings/local | Updates view's local settings (for current user). |
| GET | /browser/views/{viewId}/order | Returns view's order settings. |
| PUT | /browser/views/{viewId}/order | Updates view's order settings. |
| GET | /browser/views/{viewId}/permissions | Returns view's permissions. |
| PUT | /browser/views/{viewId}/permissions | Updates view's permissions. |
| GET | /browser/views/{viewId}/settings | Returns view's settings. |
| PUT | /browser/views/{viewId}/settings | Updates view's settings. |
| GET | /browser/views/details/for/{className}/{viewId} | Returns view's detailed information, suitable for browser. |
| POST | /browser/views/details/for/{className}/{viewId} | Selects given view as current and returns its detailed information, suitable for browser. |
| PUT | /browser/views/{viewId}/filter/{filterProperty} | Updates view's filter property. |

### accounting
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounting/customers/invoices | Lists all client invoices in all statuses (including not ready and drafts) that have been updated since a specific date. |
| POST | /accounting/customers/invoices | Creates a new invoice. |
| GET | /accounting/customers/invoices/{invoiceId}/payments | Returns all payments for the client invoice. |
| POST | /accounting/customers/invoices/{invoiceId}/payments | Adds a new payment to the client invoice. The invoice payment status (Not Paid, Partially Paid, Fully Paid) is automatically recalculated. |
| GET | /accounting/customers/invoices/{invoiceId} | Returns client invoice details. |
| DELETE | /accounting/customers/invoices/{invoiceId} | Removes a client invoice. |
| POST | /accounting/customers/invoices/documents | Allows for downloading multiple client invoice documents. |
| POST | /accounting/customers/invoices/xmlDocuments | Allows for downloading multiple client invoice xml documents. |
| POST | /accounting/customers/invoices/{invoiceId}/duplicate | Duplicate client invoice. |
| POST | /accounting/customers/invoices/{invoiceId}/duplicate/proForma | Duplicate client invoice as pro forma. |
| GET | /accounting/customers/invoices/ids | Returns client invoices' internal identifiers. |
| GET | /accounting/customers/invoices/{invoiceId}/dates | Returns dates of a given client invoice. |
| GET | /accounting/customers/invoices/{invoiceId}/document | Allows for downloading a given client invoice document. |
| GET | /accounting/customers/invoices/{invoiceId}/paymentTerms | Returns payment terms of a given client invoice. |
| GET | /accounting/customers/invoices/{invoiceId}/xmlDocument | Allows for downloading a given client invoice xml document. |
| POST | /accounting/customers/invoices/{invoiceId}/sendReminder | Sends reminder. |
| POST | /accounting/customers/invoices/sendReminders | Sends reminders. Returns number of sent e-mails. |
| DELETE | /accounting/customers/payments/{paymentId} | Removes a customer payment. |
| GET | /accounting/providers/invoices | Lists all vendor invoices in all statuses (including not ready and drafts) that have been updated since a specific date. |
| POST | /accounting/providers/invoices | Creates a new invoice. |
| GET | /accounting/providers/invoices/{invoiceId}/payments | Returns all payments for the vendor invoice. |
| POST | /accounting/providers/invoices/{invoiceId}/payments | Creates a new payment on the vendor account and assigns the payment to the invoice. |
| GET | /accounting/providers/invoices/{invoiceId} | Returns provider invoice details. |
| DELETE | /accounting/providers/invoices/{invoiceId} | Removes a provider invoice. |
| GET | /accounting/providers/invoices/ids | Returns vendor invoices' internal identifiers. |
| GET | /accounting/providers/invoices/{invoiceId}/document | Generates provider invoice document (PDF). |
| POST | /accounting/providers/invoices/{invoiceId}/send | Sends a provider invoice. |
| POST | /accounting/providers/invoices/{invoiceId}/status | Changes invoice status to given status. |
| DELETE | /accounting/providers/payments/{paymentId} | Removes a provider payment. |

### customers
| Method | Path | Description |
|--------|------|-------------|
| POST | /customers/persons | Creates a new person. |
| GET | /customers/persons/{personId} | Returns person details. |
| PUT | /customers/persons/{personId} | Updates an existing person. |
| DELETE | /customers/persons/{personId} | Removes a person. |
| POST | /customers/persons/accessToken | Generates a single use sign-in token. |
| GET | /customers/persons/ids | Returns persons' internal identifiers. |
| GET | /customers/persons/{personId}/contact | Returns contact of a given person. |
| PUT | /customers/persons/{personId}/contact | Updates contact of a given person. |
| GET | /customers/persons/{personId}/customFields | Returns custom fields of a given person. |
| PUT | /customers/persons/{personId}/customFields | Updates custom fields of a given person. |
| DELETE | /customers/priceLists/{priceListId} | Removes a customer price list. |
| GET | /customers | Returns list of simple clients representations |
| POST | /customers | Creates a new client. |
| GET | /customers/{customerId} | Returns client details. |
| PUT | /customers/{customerId} | Updates an existing client. |
| DELETE | /customers/{customerId} | Removes a client. |
| GET | /customers/{customerId}/priceProfiles/active | Returns list of active price profiles for a client. |
| GET | /customers/{customerId}/address | Returns address of a given client. |
| PUT | /customers/{customerId}/address | Updates address of a given client. |
| GET | /customers/ids | Returns clients' internal identifiers. |
| GET | /customers/{customerId}/budgetCodes | Returns list of available budget codes for a client. |
| GET | /customers/byAlias | Returns client details. |
| GET | /customers/{customerId}/categories | Returns categories of a given client. |
| PUT | /customers/{customerId}/categories | Updates categories of a given client. |
| GET | /customers/{customerId}/contact | Returns contact of a given client. |
| PUT | /customers/{customerId}/contact | Updates contact of a given client. |
| GET | /customers/{customerId}/correspondenceAddress | Returns correspondence address of a given client. |
| PUT | /customers/{customerId}/correspondenceAddress | Updates correspondence address of a given client. |
| GET | /customers/{customerId}/customFields/{customFieldKey} | Returns custom field of a given client. |
| PUT | /customers/{customerId}/customFields/{customFieldKey} | Updates given custom field of a given client. |
| GET | /customers/{customerId}/customFields | Returns custom fields of a given client. |
| PUT | /customers/{customerId}/customFields | Updates custom fields of a given client. |
| GET | /customers/{customerId}/settings/specializations | Returns specializations available for a given client in the Client Portal. |
| GET | /customers/{customerId}/industries | Returns industries of a given client. |
| PUT | /customers/{customerId}/industries | Updates industries of a given client. |
| GET | /customers/{customerId}/settings/languages | Returns languages available for a given client in the Client Portal. |
| GET | /customers/{customerId}/offices | Returns list of offices in the office structure in which the client is located. |
| GET | /customers/{customerId}/services | Returns list of available services for a client. |

### files
| Method | Path | Description |
|--------|------|-------------|
| POST | /files | Uploads a temporary file (ie. for XML import). Returns token which can be used in other API calls. |

### license
| Method | Path | Description |
|--------|------|-------------|
| GET | /license | Returns license content. |
| POST | /license/refresh | Refreshes license content. |

### macros
| Method | Path | Description |
|--------|------|-------------|
| POST | /macros/{macroId}/run | Executes a macro. |

### confidential-groups
| Method | Path | Description |
|--------|------|-------------|
| POST | /confidential-groups/sensitiveClients/client | Adds client to sensitive clients list. |
| GET | /confidential-groups/sensitiveClients | Returns sensitive clients list. |
| PUT | /confidential-groups/sensitiveClients | Updates sensitive clients list. |
| GET | /confidential-groups/sensitiveClients/isSensitive/{clientId} | Check if client is sensitive. |
| DELETE | /confidential-groups/sensitiveClients/client/{sensitiveClientId} | Removes sensitive client from sensitive clients list. |
| POST | /confidential-groups/trustedVendors/vendor | Adds vendor to trusted vendors list. |
| GET | /confidential-groups/trustedVendors | Returns trusted vendors list. |
| PUT | /confidential-groups/trustedVendors | Updates trusted vendors list. |
| DELETE | /confidential-groups/trustedVendors/vendor/{trustedVendorId} | Removes trusted vendor from trusted vendors list. |

### projectGroups
| Method | Path | Description |
|--------|------|-------------|
| GET | /projectGroups | Returns all project groups. |
| POST | /projectGroups | Creates a new Project Groups. |
| GET | /projectGroups/{projectGroupId} | Returns project group details. |
| PUT | /projectGroups/{projectGroupId} | Update project group details. |
| DELETE | /projectGroups/{projectGroupId} | Removes a project group. |
| PUT | /projectGroups/{projectGroupId}/linkProjects | Add projects to project group. |
| PUT | /projectGroups/{projectGroupId}/linkQuotes | Add quotes to project group. |
| PUT | /projectGroups/{projectGroupId}/unlinkProjects | Remove projects from project group. |
| PUT | /projectGroups/{projectGroupId}/unlinkQuotes | Remove quotes from project group. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/persons/{personId} | Returns person details. |
| DELETE | /providers/persons/{personId} | Removes a person. |
| GET | /providers/persons/ids | Returns persons' internal identifiers. |
| GET | /providers/persons/{personId}/contact | Returns contact of a given person. |
| GET | /providers/persons/{personId}/customFields | Returns custom fields of a given person. |
| POST | /providers/persons/{personId}/notification/invitation | Sends invitation to Vendor Portal. |
| DELETE | /providers/priceLists/{priceListId} | Removes a provider price list. |
| GET | /providers/{providerId} | Returns provider details. |
| DELETE | /providers/{providerId} | Removes a provider. |
| GET | /providers/{providerId}/address | Returns address of a given provider. |
| GET | /providers/ids | Returns providers' internal identifiers. |
| GET | /providers/{providerId}/competencies | Returns competencies of a given provider. |
| GET | /providers/{providerId}/contact | Returns contact of a given provider. |
| GET | /providers/{providerId}/correspondenceAddress | Returns correspondence address of a given provider. |
| GET | /providers/{providerId}/customFields | Returns custom fields of a given provider. |
| POST | /providers/{providerId}/notification/invitation | Sends invitations to Vendor Portal. |

### reports
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /reports/{reportId} | Removes a report. |
| POST | /reports/{reportId}/duplicate | Duplicates a report. |
| POST | /reports/export/xml | Exports reports definition to XML. |
| GET | /reports/{reportId}/result/csv | Generates CSV content for a report. |
| GET | /reports/{reportId}/result/printerFriendly | Generates printer friendly content for a report. |
| POST | /reports/import/xml | Imports reports definition from XML. |
| PUT | /reports/{reportId}/preferred | Marks report as preferred or not. |

### services
| Method | Path | Description |
|--------|------|-------------|
| GET | /services/all | Returns services list |
| GET | /services/active | Returns active services list |

### settings
| Method | Path | Description |
|--------|------|-------------|
| GET | /settings/customFields | Returns Custom Fields configuration. |

### subscription
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscription/supports | This method can be used to determine if hooks are supported. |
| GET | /subscription | Returns all subscriptions |
| POST | /subscription | Subscribe to event |
| DELETE | /subscription/{subscriptionId} | Unsubscribe from event |

### system
| Method | Path | Description |
|--------|------|-------------|
| GET | /system/configuration/email | Get email configuration |
| GET | /system/configuration/ftp | Get FTP configuration |
| GET | /system/configuration | Get basic system configuration |
| GET | /system/timeZone | Get system timezone information |

### users
| Method | Path | Description |
|--------|------|-------------|
| PUT | /users/{userId}/password | Sets user's password to a new value. |
| GET | /users | Returns list of simple users representations |
| GET | /users/{userId} | Returns user details. |
| PUT | /users/{userId} | Updates an existing user. |
| GET | /users/{userId}/customFields/{customFieldKey} | Returns custom field of a given user. |
| PUT | /users/{userId}/customFields/{customFieldKey} | Updates given custom field of a given user. |
| GET | /users/{userId}/customFields | Returns custom fields of a given user. |
| PUT | /users/{userId}/customFields | Updates custom fields of a given user. |
| GET | /users/me | Returns currently signed in user details. |
| GET | /users/me/timeZone | Returns time zone preferred by user currently signed in. |

### dictionaries
| Method | Path | Description |
|--------|------|-------------|
| GET | /dictionaries/active | Returns active dictionary entities for all types. |
| GET | /dictionaries/{type}/active | Returns active values from a given dictionary. |
| GET | /dictionaries/all | Returns dictionary entities for all types. Both active and not active ones. |
| GET | /dictionaries/{type}/all | Returns all values (both active and not active) from a given dictionary. |
| GET | /dictionaries/{type}/{id} | Returns specific value from a given dictionary. |
| GET | /dictionaries/{type}/all/default | Returns a default value from a given dictionary. |
| GET | /dictionaries/currency/{isoCode}/exchangeRate | Returns currency exchange rates. |
| POST | /dictionaries/currency/{isoCode}/exchangeRate | Adding currency exchange rates. |
| POST | /v2/dictionaries/language |  |
| PATCH | /v2/dictionaries/language/{languageId} |  |
| POST | /v2/dictionaries/specialization |  |
| PATCH | /v2/dictionaries/specialization/{specializationId} |  |

### jobs
| Method | Path | Description |
|--------|------|-------------|
| POST | /jobs/{jobId}/files/output |  |
| PUT | /jobs/{jobId}/vendor | Assigns vendor to a job in a project. |
| PUT | /jobs/{jobId}/status | Changes job status if possible (400 Bad Request is returned otherwise). |
| GET | /jobs/{jobId} | Returns job details by jobId. |
| GET | /jobs/{jobId}/files | Returns list of input and output files of a job. |
| GET | /jobs/{jobId}/files/{fileId} | Returns file metadata. |
| PUT | /jobs/{jobId}/dates | Updates dates of a given job. |
| PUT | /jobs/{jobId}/instructions | Updates instructions for a job. |
| POST | /v2/jobs/{jobId}/files/addExternalLink |  |
| POST | /v2/jobs/{jobId}/files/delivered/addLink | Adds file link to the project as a link delivered in the job. |
| PUT | /v2/jobs/{jobId}/files/delivered/add | Adds files to the project as delivered in the job. |
| PUT | /v2/jobs/{jobId}/vendor | Assigns vendor to a job in a project. |
| PUT | /v2/jobs/{jobId}/dates | Updates dates of a given job. |
| PUT | /v2/jobs/{jobId}/status | Changes job status if possible (400 Bad Request is returned otherwise). |
| GET | /v2/jobs/{jobId} | Returns details for a job. |
| DELETE | /v2/jobs/{jobId} | Deletes a job. |
| GET | /v2/jobs/for-external-id |  |
| GET | /v2/jobs/{jobId}/files/delivered | Returns list of files delivered in the job. |
| GET | /v2/jobs/{jobId}/files/sharedReferenceFiles | Returns list of files shared with the job as Reference Files. |
| GET | /v2/jobs/{jobId}/files/sharedWorkFiles | Returns list of files shared with the job as Work Files. |
| POST | /v2/jobs/merge | Merges given list of jobs into one job. |
| PUT | /v2/jobs/{jobId}/files/sharedReferenceFiles/share | Shares selected files as Reference Files with a job in a project. |
| PUT | /v2/jobs/{jobId}/files/sharedWorkFiles/share | Shares selected files as Work Files with a job in a project. |
| PUT | /v2/jobs/{jobId}/files/stopSharing | Stops sharing selected files with a job in a project. |
| PUT | /v2/jobs/{jobId}/instructions | Updates instructions for a job. |
| POST | /v2/jobs/{jobId}/files/delivered/upload | Uploads file to the project as a file delivered in the job. |
| POST | /v2/jobs/{jobId}/files/delivered/uploadFileByVendor | Uploads file to the project as a file delivered in the job, added by vendor. |

### projects
| Method | Path | Description |
|--------|------|-------------|
| POST | /projects | Creates a new Classic Project. |
| POST | /projects/{projectId}/languageCombinations | Creates a new language combination for a given project without creating a task. |
| POST | /projects/{projectId}/finance/payables | Adds a payable to a project. |
| POST | /projects/{projectId}/finance/receivables | Adds a receivable to a project. |
| POST | /projects/{projectId}/tasks | Creates a new task for a given project. |
| GET | /projects/{projectId} | Returns project details. |
| DELETE | /projects/{projectId} | Removes a project. |
| PUT | /projects/{projectId}/finance/payables/{payableId} | Updates a simple payable. |
| DELETE | /projects/{projectId}/finance/payables/{payableId} | Deletes a payable. |
| PUT | /projects/{projectId}/finance/receivables/{receivableId} | Updates a simple receivable. |
| DELETE | /projects/{projectId}/finance/receivables/{receivableId} | Deletes a receivable. |
| GET | /projects/ids | Returns projects' internal identifiers. |
| GET | /projects/{projectId}/contacts | Returns contacts of a given project. |
| PUT | /projects/{projectId}/contacts | Updates contacts of a given project. |
| GET | /projects/{projectId}/customFields | Returns custom fields of a given project. |
| PUT | /projects/{projectId}/customFields | Updates custom fields of a given project. |
| GET | /projects/{projectId}/dates | Returns dates of a given project. |
| PUT | /projects/{projectId}/dates | Updates dates of a given project. |
| GET | /projects/files/{fileId}/download | Downloads a file. |
| GET | /projects/{projectId}/finance | Returns finance of a given project. |
| GET | /projects/{projectId}/instructions | Returns instructions of a given project. |
| PUT | /projects/{projectId}/instructions | Updates instructions of a given project. |
| POST | /v2/projects/{projectId}/files/addExternalLinks |  |
| POST | /v2/projects/{projectId}/externalInfo |  |
| POST | /v2/projects/{projectId}/files/addLink | Adds file links to the project as added by PM. |
| PUT | /v2/projects/{projectId}/files/add | Adds files to the project as added by PM. |
| POST | /v2/projects/{projectId}/addJob |  |
| PUT | /v2/projects/{projectId}/files/addTargetFile | Adds target file to the project as added by PM. |
| POST | /v2/projects/files/archive | Prepares a ZIP archive that contains the specified files. |
| PUT | /v2/projects/{projectId}/status | Changes project status if possible (400 Bad Request is returned otherwise). |
| POST | /v2/projects | Creates a new Smart Project. |
| POST | /v2/projects/{projectId}/createCatToolProject | Creates Cat Tool Project corresponding to XTRF project. |
| POST | /v2/projects/{projectId}/finance/payables | Adds a payable to a project. |
| POST | /v2/projects/{projectId}/finance/receivables | Adds a receivable to a project. |
| DELETE | /v2/projects/{projectId}/files/{fileId} | Deletes a file. |
| PUT | /v2/projects/{projectId}/finance/payables/{payableId} | Updates a simple payable. |
| DELETE | /v2/projects/{projectId}/finance/payables/{payableId} | Deletes a payable. |
| PUT | /v2/projects/{projectId}/finance/receivables/{receivableId} | Updates a simple receivable. |
| DELETE | /v2/projects/{projectId}/finance/receivables/{receivableId} | Deletes a receivable. |
| GET | /v2/projects/for-external-id/{externalProjectId} | Returns project details. |
| GET | /v2/projects/{projectId} | Returns project details. |
| GET | /v2/projects/{projectId}/catToolProject | Returns if cat tool project is created or queued. |
| GET | /v2/projects/catToolProjectTemplates | Returns CAT Tool project templates available for selection in XTRF. |
| GET | /v2/projects/{projectId}/clientContacts | Returns Client Contacts information for a project. |
| PUT | /v2/projects/{projectId}/clientContacts | Updates Client Contacts for a project. |
| GET | /v2/projects/{projectId}/customFields | Returns a list of custom field keys and values for a project. |
| GET | /v2/projects/{projectId}/files/deliverable | Returns list of files in a project, that are ready to be delivered to client. |
| GET | /v2/projects/files/{fileId} | Returns details of a file. |
| GET | /v2/projects/files/{fileId}/download/{fileName} | Downloads a file content. |
| GET | /v2/projects/{projectId}/files | Returns list of files in a project. |
| GET | /v2/projects/{projectId}/finance | Returns finance information for a project. |
| GET | /v2/projects/{projectId}/jobs | Returns list of jobs in a project. |
| GET | /v2/projects/{projectId}/process | Returns process id. |
| PUT | /v2/projects/{projectId}/catToolProjectTemplateDetails | Updates template details for a project. |
| PUT | /v2/projects/{projectId}/clientDeadline | Updates Client Deadline for a project. |
| PUT | /v2/projects/{projectId}/clientNotes | Updates Client Notes for a project. |
| PUT | /v2/projects/{projectId}/clientReferenceNumber | Updates Client Reference Number for a project. |
| PUT | /v2/projects/{projectId}/customFields/{key} | Updates a custom field with a specified key in a project |
| PUT | /v2/projects/{projectId}/internalNotes | Updates Internal Notes for a project. |
| PUT | /v2/projects/{projectId}/orderDate | Updates Order Date for a project. |
| PUT | /v2/projects/{projectId}/processType |  |
| PUT | /v2/projects/{projectId}/sourceLanguage | Updates source language for a project. |
| PUT | /v2/projects/{projectId}/specialization | Updates specialization for a project. |
| PUT | /v2/projects/{projectId}/targetLanguages | Updates target languages for a project. |
| PUT | /v2/projects/{projectId}/vendorInstructions | Updates instructions for all vendors performing the jobs in a project. |
| PUT | /v2/projects/{projectId}/volume | Updates volume for a project. |
| POST | /v2/projects/{projectId}/files/upload | Uploads file to the project as a file uploaded by PM. |

### quotes
| Method | Path | Description |
|--------|------|-------------|
| POST | /quotes/{quoteId}/languageCombinations | Creates a new language combination for a given quote without creating a task. |
| POST | /quotes/{quoteId}/finance/payables | Adds a payable. |
| POST | /quotes/{quoteId}/finance/receivables | Adds a receivable. |
| POST | /quotes/{quoteId}/tasks | Creates a new task for a given quote. |
| GET | /quotes/{quoteId} | Returns quote details. |
| DELETE | /quotes/{quoteId} | Removes a quote. |
| PUT | /quotes/{quoteId}/finance/payables/{payableId} | Updates a simple payable. |
| DELETE | /quotes/{quoteId}/finance/payables/{payableId} | Deletes a payable. |
| PUT | /quotes/{quoteId}/finance/receivables/{receivableId} | Updates a simple receivable. |
| DELETE | /quotes/{quoteId}/finance/receivables/{receivableId} | Deletes a receivable. |
| GET | /quotes/ids | Returns quotes' internal identifiers. |
| GET | /quotes/{quoteId}/customFields | Returns custom fields of a given quote. |
| PUT | /quotes/{quoteId}/customFields | Updates custom fields of a given quote. |
| GET | /quotes/{quoteId}/dates | Returns dates of a given quote. |
| GET | /quotes/{quoteId}/finance | Returns finance of a given quote. |
| GET | /quotes/{quoteId}/instructions | Returns instructions of a given quote. |
| PUT | /quotes/{quoteId}/instructions | Updates instructions of a given quote. |
| POST | /quotes/{quoteId}/confirmation/send | Sends a quote for customer confirmation. |
| POST | /quotes/{quoteId}/start | Starts a quote. |
| POST | /v2/quotes/{quoteId}/files/addExternalLinks |  |
| POST | /v2/quotes/{quoteId}/externalInfo |  |
| POST | /v2/quotes/{quoteId}/files/addLink | Adds file links to the quote as added by PM. |
| PUT | /v2/quotes/{quoteId}/files/add | Adds files to the quote as added by PM. |
| POST | /v2/quotes/{quoteId}/addJob |  |
| PUT | /v2/quotes/{quoteId}/files/addTargetFile | Adds target file to the quote as added by PM. |
| POST | /v2/quotes/files/archive | Prepares a ZIP archive that contains the specified files. |
| PUT | /v2/quotes/{quoteId}/status | Changes quote status if possible (400 Bad Request is returned otherwise). |
| POST | /v2/quotes | Creates a new Smart Quote. |
| POST | /v2/quotes/{quoteId}/finance/payables | Adds a payable to a quote. |
| POST | /v2/quotes/{quoteId}/finance/receivables | Adds a receivable to a quote. |
| DELETE | /v2/quotes/{quoteId}/files/{fileId} | Deletes a file. |
| PUT | /v2/quotes/{quoteId}/finance/payables/{payableId} | Updates a simple payable. |
| DELETE | /v2/quotes/{quoteId}/finance/payables/{payableId} | Deletes a payable. |
| PUT | /v2/quotes/{quoteId}/finance/receivables/{receivableId} | Updates a simple receivable. |
| DELETE | /v2/quotes/{quoteId}/finance/receivables/{receivableId} | Deletes a receivable. |
| GET | /v2/quotes/for-external-id/{externalProjectId} | Returns quote details. |
| GET | /v2/quotes/{quoteId} | Returns quote details. |
| GET | /v2/quotes/{quoteId}/clientContacts | Returns Client Contacts information for a quote. |
| PUT | /v2/quotes/{quoteId}/clientContacts | Updates Client Contacts for a quote. |
| GET | /v2/quotes/{quoteId}/customFields | Returns a list of custom field keys and values for a project. |
| GET | /v2/quotes/files/{fileId} | Returns details of a file. |
| GET | /v2/quotes/files/{fileId}/download/{fileName} | Downloads a file content. |
| GET | /v2/quotes/{quoteId}/files | Returns list of files in a quote. |
| GET | /v2/quotes/{quoteId}/finance | Returns finance information for a quote. |
| GET | /v2/quotes/{quoteId}/jobs | Returns list of jobs in a quote. |
| GET | /v2/quotes/{quoteId}/process | Returns process id. |
| PUT | /v2/quotes/{quoteId}/businessDays | Updates Business Days for a quote. |
| PUT | /v2/quotes/{quoteId}/catToolProjectTemplateDetails | Updates template details for a quote. |
| PUT | /v2/quotes/{quoteId}/clientNotes | Updates Client Notes for a quote. |
| PUT | /v2/quotes/{quoteId}/clientReferenceNumber | Updates Client Reference Number for a quote. |
| PUT | /v2/quotes/{quoteId}/customFields/{key} | Updates a custom field with a specified key in a quote. |
| PUT | /v2/quotes/{quoteId}/expectedDeliveryDate | Updates Expected Delivery Date for a quote. |
| PUT | /v2/quotes/{quoteId}/internalNotes | Updates Internal Notes for a quote. |
| PUT | /v2/quotes/{quoteId}/processType |  |
| PUT | /v2/quotes/{quoteId}/quoteExpiry | Updates Quote Expiry Date for a quote. |
| PUT | /v2/quotes/{quoteId}/sourceLanguage | Updates source language for a quote. |
| PUT | /v2/quotes/{quoteId}/specialization | Updates specialization for a quote. |
| PUT | /v2/quotes/{quoteId}/targetLanguages | Updates target languages for a quote. |
| PUT | /v2/quotes/{quoteId}/vendorInstructions | Updates instructions for all vendors performing the jobs in a quote. |
| PUT | /v2/quotes/{quoteId}/volume | Updates volume for a quote. |
| POST | /v2/quotes/{quoteId}/files/upload | Uploads file to the quote as a file uploaded by PM. |

### tasks
| Method | Path | Description |
|--------|------|-------------|
| POST | /tasks/{taskId}/files/input | Adds files to a given task. |
| DELETE | /tasks/{taskId} | Removes a task. |
| GET | /tasks/{taskId}/contacts | Returns contacts of a given task. |
| PUT | /tasks/{taskId}/contacts | Updates contacts of a given task. |
| GET | /tasks/{taskId}/customFields | Returns custom fields of a given task. |
| PUT | /tasks/{taskId}/customFields | Updates custom fields of a given task. |
| GET | /tasks/{taskId}/dates | Returns dates of a given task. |
| PUT | /tasks/{taskId}/dates | Updates dates of a given task. |
| GET | /tasks/{taskId}/instructions | Returns instructions of a given task. |
| PUT | /tasks/{taskId}/instructions | Updates instructions of a given task. |
| GET | /tasks/{taskId}/progress | Returns progress of a given task. |
| GET | /tasks/{taskId}/files | Returns lists of files of a given task. |
| POST | /tasks/{taskId}/start | Starts a task. |
| PUT | /tasks/{taskId}/clientTaskPONumber | Updates Client Task PO Number of a given task. |
| PUT | /tasks/{taskId}/name | Updates name of a given task. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all customers?" -> GET /customers
- "How do I create a new translation project?" -> POST /v2/projects
- "What invoices were updated recently?" -> GET /accounting/customers/invoices (with updatedSince)
- "How do I assign a vendor to a job?" -> PUT /v2/jobs/{jobId}/vendor
- "How do I check a project's financial summary?" -> GET /v2/projects/{projectId}/finance
- "How do I upload a file to a project?" -> POST /v2/projects/{projectId}/files/upload
- "How do I change a job's status?" -> PUT /v2/jobs/{jobId}/status
- "How do I find a customer by email?" -> GET /customers/ids (with emailEquals)
- "How do I send an invoice reminder?" -> POST /accounting/customers/invoices/{invoiceId}/sendReminder
- "How do I convert a quote into a project?" -> POST /quotes/{quoteId}/start
- "What languages and specializations are available?" -> GET /dictionaries/{type}/active
- "How do I get the current exchange rate for a currency?" -> GET /dictionaries/currency/{isoCode}/exchangeRate
- "How do I check who I am authenticated as?" -> GET /users/me
- "How do I add a language combination to a project?" -> POST /projects/{projectId}/languageCombinations
- "How do I look up a project created by an external system?" -> GET /v2/projects/for-external-id/{externalProjectId}

## Response Tips

- **Browser/views**: Returns paginated table data; use `page` and `maxRows` params to control result size. Column metadata is nested under `columns`.
- **Customers/providers**: Use `embed` param on detail endpoints to inline nested objects (addresses, contacts) and reduce follow-up calls. The `updatedSince` param takes epoch milliseconds.
- **Accounting/invoices**: 204 responses on payment and reminder endpoints mean success with no body. Invoice detail supports `embed` for nested payment terms and dates.
- **Projects/quotes**: IDs are strings (not integers) -- these are smart IDs like "P12345". Finance sub-objects contain `languageCombination` maps and enum fields (`rateOrigin`, `type`).
- **Jobs**: Job IDs are strings. File endpoints return 200 with file metadata objects. Status updates return 204 with no body.
- **Dictionaries**: Returns arrays of dictionary entries. Use `type` path param (e.g., "language", "specialization", "currency") to filter. The `nameEquals` param does exact matching.
- **Tasks**: All GET endpoints return 200 explicitly. Dates use nested `{value: int(int64)}` wrapper objects for epoch-millisecond timestamps.
- **Delete operations**: Universally return 204. Some (like task delete) accept flags like `removeFilesFromDisc` and `forceJobsRemoval` -- omitting these defaults to safe/non-destructive behavior.

## Anomaly Flags

- **409 on subscription creation**: The only endpoint declaring a conflict error. Surface this when a subscription already exists to prevent confusion.
- **Duplicate parameter names**: `confidential-groups` endpoints declare `clientId`/`sensitiveClientId`/`trustedVendorId` twice in required params -- likely a spec artifact. Warn if requests fail unexpectedly.
- **Date format inconsistency**: Some dates are raw `int(int64)` epoch millis (jobs, invoices), others use `map{value: int(int64)}` wrappers (projects, tasks, quotes). Flag this mismatch when constructing payloads.
- **v1 vs v2 endpoint duplication**: Projects, quotes, jobs, and dictionaries exist in both v1 and v2 forms with different schemas. Surface a warning if a user mixes versions in a workflow.
- **204 vs 200 inconsistency on updates**: Some PUT endpoints return 200 with a body (task contacts, task custom fields), while others return 204 with no body (job dates, project status). Flag when a response body is expected but absent.
- **String vs integer IDs**: Customers and providers use `int(int64)` IDs, but projects, quotes, jobs, and tasks use `str` IDs (smart IDs). Alert if an integer is passed where a string is expected.
- **Mass reminder sends**: `POST /accounting/customers/invoices/sendReminders` (no invoiceId) sends reminders in bulk -- surface confirmation before calling.

## Playbook

### 1. Create a Translation Project End-to-End

1. Look up the client: `GET /customers/ids?nameEquals=ClientName` to get the customer ID
2. Retrieve available services: `GET /services/active` to find the right service ID
3. Create the project: `POST /v2/projects` with `name`, `clientId`, and `serviceId`
4. Set source and target languages: `PUT /v2/projects/{projectId}/sourceLanguage` then `PUT /v2/projects/{projectId}/targetLanguages`
5. Upload source files: `POST /v2/projects/{projectId}/files/upload`
6. Add a job to the project: `POST /v2/projects/{projectId}/addJob`
7. Assign a vendor to the job: `PUT /v2/jobs/{jobId}/vendor`
8. Set the client deadline: `PUT /v2/projects/{projectId}/clientDeadline`

### 2. Invoice a Customer and Track Payment

1. Create the customer invoice: `POST /accounting/customers/invoices`
2. Retrieve the invoice to confirm details: `GET /accounting/customers/invoices/{invoiceId}?embed=payments`
3. Generate the invoice document: `POST /accounting/customers/invoices/documents`
4. Send a payment reminder if overdue: `POST /accounting/customers/invoices/{invoiceId}/sendReminder`
5. Record a payment when received: `POST /accounting/customers/invoices/{invoiceId}/payments`
6. Verify payment status: `GET /accounting/customers/invoices/{invoiceId}/payments`

### 3. Quote-to-Project Conversion

1. Create a quote: `POST /v2/quotes` with `name`, `clientId`, `serviceId`
2. Configure languages and specialization: `PUT /v2/quotes/{quoteId}/sourceLanguage`, `PUT /v2/quotes/{quoteId}/targetLanguages`, `PUT /v2/quotes/{quoteId}/specialization`
3. Add financial receivables: `POST /quotes/{quoteId}/finance/receivables`
4. Send the quote confirmation to the client: `POST /quotes/{quoteId}/confirmation/send`
5. Once approved, start the quote (converts to project): `POST /quotes/{quoteId}/start`
6. Retrieve the resulting project and continue with project workflows

### 4. Onboard a New Customer

1. Create the customer record: `POST /customers` with name, billing address, contact info, and status `ACTIVE`
2. Add contact persons: include `persons` array in the POST body, or create individually via `POST /customers/persons`
3. Set industry and category classifications: `PUT /customers/{customerId}/industries` and `PUT /customers/{customerId}/categories`
4. Configure custom fields if needed: `PUT /customers/{customerId}/customFields`
5. Verify the record: `GET /customers/{customerId}?embed=all`

### 5. Manage Provider Jobs and Deliverables

1. Find jobs for an external project: `GET /v2/jobs/for-external-id?externalProjectId=EXT123`
2. Review job details: `GET /v2/jobs/{jobId}`
3. Update job dates and instructions: `PUT /v2/jobs/{jobId}/dates` and `PUT /v2/jobs/{jobId}/instructions`
4. Upload delivered files from vendor: `POST /v2/jobs/{jobId}/files/delivered/upload`
5. Update job status to completed: `PUT /v2/jobs/{jobId}/status` with `status` field
6. Create the provider invoice: `POST /accounting/providers/invoices` with `jobsIds`
7. Send the invoice to the provider: `POST /accounting/providers/invoices/{invoiceId}/send`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
