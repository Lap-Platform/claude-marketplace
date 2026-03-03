---
name: gsmtasks-project-api
description: "GSMTasks Project API skill. Use when working with GSMTasks Project for account_roles, accounts, addons. Covers 261 endpoints."
version: 1.0.0
generator: lapsh
---

# GSMTasks Project API
API version: 2.4.13

## Auth
ApiKey Authorization in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /account_roles/ -- verify access
3. POST /account_roles/ -- create first account_roles

## Endpoints

261 endpoints across 55 groups. See references/api-spec.lap for full details.

### account_roles
| Method | Path | Description |
|--------|------|-------------|
| GET | /account_roles/ |  |
| POST | /account_roles/ |  |
| GET | /account_roles/{id}/ |  |
| PUT | /account_roles/{id}/ |  |
| PATCH | /account_roles/{id}/ |  |
| DELETE | /account_roles/{id}/ |  |
| POST | /account_roles/{id}/activate/ |  |
| POST | /account_roles/{id}/notify/ |  |
| GET | /account_roles/{id}/token/ |  |

### accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounts/ |  |
| GET | /accounts/{id}/ |  |
| PUT | /accounts/{id}/ |  |
| PATCH | /accounts/{id}/ |  |
| GET | /accounts/{id}/braintree_customer/ |  |
| POST | /accounts/{id}/change_owner/ |  |
| GET | /accounts/{id}/managers/ |  |
| POST | /accounts/{id}/managers/ |  |
| DELETE | /accounts/{id}/managers/ |  |
| PUT | /accounts/{id}/stripe_attach_payment_method/ | Action to (re)set the account stripe customer and payment method to new values. |
| POST | /accounts/{id}/stripe_create_setup_intent/ | Action to start a new setup intent. |
| PUT | /accounts/{id}/stripe_create_setup_intent/ | Action to start a new setup intent. |
| PUT | /accounts/{id}/stripe_detach_payment_method/ | Detached payment method from the customer. |
| GET | /accounts/{id}/stripe_get_payment_method/ | Fetch a single payment method from stripe. |
| GET | /accounts/{id}/stripe_get_setup_attempt/ | Fetch a single setup intent |
| GET | /accounts/{id}/stripe_get_setup_intent/ | Fetch a single setup intent |
| GET | /accounts/{id}/stripe_payment_methods/ | Fetch all customer payment methods. |
| PUT | /accounts/{id}/stripe_set_default_payment_method/ | Action to set a payment method to default. |
| GET | /accounts/{id}/stripe_setup_intents/ | Fetch existing setup intents |
| GET | /accounts/{id}/workers/ |  |
| POST | /accounts/{id}/workers/ |  |
| DELETE | /accounts/{id}/workers/ |  |

### addons
| Method | Path | Description |
|--------|------|-------------|
| GET | /addons/ |  |
| GET | /addons/{id}/ |  |

### authenticate
| Method | Path | Description |
|--------|------|-------------|
| POST | /authenticate/ |  |

### billing
| Method | Path | Description |
|--------|------|-------------|
| GET | /billing/customers/ |  |
| POST | /billing/customers/ |  |
| GET | /billing/customers/{id}/ |  |
| PUT | /billing/customers/{id}/ |  |
| PATCH | /billing/customers/{id}/ |  |
| GET | /billing/customers/{id}/client_token/ |  |
| GET | /billing/invoices/ |  |
| GET | /billing/invoices/{id}/ |  |
| PUT | /billing/invoices/{id}/ |  |
| PATCH | /billing/invoices/{id}/ |  |
| POST | /billing/invoices/{id}/mark_as_paid/ |  |
| GET | /billing/stripe_payments/ |  |
| GET | /billing/stripe_payments/{id}/ |  |
| GET | /billing/transactions/ |  |
| GET | /billing/transactions/{id}/ |  |

### client_roles
| Method | Path | Description |
|--------|------|-------------|
| GET | /client_roles/ |  |
| POST | /client_roles/ |  |
| GET | /client_roles/{id}/ |  |
| PUT | /client_roles/{id}/ |  |
| PATCH | /client_roles/{id}/ |  |
| POST | /client_roles/{id}/notify/ |  |

