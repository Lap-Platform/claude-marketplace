---
name: xero-payroll-au-api
description: "Xero Payroll AU API skill. Use when working with Xero Payroll AU for Employees, LeaveApplications, PayItems. Covers 32 endpoints."
version: 1.0.0
generator: lapsh
---

# Xero Payroll AU API
API version: 11.1.0

## Auth
OAuth2

## Base URL
https://api.xero.com/payroll.xro/1.0

## Setup
1. Configure auth: OAuth2
2. GET /Employees -- verify access
3. POST /Employees -- create first Employees

## Endpoints

32 endpoints across 10 groups. See references/api-spec.lap for full details.

### Employees
| Method | Path | Description |
|--------|------|-------------|
| GET | /Employees | Searches payroll employees |
| POST | /Employees | Creates a payroll employee |
| GET | /Employees/{EmployeeID} | Retrieves an employee's detail by unique employee id |
| POST | /Employees/{EmployeeID} | Updates an employee's detail |

### LeaveApplications
| Method | Path | Description |
|--------|------|-------------|
| GET | /LeaveApplications | Retrieves leave applications |
| POST | /LeaveApplications | Creates a leave application |
| GET | /LeaveApplications/v2 | Retrieves leave applications including leave requests |
| GET | /LeaveApplications/{LeaveApplicationID} | Retrieves a leave application by a unique leave application id |
| POST | /LeaveApplications/{LeaveApplicationID} | Updates a specific leave application |
| POST | /LeaveApplications/{LeaveApplicationID}/approve | Approve a requested leave application by a unique leave application id |
| POST | /LeaveApplications/{LeaveApplicationID}/reject | Reject a leave application by a unique leave application id |

### PayItems
| Method | Path | Description |
|--------|------|-------------|
| GET | /PayItems | Retrieves pay items |
| POST | /PayItems | Creates a pay item |

### PayrollCalendars
| Method | Path | Description |
|--------|------|-------------|
| GET | /PayrollCalendars | Retrieves payroll calendars |
| POST | /PayrollCalendars | Creates a Payroll Calendar |
| GET | /PayrollCalendars/{PayrollCalendarID} | Retrieves payroll calendar by using a unique payroll calendar ID |

### PayRuns
| Method | Path | Description |
|--------|------|-------------|
| GET | /PayRuns | Retrieves pay runs |
| POST | /PayRuns | Creates a pay run |
| GET | /PayRuns/{PayRunID} | Retrieves a pay run by using a unique pay run id |
| POST | /PayRuns/{PayRunID} | Updates a pay run |

### Payslip
| Method | Path | Description |
|--------|------|-------------|
| GET | /Payslip/{PayslipID} | Retrieves for a payslip by a unique payslip id |
| POST | /Payslip/{PayslipID} | Updates a payslip |

### Settings
| Method | Path | Description |
|--------|------|-------------|
| GET | /Settings | Retrieves payroll settings |

### Superfunds
| Method | Path | Description |
|--------|------|-------------|
| GET | /Superfunds | Retrieves superfunds |
| POST | /Superfunds | Creates a superfund |
| GET | /Superfunds/{SuperFundID} | Retrieves a superfund by using a unique superfund ID |
| POST | /Superfunds/{SuperFundID} | Updates a superfund |

### SuperfundProducts
| Method | Path | Description |
|--------|------|-------------|
| GET | /SuperfundProducts | Retrieves superfund products |

### Timesheets
| Method | Path | Description |
|--------|------|-------------|
| GET | /Timesheets | Retrieves timesheets |
| POST | /Timesheets | Creates a timesheet |
| GET | /Timesheets/{TimesheetID} | Retrieves a timesheet by using a unique timesheet id |
| POST | /Timesheets/{TimesheetID} | Updates a timesheet |

## Enhanced Skill Content
## Question Mapping

- "How do I list all employees?" -> GET /Employees
- "How do I add a new employee to payroll?" -> POST /Employees
- "How do I get details for a specific employee?" -> GET /Employees/{EmployeeID}
- "How do I update an employee's information?" -> POST /Employees/{EmployeeID}
- "How do I see all pending leave requests?" -> GET /LeaveApplications
- "How do I approve a leave application?" -> POST /LeaveApplications/{LeaveApplicationID}/approve
- "How do I reject a leave request?" -> POST /LeaveApplications/{LeaveApplicationID}/reject
- "What earnings rates, deduction types, and leave types are configured?" -> GET /PayItems
- "How do I create a new earnings rate or deduction type?" -> POST /PayItems
- "How do I view payroll calendars and pay schedules?" -> GET /PayrollCalendars
- "How do I run payroll?" -> POST /PayRuns
- "How do I get a specific employee's payslip?" -> GET /Payslip/{PayslipID}
- "How do I look up a super fund by ABN or USI?" -> GET /SuperfundProducts
- "How do I submit a timesheet for an employee?" -> POST /Timesheets
- "What are the current payroll settings and tracking categories?" -> GET /Settings

## Response Tips

