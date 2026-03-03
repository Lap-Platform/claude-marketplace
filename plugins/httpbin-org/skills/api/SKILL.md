---
name: httpbinorg
description: "httpbin.org API skill. Use when working with httpbin.org for absolute-redirect, anything, base64. Covers 73 endpoints."
version: 1.0.0
generator: lapsh
---

# httpbin.org
API version: 0.9.2

## Auth
ApiKey Authorization in header

## Base URL
https://httpbin.org/

## Setup
1. Set your API key in the appropriate header
2. GET /anything -- verify access
3. POST /anything -- create first anything

## Endpoints

73 endpoints across 41 groups. See references/api-spec.lap for full details.

### absolute-redirect
| Method | Path | Description |
|--------|------|-------------|
| GET | /absolute-redirect/{n} | Absolutely 302 Redirects n times. |

### anything
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /anything | Returns anything passed in request data. |
| GET | /anything | Returns anything passed in request data. |
| PATCH | /anything | Returns anything passed in request data. |
| POST | /anything | Returns anything passed in request data. |
| PUT | /anything | Returns anything passed in request data. |
| DELETE | /anything/{anything} | Returns anything passed in request data. |
| GET | /anything/{anything} | Returns anything passed in request data. |
| PATCH | /anything/{anything} | Returns anything passed in request data. |
| POST | /anything/{anything} | Returns anything passed in request data. |
| PUT | /anything/{anything} | Returns anything passed in request data. |

### base64
| Method | Path | Description |
|--------|------|-------------|
| GET | /base64/{value} | Decodes base64url-encoded string. |

### basic-auth
| Method | Path | Description |
|--------|------|-------------|
| GET | /basic-auth/{user}/{passwd} | Prompts the user for authorization using HTTP Basic Auth. |

### bearer
| Method | Path | Description |
|--------|------|-------------|
| GET | /bearer | Prompts the user for authorization using bearer authentication. |

### brotli
| Method | Path | Description |
|--------|------|-------------|
| GET | /brotli | Returns Brotli-encoded data. |

### bytes
| Method | Path | Description |
|--------|------|-------------|
| GET | /bytes/{n} | Returns n random bytes generated with given seed |

### cache
| Method | Path | Description |
|--------|------|-------------|
| GET | /cache | Returns a 304 if an If-Modified-Since header or If-None-Match is present. Returns the same as a GET otherwise. |
| GET | /cache/{value} | Sets a Cache-Control header for n seconds. |

### cookies
| Method | Path | Description |
|--------|------|-------------|
| GET | /cookies | Returns cookie data. |
| GET | /cookies/delete | Deletes cookie(s) as provided by the query string and redirects to cookie list. |
| GET | /cookies/set | Sets cookie(s) as provided by the query string and redirects to cookie list. |
| GET | /cookies/set/{name}/{value} | Sets a cookie and redirects to cookie list. |

### deflate
| Method | Path | Description |
|--------|------|-------------|
| GET | /deflate | Returns Deflate-encoded data. |

### delay
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /delay/{delay} | Returns a delayed response (max of 10 seconds). |
| GET | /delay/{delay} | Returns a delayed response (max of 10 seconds). |
| PATCH | /delay/{delay} | Returns a delayed response (max of 10 seconds). |
| POST | /delay/{delay} | Returns a delayed response (max of 10 seconds). |
| PUT | /delay/{delay} | Returns a delayed response (max of 10 seconds). |

### delete
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /delete | The request's DELETE parameters. |

### deny
| Method | Path | Description |
|--------|------|-------------|
| GET | /deny | Returns page denied by robots.txt rules. |

### digest-auth
| Method | Path | Description |
|--------|------|-------------|
| GET | /digest-auth/{qop}/{user}/{passwd} | Prompts the user for authorization using Digest Auth. |
| GET | /digest-auth/{qop}/{user}/{passwd}/{algorithm} | Prompts the user for authorization using Digest Auth + Algorithm. |
| GET | /digest-auth/{qop}/{user}/{passwd}/{algorithm}/{stale_after} | Prompts the user for authorization using Digest Auth + Algorithm. |

### drip
| Method | Path | Description |
|--------|------|-------------|
| GET | /drip | Drips data over a duration after an optional initial delay. |

### encoding
| Method | Path | Description |
|--------|------|-------------|
| GET | /encoding/utf8 | Returns a UTF-8 encoded body. |

### etag
| Method | Path | Description |
|--------|------|-------------|
| GET | /etag/{etag} | Assumes the resource has the given etag and responds to If-None-Match and If-Match headers appropriately. |

### get
| Method | Path | Description |
|--------|------|-------------|
| GET | /get | The request's query parameters. |

### gzip
| Method | Path | Description |
|--------|------|-------------|
| GET | /gzip | Returns GZip-encoded data. |

### headers
| Method | Path | Description |
|--------|------|-------------|
| GET | /headers | Return the incoming request's HTTP headers. |

### hidden-basic-auth
| Method | Path | Description |
|--------|------|-------------|
| GET | /hidden-basic-auth/{user}/{passwd} | Prompts the user for authorization using HTTP Basic Auth. |