### clients
| Method | Path | Description |
|--------|------|-------------|
| GET | /clients/ |  |
| POST | /clients/ |  |
| GET | /clients/{id}/ |  |
| PUT | /clients/{id}/ |  |
| PATCH | /clients/{id}/ |  |

### configurations
| Method | Path | Description |
|--------|------|-------------|
| GET | /configurations/ |  |

### contact_address_exports
| Method | Path | Description |
|--------|------|-------------|
| GET | /contact_address_exports/ | This view has multiple renderer classes available: `json` and `xlsx`. In order to export the data as an excel file, just set query argument `format` to `xlsx`.When downloading `xlsx` format, use Accept header `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet; version=...` |

### contact_address_import
| Method | Path | Description |
|--------|------|-------------|
| GET | /contact_address_import/ |  |
| POST | /contact_address_import/ |  |
| GET | /contact_address_import/{id}/ |  |

### contact_addresses
| Method | Path | Description |
|--------|------|-------------|
| GET | /contact_addresses/ |  |
| POST | /contact_addresses/ |  |
| GET | /contact_addresses/{id}/ |  |
| PUT | /contact_addresses/{id}/ |  |
| PATCH | /contact_addresses/{id}/ |  |

### devices
| Method | Path | Description |
|--------|------|-------------|
| GET | /devices/ |  |
| POST | /devices/ |  |
| GET | /devices/{id}/ |  |

### docs
| Method | Path | Description |
|--------|------|-------------|
| GET | /docs/schema/ | OpenApi3 schema for this API. Format can be selected via content negotiation. |

### documents
| Method | Path | Description |
|--------|------|-------------|
| GET | /documents/ |  |
| POST | /documents/ |  |
| GET | /documents/{id}/ |  |
| DELETE | /documents/{id}/ |  |
| POST | /documents/batch_delete/ | Available from version 2.4.2 |

### emails
| Method | Path | Description |
|--------|------|-------------|
| GET | /emails/ |  |
| POST | /emails/ |  |
| GET | /emails/{id}/ |  |
| PUT | /emails/{id}/ |  |
| PATCH | /emails/{id}/ |  |
| DELETE | /emails/{id}/ |  |
| POST | /emails/{id}/resend/ |  |

### exports
| Method | Path | Description |
|--------|------|-------------|
| GET | /exports/ |  |
| POST | /exports/ |  |
| GET | /exports/{id}/ |  |
| PUT | /exports/{id}/ |  |
| PATCH | /exports/{id}/ |  |
| DELETE | /exports/{id}/ |  |

### file_uploads
| Method | Path | Description |
|--------|------|-------------|
| GET | /file_uploads/ |  |
| POST | /file_uploads/ |  |
| GET | /file_uploads/{id}/ |  |

### formrules
| Method | Path | Description |
|--------|------|-------------|
| GET | /formrules/ |  |
| POST | /formrules/ |  |
| GET | /formrules/{id}/ |  |
| PUT | /formrules/{id}/ |  |
| PATCH | /formrules/{id}/ |  |
| DELETE | /formrules/{id}/ |  |

### integrations
| Method | Path | Description |
|--------|------|-------------|
| POST | /integrations/ |  |

### metafields
| Method | Path | Description |
|--------|------|-------------|
| GET | /metafields/ |  |
| POST | /metafields/ |  |
| GET | /metafields/{id}/ |  |
| PUT | /metafields/{id}/ |  |
| PATCH | /metafields/{id}/ |  |
| DELETE | /metafields/{id}/ |  |

### notification_templates
| Method | Path | Description |
|--------|------|-------------|
| GET | /notification_templates/ |  |
| POST | /notification_templates/ |  |
| GET | /notification_templates/{id}/ |  |
| PUT | /notification_templates/{id}/ |  |
| PATCH | /notification_templates/{id}/ |  |
| DELETE | /notification_templates/{id}/ |  |
| POST | /notification_templates/{id}/render/ |  |

