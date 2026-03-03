---
name: feature-flags-api
description: "Feature Flags API skill. Use when working with Feature Flags for flags. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Feature Flags API
API version: 1.0.0

## Auth
Requires API key (token parameter)

## Base URL
Not specified.

## Setup
1. Include your API key via the token parameter
2. GET /flags -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### flags
| Method | Path | Description |
|--------|------|-------------|
| GET | /flags | Evaluate Feature Flags (GET) |
| GET | /flags/definitions | Get Feature Flag Definitions |

## Enhanced Skill Content
## Question Mapping

- "What feature flags are enabled for this user?" -> GET /flags
- "Which flags apply in the production context?" -> GET /flags
- "Is the dark-mode flag turned on?" -> GET /flags
- "List all flag definitions" -> GET /flags/definitions
- "What flags exist in the system?" -> GET /flags/definitions
- "Show me the schema for each feature flag" -> GET /flags/definitions
- "What flags are active for context 'beta-testers'?" -> GET /flags
- "Are there any flags I can toggle for staging?" -> GET /flags
- "Give me the full flag catalog" -> GET /flags/definitions
- "What does the 'new-checkout' flag control?" -> GET /flags/definitions
- "Evaluate all flags for user segment 'enterprise'" -> GET /flags
- "Which flags exist but are currently disabled for my context?" -> GET /flags + GET /flags/definitions
- "Compare available flags against what my context actually receives" -> GET /flags/definitions then GET /flags

## Response Tips

- **Flag evaluation (GET /flags):** Response `flags` is a map -- keys are flag names, values are the resolved states (may be booleans, strings, or numbers depending on flag type). Always check the value type before branching logic.
- **Flag definitions (GET /flags/definitions):** Response `flags` is an array of maps. Each entry describes a flag's metadata. Iterate the array to build a lookup table by flag name.
- **Errors:** 400 means a missing or malformed `context` parameter. 401 means the token is invalid or expired. 403 means the token lacks permission for the requested resource.

## Anomaly Flags

- **401 on previously working tokens:** Surface immediately -- the token may have been revoked or rotated.
- **403 after context change:** Flag evaluation scopes may differ per context; warn the user their token may lack access to the new context.
- **Empty flags map:** If GET /flags returns an empty map, flag the discrepancy when GET /flags/definitions shows definitions exist -- the context may be misconfigured.
- **Flag type mismatches:** If a flag value comes back as a string when prior calls returned a boolean, surface this as a potential upstream configuration change.
- **Definitions without evaluations:** If definitions list flags that never appear in evaluated results across multiple contexts, flag them as potentially stale or orphaned.

## Playbook

### 1. Evaluate Flags for a User Context

1. Call `GET /flags` with `token` and `context` set to the target user or environment identifier.
2. Inspect the returned `flags` map for the flag names you care about.
3. Branch application logic based on each flag's resolved value.

### 2. Audit All Available Flags

1. Call `GET /flags/definitions` with your `token` to retrieve the full catalog.
2. Review each definition entry for flag name, type, and metadata.
3. Cross-reference with `GET /flags` using a representative context to see which are active vs inactive.

### 3. Detect Flag Drift Between Environments

1. Call `GET /flags` with `context` set to `staging`.
2. Call `GET /flags` with `context` set to `production`.
3. Diff the two `flags` maps -- any keys present in one but missing in the other, or with differing values, indicate drift.
4. Call `GET /flags/definitions` to confirm whether missing flags are defined but disabled or entirely absent.

### 4. Validate Token Permissions

1. Call `GET /flags/definitions` with the token under test.
2. If 401 is returned, the token is invalid -- request a new one.
3. If 403 is returned, the token exists but lacks read access to definitions -- escalate permissions.
4. On success, call `GET /flags` with a known context to confirm evaluation access as well.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
