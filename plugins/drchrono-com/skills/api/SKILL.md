---
name: api
description: " API skill. Use when working with  for api. Covers 327 endpoints."
version: 1.0.0
generator: lapsh
---

# 
API version: v4 - Hunt Valley

## Auth
OAuth2

## Base URL
https://app.drchrono.com

## Setup
1. Configure auth: OAuth2
2. GET /api/day_sheet_charges -- verify access
3. POST /api/claim_billing_notes -- create first claim_billing_notes

## Endpoints

327 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/day_sheet_charges | Retrieve daysheet charges report for a given date range |
| POST | /api/claim_billing_notes | Create a new billing note |
| GET | /api/claim_billing_notes | Retrieve or search billing notes |
| POST | /api/signed_consent_forms | signed_consent_forms Create |
| PATCH | /api/signed_consent_forms | signed_consent_forms Update |
| GET | /api/signed_consent_forms | signed_consent_forms Get |
| POST | /api/custom_appointment_fields | Create custom appointment fields |
| GET | /api/custom_appointment_fields | Retrieve or search custom appointment fields |
| PUT | /api/lab_orders/{id} | Update an existing lab order |
| PATCH | /api/lab_orders/{id} | Update an existing lab order |
| GET | /api/lab_orders/{id} | Retrieve an existing lab order |
| DELETE | /api/lab_orders/{id} | Delete an existing lab order |
| POST | /api/clinical_notes_list | Create clinical note list request.  Use the UUID returned in the response to retrieve the batch of records. Results returned in order of ID. |
| GET | /api/clinical_notes_list | Retrieve or search clinical notes in batches. Results returned in order of ID. |
| GET | /api/custom_vitals/{id} | Retrieve an existing custom vital type |
| PUT | /api/sublabs/{id} | Update an existing sub vendor |
| PATCH | /api/sublabs/{id} | Update an existing sub vendor |
| GET | /api/sublabs/{id} | Retrieve an existing sub vendor |
| DELETE | /api/sublabs/{id} | Delete an existing sub vendor |
| GET | /api/patients/{id}/qrda1 | Retrieve patient QRDA1 |
| POST | /api/problems | Create patient problems |
| GET | /api/problems | Retrieve or search patient problems |
| GET | /api/staff |  |
| PUT | /api/patient_messages/{id} |  |
| PATCH | /api/patient_messages/{id} |  |
| GET | /api/patient_messages/{id} |  |
| POST | /api/yellow_notepad | Create or update yellow notepad content for a specific appointment and template combination. |
| GET | /api/yellow_notepad | Retrieve yellow notepad content for a specific appointment and template combination. |
| GET | /api/eligibility_checks | Retrieve or search past eligibility checks for patient |
| PUT | /api/doctor_work_schedule/{id} | Update an existing doctor's entire work schedule |
| PATCH | /api/doctor_work_schedule/{id} | Update an existing doctor's work schedule |
| GET | /api/doctor_work_schedule/{id} | Retrieve a work schedule for the doctor (beta) |
| POST | /api/medications | Create patient medications |
| GET | /api/medications | Retrieve or search patient medications |
| POST | /api/custom_demographics | Create custom demographics fields |
| GET | /api/custom_demographics | Retrieve or search custom demographics fields |
| POST | /api/appointments_list |  |
| GET | /api/appointments_list |  |
| POST | /api/appointment_profiles | Create appointment profiles for a doctor's calendar |
| GET | /api/appointment_profiles | Retrieve or search appointment profiles for a doctor's calendar |
| POST | /api/patient_communications | Create patient communication for CQM |
| GET | /api/patient_communications | Retrieve or search patient communications for CQM |
| GET | /api/patient_authorizations | Retrieve or search patient authorizations |
| PUT | /api/appointment_profiles/{id} | Update an existing appointment profile |
| PATCH | /api/appointment_profiles/{id} | Update an existing appointment profile |
| GET | /api/appointment_profiles/{id} | Retrieve an existing appointment profile |
| DELETE | /api/appointment_profiles/{id} | Delete an existing appointment profile |
| POST | /api/messages | Create messages in doctor's message center |
| GET | /api/messages | Retrieve or search messages in doctor's message center |
| PUT | /api/clinical_note_field_values/{id} | Update an existing clinical note field value |
| PATCH | /api/clinical_note_field_values/{id} | Update an existing clinical note field value |
| GET | /api/clinical_note_field_values/{id} | Retrieve an existing clinical note field value |
| POST | /api/task_categories | Create a task category |
| GET | /api/task_categories | Retrieve or search task categories |
| GET | /api/fee_schedules_v2 |  |
| GET | /api/custom_insurance_plan_names/{id} | Retrieve an existing custom insurance plan name |
| GET | /api/care_team_members |  |
| GET | /api/user_groups | Retrieve or search user groups |
| POST | /api/line_items_list | Create a billing line items list request |
| GET | /api/line_items_list | Retrieve the list of billing line items |
| POST | /api/consent_forms/{id}/unapply_from_appointment | Unassign (unapply) a consent form from appointment |
| POST | /api/consent_forms/{id}/apply_to_appointment | Assign (apply) a consent form to appointment |
| POST | /api/consent_forms | Create a patient consent form |
| GET | /api/consent_forms | Retrieve or search patient consent forms |
| PUT | /api/reminder_profiles/{id} | Update an existing reminder profile |
| PATCH | /api/reminder_profiles/{id} | Update an existing reminder profile |
| GET | /api/reminder_profiles/{id} | Retrieve an existing reminder profile |
| DELETE | /api/reminder_profiles/{id} | Delete an existing reminder profile |
| GET | /api/day_sheet_patient_payments | Retrieve daysheet cash report for a given date range |
| POST | /api/offices/{id}/add_exam_room | Add an exam room to the office |
| GET | /api/eligibility_checks/{id} | Retrieve an existing past eligibility check |
| POST | /api/patients_list | Submit patient list request.  Use the UUID returned in the response to retrieve the batch of patients. |
| GET | /api/patients_list | Retrieve or search patients in batches. This resource returns identical data to `GET /api/patients` but uses an asynchronous batch-based approach to data delivery. This is an efficient choice for large historical record loading use cases. Retrieve the results/status of a previously created patient_list request using the UUID returned in the response. Results are ordered by patient ID number. |
| POST | /api/patient_interventions | Create patient intervention for CQM |
| GET | /api/patient_interventions | Retrieve or search patient interventions for CQM |
| POST | /api/patient_messages |  |
| GET | /api/patient_messages |  |
| PUT | /api/patient_physical_exams/{id} | Update an existing patient physical exam for CQM |
| PATCH | /api/patient_physical_exams/{id} | Update an existing patient physical exam for CQM |
| GET | /api/patient_physical_exams/{id} | Retrieve an existing patient physical exam for CQM |
| POST | /api/clinical_note_field_values | Create clinical note field value |
| GET | /api/clinical_note_field_values | Retrieve or search clinical note field values |
| GET | /api/inventory_vaccines/{id} | Retrieve an existing vaccine inventory |
| POST | /api/patients | Create patient |
| GET | /api/patients | Retrieve or search patients |
| GET | /api/implantable_devices/{id} | Retrieve an existing implantable device |
| PUT | /api/patient_communications/{id} | Update an existing patient communication for CQM |
| PATCH | /api/patient_communications/{id} | Update an existing patient communication for CQM |
| GET | /api/patient_communications/{id} | Retrieve an existing patient communication for CQM |
| GET | /api/offices | Retrieve or search offices |
| GET | /api/prescription_messages/{id} | Retrieve an existing prescription message |
| GET | /api/implantable_devices | Retrieve or search implantable devices |
| POST | /api/patient_risk_assessments |  |
| GET | /api/patient_risk_assessments |  |
| PUT | /api/task_statuses/{id} | Update an existing task status |
| PATCH | /api/task_statuses/{id} | Update an existing task status |
| GET | /api/task_statuses/{id} | Retrieve an existing task status |
| POST | /api/patients_summary |  |
| GET | /api/patients_summary |  |
| PUT | /api/documents/{id} | Update an existing appointment template |
| PATCH | /api/documents/{id} | Update an existing appointment template |
| GET | /api/documents/{id} | Retrieve an existing appointment template |
| DELETE | /api/documents/{id} | Delete an existing appointment template |
| GET | /api/office_work_schedule | Get the work schedule for the authed doctor's primary office (beta) |
| POST | /api/patients/{id}/onpatient_access | Send new onpatient invite to patient |
| GET | /api/patients/{id}/onpatient_access | Retrieve or search existing onpatient access invites |
| DELETE | /api/patients/{id}/onpatient_access | Revoke sent onpatient invites |
| POST | /api/comm_logs | Create communication (phone call) logs |
| GET | /api/comm_logs | Retrieve or search communicatioin (phone call) logs |
| PUT | /api/lab_results/{id} | Update an existing lab result |
| PATCH | /api/lab_results/{id} | Update an existing lab result |
| GET | /api/lab_results/{id} | Retrieve an existing lab result |
| DELETE | /api/lab_results/{id} | Delete an existing lab result |
| PUT | /api/medications/{id} | Update an existing patient medications |
| PATCH | /api/medications/{id} | Update an existing patient medications |
| GET | /api/medications/{id} | Retrieve an existing patient medications |
| GET | /api/day_sheet_credits | Retrieve daysheet credits/adjustments report for a given date range |
| POST | /api/task_templates | Create a task template |
| GET | /api/task_templates | Retrieve or search task templates |
| POST | /api/transactions_list | Create transactions list request.  Use the UUID returned in the response to retrieve the batch of records. Results returned in order of id or updated_at. |
| GET | /api/transactions_list | Retrieve or search transactions in batches. Results returned in order of ID or updated_at. |
| PATCH | /api/medications/{id}/append_to_pharmacy_note | Append a message to the "pharmacy_note" section of the prescription, in a new paragraph |
| PUT | /api/office_work_schedule/{id} | Update an existing office's entire work schedule |
| PATCH | /api/office_work_schedule/{id} | Update an existing office's work schedule |
| GET | /api/office_work_schedule/{id} | Retrieve a work schedule (beta) |
| PUT | /api/patient_vaccine_records/{id} | Update an existing patient vaccine records |
| PATCH | /api/patient_vaccine_records/{id} | Update an existing patient vaccine records |
| GET | /api/patient_vaccine_records/{id} | Retrieve an existing patient vaccine records |
| PUT | /api/patient_flag_types/{id} | Update an existing patient flag type |
| PATCH | /api/patient_flag_types/{id} | Update an existing patient flag type |
| GET | /api/patient_flag_types/{id} | Retrieve an existing patient flag type |
| GET | /api/inventory_categories/{id} | Retrieve an existing inventory category |
| PATCH | /api/clinical_note_field_types/{id} | Update the `freedraw_image_size` of an existing clinical note FreeDraw Field |
| GET | /api/clinical_note_field_types/{id} | Retrieve an existing clinial note field type |
| PUT | /api/tasks/{id} | Update an existing task |
| PATCH | /api/tasks/{id} | Update an existing task |
| GET | /api/tasks/{id} | Retrieve an existing task |
| GET | /api/doctor_work_schedule | Get the work schedule for the authed doctor's primary office (beta) |
| GET | /api/doctor_options | Retrieve or search doctor options within practice group |
| GET | /api/fee_schedules |  |
| PUT | /api/patient_risk_assessments/{id} |  |
| PATCH | /api/patient_risk_assessments/{id} |  |
| GET | /api/patient_risk_assessments/{id} |  |
| GET | /api/inventory_categories | Retrieve or search inventory categories |
| PUT | /api/lab_documents/{id} | Update an existing lab order document |
| PATCH | /api/lab_documents/{id} | Update an existing lab order document |
| GET | /api/lab_documents/{id} | Retrieve an existing lab order document |
| DELETE | /api/lab_documents/{id} | Delete an existing lab order document |
| PUT | /api/appointment_templates/{id} | Update an existing appointment template |
| PATCH | /api/appointment_templates/{id} | Update an existing appointment template |
| GET | /api/appointment_templates/{id} | Retrieve an existing appointment template |
| DELETE | /api/appointment_templates/{id} | Delete an existing appointment template |
| PUT | /api/patient_interventions/{id} | Update an existing patient intervention for CQM |
| PATCH | /api/patient_interventions/{id} | Update an existing patient intervention for CQM |
| GET | /api/patient_interventions/{id} | Retrieve an existing patient intervention for CQM |
| POST | /api/task_statuses | Create a task status |
| GET | /api/task_statuses | Retrieve or search task statuses |
| PUT | /api/allergies/{id} | Update an existing patient allergy |
| PATCH | /api/allergies/{id} | Update an existing patient allergy |
| GET | /api/allergies/{id} | Retrieve an existing patient allergy |
| GET | /api/patients/{id}/ccda | Retrieve patient CCDA |
| GET | /api/patient_payments/{id} | Retrieve an existing patient payment |
| GET | /api/lab_orders_summary |  |
| POST | /api/patient_payments | Create patient payment |
| GET | /api/patient_payments | Retrieve or search patient payments |
| POST | /api/clinical_note_field_values_list | Create clinical note field value list request.  Use the UUID returned in the response to retrieve the batch of records. Results returned in order of ID. |
| GET | /api/clinical_note_field_values_list | Retrieve or search clinical note values (soap notes) in batches. Results returned in order of ID or by updated_at. |
| GET | /api/care_plans/{id} | Retrieve an existing care plan |
| GET | /api/billing_profiles | Retrieve or search billing profiles |
| GET | /api/billing_profiles/{id} | Retrieve an existing billing profiles |
| GET | /api/availability | Retrieve availability slots for the given date and office, doctor, or exam room. |
| PUT | /api/task_templates/{id} | Update an existing task template |
| PATCH | /api/task_templates/{id} | Update an existing task template |
| GET | /api/task_templates/{id} | Retrieve an existing task template |
| GET | /api/fee_schedules/{id} |  |
| PUT | /api/appointments/{id} | Update an existing appointment or break |
| PATCH | /api/appointments/{id} | Update an existing appointment or break |
| GET | /api/appointments/{id} | Retrieve an existing appointment or break |
| DELETE | /api/appointments/{id} | Delete an existing appointment or break |
| POST | /api/telehealth_appointments |  |
| GET | /api/telehealth_appointments |  |
| GET | /api/care_plans | Retrieve or search care plans |
| POST | /api/patient_physical_exams | Create patient physical exam for CQM |
| GET | /api/patient_physical_exams | Retrieve or search patient physical exams for CQM |
| GET | /api/line_item_deletions | Retrieve or search billing line item deletions. When a billing line item is deleted, a record of its original ID and the appointment it was attached to will be logged and is accessible from this resource. |
| GET | /api/signed_consent_forms/{id} | signed_consent_forms Read |
| GET | /api/clinical_note_templates/{id} | Retrieve an existing clinical note tempalte |
| GET | /api/transactions | Retrieve or search insurance transactions associated with billing line items |
| POST | /api/lab_results | Create lab results. An example lab workflow is as following: |
| GET | /api/lab_results | Retrieve or search lab results |
| GET | /api/custom_insurance_plan_names | Retrieve or search custom insurance plan names |
| PUT | /api/problems/{id} | Update an existing patient problems |
| PATCH | /api/problems/{id} | Update an existing patient problems |
| GET | /api/problems/{id} | Retrieve an existing patient problems |
| POST | /api/amendments | Create patient amendments to a patient's clinical records |
| GET | /api/amendments | Retrieve or search patient amendments. You can only interact with amendments created by your API application |
| POST | /api/lab_orders | Create lab orders. An example lab workflow is as following: |
| GET | /api/lab_orders | Retrieve or search lab orders |
| GET | /api/doctors/{id} | Retrieve an existing doctor |
| POST | /api/patient_flag_types | Create patient flag types |
| GET | /api/patient_flag_types | Retrieve or search patient flag types |
| GET | /api/day_sheet_totals | Retrieve daysheet totals report for a given date range |
| PUT | /api/custom_appointment_fields/{id} | Update an existing custom appointment field |
| PATCH | /api/custom_appointment_fields/{id} | Update an existing custom appointment field |
| GET | /api/custom_appointment_fields/{id} | Retrieve an existing custom appointment field |
| POST | /api/eobs | Create EOB object |
| GET | /api/eobs | Retrieve or search EOB objects |
| GET | /api/users/{id} | Retrieve an existing user, `/api/users/current` can be used to identify logged in user, it will redirect to `/api/users/{current_user_id}` |
| GET | /api/insurances |  |
| POST | /api/telehealth_appointment_history |  |
| GET | /api/telehealth_appointment_history |  |
| POST | /api/task_notes | Create a task note |
| GET | /api/task_notes | Retrieve or search task notes |
| POST | /api/tasks | Create a task |
| GET | /api/tasks | Retrieve or search tasks |
| PUT | /api/patients_summary/{id} |  |
| PATCH | /api/patients_summary/{id} |  |
| GET | /api/patients_summary/{id} |  |
| DELETE | /api/patients_summary/{id} |  |
| POST | /api/lab_documents | Create lab order documents. An example lab workflow is as following: |
| GET | /api/lab_documents | Retrieve or search lab order documents |
| PUT | /api/consent_forms/{id} | Update an existing patient consent form |
| PATCH | /api/consent_forms/{id} | Update an existing patient consent form |
| GET | /api/consent_forms/{id} | Retrieve an existing patient consent form |
| PUT | /api/lab_tests/{id} | Update an existing lab test |
| PATCH | /api/lab_tests/{id} | Update an existing lab test |
| GET | /api/lab_tests/{id} | Retrieve an existing lab test |
| DELETE | /api/lab_tests/{id} | Delete an existing lab test |
| POST | /api/prescription_messages_list | Create prescription messages list request.  Use the UUID returned in the response to retrieve the batch of records. Results returned in order of id or updated_at. |
| GET | /api/prescription_messages_list | Retrieve or search prescription messages in batches. Results returned in order of ID or updated_at. |
| PUT | /api/patients/{id} | Update an existing patient |
| PATCH | /api/patients/{id} | Update an existing patient |
| GET | /api/patients/{id} | Retrieve an existing patient |
| DELETE | /api/patients/{id} | Delete an existing patient |
| GET | /api/patients/{id}/ccda_async | Retrieve patient CCDA async. |
| GET | /api/custom_vitals | Retrieve or search custom vital types |
| POST | /api/schedule_blocks | Create a schedule block |
| GET | /api/schedule_blocks | Retrieve and search schedule blocks |
| GET | /api/care_team_members/{id} |  |
| GET | /api/claim_billing_notes/{id} | Retrieve an existing billing note |
| POST | /api/inventory_vaccines | Create vaccine inventory |
| GET | /api/inventory_vaccines | Retrieve or search vaccine inventories |
| GET | /api/transactions/{id} | Retrieve an existing insurance transaction |
| GET | /api/procedures |  |
| PUT | /api/patient_lab_results/{id} |  |
| PATCH | /api/patient_lab_results/{id} |  |
| GET | /api/patient_lab_results/{id} |  |
| DELETE | /api/patient_lab_results/{id} |  |
| PUT | /api/amendments/{id} | Update an existing patient amendment, you can only interact with amendments created by your API application |
| PATCH | /api/amendments/{id} | Update an existing patient amendment, you can only interact with amendments created by your API application |
| GET | /api/amendments/{id} | Retrieve an existing patient amendment, you can only interact with amendments created by your API application |
| DELETE | /api/amendments/{id} | Delete an existing patient amendment, you can only interact with amendments created by your API application |
| POST | /api/lab_tests | Create lab tests. An example lab workflow is as following: |
| GET | /api/lab_tests | Retrieve or search lab tests |
| PUT | /api/appointments_list/{id} |  |
| PATCH | /api/appointments_list/{id} |  |
| GET | /api/appointments_list/{id} |  |
| DELETE | /api/appointments_list/{id} |  |
| POST | /api/patient_lab_results |  |
| GET | /api/patient_lab_results |  |
| PUT | /api/task_categories/{id} | Update an existing task category |
| PATCH | /api/task_categories/{id} | Update an existing task category |
| GET | /api/task_categories/{id} | Retrieve an existing task category |
| GET | /api/fee_schedules_v2/{id} |  |
| GET | /api/insurances/{id} |  |
| GET | /api/clinical_notes |  |
| POST | /api/eligibility_checks_list | Create eligibility checks list request.  Use the UUID returned in the response to retrieve the batch of records. Results returned in order of id or updated_at. |
| GET | /api/eligibility_checks_list | Retrieve or search eligibility checks in batches. Results returned in order of ID or updated_at. |
| GET | /api/telehealth_appointment_history/{id} |  |
| GET | /api/clinical_notes/{id} |  |
| GET | /api/clinical_note_field_types | Retrieve or search clinical note field types |
| POST | /api/documents | Create documents |
| GET | /api/documents | Retrieve or search documents |
| GET | /api/staff/{id} |  |
| GET | /api/users | Retrieve or search users, `/api/users/current` can be used to identify logged in user, it will redirect to `/api/users/{current_user_id}` |
| PUT | /api/schedule_blocks/{id} | Update a schedule block |
| PATCH | /api/schedule_blocks/{id} | Partially update a schedule block |
| GET | /api/schedule_blocks/{id} | Retrieve a schedule block |
| DELETE | /api/schedule_blocks/{id} | Delete a schedule block |
| GET | /api/lab_orders_summary/{id} |  |
| GET | /api/audit_log | Retrieve or search audit logs. |
| PUT | /api/task_notes/{id} | Update an existing task note |
| PATCH | /api/task_notes/{id} | Update an existing task note |
| GET | /api/task_notes/{id} | Retrieve an existing task note |
| PUT | /api/custom_demographics/{id} | Update an existing custom demographics field |
| PATCH | /api/custom_demographics/{id} | Update an existing custom demographics field |
| GET | /api/custom_demographics/{id} | Retrieve an existing custom demographics field |
| PUT | /api/messages/{id} | Update an existing message in doctor's message center |
| PATCH | /api/messages/{id} | Update an existing message in doctor's message center |
| GET | /api/messages/{id} | Retrieve an existing message in doctor's message center |
| DELETE | /api/messages/{id} | Delete an existing message in doctor's message center |
| GET | /api/eobs/{id} | Retrieve an existing EOB object |
| GET | /api/doctor_options/{id} | Retrieve existing options for a doctor |
| POST | /api/allergies | Create patient allergy |
| GET | /api/allergies | Retrieve or search patient allergies |
| POST | /api/appointments | Create a new appointment or break on doctor's calendar |
| GET | /api/appointments | Retrieve or search appointment or breaks. |
| GET | /api/procedures/{id} |  |
| GET | /api/clinical_note_templates | Retrieve or search clinical note templates |
| PUT | /api/line_items/{id} |  |
| PATCH | /api/line_items/{id} |  |
| GET | /api/line_items/{id} | Retrieve an existing billing line item |
| DELETE | /api/line_items/{id} |  |
| GET | /api/doctors | Retrieve or search doctors within practice group |
| POST | /api/reminder_profiles | Create reminder profile |
| GET | /api/reminder_profiles | Retrieve or search reminder profiles |
| GET | /api/patient_payment_log | Retrieve or search patient payment logs |
| PUT | /api/offices/{id} | Update an existing office |
| PATCH | /api/offices/{id} | Update an existing office |
| GET | /api/offices/{id} | Retrieve an existing office |
| GET | /api/patient_payment_log/{id} | Retrieve an existing patient payment log |
| POST | /api/appointment_templates | Create appointment templates for a doctor's calendar |
| GET | /api/appointment_templates | Retrieve or search appointment templates for a doctor's calendar |
| POST | /api/patient_vaccine_records | Create patient vaccine records |
| GET | /api/patient_vaccine_records | Retrieve or search patient vaccine records |
| PUT | /api/telehealth_appointments/{id} |  |
| PATCH | /api/telehealth_appointments/{id} |  |
| GET | /api/telehealth_appointments/{id} |  |
| PUT | /api/comm_logs/{id} | Update an existing communication (phone call) logs |
| PATCH | /api/comm_logs/{id} | Update an existing communication (phone call) logs |
| GET | /api/comm_logs/{id} | Retrieve an existing communication (phone call) logs |
| GET | /api/prescription_messages | Retrieve or search prescription messages |
| GET | /api/user_groups/{id} | Retrieve an existing user group |
| POST | /api/line_items | Create billing line item for appointments |
| GET | /api/line_items | Retrieve or search billing line items |
| POST | /api/sublabs | Create sub-vendors |
| GET | /api/sublabs | Retrieve or search sub vendors |