### notifications
| Method | Path | Description |
|--------|------|-------------|
| GET | /notifications/ |  |
| POST | /notifications/ |  |
| GET | /notifications/{id}/ |  |

### orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /orders/ |  |
| POST | /orders/ |  |
| GET | /orders/{id}/ |  |
| PUT | /orders/{id}/ |  |
| PATCH | /orders/{id}/ |  |

### password_change
| Method | Path | Description |
|--------|------|-------------|
| POST | /password_change/ |  |

### password_reset
| Method | Path | Description |
|--------|------|-------------|
| POST | /password_reset/ |  |

### password_reset_confirm
| Method | Path | Description |
|--------|------|-------------|
| POST | /password_reset_confirm/ |  |

### push_notifications
| Method | Path | Description |
|--------|------|-------------|
| GET | /push_notifications/ |  |
| POST | /push_notifications/ |  |
| GET | /push_notifications/{id}/ |  |
| PUT | /push_notifications/{id}/ |  |
| PATCH | /push_notifications/{id}/ |  |
| DELETE | /push_notifications/{id}/ |  |
| POST | /push_notifications/{id}/resend/ |  |

### recurrences
| Method | Path | Description |
|--------|------|-------------|
| GET | /recurrences/ |  |
| POST | /recurrences/ |  |
| GET | /recurrences/{id}/ |  |
| PUT | /recurrences/{id}/ |  |
| PATCH | /recurrences/{id}/ |  |

### register
| Method | Path | Description |
|--------|------|-------------|
| POST | /register/ |  |

### reports
| Method | Path | Description |
|--------|------|-------------|
| GET | /reports/tasks/states_count/ |  |

### reviews
| Method | Path | Description |
|--------|------|-------------|
| GET | /reviews/ |  |
| POST | /reviews/ |  |
| GET | /reviews/{id}/ |  |

### route_optimizations
| Method | Path | Description |
|--------|------|-------------|
| GET | /route_optimizations/ |  |
| POST | /route_optimizations/ |  |
| GET | /route_optimizations/{id}/ |  |
| POST | /route_optimizations/{id}/commit/ |  |
| GET | /route_optimizations/{id}/results/ |  |
| GET | /route_optimizations/{id}/routes/ |  |
| POST | /route_optimizations/{id}/routes/ |  |
| POST | /route_optimizations/{id}/schedule/ |  |

### routes
| Method | Path | Description |
|--------|------|-------------|
| GET | /routes/ |  |
| POST | /routes/ |  |
| GET | /routes/{id}/ |  |
| PUT | /routes/{id}/ |  |
| PATCH | /routes/{id}/ |  |
| DELETE | /routes/{id}/ |  |

### scenes
| Method | Path | Description |
|--------|------|-------------|
| GET | /scenes/dashboard/ |  |
| GET | /scenes/order_list/ |  |
| GET | /scenes/recurrence_list/ |  |
| GET | /scenes/task_list/ |  |

### signatures
| Method | Path | Description |
|--------|------|-------------|
| GET | /signatures/ |  |
| POST | /signatures/ |  |
| GET | /signatures/{id}/ |  |
| DELETE | /signatures/{id}/ |  |
| POST | /signatures/batch_delete/ | Available from version 2.4.2 |

### sms
| Method | Path | Description |
|--------|------|-------------|
| GET | /sms/ |  |
| POST | /sms/ |  |
| GET | /sms/{id}/ |  |
| PUT | /sms/{id}/ |  |
| PATCH | /sms/{id}/ |  |
| DELETE | /sms/{id}/ |  |
| POST | /sms/{id}/resend/ |  |

### task_address_features
| Method | Path | Description |
|--------|------|-------------|
| GET | /task_address_features/ |  |
| GET | /task_address_features/{id}/ |  |

### task_commands
| Method | Path | Description |
|--------|------|-------------|
| GET | /task_commands/ |  |
| POST | /task_commands/ |  |
| GET | /task_commands/{id}/ |  |
| PUT | /task_commands/{id}/ |  |

