---
name: avaza-api-documentation
description: "Avaza API Documentation API skill. Use when working with Avaza API Documentation for api, ScheduleSeries. Covers 94 endpoints."
version: 1.0.0
generator: lapsh
---

# Avaza API Documentation
API version: v1

## Auth
OAuth2

## Base URL
https://api.avaza.com

## Setup
1. Configure auth: OAuth2
2. GET /api/Account -- verify access
3. POST /api/Bill -- create first Bill

## Endpoints

94 endpoints across 2 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/Account | Account Details |
| GET | /api/Bill | Gets list of Bills |
| POST | /api/Bill | Create a new draft Bill |
| GET | /api/Bill/{id} | Gets a Bill by Bill ID |
| GET | /api/BillPayment | Gets list of Bill Payments |
| POST | /api/BillPayment | Create new Bill Payment and optionally assign payment allocations to Bills |
| GET | /api/BillPayment/{id} | Gets a Bill Payment by Payment Transaction ID |
| GET | /api/Company/Lookup | Gets minimal list of Companies. |
| GET | /api/Company | Gets list of Companies |
| PUT | /api/Company | Update a Company record. |
| POST | /api/Company | Create a Company |
| GET | /api/Company/{id} | Gets Company by Company ID |
| GET | /api/Contact | Gets list of Contacts |
| POST | /api/Contact | Create a Contact |
| GET | /api/Contact/{id} | Gets Contact by Contact ID |
| GET | /api/CreditNote | Gets list of CreditNotes |
| GET | /api/CreditNote/{id} | Gets Credit Note by CreditNoteID |
| GET | /api/Currency | Gets list of Currencies |
| GET | /api/Estimate | Gets list of Estimates |
| POST | /api/Estimate | Create a new draft Estimate |
| GET | /api/Estimate/{id} | Gets Estimate by Estimate ID |
| POST | /api/Expense/Attachment |  |
| POST | /api/ExpenseApproval/Submit | Submit Expenses for Approval. |
| GET | /api/Expense | Gets list of Expenses |
| PUT | /api/Expense | Update an Expense |
| POST | /api/Expense | Create an Expense |
| DELETE | /api/Expense | Delete Expense Entries |
| GET | /api/Expense/{id} | Gets an Expense Entry by Expense ID |
| GET | /api/ExpenseCategory | Gets list of Expense Categories |
| GET | /api/ExpenseGroup/Lookup | Gets minimal list of Expense Groups. |
| GET | /api/ExpenseMerchant/Lookup | Gets minimal list of Expense Merchants. |
| GET | /api/ExpensePaymentMethod/Lookup | Gets minimal list of Expense Payment Methods. |
| GET | /api/ExpenseSummary | Gets Basic Summary of Expense Statistics |
| GET | /api/FixedAmount | Gets list of Fixed Amounts |
| GET | /api/Inventory | Gets list of Inventory |
| GET | /api/Inventory/{id} | Gets InventoryItem by InventoryItem ID |
| GET | /api/Invoice | Gets list of Invoices |
| PUT | /api/Invoice | Update an Invoice |
| POST | /api/Invoice | Create a new draft invoice |
| GET | /api/Invoice/{id} | Gets Invoice by Invoice ID |
| GET | /api/Payment | Gets list of Payments |
| POST | /api/Payment | Create new Payment and optionally assign payment allocations to Invoices |
| GET | /api/Payment/{id} | Gets Payment by Payment Transaction ID |
| GET | /api/Project/Lookup | Gets minimal list of active Projects for the current user |
| GET | /api/Project | Gets list of Projects |
| PUT | /api/Project | Update an Project |
| POST | /api/Project | Create a Project |
| GET | /api/Project/{id} | Gets Project by Project ID |
| GET | /api/ProjectMember | Gets list of Project Members |
| PUT | /api/ProjectMember | Update a Member of a Project |
| POST | /api/ProjectMember | Assign a user as a Member of a Project |
| GET | /api/ProjectTimesheetCategory | Gets list of Project Timesheet Categories |
| PUT | /api/ProjectTimesheetCategory | Update a TimeSheetCategory on a Project. |
| POST | /api/ProjectTimesheetCategory | Assign a TimeSheetCategory to a Project. |
| GET | /api/RecurringInvoice | Gets list of Recurring Invoices |
| GET | /api/RecurringInvoice/{id} | Gets RecurringInvoice by ID |
| GET | /api/ScheduleAssignment | Gets list of Schedule Assignments. |
| GET | /api/ScheduleSeries | Gets list of Schedule Series |
| POST | /api/ScheduleSeries | Retrieves a list of Schedule Series. This Http Post version adds a ScheduleSeriesIDs collection filter. |
| DELETE | /api/ScheduleSeries/{id} | Delete a Schedule Series entry |
| GET | /api/Section | Gets list of Sections |
| POST | /api/Section | Create a Section |
| DELETE | /api/Section | Delete a Section |
| GET | /api/Task/Lookup | Gets minimal list of Tasks for the current user |
| GET | /api/Task | Gets list of Tasks |
| PUT | /api/Task | Update a Task. |
| POST | /api/Task | Create a Task |
| DELETE | /api/Task | Delete a Task |
| GET | /api/Task/{id} | Gets Task by Task ID |
| GET | /api/TaskDiscussion | Gets list of Task Discussion Messages |
| GET | /api/TaskStatus | Gets list of Task Statuses |
| GET | /api/TaskType | Gets list of Task Types |
| GET | /api/Tax | Get List of Taxes configured in the Avaza account. |
| GET | /api/Timesheet/deleted | Retrieves deleted (tombstone) timesheet entries. Admin access only. |
| GET | /api/Timesheet | Gets list of Timsheets |
| PUT | /api/Timesheet | Update a Timesheet |
| POST | /api/Timesheet | Create a new Timesheet Entry |
| GET | /api/Timesheet/{id} | Gets a Timesheet Entry by Timesheet ID |
| DELETE | /api/Timesheet/{id} | Delete a Timesheet Entry |
| POST | /api/TimesheetSubmission | Submit Timesheets for Approval. |
| GET | /api/TimesheetSummary | Gets Basic Summary of Timesheet Statistics |
| GET | /api/TimesheetTimer | Gets the  Running Timer if there is one for a user. |
| POST | /api/TimesheetTimer/{id} | Starts a Timer running on an existing Timesheet Entry |
| DELETE | /api/TimesheetTimer/{id} | Stop the timer running on an existing Timesheet Entry |
| GET | /api/UserProfile | Get Collection of Users who have roles in the current Avaza account. |
| GET | /api/Webhook | Get list of Webhook Subscriptions |
| POST | /api/Webhook | Subscribe to Webhook. On success, returns ID of webhook subscription. |
| DELETE | /api/Webhook | Delete webhook subscription by URL |
| GET | /api/Webhook/{id} | Get Webhook Subscription by SubscriptionID |
| DELETE | /api/Webhook/{id} | Delete Webhook Subscription by ID |

