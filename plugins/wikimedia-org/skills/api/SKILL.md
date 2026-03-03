---
name: math-api
description: "Math API skill. Use when working with Math for media. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Math API
API version: 1.0.0

## Auth
ApiKey cookie in header

## Base URL
https://wikimedia.org/api/rest_v1

## Setup
1. Set your API key in the appropriate header
2. GET /media/math/formula/{hash} -- verify access
3. POST /media/math/check/{type} -- create first check

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### media
| Method | Path | Description |
|--------|------|-------------|
| POST | /media/math/check/{type} | Check and normalize a TeX formula. |
| GET | /media/math/formula/{hash} | Get a previously-stored formula |
| GET | /media/math/render/{format}/{hash} | Get rendered formula in the given format. |

## Enhanced Skill Content


## Question Mapping

- "How do I validate a LaTeX equation?" -> POST /media/math/check/tex
- "Can I check if a chemical formula is valid?" -> POST /media/math/check/chem
- "How do I validate an inline TeX expression?" -> POST /media/math/check/inline-tex
- "How do I get the stored formula for a given hash?" -> GET /media/math/formula/{hash}
- "How do I render a math expression as SVG?" -> GET /media/math/render/svg/{hash}
- "Can I get a PNG image of a formula?" -> GET /media/math/render/png/{hash}
- "How do I get MathML output for a formula?" -> GET /media/math/render/mml/{hash}
- "How do I go from a raw LaTeX string to a rendered image?" -> POST /media/math/check/tex then GET /media/math/render/png/{hash}
- "What hash corresponds to my equation?" -> POST /media/math/check/tex (hash is returned in response headers/body)
- "How do I embed a formula in a web page?" -> POST /media/math/check/tex then GET /media/math/render/svg/{hash}
- "Can I re-render a previously checked formula in a different format?" -> GET /media/math/render/{format}/{hash}
- "How do I check a formula and get its MathML representation?" -> POST /media/math/check/tex then GET /media/math/render/mml/{hash}
- "Is there a way to retrieve a formula without re-submitting it?" -> GET /media/math/formula/{hash}

## Response Tips

- **check**: Returns the hash of the validated expression; use this hash for all subsequent formula/render calls. A 400 means the input is malformed for the given type.
- **formula**: Returns the stored formula object. A 404 means the hash was never checked or has expired -- re-submit via check first.
- **render**: Returns binary content (image/svg+xml, image/png, or MathML). Consume the response body as a blob/stream, not JSON. A 404 means the hash is unknown.

## Anomaly Flags

- **404 on formula/render**: The hash does not exist. Surface this proactively and suggest re-checking the expression via POST /media/math/check/{type} to obtain a fresh hash.
- **400 on check**: The expression is syntactically invalid for the specified type. Surface the error detail and suggest verifying the type parameter (tex vs inline-tex vs chem).
- **Wrong type parameter**: If a user passes an unsupported value for `{type}` or `{format}`, flag it immediately with the allowed values (tex/inline-tex/chem and svg/mml/png).
- **Missing ApiKey cookie**: Auth is via cookie header. If requests return 401/403, surface that the authentication cookie may be missing or expired.
- **Hash mismatch**: If a user provides a hash manually rather than from a check response, warn that hashes are server-generated and may not match expectations.

## Playbook

### 1. Validate and Render a LaTeX Formula

1. POST /media/math/check/tex with the LaTeX expression in the request body
2. Extract the hash from the response
3. GET /media/math/render/svg/{hash} to retrieve the SVG rendering
4. Use the SVG directly in HTML via an `<img>` tag or inline SVG

### 2. Validate a Chemical Formula

1. POST /media/math/check/chem with the chemical formula in the request body
2. If 200, the formula is valid -- extract the hash for later use
3. If 400, inspect the error to fix syntax issues in the formula
4. Optionally GET /media/math/render/png/{hash} for a rendered image

### 3. Retrieve a Previously Checked Formula

1. Use the hash obtained from a prior POST /media/math/check call
2. GET /media/math/formula/{hash} to retrieve the stored formula object
3. If 404, the formula is no longer available -- re-submit via POST /media/math/check/{type}

### 4. Render a Formula in Multiple Formats

1. POST /media/math/check/tex with the expression to obtain a hash
2. GET /media/math/render/svg/{hash} for scalable vector output
3. GET /media/math/render/png/{hash} for raster image output
4. GET /media/math/render/mml/{hash} for MathML markup
5. Choose the format best suited to the target platform (SVG for web, PNG for documents, MML for accessibility)

### 5. Debug a Failing Formula

1. POST /media/math/check/tex with the suspect expression
2. If 400, read the error response for syntax details
3. Try POST /media/math/check/inline-tex if the expression uses inline conventions
4. Try POST /media/math/check/chem if the expression is chemical rather than mathematical
5. Once validation passes, confirm rendering works via GET /media/math/render/svg/{hash}


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