### task_event_tracks
| Method | Path | Description |
|--------|------|-------------|
| GET | /task_event_tracks/ |  |
| GET | /task_event_tracks/{id}/ |  |

### task_events
| Method | Path | Description |
|--------|------|-------------|
| GET | /task_events/ | Mixin which allows the override of the filename being |
| GET | /task_events/{id}/ | Mixin which allows the override of the filename being |

### task_exports
| Method | Path | Description |
|--------|------|-------------|
| GET | /task_exports/ | This view has multiple renderer classes available: `json` and `xlsx`. In order to export the data as an excel file, just set query argument `format` to `xlsx`.When downloading `xlsx` format, use Accept header `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet; version=...` |

### task_forms
| Method | Path | Description |
|--------|------|-------------|
| GET | /task_forms/ |  |
| POST | /task_forms/ |  |
| GET | /task_forms/{id}/ |  |
| PUT | /task_forms/{id}/ |  |
| PATCH | /task_forms/{id}/ |  |
| DELETE | /task_forms/{id}/ |  |

### task_import
| Method | Path | Description |
|--------|------|-------------|
| GET | /task_import/ |  |
| POST | /task_import/ |  |
| GET | /task_import/{id}/ |  |

### task_import_mapping
| Method | Path | Description |
|--------|------|-------------|
| GET | /task_import_mapping/ |  |
| POST | /task_import_mapping/ |  |
| GET | /task_import_mapping/{id}/ |  |

### task_metadatas
| Method | Path | Description |
|--------|------|-------------|
| GET | /task_metadatas/ |  |
| GET | /task_metadatas/{id}/ |  |

### tasks
| Method | Path | Description |
|--------|------|-------------|
| GET | /tasks/ |  |
| POST | /tasks/ |  |
| GET | /tasks/{id}/ |  |
| PUT | /tasks/{id}/ |  |
| PATCH | /tasks/{id}/ |  |
| POST | /tasks/{id}/accept/ |  |
| POST | /tasks/{id}/account_change/ |  |
| POST | /tasks/{id}/activate/ |  |
| POST | /tasks/{id}/assign/ |  |
| POST | /tasks/{id}/cancel/ |  |
| POST | /tasks/{id}/complete/ |  |
| GET | /tasks/{id}/documents/ |  |
| GET | /tasks/{id}/events/ |  |
| POST | /tasks/{id}/fail/ |  |
| POST | /tasks/{id}/reject/ |  |
| GET | /tasks/{id}/signatures/ |  |
| POST | /tasks/{id}/transit/ |  |
| POST | /tasks/{id}/unaccept/ |  |
| POST | /tasks/{id}/unassign/ |  |
| POST | /tasks/reorder/ |  |
| POST | /tasks/reposition/ |  |

### time_location_features
| Method | Path | Description |
|--------|------|-------------|
| GET | /time_location_features/ |  |
| POST | /time_location_features/ |  |
| GET | /time_location_features/{id}/ |  |
| PUT | /time_location_features/{id}/ |  |
| PATCH | /time_location_features/{id}/ |  |
| DELETE | /time_location_features/{id}/ |  |

### time_locations
| Method | Path | Description |
|--------|------|-------------|
| GET | /time_locations/ |  |
| POST | /time_locations/ |  |
| GET | /time_locations/{id}/ |  |

### trackers
| Method | Path | Description |
|--------|------|-------------|
| GET | /trackers/ |  |
| POST | /trackers/ |  |
| GET | /trackers/{id}/ |  |
| PUT | /trackers/{id}/ |  |
| PATCH | /trackers/{id}/ |  |
| GET | /trackers/{id}/public/ |  |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/ |  |
| POST | /users/ |  |
| GET | /users/{id}/ |  |
| PUT | /users/{id}/ |  |
| PATCH | /users/{id}/ |  |
| DELETE | /users/{id}/ |  |
| POST | /users/{id}/activate/ |  |
| GET | /users/{id}/on_duty/ |  |
| PUT | /users/{id}/on_duty/ |  |
| DELETE | /users/{id}/on_duty/ |  |