## Enhanced Skill Content
## Question Mapping

- "How do I find all appointments for a specific patient on a given date?" -> GET /api/appointments?patient={id}&date={date}
- "What medications is this patient currently taking?" -> GET /api/medications?patient={id}
- "How do I schedule a new appointment?" -> POST /api/appointments (requires office, scheduled_time, doctor, patient, exam_room)
- "What are the patient's known allergies?" -> GET /api/allergies?patient={id}
- "How do I record a patient payment?" -> POST /api/patient_payments
- "Can I check a patient's insurance eligibility before their visit?" -> GET /api/eligibility_checks?patient={id}&appointment={id}
- "How do I get the day sheet charges for a date range?" -> GET /api/day_sheet_charges?start_date={date}&end_date={date}
- "What lab orders exist for this patient?" -> GET /api/lab_orders?doctor={id} then filter, or GET /api/lab_orders_summary?patient={id}
- "How do I update an appointment status to 'Checked In'?" -> PATCH /api/appointments/{id} with status=Checked In (also requires office, scheduled_time, doctor, patient, exam_room)
- "How do I look up a doctor's work schedule?" -> GET /api/doctor_work_schedule or GET /api/doctor_work_schedule/{id}
- "What open tasks are assigned to a specific user?" -> GET /api/tasks?assignee_user={id}&status={status_id}
- "How do I export a patient's CCDA document?" -> GET /api/patients/{id}/ccda (synchronous) or GET /api/patients/{id}/ccda_async (async)
- "How do I send a message to a patient?" -> POST /api/patient_messages
- "What clinical notes exist for today's appointments?" -> GET /api/clinical_notes?date={today}&doctor={id}
- "How do I add a billing line item to an appointment?" -> POST /api/line_items with appointment={id}

