---
name: browshot-api
description: "Browshot API skill. Use when working with Browshot for screenshot, batch, account. Covers 17 endpoints."
version: 1.0.0
generator: lapsh
---

# Browshot API
API version: 1.17.0

## Auth
ApiKey key in query

## Base URL
https://api.browshot.com/api/v1

## Setup
1. Set your API key in the appropriate header
2. GET /screenshot/create -- verify access
3. POST /batch/ceate -- create first ceate

## Endpoints

17 endpoints across 5 groups. See references/api-spec.lap for full details.

### screenshot
| Method | Path | Description |
|--------|------|-------------|
| GET | /screenshot/create | Request a screenshot |
| GET | /screenshot/multiple | Request multiple screenshots |
| GET | /screenshot/info | Query screenshot status |
| GET | /screenshot/list | Get information about screenshots |
| GET | /screenshot/search | Search for screenshots |
| GET | /screenshot/host | Host thumbnails on your own S3 account or on Browshot. |
| GET | /screenshot/thumbnail | Retrieve a thumbnail image |
| GET | /screenshot/share | Share a screenshot |
| GET | /screenshot/delete | Delete screenshot data |
| GET | /screenshot/html | Get the HTML code |

### batch
| Method | Path | Description |
|--------|------|-------------|
| POST | /batch/ceate | Requests thousands of screenshtos at once |
| GET | /batch/info | Get the batch status |

### account
| Method | Path | Description |
|--------|------|-------------|
| GET | /account/info | Get information about your account |

### instance
| Method | Path | Description |
|--------|------|-------------|
| GET | /instance/info | Get information about an instance |
| GET | /instance/list | Get all instances |

### browser
| Method | Path | Description |
|--------|------|-------------|
| GET | /browser/info | Get information about a browser |
| GET | /browser/list | Get all browsers |

## Enhanced Skill Content
## Question Mapping

- "Take a screenshot of a website?" -> GET /screenshot/create
- "Capture screenshots of multiple URLs at once?" -> GET /screenshot/multiple
- "What's the status of my screenshot?" -> GET /screenshot/info
- "Show me my recent screenshots?" -> GET /screenshot/list
- "Have I already screenshotted this URL?" -> GET /screenshot/search
- "Host my screenshot on S3 or cloud storage?" -> GET /screenshot/host
- "Get a smaller version of a screenshot?" -> GET /screenshot/thumbnail
- "Share a screenshot with someone?" -> GET /screenshot/share
- "Delete a screenshot I no longer need?" -> GET /screenshot/delete
- "Get the HTML source of a captured page?" -> GET /screenshot/html
- "Run a batch of screenshots from a file?" -> POST /batch/ceate
- "Check the progress of my batch job?" -> GET /batch/info
- "How many credits do I have left?" -> GET /account/info
- "What screenshot instances are available?" -> GET /instance/list
- "Which browsers can I use for screenshots?" -> GET /browser/list

## Response Tips

- **screenshot/create & multiple**: Response includes a screenshot `id` and `status` -- poll `/screenshot/info` until status is `finished` before fetching the image.
- **screenshot/list & search**: Returns arrays; use `limit` and `status` params to filter. No cursor-based pagination -- use `limit` to control result size.
- **screenshot/thumbnail**: Returns binary image data (not JSON) on success; a 404 means the screenshot is not yet ready or does not exist.
- **batch**: `POST /batch/ceate` returns a batch `id`; poll `/batch/info` to track completion of all URLs in the batch.
- **account/info**: Contains credit balance and plan details; pass `details=1` for extended billing information.
- **instance & browser**: Returns static configuration lists; responses are stable and safe to cache.

## Anomaly Flags

- **Low credit balance**: After any `GET /account/info` call, surface a warning if remaining credits are below 10% of the plan allocation.
- **Screenshot stuck in processing**: If `/screenshot/info` returns a non-terminal status for more than 5 minutes, flag it -- the job may be stalled.
- **403 on screenshot creation**: Indicates authentication failure or insufficient permissions -- verify the `key` query parameter is correct and the account is active.
- **404 on thumbnail**: The screenshot is either still processing or was deleted -- check `/screenshot/info` before retrying.
- **Batch endpoint typo**: The spec defines `POST /batch/ceate` (missing "r") -- if the API rejects the call, try `/batch/create` as a corrected path.
- **Large batch without hosting**: If a batch is created without `hosting` set, all images stay on Browshot servers temporarily -- flag that results may expire.

## Playbook

### 1. Capture and Download a Screenshot

1. Call `GET /account/info` to confirm available credits.
2. Call `GET /instance/list` to pick an appropriate instance (desktop vs mobile).
3. Call `GET /screenshot/create` with `url`, `instance_id`, and desired `screen_width`/`screen_height`.
4. Note the returned `id`.
5. Poll `GET /screenshot/info?id={id}` until `status` is `finished`.
6. Call `GET /screenshot/thumbnail?id={id}&width=1280&format=png` to download the image.

### 2. Batch Capture Multiple URLs

1. Prepare a file with one URL per line.
2. Call `POST /batch/ceate` with `instance_id` and the `file` parameter.
3. Note the returned batch `id`.
4. Poll `GET /batch/info?id={id}` until all screenshots show a terminal status.
5. For each completed screenshot, call `GET /screenshot/thumbnail` to retrieve the image.

### 3. Host a Screenshot on External Storage

1. Capture a screenshot via `GET /screenshot/create` with `hosting=s3`, `hosting_bucket`, and `hosting_file` set.
2. Wait for completion by polling `GET /screenshot/info`.
3. Alternatively, for an existing screenshot, call `GET /screenshot/host?id={id}&hosting=s3&bucket={bucket}&file={path}`.
4. The hosted URL is returned in the response.

### 4. Search and Clean Up Old Screenshots

1. Call `GET /screenshot/search?url={domain}` to find all screenshots for a given URL.
2. Review the returned list, filtering by status or age.
3. For each unwanted screenshot, call `GET /screenshot/delete?id={id}&data=1` to remove the screenshot and its stored data.
4. Verify deletion by calling `GET /screenshot/info?id={id}` -- it should return an error or deleted status.

### 5. Share a Screenshot with a Public Link

1. Capture or locate an existing screenshot (`GET /screenshot/create` or `GET /screenshot/list`).
2. Call `GET /screenshot/share?id={id}&note=Description+here` to generate a shareable link.
3. The response contains the public URL -- distribute as needed.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