### users_on_duty_log
| Method | Path | Description |
|--------|------|-------------|
| GET | /users_on_duty_log/ |  |
| POST | /users_on_duty_log/ |  |
| GET | /users_on_duty_log/{id}/ |  |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /webhooks/ |  |
| POST | /webhooks/ |  |
| GET | /webhooks/{id}/ |  |
| PUT | /webhooks/{id}/ |  |
| PATCH | /webhooks/{id}/ |  |
| DELETE | /webhooks/{id}/ |  |
| POST | /webhooks/{id}/active/ |  |
| POST | /webhooks/{id}/inactive/ |  |

### worker_features
| Method | Path | Description |
|--------|------|-------------|
| GET | /worker_features/ |  |
| GET | /worker_features/{user_id}/ |  |

### worker_tracks
| Method | Path | Description |
|--------|------|-------------|
| GET | /worker_tracks/ |  |

### working_state
| Method | Path | Description |
|--------|------|-------------|
| GET | /working_state/ |  |
| POST | /working_state/ |  |
| GET | /working_state/{id}/ |  |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the API?" -> POST /authenticate/
- "Show me all tasks for a specific worker today?" -> GET /tasks/ (with `assignee` and `complete_after__gte`/`complete_before__lte` filters)
- "How do I create a new delivery task with a pickup and drop-off?" -> POST /orders/ (with `tasks_data` containing pick_up and drop_off category tasks)
- "Which drivers are currently on duty?" -> GET /account_roles/ (with `is_worker=true` and `is_active=true`)
- "How do I assign a task to a specific driver?" -> POST /tasks/{id}/assign/
- "What is the status of a specific task?" -> GET /tasks/{id}/
- "How do I mark a task as completed?" -> POST /tasks/{id}/complete/
- "Can I optimize routes for my fleet?" -> POST /route_optimizations/
- "How do I set up a webhook for task status changes?" -> POST /webhooks/
- "Where is my driver right now?" -> GET /worker_features/{user_id}/ or GET /time_location_features/ (filtered by `user`)
- "How do I import tasks from a spreadsheet?" -> POST /task_import/ (with `tasks_data` array and optional `mapping`)
- "How do I create a recurring delivery schedule?" -> POST /recurrences/ (with `rrule` and `tasks_data`)
- "How do I send a notification to a customer about their delivery?" -> POST /notifications/ (with `task` and `recipient`)
- "How do I get a task completion report for last week?" -> GET /reports/tasks/states_count/ (with `account`, `date_from`, `date_until`)
- "How do I create a tracking link for a customer?" -> POST /trackers/ (with `tasks` array)

## Response Tips

- **List endpoints** (`GET /tasks/`, `/orders/`, etc.): Cursor-based pagination -- use `cursor` and `page_size` params; next page cursor is in the response. No total count returned by default.
- **Task state transitions** (`/accept/`, `/complete/`, `/fail/`, etc.): Return the full updated task object on 200; invalid transitions return 400 with an error describing the allowed source states.
- **Bulk/nested creates** (`POST /orders/` with `tasks_data`): The response nests created task URIs in `tasks`; individual task errors appear per-item in validation errors keyed by array index.
- **Route optimizations**: Async workflow -- POST returns 201 with `state: pending`; poll `GET /route_optimizations/{id}/` until state is `ready` or `completed`, then fetch `/results/` for the plan.
- **Webhooks/notifications/SMS/emails**: Check the `state` field for delivery status (queued/sent/failed); `error` or `disable_message` fields contain failure details.
- **Export endpoints** (`/task_exports/`, `/contact_address_exports/`): Support `fields` param to select specific columns; use `format=xlsx` for spreadsheet output with `page`-based (not cursor) pagination.

## Anomaly Flags