## Response Tips

- **List endpoints** (patients, appointments, medications, etc.): Paginated via cursor-based navigation; follow `next`/`previous` URLs. The `data` array holds results. Use `page_size` to control batch size.
- **Async list endpoints** (_list suffix like patients_list, line_items_list): Two-step pattern -- POST to start the job (returns `uuid` + `status`), then poll GET with that `uuid` until `status` is ready. Results use page-based pagination (`pagination.count`, `pagination.pages`).
- **Single-resource GETs** (e.g., /api/patients/{id}): Return the full object directly (no wrapper). Patient objects contain deeply nested maps for insurance (primary, secondary, tertiary, workers_comp, auto_accident).
- **Write operations** (PUT/PATCH): Return 204 with no body on success. PUT replaces the full resource; PATCH updates only provided fields.
- **Error responses**: All endpoints share the same error code set (400, 401, 403, 404, 405, 500). 409 appears only on appointment writes (scheduling conflicts).
- **Appointments**: The `status` field uses exact string values (Arrived, Checked In, In Session, Complete, etc.) -- not codes. `ins1_status`/`ins2_status` use verbose billing pipeline strings.
- **Lab workflow**: Results are nested under orders via `lab_order` foreign key. Documents link to orders via `lab_order` field. Chain: lab_orders -> lab_tests -> lab_results + lab_documents.