### html
| Method | Path | Description |
|--------|------|-------------|
| GET | /html | Returns a simple HTML document. |

### image
| Method | Path | Description |
|--------|------|-------------|
| GET | /image | Returns a simple image of the type suggest by the Accept header. |
| GET | /image/jpeg | Returns a simple JPEG image. |
| GET | /image/png | Returns a simple PNG image. |
| GET | /image/svg | Returns a simple SVG image. |
| GET | /image/webp | Returns a simple WEBP image. |

### ip
| Method | Path | Description |
|--------|------|-------------|
| GET | /ip | Returns the requester's IP Address. |

### json
| Method | Path | Description |
|--------|------|-------------|
| GET | /json | Returns a simple JSON document. |

### links
| Method | Path | Description |
|--------|------|-------------|
| GET | /links/{n}/{offset} | Generate a page containing n links to other pages which do the same. |

### patch
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /patch | The request's PATCH parameters. |

### post
| Method | Path | Description |
|--------|------|-------------|
| POST | /post | The request's POST parameters. |

### put
| Method | Path | Description |
|--------|------|-------------|
| PUT | /put | The request's PUT parameters. |

### range
| Method | Path | Description |
|--------|------|-------------|
| GET | /range/{numbytes} | Streams n random bytes generated with given seed, at given chunk size per packet. |

### redirect-to
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /redirect-to | 302/3XX Redirects to the given URL. |
| GET | /redirect-to | 302/3XX Redirects to the given URL. |
| PATCH | /redirect-to | 302/3XX Redirects to the given URL. |
| POST | /redirect-to | 302/3XX Redirects to the given URL. |
| PUT | /redirect-to | 302/3XX Redirects to the given URL. |

### redirect
| Method | Path | Description |
|--------|------|-------------|
| GET | /redirect/{n} | 302 Redirects n times. |

### relative-redirect
| Method | Path | Description |
|--------|------|-------------|
| GET | /relative-redirect/{n} | Relatively 302 Redirects n times. |

### response-headers
| Method | Path | Description |
|--------|------|-------------|
| GET | /response-headers | Returns a set of response headers from the query string. |
| POST | /response-headers | Returns a set of response headers from the query string. |

### robots.txt
| Method | Path | Description |
|--------|------|-------------|
| GET | /robots.txt | Returns some robots.txt rules. |

### status
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /status/{codes} | Return status code or random status code if more than one are given |
| GET | /status/{codes} | Return status code or random status code if more than one are given |
| PATCH | /status/{codes} | Return status code or random status code if more than one are given |
| POST | /status/{codes} | Return status code or random status code if more than one are given |
| PUT | /status/{codes} | Return status code or random status code if more than one are given |

### stream-bytes
| Method | Path | Description |
|--------|------|-------------|
| GET | /stream-bytes/{n} | Streams n random bytes generated with given seed, at given chunk size per packet. |

### stream
| Method | Path | Description |
|--------|------|-------------|
| GET | /stream/{n} | Stream n JSON responses |

### user-agent
| Method | Path | Description |
|--------|------|-------------|
| GET | /user-agent | Return the incoming requests's User-Agent header. |

### uuid
| Method | Path | Description |
|--------|------|-------------|
| GET | /uuid | Return a UUID4. |

### xml
| Method | Path | Description |
|--------|------|-------------|
| GET | /xml | Returns a simple XML document. |

## Enhanced Skill Content
## Question Mapping

- "What is my IP address?" -> GET /ip
- "What headers am I sending?" -> GET /headers
- "What is my user agent string?" -> GET /user-agent
- "Can I echo back a POST request with custom data?" -> POST /anything
- "How do I test basic auth with a username and password?" -> GET /basic-auth/{user}/{passwd}
- "How do I test bearer token authentication?" -> GET /bearer
- "Can I generate a random UUID?" -> GET /uuid
- "How do I simulate a delayed response of N seconds?" -> GET /delay/{delay}
- "How do I get a response with a specific HTTP status code?" -> GET /status/{codes}
- "How do I set and read cookies?" -> GET /cookies/set/{name}/{value} then GET /cookies
- "Can I decode a base64-encoded string?" -> GET /base64/{value}
- "How do I test redirect chains of N hops?" -> GET /redirect/{n}
- "How do I get a gzip-compressed response?" -> GET /gzip
- "Can I stream N bytes of random data?" -> GET /stream-bytes/{n}
- "How do I test conditional requests with ETags?" -> GET /etag/{etag}

## Response Tips