### ScheduleSeries
| Method | Path | Description |
|--------|------|-------------|
| POST | /ScheduleSeries/AddBooking | Create new Schedule Booking |
| POST | /ScheduleSeries/AddLeave | Create new Leave Booking |
| PUT | /ScheduleSeries/EditLeave | Edit Leave Booking |
| PUT | /ScheduleSeries/EditBooking | Edit Booking |

## Enhanced Skill Content
## Question Mapping

- "What account am I authenticated as?" -> GET /api/Account
- "Show me all invoices for a specific company" -> GET /api/Invoice (with CompanyIDFK filter)
- "How many hours did a user log this week?" -> GET /api/Timesheet (with EntryDateFrom, EntryDateTo, UserID)
- "Create a new project and assign team members" -> POST /api/Project, then POST /api/ProjectMember
- "Which tasks are overdue?" -> GET /api/Task (with DueDateTo set to today, isComplete=false)
- "Record a timesheet entry and start a timer" -> POST /api/Timesheet, then POST /api/TimesheetTimer/{id}
- "Submit expenses for approval" -> POST /api/ExpenseApproval/Submit (with ExpenseIDs)
- "Find a company by name" -> GET /api/Company/Lookup (with search parameter)
- "Get a summary of billable vs non-billable time on a project" -> GET /api/TimesheetSummary (with model.projectID, model.isBillable)
- "Schedule a team member for a booking" -> POST /ScheduleSeries/AddBooking
- "What changed since yesterday across invoices and bills?" -> GET /api/Invoice (UpdatedAfter), GET /api/Bill (UpdatedAfter)
- "Delete a timesheet entry" -> DELETE /api/Timesheet/{id}
- "List all active projects for a specific client" -> GET /api/Project (with CompanyID, ProjectStatusCode)
- "Upload a receipt to an expense" -> POST /api/Expense/Attachment (with File)
- "Who is currently running a timer?" -> GET /api/TimesheetTimer

## Response Tips