## Anomaly Flags

- **409 Conflict on appointment creation/update**: Surface immediately -- indicates a scheduling collision (double-booking). Check `allow_overlapping` and exam room availability.
- **Abnormal lab results**: When `is_abnormal` is truthy or `abnormal_status` is set on lab_results, flag for clinical review.
- **Deleted or archived records**: Many resources have `deleted_flag` or `archived` booleans. Surface when these appear unexpectedly in active workflows.
- **Missing doctor signoff on lab results**: When `doctor_signoff` is false on patient_lab_results, flag as pending review.
- **Insurance claim rejections**: Watch for `ins1_status`/`ins2_status` containing "Rejected" in any form (Rejected Emdeon, Rejected Payor, Rejected Waystar, etc.).
- **Stale async jobs**: If polling a `_list` endpoint and `status` does not resolve after multiple attempts, surface the stuck UUID.
- **Patient with date_of_death set**: Flag when attempting to schedule new appointments or send messages to deceased patients.
- **Clinical note locked status**: When `clinical_note.locked` is true, no further edits are possible -- surface before attempting updates.
- **Vaccine inventory low**: Compare `current_quantity` against `original_quantity` on inventory_vaccines; flag when stock is critically low or expired (`expiry` in the past).
- **OAuth2 token expiry**: All endpoints can return 401 -- surface with a clear re-authentication prompt rather than retrying.

