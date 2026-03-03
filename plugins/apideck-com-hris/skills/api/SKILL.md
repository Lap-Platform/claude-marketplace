---
name: hris-api
description: "HRIS API skill. Use when working with HRIS for hris. Covers 25 endpoints."
version: 1.0.0
generator: lapsh
---

# HRIS API
API version: 10.24.0

## Auth
ApiKey Authorization in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /hris/employees -- verify access
3. POST /hris/employees -- create first employees

## Endpoints

25 endpoints across 1 groups. See references/api-spec.lap for full details.

### hris
| Method | Path | Description |
|--------|------|-------------|
| GET | /hris/employees | List Employees |
| POST | /hris/employees | Create Employee |
| GET | /hris/employees/{id} | Get Employee |
| PATCH | /hris/employees/{id} | Update Employee |
| DELETE | /hris/employees/{id} | Delete Employee |
| GET | /hris/companies | List Companies |
| POST | /hris/companies | Create Company |
| GET | /hris/companies/{id} | Get Company |
| PATCH | /hris/companies/{id} | Update Company |
| DELETE | /hris/companies/{id} | Delete Company |
| GET | /hris/departments | List Departments |
| POST | /hris/departments | Create Department |
| GET | /hris/departments/{id} | Get Department |
| PATCH | /hris/departments/{id} | Update Department |
| DELETE | /hris/departments/{id} | Delete Department |
| GET | /hris/payrolls | List Payroll |
| GET | /hris/payrolls/{payroll_id} | Get Payroll |
| GET | /hris/payrolls/employees/{employee_id} | List Employee Payrolls |
| GET | /hris/payrolls/employees/{employee_id}/payrolls/{payroll_id} | Get Employee Payroll |
| GET | /hris/schedules/employees/{employee_id} | List Employee Schedules |
| GET | /hris/time-off-requests | List Time Off Requests |
| POST | /hris/time-off-requests | Create Time Off Request |
| GET | /hris/time-off-requests/employees/{employee_id}/time-off-requests/{id} | Get Time Off Request |
| PATCH | /hris/time-off-requests/employees/{employee_id}/time-off-requests/{id} | Update Time Off Request |
| DELETE | /hris/time-off-requests/employees/{employee_id}/time-off-requests/{id} | Delete Time Off Request |

## Enhanced Skill Content
## Question Mapping

- "How do I list all employees?" -> GET /hris/employees
- "How do I find a specific employee by ID?" -> GET /hris/employees/{id}
- "How do I add a new employee to the system?" -> POST /hris/employees
- "How do I update an employee's job title or department?" -> PATCH /hris/employees/{id}
- "How do I terminate or remove an employee record?" -> DELETE /hris/employees/{id}
- "What companies are in the system?" -> GET /hris/companies
- "How do I look up payroll details for a specific pay period?" -> GET /hris/payrolls/{payroll_id}
- "How do I see all payrolls for a particular employee?" -> GET /hris/payrolls/employees/{employee_id}
- "How do I submit a time-off request for an employee?" -> POST /hris/time-off-requests
- "How do I check the status of an employee's time-off request?" -> GET /hris/time-off-requests/employees/{employee_id}/time-off-requests/{id}
- "How do I approve or decline a time-off request?" -> PATCH /hris/time-off-requests/employees/{employee_id}/time-off-requests/{id}
- "What departments exist in the organization?" -> GET /hris/departments
- "How do I create a new department?" -> POST /hris/departments
- "How do I view an employee's work schedule?" -> GET /hris/schedules/employees/{employee_id}
- "How do I get a single payroll record for a specific employee?" -> GET /hris/payrolls/employees/{employee_id}/payrolls/{payroll_id}

## Response Tips

