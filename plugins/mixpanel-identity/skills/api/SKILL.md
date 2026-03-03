---
name: identity-api
description: "Identity API skill. Use when working with Identity for track#create-identity, track#identity-create-alias, import. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Identity API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
https://{region}.mixpanel.com

## Setup
1. No auth setup needed
3. POST /track#create-identity -- create first track#create-identity

## Endpoints

3 endpoints across 3 groups. See references/api-spec.lap for full details.

### track#create-identity
| Method | Path | Description |
|--------|------|-------------|
| POST | /track#create-identity | Create Identity |

### track#identity-create-alias
| Method | Path | Description |
|--------|------|-------------|
| POST | /track#identity-create-alias | Create Alias |

### import
| Method | Path | Description |
|--------|------|-------------|
| POST | /import | Merge Identities |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new user identity in Mixpanel?" -> POST /track#create-identity
- "How do I link two user profiles together?" -> POST /track#identity-create-alias
- "How do I merge an anonymous user with a known user?" -> POST /track#identity-create-alias
- "How do I import historical events into Mixpanel?" -> POST /import
- "How do I bulk import records?" -> POST /import
- "Can I import data without strict validation?" -> POST /import (set strict=0)
- "How do I associate a device ID with a user ID?" -> POST /track#identity-create-alias
- "How do I import events into a specific project?" -> POST /import (use project_id param)
- "How do I set up identity management before tracking events?" -> POST /track#create-identity, then POST /track#identity-create-alias
- "What happens if I import invalid data?" -> POST /import (strict=1 rejects malformed records)
- "How do I migrate user data from another analytics platform?" -> POST /import (batch historical events)
- "How do I connect pre-login and post-login activity for the same user?" -> POST /track#create-identity + POST /track#identity-create-alias

## Response Tips

- **Identity endpoints** (`/track#create-identity`, `/track#identity-create-alias`): Return 200 on success with minimal body. A 401 means invalid credentials; 403 means the project does not permit identity operations.
- **Import endpoint** (`/import`): Response includes `num_records_imported` and `status` -- always compare `num_records_imported` against the number you sent to detect partial failures. A 400 typically means malformed payload or validation failure when `strict=1`.

## Anomaly Flags

- **Partial imports**: `num_records_imported` is less than the number of records submitted -- surface the discrepancy and suggest retrying failed records with `strict=0` for diagnostics.
- **Region mismatch**: Base URL uses `{region}.mixpanel.com` -- flag if requests return 401 unexpectedly, as this often indicates the wrong region (e.g., `eu` vs `us`).
- **Strict mode rejections**: When `strict=1` (default), any malformed record causes rejection -- flag 400 errors and recommend a dry run with `strict=0` to identify problematic records.
- **Auth failures on identity ops**: 403 on identity endpoints may indicate the project has ID merge disabled -- surface this as a configuration issue, not a credentials problem.
- **Duplicate alias creation**: Repeated alias calls for the same pair may silently succeed but can cause identity cluster issues -- flag if the same alias mapping is sent more than once.

## Playbook

### 1. Setting Up Identity Management for a New User

1. Call `POST /track#create-identity` with the canonical user ID (e.g., database ID) to register the identity.
2. Call `POST /track#identity-create-alias` to link anonymous/device IDs to the canonical ID.
3. Confirm both return 200 before sending any tracked events for that user.

### 2. Merging Anonymous Sessions After Login

1. Capture the anonymous/device ID used during the pre-login session.
2. On login, call `POST /track#create-identity` with the authenticated user ID.
3. Call `POST /track#identity-create-alias` mapping the anonymous ID to the authenticated ID.
4. All prior anonymous events now resolve to the authenticated profile.

### 3. Bulk Importing Historical Data

1. Format records according to Mixpanel's import schema.
2. Call `POST /import` with `strict=0` and the target `project_id` to validate data without rejecting on minor issues.
3. Review the response: check `num_records_imported` matches expected count.
4. If satisfied, re-import with `strict=1` (default) for production-grade validation.
5. Investigate any gap between submitted and imported counts.

### 4. Cross-Project Data Import

1. Identify the target project ID from Mixpanel project settings.
2. Call `POST /import` with the `project_id` parameter set explicitly.
3. Verify `status` is successful and `num_records_imported` matches expectations.
4. Repeat for each target project as needed.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