## Playbook

### 1. Schedule and Confirm a New Patient Appointment

1. Look up the patient: GET /api/patients?last_name={name}&date_of_birth={dob}
2. Get available offices: GET /api/offices?doctor={doctor_id}
3. Check doctor availability: GET /api/availability?doctor={doctor_id}&date={date}&office={office_id}
4. Find an appointment profile: GET /api/appointment_profiles?doctor={doctor_id}
5. Create the appointment: POST /api/appointments with office, scheduled_time, doctor, patient, exam_room, and optionally profile and duration
6. Set up a reminder profile: GET /api/reminder_profiles?doctor={doctor_id}, then attach via the appointment's reminder_profile field
7. Verify the appointment was created: GET /api/appointments/{id}

### 2. Complete a Patient Visit (Check-in to Checkout)

1. Update appointment status to "Checked In": PATCH /api/appointments/{id} with status="Checked In"
2. Record vitals: PATCH /api/appointments/{id} with the vitals map (blood_pressure, pulse, temperature, weight, height, etc.)
3. Document the clinical note: POST /api/clinical_note_field_values with appointment, clinical_note_field, and value
4. Add any problems or diagnoses: POST /api/problems with patient and ICD codes
5. Prescribe medications if needed: POST /api/medications with patient, rxnorm, dosage details
6. Add billing line items: POST /api/line_items with appointment, CPT code, and service_date
7. Mark appointment complete: PATCH /api/appointments/{id} with status="Complete"

