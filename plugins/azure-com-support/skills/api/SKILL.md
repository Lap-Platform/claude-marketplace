---
name: microsoftsupport
description: "Microsoft.Support API skill. Use when working with Microsoft.Support for providers, subscriptions. Covers 14 endpoints."
version: 1.0.0
generator: lapsh
---

# Microsoft.Support
API version: 2019-05-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Support/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Support/checkNameAvailability -- create first checkNameAvailability

## Endpoints

14 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Support/operations | This lists all the available Microsoft Support REST API operations. |
| GET | /providers/Microsoft.Support/services | Lists all the Azure services available for support ticket creation. Here are the Service Ids for **Billing**, **Subscription Management**, and **Service and subscription limits (Quotas)** issues: <br/><table><tr><td><u>Issue type</u></td><td><u>Service Id</u></td></tr><tr><td>Billing</td><td>'/providers/Microsoft.Support/services/517f2da6-78fd-0498-4e22-ad26996b1dfc'</td></tr><tr><td>Subscription Management</td><td>'/providers/Microsoft.Support/services/f3dc5421-79ef-1efa-41a5-42bf3cbb52c6'</td></tr><tr><td>Quota</td><td>'/providers/Microsoft.Support/services/06bfd9d3-516b-d5c6-5802-169c800dec89'</td></tr></table> <br/><br/> For **Technical** issues, select the Service Id that maps to the Azure service/product as displayed in the **Services** drop-down list on the Azure portal's <a target='_blank' href='https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview'>New support request</a> page. <br/><br/> Always use the service and it's corresponding problem classification(s) obtained programmatically for support ticket creation. This practice ensures that you always have the most recent set of service and problem classification Ids. |
| GET | /providers/Microsoft.Support/services/{serviceName} | Gets a specific Azure service for support ticket creation. |
| GET | /providers/Microsoft.Support/services/{serviceName}/problemClassifications | Lists all the problem classifications (categories) available for a specific Azure service.<br/><br/> Always use the service and problem classifications obtained programmatically. This practice ensures that you always have the most recent set of service and problem classification Ids. |
| GET | /providers/Microsoft.Support/services/{serviceName}/problemClassifications/{problemClassificationName} | Gets the details of a specific problem classification for a specific Azure service. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Support/checkNameAvailability | Check the availability of a resource name. This API should to be used to check the uniqueness of the name for support ticket creation for the selected subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets | Lists all the support tickets for an Azure subscription. <br/><br/>You can also filter the support tickets by <i>Status</i> or <i>CreatedDate</i> using the $filter parameter. Output will be a paged result with <i>nextLink</i>, using which you can retrieve the next set of support tickets. <br/><br/>Support ticket data is available for 18 months after ticket creation. If a ticket was created more than 18 months ago, a request for data might cause an error. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName} | Gets details for a specific support ticket in an Azure subscription. <br/><br/>Support ticket data is available for 18 months after ticket creation. If a ticket was created more than 18 months ago, a request for data might cause an error. |
| PATCH | /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName} | This API allows you to update the severity level or your contact information in the support ticket. <br/><br/> Note: The severity levels cannot be changed if a support ticket is actively being worked upon by an Azure support engineer. In such a case, contact your support engineer to request severity update by adding a new communication using the Communications API. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName} | Creates a new support ticket for Quota increase, Technical, Billing, and Subscription Management issues for the specified subscription. <br/><br/>A paid technical support plan is required to create a support ticket using this API. <a href='https://aka.ms/supportticketAPI'>Learn more</a> <br/><br/> Use the Services API to map the right Service Id to the issue type. For example: For billing tickets set *serviceId* to *'/providers/Microsoft.Support/services/517f2da6-78fd-0498-4e22-ad26996b1dfc'*. <br/> For Technical issues, the Service id will map to the Azure service you want to raise a support ticket for. <br/><br/>Always call the Services and ProblemClassifications API to get the most recent set of services and problem categories required for support ticket creation. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName}/checkNameAvailability | Check the availability of a resource name. This API should to be used to check the uniqueness of the name for adding a new communication to the support ticket. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName}/communications | Lists all communications (attachments not included) for a support ticket. <br/></br> You can also filter support ticket communications by <i>CreatedDate</i>�or <i>CommunicationType</i> using the $filter parameter. The only type of communication supported today is <i>Web</i>. Output will be a paged result with <i>nextLink</i>, using which you can retrieve the next set of Communication results. <br/><br/> Support ticket data is available for 18 months after ticket creation. If a ticket was created more than 18 months ago, a request for data might cause an error. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName}/communications/{communicationName} | Returns details of a specific communication in a support ticket. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName}/communications/{communicationName} | Adds a new customer communication to an Azure support ticket. Adding attachments are not currently supported via the API. <br/>To add a file to a support ticket, visit the <a target='_blank' href='https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/managesupportrequest'>Manage support ticket</a> page in the Azure portal, select the support ticket, and use the file upload control to add a new file. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available in the Microsoft Support API?" -> GET /providers/Microsoft.Support/operations
- "What Azure support services can I use?" -> GET /providers/Microsoft.Support/services
- "Get details about a specific support service" -> GET /providers/Microsoft.Support/services/{serviceName}
- "What problem categories exist for a given service?" -> GET /providers/Microsoft.Support/services/{serviceName}/problemClassifications
- "Look up a specific problem classification" -> GET /providers/Microsoft.Support/services/{serviceName}/problemClassifications/{problemClassificationName}
- "List all support tickets in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets
- "Show me details for a specific support ticket" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName}
- "Create a new Azure support ticket" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName}
- "Update the severity or status of a support ticket" -> PATCH /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName}
- "Check if a support ticket name is available before creating one" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Support/checkNameAvailability
- "Check if a communication name is available on a ticket" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName}/checkNameAvailability
- "List all communications on a support ticket" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName}/communications
- "Read a specific communication message on a ticket" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName}/communications/{communicationName}
- "Add a reply or communication to an existing support ticket" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName}/communications/{communicationName}

