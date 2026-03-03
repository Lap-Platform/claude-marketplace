---
name: zapier-ai-actions-api
description: "Zapier AI Actions API skill. Use when working with Zapier AI Actions for api. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Zapier AI Actions API
API version: main_api_v1

## Auth
ApiKey x-api-key in header | ApiKey api_key in query | OAuth2 | ApiKey nlasession in cookie

## Base URL
https://actions.zapier.com

## Setup
1. Set your API key in the appropriate header
2. GET /api/v1/check/ -- verify access
3. POST /api/v1/exposed/{exposed_app_action_id}/execute/ -- create first execute

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/v1/check/ | Check |
| GET | /api/v1/configuration-link/ | Get Configuration Link |
| GET | /api/v1/exposed/ | List Exposed Actions |
| POST | /api/v1/exposed/{exposed_app_action_id}/execute/ | Execute App Action Endpoint |
| GET | /api/v1/execution-log/{execution_log_id}/ | Get Execution Log Endpoint |

## Enhanced Skill Content
## Question Mapping

- "What actions are available?" -> GET /api/v1/exposed/
- "List my configured Zapier actions" -> GET /api/v1/exposed/
- "How do I set up or configure my actions?" -> GET /api/v1/configuration-link/
- "Run a Zapier action with these instructions" -> POST /api/v1/exposed/{exposed_app_action_id}/execute/
- "Execute action {id} to send an email" -> POST /api/v1/exposed/{exposed_app_action_id}/execute/
- "Preview what an action would do without running it" -> POST /api/v1/exposed/{exposed_app_action_id}/execute/ (set preview_only=True)
- "What happened with execution {id}?" -> GET /api/v1/execution-log/{execution_log_id}/
- "Did my action succeed or fail?" -> GET /api/v1/execution-log/{execution_log_id}/
- "Is the Zapier API working?" -> GET /api/v1/check/
- "Show me the result of the last action I ran" -> GET /api/v1/execution-log/{execution_log_id}/
- "I want to test an action before committing" -> POST /api/v1/exposed/{exposed_app_action_id}/execute/ (preview_only=True)
- "Where can I manage which actions are exposed?" -> GET /api/v1/configuration-link/
- "What input parameters were used for execution {id}?" -> GET /api/v1/execution-log/{execution_log_id}/

## Response Tips

- **Check/Config** (`/check/`, `/configuration-link/`): Simple responses; use these to verify connectivity and get the setup URL before attempting actions.
- **Exposed actions** (`/exposed/`): Returns `results` array of action maps and a `configuration_link`; iterate `results` to find the `exposed_app_action_id` (UUID) needed for execution.
- **Execute** (`/execute/`): Response contains `status` (check for success/error), `result` (primary output), `additional_results` (array of supplementary data), and `error` (non-null on failure); always read `assistant_hint` when present as it contains guidance from Zapier.
- **Execution log** (`/execution-log/`): Same shape as execute response; use `review_url` to let the user inspect the action in Zapier's UI.

## Anomaly Flags

- **`error` is non-null**: Surface immediately with the full error content; do not silently retry.
- **`status` is not "success"**: Flag the status value and check `assistant_hint` for remediation guidance.
- **`assistant_hint` present**: Always surface this to the user -- it contains Zapier's contextual advice.
- **400 errors on execute or log**: Likely a malformed UUID or missing `instructions`; flag the specific missing/invalid field.
- **Empty `results` on /exposed/**: The user has no configured actions; proactively provide the `configuration_link` so they can set up actions.
- **`review_url` returned**: Mention it to the user so they can verify the action in Zapier's dashboard before trusting the result.
- **`preview_only` was false and action had side effects**: Remind the user the action was actually executed, not just previewed.

## Playbook

### 1. First-time setup: discover and run an action

1. Call `GET /api/v1/check/` to verify API connectivity and auth.
2. Call `GET /api/v1/exposed/` to list available actions.
3. If `results` is empty, share the `configuration_link` and ask the user to configure actions in Zapier first.
4. Pick the target action's `exposed_app_action_id` from the results.
5. Call `POST /api/v1/exposed/{id}/execute/` with `preview_only: true` and natural language `instructions` to preview.
6. Review the preview result with the user; if acceptable, re-execute with `preview_only: false`.

### 2. Safe execution with preview

1. Call `POST /api/v1/exposed/{id}/execute/` with `preview_only: true` and the user's instructions.
2. Present `input_params` and `result` to the user for confirmation.
3. If approved, call the same endpoint with `preview_only: false`.
4. Check `status` and `error` in the response; surface `assistant_hint` if present.
5. Provide the `review_url` for the user to verify in Zapier.

### 3. Checking on a past execution

1. Obtain the `execution_log_id` (UUID) from a previous execute response's `id` field.
2. Call `GET /api/v1/execution-log/{execution_log_id}/`.
3. Report `status`, `result`, and any `error` to the user.
4. If `additional_results` is non-empty, summarize the extra data.
5. Share the `review_url` for full details in Zapier's UI.

### 4. Troubleshooting a failed action

1. Check the execute response's `error` field for the failure reason.
2. Read `assistant_hint` for Zapier-provided remediation steps.
3. Verify the `exposed_app_action_id` is valid by calling `GET /api/v1/exposed/`.
4. If the action is missing from exposed list, direct the user to `configuration_link` to reconfigure.
5. Retry with corrected `instructions` or parameters, using `preview_only: true` first.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
