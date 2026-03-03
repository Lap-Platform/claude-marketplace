---
name: twilio-lookups
description: "Twilio - Lookups API skill. Use when working with Twilio - Lookups for PhoneNumbers, batch, RateLimits. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio - Lookups
API version: 1.0.0

## Auth
Bearer basic

## Base URL
https://lookups.twilio.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v2/RateLimits -- verify access
3. POST /v2/batch/query -- create first query

## Endpoints

10 endpoints across 3 groups. See references/api-spec.lap for full details.

### PhoneNumbers
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/PhoneNumbers/{PhoneNumber} | Full API documentation: https://www.twilio.com/docs/lookup/v2-api |
| GET | /v2/PhoneNumbers/{PhoneNumber}/Overrides/{Field} | Get Overrides for a Phone Number for a specific field. |
| POST | /v2/PhoneNumbers/{PhoneNumber}/Overrides/{Field} | Create Override for a Phone Number for a specific field |
| PUT | /v2/PhoneNumbers/{PhoneNumber}/Overrides/{Field} | Update Override for a Phone Number for a specific field |
| DELETE | /v2/PhoneNumbers/{PhoneNumber}/Overrides/{Field} | Delete an Override for a Phone Number for a specific field |

### batch
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/batch/query | In Request Bulk |

### RateLimits
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/RateLimits | Get account rate limits |
| GET | /v2/RateLimits/Fields/{Field}/Bucket/{Bucket} | Get rate limit |
| DELETE | /v2/RateLimits/Fields/{Field}/Bucket/{Bucket} | Delete rate limit |
| PUT | /v2/RateLimits/Fields/{Field}/Bucket/{Bucket} | Upsert rate limit |

## Enhanced Skill Content
## Question Mapping

- "Is this phone number valid?" -> GET /v2/PhoneNumbers/{PhoneNumber}
- "What carrier does this number belong to?" -> GET /v2/PhoneNumbers/{PhoneNumber} (with Fields=line_type_intelligence)
- "Has this SIM been swapped recently?" -> GET /v2/PhoneNumbers/{PhoneNumber} (with Fields=sim_swap)
- "Is call forwarding enabled on this number?" -> GET /v2/PhoneNumbers/{PhoneNumber} (with Fields=call_forwarding)
- "Does this person's name match the phone number owner?" -> GET /v2/PhoneNumbers/{PhoneNumber} (with Fields=identity_match, FirstName, LastName)
- "Has this number been reassigned to someone else?" -> GET /v2/PhoneNumbers/{PhoneNumber} (with Fields=reassigned_number, LastVerifiedDate)
- "What is the SMS pumping risk score for this number?" -> GET /v2/PhoneNumbers/{PhoneNumber} (with Fields=sms_pumping_risk)
- "Is this a mobile or landline number?" -> GET /v2/PhoneNumbers/{PhoneNumber} (with Fields=line_type_intelligence)
- "Look up multiple phone numbers at once" -> POST /v2/batch/query
- "What line type override exists for this number?" -> GET /v2/PhoneNumbers/{PhoneNumber}/Overrides/{Field}
- "Override the line type classification for a number" -> POST /v2/PhoneNumbers/{PhoneNumber}/Overrides/{Field}
- "Update an existing line type override" -> PUT /v2/PhoneNumbers/{PhoneNumber}/Overrides/{Field}
- "Remove a line type override" -> DELETE /v2/PhoneNumbers/{PhoneNumber}/Overrides/{Field}
- "What are my current rate limits?" -> GET /v2/RateLimits
- "Update the rate limit for a specific bucket" -> PUT /v2/RateLimits/Fields/{Field}/Bucket/{Bucket}

## Response Tips

- **PhoneNumbers lookup**: The `valid` field is the primary validity indicator; `validation_errors` contains reasons when invalid. Each enrichment field (`sim_swap`, `caller_name`, `line_type_intelligence`, etc.) is a nested map that includes its own `error_code` -- check this per-field, as partial failures are common (one field succeeds while another errors).
- **Batch query**: Returns a flat array of result maps in `phone_numbers`; correlate results back to input using the `correlation_id` you provide per entry.
- **Overrides**: 201 on create, 200 on update, 204 on delete (no body). The response echoes both `original_line_type` and `overridden_line_type` so you can confirm the change.
- **RateLimits**: List returns an array of maps; individual bucket lookups return scalar fields (`limit`, `ttl`). 404 means the field/bucket combination does not exist.