## Response Tips

- **Operations/Services/ProblemClassifications** (provider group): Responses are flat lists under a `value` array; no pagination -- iterate the full array directly.
- **Support Tickets listing**: Supports `$top` and `$filter` query params; look for `nextLink` in the response body to paginate through large result sets.
- **Single Ticket / Communication GET**: Returns a single resource object; key fields are nested under `properties` (status, severity, contactDetails, serviceId).
- **PUT (create) endpoints**: May return 200 (created synchronously) or 202 (accepted, long-running); on 202, check the `Azure-AsyncOperation` or `Location` header to poll for completion.
- **PATCH (update)**: Returns 200 with the updated resource; only fields included in `updateSupportTicket` are modified.
- **Communications listing**: Also supports `$top`/`$filter`; paginate via `nextLink` the same way as tickets.
- **Name availability checks (POST)**: Response contains `nameAvailable` (boolean) and, if false, a `reason` and `message` explaining the conflict.

## Anomaly Flags

- **202 Accepted on PUT**: Ticket or communication creation is async -- surface the polling URL and remind the user to check status before assuming completion.
- **Missing `api-version` query param**: All endpoints require `api-version=2019-05-01-preview`; flag immediately if omitted, as Azure returns opaque 400 errors.
- **Preview API version**: This spec uses `2019-05-01-preview` -- flag that this is a preview version and behavior may change or be deprecated without notice.
- **`$filter` syntax errors**: OData filter expressions on ticket/communication listings often fail silently or return unfiltered results; flag when filter returns unexpectedly large or empty sets.
- **Name conflicts on PUT**: If `checkNameAvailability` returns `nameAvailable: false` but the user proceeds with PUT, surface the conflict reason proactively.
- **Subscription-level auth failures**: 401/403 on subscription endpoints usually means the OAuth token lacks the `Microsoft.Support/*` RBAC role -- flag with remediation steps.
- **Empty problem classifications**: If a service returns zero problem classifications, flag it as the service may not support ticket creation through the API.

## Playbook

### 1. Create a new support ticket

1. Call GET `/providers/Microsoft.Support/services` to list available services
2. Pick the relevant service and call GET `/providers/Microsoft.Support/services/{serviceName}/problemClassifications` to get valid categories
3. Call POST `/subscriptions/{subscriptionId}/providers/Microsoft.Support/checkNameAvailability` with your desired ticket name
4. If available, call PUT `/subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName}` with `createSupportTicketParameters` including serviceId, problemClassificationId, severity, contactDetails, title, and description
5. If response is 202, poll the `Azure-AsyncOperation` URL until the ticket is provisioned

### 2. Reply to an existing support ticket

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets/{supportTicketName}` to confirm the ticket exists and check its status
2. Call POST `.../supportTickets/{supportTicketName}/checkNameAvailability` to validate your communication name
3. Call PUT `.../supportTickets/{supportTicketName}/communications/{communicationName}` with `createCommunicationParameters` containing subject and body
4. If response is 202, poll for completion before confirming the reply was posted

### 3. List and filter open support tickets

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Support/supportTickets` with `$filter=status eq 'Open'` and optionally `$top=10`
2. Iterate through the `value` array in the response
3. If `nextLink` is present, follow it to fetch the next page
4. Repeat until `nextLink` is absent

### 4. Escalate a support ticket's severity

1. Call GET `.../supportTickets/{supportTicketName}` to read the current severity and status
2. Call PATCH `.../supportTickets/{supportTicketName}` with `updateSupportTicket` containing the new `severity` value (e.g., `"critical"`)
3. Verify the 200 response reflects the updated severity in `properties.severity`

### 5. Audit all communications on a ticket

1. Call GET `.../supportTickets/{supportTicketName}/communications` with no filter to get all messages
2. Page through results using `nextLink` if present
3. For each communication, note `properties.communicationType` (web or phone), `properties.createdDate`, and `properties.sender`
4. To inspect a specific message in full, call GET `.../communications/{communicationName}`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
