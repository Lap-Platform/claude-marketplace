---
name: call-control-api
description: "Call Control API skill. Use when working with Call Control for api. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Call Control API
API version: 2015-11-01

## Auth
ApiKey apiKey in header

## Base URL
https://api.callcontrol.com

## Setup
1. Set your API key in the appropriate header
2. GET /api/2015-11-01/Complaints/{phoneNumber} -- verify access
3. POST /api/2015-11-01/Enterprise/UpsertUser -- create first UpsertUser

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/2015-11-01/Complaints/{phoneNumber} | Complaints: Free service (with registration), providing community and government complaint lookup by phone number for up to 2,000 queries per month.  Details include number complaint rates from (FTC, FCC, IRS, Indiana Attorney  General) and key entity tag extractions from complaints. |
| GET | /api/2015-11-01/Enterprise/ShouldBlock/{phoneNumber}/{userPhoneNumber} | Enterprise  GET: ShouldBlock |
| GET | /api/2015-11-01/Enterprise/GetUser/{phoneNumber} | Enterprise  GET: GetUser |
| POST | /api/2015-11-01/Enterprise/UpsertUser | UpsertUser: insert or update all properties from a user |
| GET | /api/2015-11-01/Reputation/{phoneNumber} | Reputation: |
| POST | /api/2015-11-01/Report | Report: report spam calls received to better tune our algorithms based upon spam calls you receive |

## Enhanced Skill Content
## Question Mapping

- "Is this phone number a spam caller?" -> GET /api/2015-11-01/Reputation/{phoneNumber}
- "How many complaints does this number have?" -> GET /api/2015-11-01/Complaints/{phoneNumber}
- "Should I block this incoming call?" -> GET /api/2015-11-01/Enterprise/ShouldBlock/{phoneNumber}/{userPhoneNumber}
- "Look up complaint history for +15551234567" -> GET /api/2015-11-01/Complaints/{phoneNumber}
- "Get the reputation score for a number" -> GET /api/2015-11-01/Reputation/{phoneNumber}
- "Report a robocall I just received" -> POST /api/2015-11-01/Report
- "File a spam complaint about a phone number" -> POST /api/2015-11-01/Report
- "Check if a number is safe before answering" -> GET /api/2015-11-01/Reputation/{phoneNumber}
- "Get my enterprise user profile" -> GET /api/2015-11-01/Enterprise/GetUser/{phoneNumber}
- "Create or update an enterprise user" -> POST /api/2015-11-01/Enterprise/UpsertUser
- "Should my enterprise block this caller for user X?" -> GET /api/2015-11-01/Enterprise/ShouldBlock/{phoneNumber}/{userPhoneNumber}
- "Register a new user in our call control system" -> POST /api/2015-11-01/Enterprise/UpsertUser
- "What do other people say about this number?" -> GET /api/2015-11-01/Complaints/{phoneNumber}
- "Check a number's reputation and then report it if it's bad" -> GET /api/2015-11-01/Reputation/{phoneNumber} + POST /api/2015-11-01/Report

## Response Tips

- **Complaints** (GET /Complaints): Response likely contains a list of complaint records. Check for empty arrays meaning no complaints on file, not that the number is safe.
- **ShouldBlock** (GET /Enterprise/ShouldBlock): Returns a blocking recommendation. Treat the response as advisory -- combine with reputation data for stronger confidence. 400 means invalid phone number format.
- **GetUser** (GET /Enterprise/GetUser): Returns enterprise user profile. A 400 likely means the phone number is not registered as an enterprise user.
- **UpsertUser** (POST /Enterprise/UpsertUser): Creates or updates. A 200 applies to both create and update -- check response body to confirm which occurred. The `user` map structure must match the expected schema exactly.
- **Reputation** (GET /Reputation): Returns a reputation score or classification. Higher complaint volumes or known spam databases will reflect here. A 400 means malformed phone number.
- **Report** (POST /Report): No 200 explicitly documented -- success may return 201 or 204. A 400 means the `callReport` payload was malformed or missing required fields.

## Anomaly Flags

- **Missing 200 on Report endpoint**: The POST /Report spec lists no success code, only 400. Surface this if a non-400 response code is unexpected or undocumented.
- **400 errors on phone number lookups**: Likely a formatting issue. Proactively suggest E.164 format (+1XXXXXXXXXX) when users provide bare digits.
- **Reputation vs. Complaints mismatch**: If reputation returns clean but complaints exist (or vice versa), flag the discrepancy -- data sources may update at different rates.
- **Enterprise endpoints without user setup**: ShouldBlock and GetUser will likely fail if the enterprise user hasn't been created via UpsertUser first. Flag when a 400 on these endpoints follows a missing UpsertUser call.
- **Stale API version (2015-11-01)**: This API version is dated. Surface a note if the provider has published newer versions or if deprecation notices appear in response headers.
- **Rate limiting**: Watch for 429 responses or rate-limit headers (X-RateLimit-Remaining, Retry-After) even though not in the spec -- production APIs commonly enforce them silently.

## Playbook

### 1. Screen an Unknown Caller

1. Call GET /api/2015-11-01/Reputation/{phoneNumber} with the incoming number
2. If reputation is negative or suspicious, call GET /api/2015-11-01/Complaints/{phoneNumber} to see specific complaint details
3. Present the combined reputation score and complaint count to the user
4. If clearly spam, optionally submit a report via POST /api/2015-11-01/Report

### 2. Set Up Enterprise Call Blocking for a New User

1. Call POST /api/2015-11-01/Enterprise/UpsertUser with the new user's phone number and profile in the `user` map
2. Verify the user was created by calling GET /api/2015-11-01/Enterprise/GetUser/{phoneNumber}
3. Test the blocking logic by calling GET /api/2015-11-01/Enterprise/ShouldBlock/{testNumber}/{userPhoneNumber} with a known spam number

### 3. Report and Verify a Spam Number

1. Call GET /api/2015-11-01/Reputation/{phoneNumber} to check current reputation
2. Call GET /api/2015-11-01/Complaints/{phoneNumber} to see if others have reported it
3. Submit your report via POST /api/2015-11-01/Report with the `callReport` payload including the phone number and reason
4. Optionally re-check GET /api/2015-11-01/Reputation/{phoneNumber} after some time to confirm the report was factored in

### 4. Enterprise Block Decision Workflow

1. Receive an incoming call to enterprise user's number
2. Call GET /api/2015-11-01/Enterprise/ShouldBlock/{incomingNumber}/{userPhoneNumber}
3. If the response recommends blocking, reject the call
4. If uncertain, fall back to GET /api/2015-11-01/Reputation/{incomingNumber} for additional context
5. Log the decision and optionally POST /api/2015-11-01/Report if the call was confirmed spam


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