- **Request inspection** (`/get`, `/post`, `/anything`, `/headers`, `/ip`, `/user-agent`): Returns a JSON object echoing back `args`, `headers`, `origin`, `url`, and for POST/PUT/PATCH the `data`, `files`, `form`, and `json` fields. Check `origin` for your public IP.
- **Auth endpoints** (`/basic-auth`, `/bearer`, `/digest-auth`, `/hidden-basic-auth`): Return `{ authenticated: true, user: "..." }` on success. Failures return 401 (or 404 for hidden-basic-auth) with no body -- do not parse the response on error.
- **Redirect endpoints** (`/redirect`, `/absolute-redirect`, `/relative-redirect`, `/redirect-to`): Never return 200 directly -- expect 302 responses. Disable auto-follow redirects in your HTTP client to inspect each hop.
- **Data format endpoints** (`/gzip`, `/brotli`, `/deflate`): Return JSON with an `origin`, `headers`, and a boolean field (`gzipped`, `brotli`, `deflated`) confirming the encoding. Your client must support decompression.
- **Binary/streaming endpoints** (`/bytes`, `/stream-bytes`, `/range`, `/stream`, `/drip`, `/image`): Return raw binary or chunked data, not JSON. Set `Accept` headers for `/image` content negotiation. `/stream/{n}` returns newline-delimited JSON objects, not an array.
- **Cookie endpoints** (`/cookies`, `/cookies/set`, `/cookies/delete`): Responses reflect current cookie jar state. `/cookies/set` and `/cookies/delete` issue redirects to `/cookies` -- ensure your client follows redirects with cookie persistence.
- **Status endpoints** (`/status/{codes}`): Can return any HTTP status. Pass comma-separated codes (e.g., `200,300,500`) to get a random one from the set.

## Anomaly Flags

- **Unexpected 403 on any endpoint**: httpbin.org sits behind Cloudflare; a missing `User-Agent` header or bot-like traffic pattern triggers a block. Surface this immediately with a suggestion to add a standard User-Agent.
- **Timeouts on `/delay` or `/drip`**: If `{delay}` exceeds 10 seconds, the server caps it. Flag when the actual response time does not match the requested delay.
- **Redirect loops**: `/redirect/{n}` with large N or `/redirect-to` pointing back to itself can create loops. Flag when redirect count exceeds 10.
- **Binary response where JSON was expected**: Endpoints like `/bytes`, `/stream-bytes`, and `/image` return non-JSON. Flag if the caller is attempting to parse these as JSON.
- **401 from auth endpoints with correct credentials**: Digest auth with `stale_after` parameter intentionally returns stale nonces. Surface when repeated 401s occur despite valid credentials -- the stale nonce mechanism may be in play.
- **304 Not Modified on `/cache` or `/etag`**: Not an error -- conditional caching is working. Flag only if the caller expected fresh data but sent `If-None-Match` or `If-Modified-Since` headers unintentionally.
- **Status code randomization**: When `/status/{codes}` receives multiple comma-separated codes, the response status is random. Flag non-deterministic behavior if the caller seems to expect a consistent result.

## Playbook

### 1. Debug outbound request headers and payload

1. Send your request to `POST /anything` with the same headers, body, and query params you intend to send to the real API.
2. Inspect the response JSON: `headers` shows what the server received, `data` or `json` shows the parsed body, `args` shows query parameters.
3. Compare against what you expected. Fix discrepancies in your client configuration.
4. Repeat with `GET /anything/{anything}` to test path parameter encoding.

### 2. Test authentication flows

1. **Basic auth**: Call `GET /basic-auth/{user}/{passwd}` with an `Authorization: Basic` header. Confirm `{ authenticated: true }`.
2. **Bearer token**: Call `GET /bearer` with `Authorization: Bearer <token>`. Confirm `{ authenticated: true, token: "<token>" }`.
3. **Digest auth**: Call `GET /digest-auth/{qop}/{user}/{passwd}` -- the first request returns 401 with a `WWW-Authenticate` challenge. Resend with the computed digest. Confirm 200.
4. **Negative test**: Omit or corrupt credentials and verify you get 401 (or 404 for `/hidden-basic-auth`).

### 3. Simulate error handling and retries

1. Call `GET /status/500` to trigger a server error. Verify your retry logic activates.
2. Call `GET /status/429` to simulate rate limiting. Check that your backoff strategy engages.
3. Call `GET /status/200,500,503` to get random failures. Run multiple times to exercise both success and error paths.
4. Call `GET /delay/5` to simulate slow responses. Verify your timeout settings fire correctly.
5. Call `GET /status/204` to test empty-body success handling.

### 4. Validate cookie and session management

1. Call `GET /cookies/set/session_id/abc123` to set a cookie. Your client must follow the redirect.
2. Call `GET /cookies` to confirm `{ cookies: { session_id: "abc123" } }`.
3. Call `GET /cookies/set?theme=dark&lang=en` to set multiple cookies via query params.
4. Call `GET /cookies` again to verify all cookies persist.
5. Call `GET /cookies/delete?session_id=` to remove the session cookie.
6. Call `GET /cookies` to confirm deletion.

### 5. Test redirect handling and chain following

1. Call `GET /redirect/3` with auto-redirect disabled. Verify you receive a 302 with a `Location` header.
2. Follow the chain manually, confirming each hop decrements the counter.
3. Call `GET /redirect-to?url=https://example.com&status_code=301` to test custom redirect targets and status codes.
4. Call `GET /absolute-redirect/2` and `GET /relative-redirect/2` to compare absolute vs relative `Location` headers.
5. Verify your client handles both redirect styles correctly and terminates after the final hop returns 200.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