## Anomaly Flags

- **Per-field error codes**: Surface any non-null `error_code` inside nested lookup fields (`sim_swap.error_code`, `identity_match.error_code`, etc.) -- these indicate the enrichment provider failed even though the overall request returned 200.
- **Number reassignment detected**: Flag when `reassigned_number.is_number_reassigned` returns `"yes"` -- downstream workflows using this number may be reaching the wrong person.
- **SIM swap recency**: Alert when `sim_swap.last_sim_swap` is within the last 24-48 hours -- strong fraud signal.
- **SMS pumping risk score**: Surface scores above 50 and flag `number_blocked: true` or `number_blocked_last_3_months: true` as active threats.
- **Identity match low scores**: Flag when `identity_match.summary_score` is below 50 or individual match fields return `"no_match"` -- possible fraud or data mismatch.
- **Validation errors present**: Surface the contents of `validation_errors` array when `valid` is false -- callers often miss these details.
- **Rate limit TTL approaching zero**: When checking rate limits, flag buckets where remaining TTL is very low or limit is near exhaustion.

## Playbook

### 1. Verify a phone number before sending SMS

1. Call `GET /v2/PhoneNumbers/{PhoneNumber}?Fields=validation,line_type_intelligence,sms_pumping_risk`
2. Check `valid` is `true` and `validation_errors` is empty
3. Confirm `line_type_intelligence.type` is `"mobile"` (SMS-capable)
4. Check `sms_pumping_risk.sms_pumping_risk_score` -- reject or flag if above your threshold
5. Check `sms_pumping_risk.number_blocked` -- do not send if `true`
6. Proceed with SMS send only if all checks pass

### 2. Fraud screening with identity and SIM swap checks

1. Call `GET /v2/PhoneNumbers/{PhoneNumber}?Fields=identity_match,sim_swap,reassigned_number&FirstName={first}&LastName={last}&LastVerifiedDate={date}`
2. Check `identity_match.summary_score` -- scores below 50 warrant manual review
3. Inspect `identity_match.first_name_match` and `last_name_match` for `"no_match"` values
4. Check `sim_swap.last_sim_swap` -- recent swaps (within 48h) are a strong fraud indicator
5. Check `reassigned_number.is_number_reassigned` -- if `"yes"`, the number may belong to someone else
6. Combine signals to produce a risk decision: approve, step-up auth, or reject

### 3. Bulk phone number validation

1. Build the request body with an array of `phone_numbers`, each containing `phone_number`, a unique `correlation_id`, and desired `fields`
2. Call `POST /v2/batch/query` with the full array
3. Iterate over the response `phone_numbers` array, matching each result by `correlation_id`
4. For each result, apply the same validation logic as single lookups (check `valid`, `error_code` per field)
5. Aggregate failures and partial errors into a report for review

### 4. Override and manage line type classifications

1. Check the current override: `GET /v2/PhoneNumbers/{PhoneNumber}/Overrides/{Field}`
2. If 404, no override exists -- create one: `POST /v2/PhoneNumbers/{PhoneNumber}/Overrides/{Field}` with `line_type` and `reason`
3. If an override exists but needs updating: `PUT /v2/PhoneNumbers/{PhoneNumber}/Overrides/{Field}` with the new `line_type`
4. Verify the response shows the correct `overridden_line_type`
5. To remove an override: `DELETE /v2/PhoneNumbers/{PhoneNumber}/Overrides/{Field}` (expect 204)

### 5. Monitor and adjust rate limits

1. List all current rate limits: `GET /v2/RateLimits`
2. Inspect a specific bucket: `GET /v2/RateLimits/Fields/{Field}/Bucket/{Bucket}`
3. Note the current `limit` and `ttl` values
4. Adjust as needed: `PUT /v2/RateLimits/Fields/{Field}/Bucket/{Bucket}` with new `limit` and/or `ttl`
5. To remove a rate limit bucket entirely: `DELETE /v2/RateLimits/Fields/{Field}/Bucket/{Bucket}` (expect 204)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
