---
name: aws-elemental-mediastore-data-plane
description: "AWS Elemental MediaStore Data Plane API skill. Use when working with AWS Elemental MediaStore Data Plane for {Path+}, root. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Elemental MediaStore Data Plane
API version: 2017-09-01

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET / -- verify access

## Endpoints

5 endpoints across 2 groups. See references/api-spec.lap for full details.

### {Path+}
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /{Path+} | Deletes an object at the specified path. |
| HEAD | /{Path+} | Gets the headers for an object at the specified path. |
| GET | /{Path+} | Downloads the object at the specified path. If the object’s upload availability is set to streaming, AWS Elemental MediaStore downloads the object even if it’s still uploading the object. |
| PUT | /{Path+} | Uploads an object to the specified path. Object sizes are limited to 25 MB for standard upload availability and 10 MB for streaming upload availability. |

### root
| Method | Path | Description |
|--------|------|-------------|
| GET | / | Provides a list of metadata entries about folders and objects in the specified folder. |

## Enhanced Skill Content
## Question Mapping

- "How do I upload a video file to MediaStore?" -> PUT /{Path+}
- "How do I download an object from the container?" -> GET /{Path+}
- "How do I delete a media object?" -> DELETE /{Path+}
- "What objects are stored in my container?" -> GET /
- "How do I check if an object exists without downloading it?" -> HEAD /{Path+}
- "What is the content type of a specific object?" -> HEAD /{Path+}
- "How do I upload with a specific storage class?" -> PUT /{Path+} (use x-amz-storage-class header)
- "How do I list objects under a specific path prefix?" -> GET / (use Path parameter)
- "How do I paginate through a large list of objects?" -> GET / (use NextToken + MaxResults)
- "How do I stream a partial range of a video?" -> GET /{Path+} (use Range header)
- "How do I set cache headers on an uploaded object?" -> PUT /{Path+} (use Cache-Control header)
- "When was an object last modified?" -> HEAD /{Path+} (check LastModified in response)
- "How do I replace an existing object?" -> PUT /{Path+} (same path overwrites)
- "How do I verify upload integrity?" -> PUT /{Path+} (check ContentSHA256 in response)

## Response Tips

- **Object operations (GET/HEAD/PUT /{Path+})**: Responses include ETag for conditional requests and cache invalidation. ContentLength is int64 -- handle large files. LastModified is a timestamp string, not epoch.
- **Listing (GET /)**: Returns an Items array that may be null (empty container). Pagination uses NextToken -- keep calling until NextToken is absent or null.
- **Upload (PUT)**: Returns ContentSHA256 for integrity verification. StorageClass reflects the applied tier -- may differ from requested if unavailable.
- **Delete (DELETE)**: No response body on success. A missing object may still return 200 -- confirm removal with a follow-up HEAD.
- **Errors**: AWS-standard error XML/JSON with Code and Message fields. Watch for 404 (ObjectNotFoundException), 409 (container ACTIVE state required), and 429 (throttling).

## Anomaly Flags

- **429 ThrottlingException**: Surface immediately with retry-after guidance. MediaStore has per-container TPS limits that vary by operation type.
- **x-amz-upload-availability set to "streaming"**: Flag that the object may not be immediately readable after upload returns 200.
- **Missing ETag in HEAD/GET response**: Unusual -- may indicate an incomplete or corrupted upload.
- **ContentLength mismatch**: If HEAD and GET return different ContentLength values for the same path, flag potential concurrent modification.
- **NextToken looping**: If the same NextToken appears in consecutive list responses, surface as a potential pagination bug to avoid infinite loops.
- **StorageClass in PUT response differs from request**: The requested storage class was not applied -- surface so the user can investigate container settings.
- **Null Items array on GET /**: Distinguish between empty container (valid) and permission issues that silently return empty results.

## Playbook

### Upload and Verify a Media Object

1. PUT /{Path+} with Body, Content-Type, and optional Cache-Control
2. Capture ContentSHA256 and ETag from the response
3. HEAD /{Path+} to confirm the object exists and metadata matches
4. Compare ETag values between PUT response and HEAD response to verify consistency

### List All Objects with Pagination

1. GET / with MaxResults set to desired page size (e.g., 100)
2. Process the Items array from the response
3. If NextToken is present, repeat GET / passing the NextToken value
4. Continue until NextToken is absent or null in the response
5. Optionally filter by prefix using the Path parameter to narrow results

### Download a Large Object in Chunks

1. HEAD /{Path+} to retrieve ContentLength and ContentType
2. Calculate byte ranges based on ContentLength (e.g., 10MB chunks)
3. GET /{Path+} with Range header set to first chunk (e.g., "bytes=0-10485759")
4. Verify ContentRange in response matches requested range
5. Repeat for subsequent ranges until the full object is retrieved

### Replace an Object and Confirm Update

1. HEAD /{Path+} to capture the current ETag and LastModified
2. PUT /{Path+} with new Body and updated metadata headers
3. HEAD /{Path+} again to confirm ETag has changed
4. Verify LastModified is more recent than the original value

### Clean Up Objects Under a Path Prefix

1. GET / with Path set to the target prefix to list matching objects
2. For each item in the Items array, call DELETE /{Path+}
3. If NextToken is present, paginate and continue deleting
4. GET / with the same Path prefix to confirm zero Items remain


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
