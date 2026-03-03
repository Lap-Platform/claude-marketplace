---
name: json-storage
description: "JSON storage API skill. Use when working with JSON storage for bin. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# JSON storage
API version: 0.1

## Auth
No authentication required.

## Base URL
https://extendsclass.com/api/json-storage

## Setup
1. No auth setup needed
2. GET /bin/{id} -- verify access
3. POST /bin -- create first bin

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### bin
| Method | Path | Description |
|--------|------|-------------|
| GET | /bin/{id} | Return a json bin |
| PUT | /bin/{id} | Update a json bin |
| PATCH | /bin/{id} | Partially update a json bin with JSON Merge Patch |
| DELETE | /bin/{id} | Delete a json bin |
| POST | /bin | Create a json bin |

## Enhanced Skill Content
## Question Mapping

- "How do I store JSON data?" -> POST /bin
- "How do I retrieve my stored JSON?" -> GET /bin/{id}
- "How do I update my entire JSON bin?" -> PUT /bin/{id}
- "How do I partially update a JSON bin?" -> PATCH /bin/{id}
- "How do I delete a stored JSON bin?" -> DELETE /bin/{id}
- "How do I create a temporary JSON endpoint for testing?" -> POST /bin
- "How do I merge new fields into an existing bin?" -> PATCH /bin/{id}
- "How do I replace all data in a bin without changing its ID?" -> PUT /bin/{id}
- "How do I check if a bin still exists?" -> GET /bin/{id}
- "How do I create a bin, then update it later?" -> POST /bin, then PUT /bin/{id}
- "What happens if I send too large a payload?" -> POST /bin or PUT /bin/{id} (expect 413)
- "How do I clean up bins I no longer need?" -> DELETE /bin/{id}
- "How do I back up a bin's contents before replacing them?" -> GET /bin/{id}, then PUT /bin/{id}

## Response Tips

- **GET /bin/{id}**: Returns raw JSON content directly. A 404 means the bin was deleted or never existed; 422 means malformed bin ID.
- **POST /bin**: Returns `{status, uri, id}` -- save the `id` for all subsequent operations; `uri` is the full retrieval URL.
- **PUT /bin/{id}** and **PATCH /bin/{id}**: Return `{status, data}` -- `data` contains the full bin contents after the write. 401 means the bin is access-protected and your request lacks the correct security key. 413 means payload too large.
- **DELETE /bin/{id}**: Returns `{status}` only. 401 indicates missing or wrong security key.

## Anomaly Flags

- **413 Payload Too Large**: Surface immediately when creating or updating bins -- the user needs to reduce payload size before retrying.
- **401 Unauthorized on modification**: The bin likely has a security key set. Prompt the user to include the `Security-key` header.
- **422 Unprocessable Entity**: Likely malformed JSON body or invalid bin ID format. Flag the specific input that may be malformed.
- **Repeated 404s**: The bin may have been deleted or expired. Suggest creating a new bin if the ID is confirmed correct.
- **Missing `id` in POST response**: If the response shape is unexpected, flag it -- the bin may not have been created successfully despite a 200 status.

## Playbook

### 1. Create and Retrieve a JSON Bin

1. POST /bin with your JSON body to create a new bin.
2. Save the `id` from the response.
3. GET /bin/{id} to confirm the data was stored correctly.

### 2. Update a Bin (Full Replace vs Partial Merge)

1. GET /bin/{id} to review current contents.
2. To replace everything: PUT /bin/{id} with the complete new JSON body.
3. To merge specific fields: PATCH /bin/{id} with only the fields to update.
4. Verify the `data` field in the response matches your expectations.

### 3. Safe Delete with Backup

1. GET /bin/{id} to fetch current contents.
2. Store the response locally as a backup.
3. DELETE /bin/{id} to remove the bin.
4. Confirm deletion by checking for a 404 on GET /bin/{id}.

### 4. Use a Bin as a Temporary Mock API

1. POST /bin with sample response data your frontend or tests expect.
2. Note the `uri` from the response -- this is your mock endpoint URL.
3. Point your client code at the `uri` for development/testing.
4. PATCH /bin/{id} to adjust mock data as test scenarios change.
5. DELETE /bin/{id} when testing is complete.

### 5. Recover from a Failed Update

1. If PUT or PATCH returns 413, reduce your payload size and retry.
2. If PUT or PATCH returns 401, add the `Security-key` header matching the bin's key.
3. If PUT or PATCH returns 404, the bin no longer exists -- POST /bin to create a new one with the data.
4. GET /bin/{id} after any successful update to confirm the final state.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