- **Webhook disabled**: Surface when `GET /webhooks/` returns entries with `state: disabled` or `failure_count > 3` -- the integration is silently broken.
- **Route optimization failed**: Flag `state: failed` or `state: over_quota` on route optimizations -- tasks remain unoptimized and need manual assignment.
- **Geocode failures**: Watch for `address.geocode_failed_at` being populated on tasks or contact addresses -- delivery locations are unresolvable and tasks may fail.
- **SMS/email over quota**: Flag notifications with `state: over_quota` -- customer communications are being dropped silently.
- **Stale worker location**: If `time_location_features` for an on-duty worker has a `time` older than 15 minutes, the worker's app may be offline or GPS disabled.
- **Recurrence errors**: Flag recurrences where `last_errored_at` is more recent than `last_recurred_at` -- scheduled task generation is failing.
- **Task import failures**: Surface `task_import` entries with `state: failed` -- batch uploads did not complete and `errors` map contains per-row details.
- **Account billing issues**: Invoices with `state: overdue` should be flagged immediately as they may lead to service restrictions.

## Playbook

### 1. Create and dispatch a delivery order

1. `POST /authenticate/` with username, password, and token to get an API session.
2. `POST /orders/` with `account`, `tasks_data` containing two tasks: one with `category: pick_up` and one with `category: drop_off`, each with `contact` and `address` objects.
3. Note the returned task URIs from the `tasks` field.
4. `POST /tasks/{pickup_id}/assign/` with `assignee` set to the driver's account role URI.
5. Optionally `POST /trackers/` with the task URIs to generate a customer tracking link.
6. Monitor via `GET /tasks/{id}/` or set up `POST /webhooks/` for real-time state updates.

### 2. Optimize and commit routes for the day

1. `GET /account_roles/?is_worker=true&is_active=true` to list available drivers and their vehicle profiles.
2. `GET /tasks/?state=unassigned&complete_before__date={today}` to collect all unassigned tasks for today.
3. `POST /route_optimizations/` with `assignees` (driver URIs), `tasks` (task URIs), `objective` (e.g., `transport_time`), and optionally `start_location`/`end_location`.
4. Poll `GET /route_optimizations/{id}/` until `state` becomes `ready`.
5. Review the plan via `GET /route_optimizations/{id}/results/`.
6. `POST /route_optimizations/{id}/commit/` to apply assignments and ordering to the tasks.

### 3. Set up real-time webhook integration

1. `POST /webhooks/` with `account`, `name`, `target` (your endpoint URL), `task_events: true`, and optionally `document_events`, `signature_events`, `review_events`.
2. Set `version` to `2.4.13` (latest) and provide a `shared_secret` for payload verification.
3. `POST /webhooks/{id}/active/` to activate the webhook.
4. Monitor `GET /webhooks/{id}/` periodically -- if `failure_count` increases or `state` becomes `disabled`, check your target endpoint and re-activate.
5. To pause, call `POST /webhooks/{id}/inactive/`; to resume, call `/active/` again.

### 4. Import tasks from a CSV file

1. `GET /task_import_mapping/?account={account_id}` to check for existing column mappings.
2. If no mapping exists, `POST /task_import_mapping/` with `field_names` (your CSV headers) and `lines` array mapping `from_field` to `to_field` (e.g., `{"from_field": "Address", "to_field": "address.raw_address"}`).
3. `POST /task_import/` with `account`, `tasks_data` (array of row objects), and `mapping` (URI from step 2).
4. Poll `GET /task_import/{id}/` until `state` is `completed` or `failed`.
5. On failure, inspect the `errors` map for per-row issues. On success, use `tasks_created` URIs to verify the imported tasks.

### 5. Track driver duty hours and location

1. `PUT /users/{id}/on_duty/` with `account` URI to clock a driver in.
2. Location updates flow automatically from the mobile app via `POST /time_locations/` or `POST /time_location_features/`.
3. `GET /worker_features/{user_id}/` to get the driver's latest position, speed, heading, and battery level as a GeoJSON feature.
4. `GET /users_on_duty_log/?user={user_id}&timestamp__gte={start}&timestamp__lte={end}` to pull duty history for payroll.
5. `DELETE /users/{id}/on_duty/` to clock the driver out.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