- **Employees, Companies, Departments, Time-off lists**: Paginated via cursor -- check `meta.cursors.next` and `links.next`; default page size is 20. Iterate until `next` is null.
- **Single-resource GETs**: Data lives under `data` as a flat object; nested arrays like `jobs`, `compensations`, `addresses`, `phone_numbers` may be empty arrays rather than null.
- **Create/Update/Delete responses**: Return only `data.id` -- re-fetch the resource if you need the full record after mutation.
- **Payrolls**: The `totals` sub-object contains financials (`gross_pay`, `net_pay`, `employer_taxes`, etc.) -- all fields are nullable, so check before computing.
- **Schedules**: Response nests a full `employee` object alongside `schedules` array under `data` -- do not confuse the top-level `data.employee` with a standalone employee response.
- **Errors**: All endpoints share the same error codes (400, 401, 402, 404, 422) -- 402 indicates a payment/plan issue with the upstream connector, not a billing error in your code.

## Anomaly Flags

- **402 Payment Required**: Surface immediately -- indicates the downstream HRIS connector requires a plan upgrade or billing action; no retry will fix it.
- **422 Unprocessable Entity**: Flag the specific validation failures; often caused by missing required nested fields (e.g., `number` in phone_numbers, `email` in emails, `url` in social_links) marked with `!`.
- **Empty `jobs` or `compensations` arrays**: Warn when an employee record has no job entries -- this often means the profile is incomplete or the connector does not sync job data.
- **`employment_status: terminated` with no `employment_end_date`**: Data inconsistency worth flagging to the user.
- **`deleted: true` on employee or company records**: Surface proactively -- soft-deleted records may appear in list responses and should be filtered or highlighted.
- **Null `row_version` on update targets**: The `row_version` field enables optimistic concurrency; if absent, warn that concurrent edits risk silent overwrites.
- **`_raw` field present**: When `raw=true` is passed, responses include `_raw` with the unprocessed upstream payload -- flag if this appears unexpectedly large or contains sensitive data.

## Playbook

### 1. Onboard a New Employee

1. GET /hris/companies to find the target `company_id`.
2. GET /hris/departments to find the target `department_id`.
3. POST /hris/employees with `first_name`, `last_name`, `company_id`, `department_id`, `employment_start_date`, `employment_status: "active"`, and at least one entry in `emails` and `jobs`.
4. Capture the returned `data.id`.
5. GET /hris/employees/{id} to verify the record was created correctly.

### 2. Process and Review a Payroll Cycle

1. GET /hris/payrolls with `filter` for the target date range to find available payroll runs.
2. GET /hris/payrolls/{payroll_id} to inspect totals (`gross_pay`, `net_pay`, `employer_taxes`).
3. GET /hris/employees to list all active employees (filter by `employment_status: active`).
4. For each employee, GET /hris/payrolls/employees/{employee_id}/payrolls/{payroll_id} to review individual compensation breakdowns.
5. Flag any employee whose `check_amount` is null or zero.

### 3. Submit and Track a Time-Off Request

1. GET /hris/employees/{id} to confirm the employee exists and is active.
2. POST /hris/time-off-requests with `employee_id`, `start_date`, `end_date`, `request_type` (e.g., `vacation`), `units`, and `amount`.
3. Capture the returned `data.id`.
4. GET /hris/time-off-requests/employees/{employee_id}/time-off-requests/{id} to check `status`.
5. To approve: PATCH /hris/time-off-requests/employees/{employee_id}/time-off-requests/{id} with `status: "approved"` and `approval_date`.

### 4. Reorganize Department Structure

1. GET /hris/departments to list current departments and their `parent_id` hierarchy.
2. POST /hris/departments to create any new departments (set `parent_id` to nest under an existing one).
3. GET /hris/employees with `filter` for the old `department_id` to find affected employees.
4. For each employee, PATCH /hris/employees/{id} with the new `department_id` and `department_name`.
5. DELETE /hris/departments/{id} to remove the old department once empty.

### 5. Audit Employee Data Completeness

1. GET /hris/employees with `limit: 20`, iterating via `cursor` until all pages are consumed.
2. For each employee, check for missing critical fields: `emails` (empty array), `phone_numbers` (empty array), `jobs` (empty array), `employment_status` (null).
3. GET /hris/employees/{id} for any flagged record to inspect full details including `bank_accounts`, `tax_id`, and `addresses`.
4. PATCH /hris/employees/{id} to fill in missing fields as needed.
5. Compile a summary of records still missing data after remediation.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
