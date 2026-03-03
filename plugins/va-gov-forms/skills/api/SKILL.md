---
name: va-forms
description: "VA Forms API skill. Use when working with VA Forms for forms. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# VA Forms
API version: 0.0.0

## Auth
ApiKey apikey in header

## Base URL
https://sandbox-api.va.gov/services/va_forms/{version}

## Setup
1. Set your API key in the appropriate header
2. GET /forms -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### forms
| Method | Path | Description |
|--------|------|-------------|
| GET | /forms | Returns all VA Forms and their last revision date |
| GET | /forms/{form_name} | Find form by form name |

## Enhanced Skill Content
## Question Mapping

- "What forms are available from the VA?" -> GET /forms
- "Show me all VA forms" -> GET /forms
- "Find a specific VA form by name" -> GET /forms/{form_name}
- "Get details about VA Form 10-10EZ" -> GET /forms/10-10EZ
- "Search for VA forms related to healthcare" -> GET /forms?query=healthcare
- "Does a particular VA form exist?" -> GET /forms/{form_name}
- "What is the current version of a VA form?" -> GET /forms/{form_name}
- "List forms matching a keyword" -> GET /forms?query={keyword}
- "Look up the VA disability claim form" -> GET /forms/21-526EZ
- "What forms do I need for VA benefits?" -> GET /forms?query=benefits
- "Get the PDF link for a VA form" -> GET /forms/{form_name}
- "Is form 10-10EZ still valid or has it been revised?" -> GET /forms/10-10EZ
- "Which forms were recently updated?" -> GET /forms
- "Find all forms in a specific category" -> GET /forms?query={category}

## Response Tips

- **Form listings** (`GET /forms`): Response wraps results in a `data` array. Iterate over `data[]` to access individual form objects. Empty arrays mean no matches, not an error.
- **Form details** (`GET /forms/{form_name}`): Response wraps the single form in a `data` object (not an array). Check nested fields for PDF URLs, revision dates, and related forms.
- **Errors**: 401 means missing or invalid API key in header. 404 on a specific form means the form name is wrong or does not exist. 429 means rate limit hit -- back off and retry.

## Anomaly Flags

- **429 Too Many Requests**: Surface immediately. Advise the user that the API rate limit has been reached and suggest waiting before retrying.
- **401 Unauthorized on first call**: Flag API key misconfiguration. The `apikey` header may be missing or malformed.
- **404 on form lookup**: Proactively suggest similar form names or recommend searching via `GET /forms?query=` with a partial name, since VA form names use specific formats (e.g., `10-10EZ`, `21-526EZ`).
- **Empty `data` array from search**: Surface that no forms matched the query and suggest broadening or rephrasing the search terms.
- **Sandbox vs production base URL**: Flag if the user appears to need production data but calls are hitting `sandbox-api.va.gov`.

## Playbook

### 1. Look up a specific VA form

1. Call `GET /forms/{form_name}` with the exact form name (e.g., `10-10EZ`).
2. If 404, call `GET /forms?query={partial_name}` to search for close matches.
3. Present the form details from the `data` object, including any PDF download URL.

### 2. Search for forms by topic

1. Call `GET /forms?query={keyword}` with a descriptive term (e.g., "disability", "healthcare").
2. Iterate over the `data` array and present matching form names and descriptions.
3. If the user wants details on a specific result, call `GET /forms/{form_name}` for that form.

### 3. Browse all available forms

1. Call `GET /forms` with no query parameter to retrieve the full listing.
2. Summarize the total count from the `data` array length.
3. Group or filter results by category if the user has a specific interest.

### 4. Verify a form is current

1. Call `GET /forms/{form_name}` to retrieve the form record.
2. Check revision date, valid status, and any deprecation indicators in the response.
3. If the form appears outdated, search `GET /forms?query={topic}` for a replacement.

### 5. Handle authentication setup

1. Obtain a VA API key from the VA developer portal.
2. Include the key in the `apikey` request header on every call.
3. Verify access by calling `GET /forms` and confirming a 200 response.
4. If 401 is returned, double-check the header name (`apikey`) and key value.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
