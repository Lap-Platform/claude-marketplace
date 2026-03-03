---
name: swagger-generator
description: "Swagger Generator API skill. Use when working with Swagger Generator for gen. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# Swagger Generator
API version: 2.4.49

## Auth
No authentication required.

## Base URL
https://generator.swagger.io/api

## Setup
1. No auth setup needed
2. GET /gen/servers -- verify access
3. POST /gen/servers/{framework} -- create first servers

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### gen
| Method | Path | Description |
|--------|------|-------------|
| GET | /gen/download/{fileId} | Downloads a pre-generated file |
| GET | /gen/servers | Gets languages supported by the server generator |
| GET | /gen/servers/{framework} | Returns options for a server framework |
| POST | /gen/servers/{framework} | Generates a server library |
| GET | /gen/clients/{language} | Returns options for a client library |
| POST | /gen/clients/{language} | Generates a client library |
| GET | /gen/clients | Gets languages supported by the client generator |

## Enhanced Skill Content


## Question Mapping

- "What server frameworks are available for code generation?" -> GET /gen/servers
- "What client languages can I generate SDKs for?" -> GET /gen/clients
- "What options are available for generating a Python client?" -> GET /gen/clients/{language}
- "What options does the Java server generator support?" -> GET /gen/servers/{framework}
- "Generate a TypeScript client from my OpenAPI spec" -> POST /gen/clients/{language}
- "Generate a Spring Boot server stub from my API definition" -> POST /gen/servers/{framework}
- "Download a previously generated SDK file" -> GET /gen/download/{fileId}
- "How do I get my generated code after submitting a generation request?" -> GET /gen/download/{fileId}
- "What server-side frameworks does Swagger Generator support?" -> GET /gen/servers
- "Can I generate a Go client? What config options exist?" -> GET /gen/clients/{language}
- "Generate a Node.js Express server from this spec URL" -> POST /gen/servers/{framework}
- "I submitted a generation request -- how do I retrieve the output?" -> GET /gen/download/{fileId}
- "What customization options exist for the Ruby client generator?" -> GET /gen/clients/{language}

## Response Tips

- **Listings** (GET /gen/clients, GET /gen/servers): Returns flat arrays of strings (language/framework names). No pagination.
- **Options** (GET /gen/clients/{language}, GET /gen/servers/{framework}): Returns a map of configurable options with descriptions and defaults. Use these keys in the body when generating.
- **Generation** (POST /gen/clients/{language}, POST /gen/servers/{framework}): Returns an object with a download link or fileId; extract this to fetch the result.
- **Downloads** (GET /gen/download/{fileId}): Returns binary file content (typically a zip archive); handle as a file download, not JSON.

## Anomaly Flags

- **Missing fileId in generation response**: If a POST to generate code returns 200 but no fileId or download link, surface immediately -- the generation may have silently failed.
- **Unknown language/framework 404**: If a client/server name returns an error, proactively show the user the full list from GET /gen/clients or GET /gen/servers.
- **Large spec payloads**: If the user's OpenAPI spec in the request body is very large, warn that generation may time out or fail silently.
- **Expired download links**: Download fileIds may expire; if GET /gen/download returns 404 or 410, advise the user to regenerate.
- **Deprecated generator names**: Some language/framework names may be aliases or deprecated; if the options response is unexpectedly empty, flag this and suggest checking the listings endpoint.

## Playbook

### Generate a Client SDK

1. List available languages: GET /gen/clients
2. Pick a language and check its options: GET /gen/clients/{language}
3. Build the request body with your OpenAPI spec URL and desired options
4. Submit generation request: POST /gen/clients/{language} with `{ "spec": "<url>", "options": { ... } }`
5. Extract the fileId from the response
6. Download the generated SDK: GET /gen/download/{fileId}

### Generate a Server Stub

1. List available frameworks: GET /gen/servers
2. Inspect options for your chosen framework: GET /gen/servers/{framework}
3. Submit generation request: POST /gen/servers/{framework} with your spec and options
4. Extract the fileId from the response
5. Download the generated server code: GET /gen/download/{fileId}

### Explore Generator Capabilities

1. Fetch all client languages: GET /gen/clients
2. Fetch all server frameworks: GET /gen/servers
3. For each of interest, retrieve configurable options: GET /gen/clients/{language} or GET /gen/servers/{framework}
4. Review option descriptions and defaults to plan your generation configuration

### Regenerate After Download Failure

1. If GET /gen/download/{fileId} returns 404, the file may have expired
2. Re-submit the original generation request: POST /gen/clients/{language} or POST /gen/servers/{framework}
3. Extract the new fileId from the response
4. Retry download with the fresh fileId: GET /gen/download/{fileId}


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