- **List endpoints** (Bill, Invoice, Task, Timesheet, etc.): Paginated via `pageSize` and `pageNumber` params -- always check total count in the response and loop pages if needed. Default page size is typically 100.
- **Lookup endpoints** (Company/Lookup, Project/Lookup, Task/Lookup): Lightweight search results; use `search` param for fuzzy matching and paginate with `pageSize`/`pageNumber`.
- **Single-resource GETs** (/{id} endpoints): Return the full object or 404. Expect nested objects for related entities (e.g., line items inside Invoice).
- **Summary endpoints** (TimesheetSummary, ExpenseSummary): Grouped aggregates controlled by `model.groupBy` -- the response shape changes depending on the grouping dimension.
- **Create/Update endpoints** (POST/PUT): Return the created/updated object on 200. The `model` body is a map -- inspect the returned object to discover the full field schema.
- **Delete endpoints**: Return 200 on success. Some accept an ID in the path (Timesheet/{id}), others in the body or query (Task requires TaskID, Section requires SectionID).
- **Schedule endpoints** (ScheduleSeries, ScheduleAssignment): Bookings and leave have separate create/edit paths under /ScheduleSeries; query assignments via /api/ScheduleAssignment.

## Anomaly Flags

- **401 on any endpoint**: OAuth2 token has expired or is invalid -- surface immediately and prompt for re-authentication.
- **404 on resource fetch**: The ID may have been deleted or the user lacks permission -- flag before retrying with a different ID.
- **409 on webhook creation**: A webhook with that target URL already exists -- surface the conflict and suggest listing existing webhooks first.
- **400 on timer operations**: Timer start/stop can fail if the timesheet entry is in an invalid state (already running, already submitted) -- surface the specific error message.
- **Pagination exhaustion**: If a list response returns a full page, warn the user that additional pages likely exist and offer to fetch them.
- **UpdatedAfter returning empty results**: If polling for changes yields nothing repeatedly, flag that the sync window may be too narrow or the data is stale.
- **Expense approval with no SendNotifications flag**: Surface that notifications are off by default so approvers may not be alerted.
- **Deprecated or missing fields in responses**: If an expected field returns null or is absent in a response object, flag it as a potential schema change.

## Playbook

### 1. Invoice a Client for Tracked Time

1. GET /api/Timesheet with `ProjectID`, `isBillable=true`, `isInvoiced=false`, `EntryDateFrom`, `EntryDateTo` to collect uninvoiced billable entries.
2. GET /api/Project/{id} to confirm the billing rate and client company.
3. POST /api/Invoice with line items referencing the timesheet entries and the CompanyIDFK.
4. Verify the invoice with GET /api/Invoice/{id} and confirm the total matches expectations.

### 2. Onboard a New Project

1. POST /api/Company to create the client (or GET /api/Company/Lookup to find an existing one).
2. POST /api/Project with the company ID, billing type, and budget settings.
3. POST /api/Section to create task sections/phases within the project.
4. POST /api/Task to add tasks under each section.
5. POST /api/ProjectMember for each team member, linking them to the project.
6. POST /api/ProjectTimesheetCategory to configure which time categories apply.

### 3. Weekly Timesheet Review and Submission

1. GET /api/UserProfile to identify the user(s) to review.
2. GET /api/Timesheet with `UserID`, `EntryDateFrom` (Monday), `EntryDateTo` (Sunday) to pull the week's entries.
3. GET /api/TimesheetSummary with `model.entryDateFrom`, `model.entryDateTo`, `model.userID` to check total hours.
4. For any running timers, GET /api/TimesheetTimer with `UserID`, then DELETE /api/TimesheetTimer/{id} to stop them.
5. POST /api/TimesheetSubmission with `WholeWeekOf` set to the Monday date to submit the full week.

### 4. Expense Tracking and Reimbursement

1. POST /api/Expense to log the expense with amount, category, and project.
2. POST /api/Expense/Attachment with the receipt file to attach proof.
3. Repeat steps 1-2 for each expense in the reporting period.
4. POST /api/ExpenseApproval/Submit with all ExpenseIDs and `SendNotifications=true`.
5. GET /api/ExpenseSummary with date range and `model.groupBy` to verify the totals.

### 5. Sync Changes Since Last Poll

1. Record the current timestamp as the new sync marker.
2. In parallel, call GET on each entity with `UpdatedAfter` set to the last sync timestamp: /api/Company, /api/Invoice, /api/Bill, /api/Timesheet, /api/Task, /api/Expense.
3. Page through each result set using `pageNumber` until all pages are consumed.
4. For deleted timesheets specifically, call GET /api/Timesheet/deleted with `DeletedAfter`.
5. Store the timestamp from step 1 as the new sync marker for the next run.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
