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

- "What actions are available in my Zapier account?" -> GET /api/v1/exposed/
- "How do I run a Zapier action?" -> POST /api/v1/exposed/{exposed_app_action_id}/execute/
- "Can I preview an action before it runs?" -> POST /api/v1/exposed/{exposed_app_action_id}/execute/ (set `preview_only: true`)
- "What happened with my last execution?" -> GET /api/v1/execution-log/{execution_log_id}/
- "Is the Zapier AI Actions API reachable?" -> GET /api/v1/check/
- "Where do I configure which actions are exposed?" -> GET /api/v1/configuration-link/
- "How do I send an email through Zapier?" -> GET /api/v1/exposed/ then POST /api/v1/exposed/{id}/execute/ with instructions
- "Did my action succeed or fail?" -> GET /api/v1/execution-log/{execution_log_id}/ (check `status` and `error` fields)
- "What parameters were sent to the action?" -> GET /api/v1/execution-log/{execution_log_id}/ (inspect `input_params`)
- "Can I review an action result before confirming?" -> POST /api/v1/exposed/{exposed_app_action_id}/execute/ (use `review_url` from response)
- "How do I authenticate with Zapier AI Actions?" -> Use `x-api-key` header, `api_key` query param, OAuth2, or `nlasession` cookie
- "What if the action returns additional data beyond the main result?" -> Check `additional_results` array and `result_field_labels` in the execution response

## Response Tips

- **Check/Config endpoints** (`/check/`, `/configuration-link/`): Simple 200 responses with no documented body structure; treat non-200 as service unavailable.
- **Exposed actions** (`/exposed/`): Response contains `results` (array of maps) and `configuration_link` (string); iterate `results` to find the `exposed_app_action_id` needed for execution.
- **Execute/Log** (`/execute/`, `/execution-log/`): Rich response object -- always check `status` and `error` before reading `result`; `additional_results` is an array that may be empty; `assistant_hint` may contain guidance for the next step; 400 errors indicate malformed input or invalid action ID.

## Anomaly Flags

- **`status` is not "success"**: Surface immediately when an execution returns a non-success status, along with the `error` field content.
- **`error` is non-null**: Flag the error message even if status appears normal -- the API may populate both fields.
- **`assistant_hint` is present**: Always relay this to the user; Zapier uses it to communicate action-specific guidance or warnings.
- **`review_url` returned**: Notify the user that the action may require manual review at the provided URL before taking effect.
- **Empty `results` from `/exposed/`**: Proactively suggest the user visit the `configuration_link` to enable actions, since no actions are currently available.
- **400 on execute**: Surface the error body -- common causes are invalid UUID format, missing `instructions`, or an action that was disabled since listing.
- **Auth failure (401/403)**: Flag that the API key or session may be expired and suggest re-authenticating or checking the configuration link.

## Playbook

### 1. Discover and Execute an Action

1. Call `GET /api/v1/exposed/` to list all available actions.
2. Browse `results` to find the desired action; note its `exposed_app_action_id`.
3. Call `POST /api/v1/exposed/{exposed_app_action_id}/execute/` with `instructions` describing what to do (e.g., "Send an email to alice@example.com saying hello").
4. Check `status` and `error` in the response.
5. If `review_url` is present, direct the user to review before the action finalizes.

### 2. Preview Before Executing

1. Call `GET /api/v1/exposed/` to list available actions.
2. Call `POST /api/v1/exposed/{exposed_app_action_id}/execute/` with `preview_only: true` and your `instructions`.
3. Inspect `input_params` in the response to verify what would be sent.
4. If the preview looks correct, re-call the same endpoint with `preview_only: false` (or omit it) to execute for real.

### 3. Check Execution Results

1. After executing an action, save the `id` from the response.
2. Call `GET /api/v1/execution-log/{id}/` to retrieve the full execution record.
3. Check `status` for completion state and `error` for any failures.
4. Read `result` for the primary output and `additional_results` for supplementary data.
5. Use `result_field_labels` to understand the shape of returned data.

### 4. Set Up Actions for First-Time Use

1. Call `GET /api/v1/check/` to verify the API is reachable and authenticated.
2. Call `GET /api/v1/configuration-link/` to obtain the setup URL.
3. Direct the user to the configuration link to enable and configure the actions they want exposed.
4. Call `GET /api/v1/exposed/` to confirm the newly configured actions appear in `results`.

### 5. Troubleshoot a Failed Execution

1. Call `GET /api/v1/execution-log/{execution_log_id}/` with the failed execution's ID.
2. Check `error` for the failure reason and `assistant_hint` for remediation guidance.
3. Review `input_params` to see if the inputs were malformed or unexpected.
4. If the action ID is invalid, re-fetch `GET /api/v1/exposed/` to confirm it is still enabled.
5. If no actions are exposed, direct the user to `GET /api/v1/configuration-link/` to reconfigure.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