### 3. Process Lab Orders End to End

1. Create the lab order: POST /api/lab_orders with doctor, patient (via notes/icd10_codes), sublab, and priority
2. Add lab tests to the order: POST /api/lab_tests with order={lab_order_id}
3. Monitor for results: GET /api/lab_results?order={lab_order_id} (poll or use since parameter)
4. Review results and flag abnormals: Check each result's `is_abnormal` and `abnormal_status` fields
5. Attach lab documents: GET /api/lab_documents?doctor={doctor_id}&since={order_date}
6. Update order status if needed: PATCH /api/lab_orders/{id}
7. Get a summary view: GET /api/lab_orders_summary/{id}

### 4. Run an End-of-Day Financial Report

1. Pull day sheet charges: GET /api/day_sheet_charges?start_date={today}&end_date={today}
2. Pull day sheet credits: GET /api/day_sheet_credits?start_date={today}&end_date={today}
3. Pull day sheet totals: GET /api/day_sheet_totals?start_date={today}&end_date={today}
4. Review patient payments: GET /api/day_sheet_patient_payments?start_date={today}&end_date={today}
5. Cross-reference with line items: GET /api/line_items?service_date={today}&doctor={doctor_id}
6. Check EOBs for insurance payments: GET /api/eobs?doctor={doctor_id}
7. Review any payment log discrepancies: GET /api/patient_payment_log?since={today_start}

### 5. Onboard a New Patient with Full Records

1. Create the patient record: POST /api/patients with demographics, insurance maps, and emergency contact
2. Grant patient portal access: POST /api/patients/{id}/onpatient_access
3. Record known allergies: POST /api/allergies for each allergy (with rxnorm/snomed codes)
4. Add existing medications: POST /api/medications for each active medication
5. Document medical history as problems: POST /api/problems for each known condition
6. Upload prior records as documents: POST /api/documents with patient reference
7. Record immunization history: POST /api/patient_vaccine_records for each vaccine with cvx_code
8. Collect signed consent forms: POST /api/signed_consent_forms with patient, appointment, and consent_form IDs


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