- **Employees, LeaveApplications, PayrollCalendars, PayRuns, Superfunds, Timesheets**: All list endpoints return arrays inside a named wrapper (e.g., `{Employees: [...]}`). Use the `page` parameter for pagination; results are paged server-side. Use `where` and `order` for filtering and sorting using OData-style syntax.
- **PayItems**: Returns a nested map with four sub-arrays (`EarningsRates`, `DeductionTypes`, `LeaveTypes`, `ReimbursementTypes`) -- always check each sub-array independently.
- **Payslip**: Single GET returns a flat `Payslip` object (not an array) with multiple line-item arrays (`EarningsLines`, `DeductionLines`, `SuperannuationLines`, `TaxLines`, etc.). POST returns `Payslips` (plural array).
- **Settings**: Single non-paginated response. `TrackingCategories` contains nested `EmployeeGroups` and `TimesheetCategories` maps -- not arrays.
- **SuperfundProducts**: Filter by `ABN` or `USI` query params; no pagination or `where`/`order` support.
- **Errors**: All 400 responses indicate validation failures. Check the response body for field-level error details. POST endpoints support `Idempotency-Key` headers to safely retry on network failures.

## Anomaly Flags

- **Idempotency-Key missing on retries**: Surface a warning if a POST request is retried without an `Idempotency-Key` header, which risks duplicate record creation.
- **If-Modified-Since ignored**: If a list response returns the same data after passing `If-Modified-Since`, flag that the filter may not be reducing payload as expected.
- **ValidationErrors in Timesheets**: `GET /Timesheets/{TimesheetID}` returns a `ValidationErrors` array -- proactively surface any non-empty validation errors to the user.
- **Stale UpdatedDateUTC**: If `UpdatedDateUTC` on a record is significantly older than expected after a POST update, flag a potential conflict or caching issue.
- **LeaveApplications v1 vs v2**: Two list endpoints exist (`/LeaveApplications` and `/LeaveApplications/v2`). Flag if the user is using v1 when v2 may return richer data.
- **STP2 compliance**: `Settings.EmployeesAreSTP2` indicates Single Touch Payroll Phase 2 status. Surface this when creating earnings rates or deduction types, as `AllowanceCategory` and `DeductionCategory` fields are STP2-specific.
- **CurrentRecord flag**: PayItems sub-types include `CurrentRecord` booleans. Flag any items where `CurrentRecord` is false, as these are inactive/archived and should not be assigned to employees.

## Playbook

### 1. Onboard a New Employee

1. `GET /Settings` -- confirm payroll year, tracking categories, and STP2 status.
2. `GET /PayrollCalendars` -- identify the correct pay calendar to assign.
3. `GET /Superfunds` -- find the employee's super fund, or `GET /SuperfundProducts?ABN=...` to look it up.
4. `POST /Employees` -- create the employee record with personal details, bank account, super fund membership, and pay calendar assignment. Include `Idempotency-Key`.
5. Confirm creation by checking the returned `Employees[0].EmployeeID`.

### 2. Process a Pay Run

1. `GET /PayrollCalendars` -- identify the calendar and confirm the next pay period dates.
2. `GET /Timesheets?where=Status=="Approved"` -- pull approved timesheets for the period.
3. `POST /PayRuns` -- create a new pay run for the calendar. Include `Idempotency-Key`.
4. `GET /PayRuns/{PayRunID}` -- review the draft pay run and its calculated payslips.
5. `GET /Payslip/{PayslipID}` -- inspect individual payslips for accuracy (check `EarningsLines`, `TaxLines`, `SuperannuationLines`).
6. `POST /PayRuns/{PayRunID}` -- update the pay run status to post/finalize it.

### 3. Handle a Leave Request

1. `GET /LeaveApplications/v2` -- list recent leave applications to find pending ones.
2. `GET /LeaveApplications/{LeaveApplicationID}` -- review the specific application details.
3. `POST /LeaveApplications/{LeaveApplicationID}/approve` or `/reject` -- action the request. Include `Idempotency-Key`.
4. Confirm the updated status in the response.

### 4. Configure Pay Items

1. `GET /PayItems` -- review current earnings rates, deduction types, leave types, and reimbursement types.
2. `GET /Settings` -- check `EmployeesAreSTP2` to determine if STP2 category fields are required.
3. `POST /PayItems` -- submit new or updated items in the appropriate sub-array. For earnings rates, set `EarningsType`, `RateType`, and STP2 fields (`AllowanceType`, `AllowanceCategory`) as needed. Include `Idempotency-Key`.
4. Verify the response to confirm items were created with `CurrentRecord: true`.

### 5. Submit and Review Timesheets

1. `GET /Employees` -- identify the employee(s) for timesheet entry.
2. `POST /Timesheets` -- submit a new timesheet with `EmployeeID`, `StartDate`, `EndDate`, and `TimesheetLines`. Include `Idempotency-Key`.
3. `GET /Timesheets/{TimesheetID}` -- review the submitted timesheet. Check `Status` and inspect `ValidationErrors` for any issues.
4. `POST /Timesheets/{TimesheetID}` -- update to correct errors or change status if needed.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
