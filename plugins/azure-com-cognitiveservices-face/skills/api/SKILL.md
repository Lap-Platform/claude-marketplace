---
name: face-client
description: "Face Client API skill. Use when working with Face Client for findsimilars, group, identify. Covers 63 endpoints."
version: 1.0.0
generator: lapsh
---

# Face Client
API version: 1.0

## Auth
ApiKey Ocp-Apim-Subscription-Key in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /persongroups -- verify access
3. POST /findsimilars -- create first findsimilars

## Endpoints

63 endpoints across 11 groups. See references/api-spec.lap for full details.

### findsimilars
| Method | Path | Description |
|--------|------|-------------|
| POST | /findsimilars | Given query face's faceId, to search the similar-looking faces from a faceId array, a face list or a large face list. faceId array contains the faces created by [Face - Detect With Url](https://docs.microsoft.com/rest/api/faceapi/face/detectwithurl) or [Face - Detect With Stream](https://docs.microsoft.com/rest/api/faceapi/face/detectwithstream), which will expire at the time specified by faceIdTimeToLive after creation. A "faceListId" is created by [FaceList - Create](https://docs.microsoft.com/rest/api/faceapi/facelist/create) containing persistedFaceIds that will not expire. And a "largeFaceListId" is created by [LargeFaceList - Create](https://docs.microsoft.com/rest/api/faceapi/largefacelist/create) containing persistedFaceIds that will also not expire. Depending on the input the returned similar faces list contains faceIds or persistedFaceIds ranked by similarity. |

### group
| Method | Path | Description |
|--------|------|-------------|
| POST | /group | Divide candidate faces into groups based on face similarity.<br /> |

### identify
| Method | Path | Description |
|--------|------|-------------|
| POST | /identify | 1-to-many identification to find the closest matches of the specific query person face from a person group or large person group. |

### verify
| Method | Path | Description |
|--------|------|-------------|
| POST | /verify | Verify whether two faces belong to a same person or whether one face belongs to a person. |

### persongroups
| Method | Path | Description |
|--------|------|-------------|
| POST | /persongroups/{personGroupId}/persons | Create a new person in a specified person group. |
| GET | /persongroups/{personGroupId}/persons | List all persons in a person group, and retrieve person information (including personId, name, userData and persistedFaceIds of registered faces of the person). |
| DELETE | /persongroups/{personGroupId}/persons/{personId} | Delete an existing person from a person group. The persistedFaceId, userData, person name and face feature in the person entry will all be deleted. |
| GET | /persongroups/{personGroupId}/persons/{personId} | Retrieve a person's information, including registered persisted faces, name and userData. |
| PATCH | /persongroups/{personGroupId}/persons/{personId} | Update name or userData of a person. |
| DELETE | /persongroups/{personGroupId}/persons/{personId}/persistedfaces/{persistedFaceId} | Delete a face from a person in a person group by specified personGroupId, personId and persistedFaceId. |
| GET | /persongroups/{personGroupId}/persons/{personId}/persistedfaces/{persistedFaceId} | Retrieve information about a persisted face (specified by persistedFaceId, personId and its belonging personGroupId). |
| PATCH | /persongroups/{personGroupId}/persons/{personId}/persistedfaces/{persistedFaceId} | Add a face to a person into a person group for face identification or verification. To deal with an image contains multiple faces, input face can be specified as an image with a targetFace rectangle. It returns a persistedFaceId representing the added face. No image will be stored. Only the extracted face feature will be stored on server until [PersonGroup PersonFace - Delete](https://docs.microsoft.com/rest/api/faceapi/persongroupperson/deleteface), [PersonGroup Person - Delete](https://docs.microsoft.com/rest/api/faceapi/persongroupperson/delete) or [PersonGroup - Delete](https://docs.microsoft.com/rest/api/faceapi/persongroup/delete) is called. |
| PUT | /persongroups/{personGroupId} | Create a new person group with specified personGroupId, name, user-provided userData and recognitionModel. |
| DELETE | /persongroups/{personGroupId} | Delete an existing person group. Persisted face features of all people in the person group will also be deleted. |
| GET | /persongroups/{personGroupId} | Retrieve person group name, userData and recognitionModel. To get person information under this personGroup, use [PersonGroup Person - List](https://docs.microsoft.com/rest/api/faceapi/persongroupperson/list). |
| PATCH | /persongroups/{personGroupId} | Update an existing person group's display name and userData. The properties which does not appear in request body will not be updated. |
| GET | /persongroups/{personGroupId}/training | Retrieve the training status of a person group (completed or ongoing). |
| GET | /persongroups | List person groups’ personGroupId, name, userData and recognitionModel.<br /> |
| POST | /persongroups/{personGroupId}/train | Queue a person group training task, the training task may not be started immediately. |
| POST | /persongroups/{personGroupId}/persons/{personId}/persistedfaces | Add a face to a person into a person group for face identification or verification. To deal with an image contains multiple faces, input face can be specified as an image with a targetFace rectangle. It returns a persistedFaceId representing the added face. No image will be stored. Only the extracted face feature will be stored on server until [PersonGroup PersonFace - Delete](https://docs.microsoft.com/rest/api/faceapi/persongroupperson/deleteface), [PersonGroup Person - Delete](https://docs.microsoft.com/rest/api/faceapi/persongroupperson/delete) or [PersonGroup - Delete](https://docs.microsoft.com/rest/api/faceapi/persongroup/delete) is called. |

### facelists
| Method | Path | Description |
|--------|------|-------------|
| PUT | /facelists/{faceListId} | Create an empty face list with user-specified faceListId, name, an optional userData and recognitionModel. Up to 64 face lists are allowed in one subscription. |
| GET | /facelists/{faceListId} | Retrieve a face list’s faceListId, name, userData, recognitionModel and faces in the face list. |
| PATCH | /facelists/{faceListId} | Update information of a face list. |
| DELETE | /facelists/{faceListId} | Delete a specified face list. |
| GET | /facelists | List face lists’ faceListId, name, userData and recognitionModel. <br /> |
| DELETE | /facelists/{faceListId}/persistedfaces/{persistedFaceId} | Delete a face from a face list by specified faceListId and persistedFaceId. |
| POST | /facelists/{faceListId}/persistedfaces | Add a face to a specified face list, up to 1,000 faces. |

### detect
| Method | Path | Description |
|--------|------|-------------|
| POST | /detect | Detect human faces in an image, return face rectangles, and optionally with faceIds, landmarks, and attributes.<br /> |

### largepersongroups
| Method | Path | Description |
|--------|------|-------------|
| POST | /largepersongroups/{largePersonGroupId}/persons | Create a new person in a specified large person group. |
| GET | /largepersongroups/{largePersonGroupId}/persons | List all persons in a large person group, and retrieve person information (including personId, name, userData and persistedFaceIds of registered faces of the person). |
| DELETE | /largepersongroups/{largePersonGroupId}/persons/{personId} | Delete an existing person from a large person group. The persistedFaceId, userData, person name and face feature in the person entry will all be deleted. |
| GET | /largepersongroups/{largePersonGroupId}/persons/{personId} | Retrieve a person's name and userData, and the persisted faceIds representing the registered person face feature. |
| PATCH | /largepersongroups/{largePersonGroupId}/persons/{personId} | Update name or userData of a person. |
| DELETE | /largepersongroups/{largePersonGroupId}/persons/{personId}/persistedfaces/{persistedFaceId} | Delete a face from a person in a large person group by specified largePersonGroupId, personId and persistedFaceId. |
| GET | /largepersongroups/{largePersonGroupId}/persons/{personId}/persistedfaces/{persistedFaceId} | Retrieve information about a persisted face (specified by persistedFaceId, personId and its belonging largePersonGroupId). |
| PATCH | /largepersongroups/{largePersonGroupId}/persons/{personId}/persistedfaces/{persistedFaceId} | Update a person persisted face's userData field. |
| PUT | /largepersongroups/{largePersonGroupId} | Create a new large person group with user-specified largePersonGroupId, name, an optional userData and recognitionModel. |
| DELETE | /largepersongroups/{largePersonGroupId} | Delete an existing large person group. Persisted face features of all people in the large person group will also be deleted. |
| GET | /largepersongroups/{largePersonGroupId} | Retrieve the information of a large person group, including its name, userData and recognitionModel. This API returns large person group information only, use [LargePersonGroup Person - List](https://docs.microsoft.com/rest/api/faceapi/largepersongroupperson/list) instead to retrieve person information under the large person group. |
| PATCH | /largepersongroups/{largePersonGroupId} | Update an existing large person group's display name and userData. The properties which does not appear in request body will not be updated. |
| GET | /largepersongroups/{largePersonGroupId}/training | Retrieve the training status of a large person group (completed or ongoing). |
| GET | /largepersongroups | List all existing large person groups’ largePersonGroupId, name, userData and recognitionModel.<br /> |
| POST | /largepersongroups/{largePersonGroupId}/train | Queue a large person group training task, the training task may not be started immediately. |
| POST | /largepersongroups/{largePersonGroupId}/persons/{personId}/persistedfaces | Add a face to a person into a large person group for face identification or verification. To deal with an image contains multiple faces, input face can be specified as an image with a targetFace rectangle. It returns a persistedFaceId representing the added face. No image will be stored. Only the extracted face feature will be stored on server until [LargePersonGroup PersonFace - Delete](https://docs.microsoft.com/rest/api/faceapi/largepersongroupperson/deleteface), [LargePersonGroup Person - Delete](https://docs.microsoft.com/rest/api/faceapi/largepersongroupperson/delete) or [LargePersonGroup - Delete](https://docs.microsoft.com/rest/api/faceapi/largepersongroup/delete) is called. |

### largefacelists
| Method | Path | Description |
|--------|------|-------------|
| PUT | /largefacelists/{largeFaceListId} | Create an empty large face list with user-specified largeFaceListId, name, an optional userData and recognitionModel. |
| GET | /largefacelists/{largeFaceListId} | Retrieve a large face list’s largeFaceListId, name, userData and recognitionModel. |
| PATCH | /largefacelists/{largeFaceListId} | Update information of a large face list. |
| DELETE | /largefacelists/{largeFaceListId} | Delete a specified large face list. |
| GET | /largefacelists/{largeFaceListId}/training | Retrieve the training status of a large face list (completed or ongoing). |
| GET | /largefacelists | List large face lists’ information of largeFaceListId, name, userData and recognitionModel. <br /> |
| POST | /largefacelists/{largeFaceListId}/train | Queue a large face list training task, the training task may not be started immediately. |
| DELETE | /largefacelists/{largeFaceListId}/persistedfaces/{persistedFaceId} | Delete a face from a large face list by specified largeFaceListId and persistedFaceId. |
| GET | /largefacelists/{largeFaceListId}/persistedfaces/{persistedFaceId} | Retrieve information about a persisted face (specified by persistedFaceId and its belonging largeFaceListId). |
| PATCH | /largefacelists/{largeFaceListId}/persistedfaces/{persistedFaceId} | Update a persisted face's userData field. |
| POST | /largefacelists/{largeFaceListId}/persistedfaces | Add a face to a specified large face list, up to 1,000,000 faces. |
| GET | /largefacelists/{largeFaceListId}/persistedfaces | List all faces in a large face list, and retrieve face information (including userData and persistedFaceIds of registered faces of the face). |

### snapshots
| Method | Path | Description |
|--------|------|-------------|
| POST | /snapshots | Submit an operation to take a snapshot of face list, large face list, person group or large person group, with user-specified snapshot type, source object id, apply scope and an optional user data.<br /> |
| GET | /snapshots | List all accessible snapshots with related information, including snapshots that were taken by the user, or snapshots to be applied to the user (subscription id was included in the applyScope in Snapshot - Take). |
| GET | /snapshots/{snapshotId} | Retrieve information about a snapshot. Snapshot is only accessible to the source subscription who took it, and target subscriptions included in the applyScope in Snapshot - Take. |
| PATCH | /snapshots/{snapshotId} | Update the information of a snapshot. Only the source subscription who took the snapshot can update the snapshot. |
| DELETE | /snapshots/{snapshotId} | Delete an existing snapshot according to the snapshotId. All object data and information in the snapshot will also be deleted. Only the source subscription who took the snapshot can delete the snapshot. If the user does not delete a snapshot with this API, the snapshot will still be automatically deleted in 48 hours after creation. |
| POST | /snapshots/{snapshotId}/apply | Submit an operation to apply a snapshot to current subscription. For each snapshot, only subscriptions included in the applyScope of Snapshot - Take can apply it.<br /> |

### operations
| Method | Path | Description |
|--------|------|-------------|
| GET | /operations/{operationId} | Retrieve the status of a take/apply snapshot operation. |

## Enhanced Skill Content
## Question Mapping

- "How do I detect faces in an image?" -> POST /detect
- "Can I find similar faces to a given face?" -> POST /findsimilars
- "How do I verify if two faces belong to the same person?" -> POST /verify
- "How do I identify a person from a group?" -> POST /identify
- "How do I create a person group for recognition?" -> PUT /persongroups/{personGroupId}
- "How do I add a person to a person group?" -> POST /persongroups/{personGroupId}/persons
- "How do I add a face to a person in a group?" -> POST /persongroups/{personGroupId}/persons/{personId}/persistedfaces
- "How do I train a person group after adding faces?" -> POST /persongroups/{personGroupId}/train
- "Is my person group done training?" -> GET /persongroups/{personGroupId}/training
- "How do I list all person groups?" -> GET /persongroups
- "How do I create a face list for find-similar lookups?" -> PUT /facelists/{faceListId}
- "How do I migrate data between subscriptions?" -> POST /snapshots then POST /snapshots/{snapshotId}/apply
- "How do I check the status of a long-running operation?" -> GET /operations/{operationId}
- "How do I group detected faces by visual similarity?" -> POST /group
- "When should I use large person groups instead of regular ones?" -> PUT /largepersongroups/{largePersonGroupId} (use when exceeding 1,000 persons)

## Response Tips

- **Detect/FindSimilars/Group/Identify/Verify**: Returns arrays of face objects or match results; always check the `confidence` field and compare against your threshold before trusting a match.
- **PersonGroups & LargePersonGroups (list)**: Paginated via `start` and `top` params; if the response array length equals `top`, fetch the next page using the last item's ID as `start`.
- **Train endpoints**: Return 202 Accepted with no body; poll GET .../training until `status` is `succeeded` or `failed` before using the group for identification.
- **Snapshots & Operations**: 202 responses include an `Operation-Location` header; extract the operation ID and poll GET /operations/{operationId} for completion status.
- **Error responses**: All errors return a JSON object with `error.code` and `error.message`; common codes include `RateLimitExceeded`, `PersonGroupNotFound`, `PersonGroupNotTrained`, and `InvalidImage`.

## Anomaly Flags

- **Rate limit approaching**: Surface `Retry-After` headers immediately; the API enforces per-second and per-minute quotas (typically 10 TPS on free tier) and 429 responses should trigger a backoff alert.
- **Training failures**: If GET .../training returns `status: "failed"`, surface the `message` field -- common causes are insufficient faces or corrupted data.
- **Stale faceId usage**: Detected face IDs expire after `faceIdTimeToLive` (default 24h); flag any attempt to use a faceId that may have expired.
- **Recognition model mismatch**: If `returnRecognitionModel` reveals faces or groups created with different recognition models, flag that they cannot be compared to each other.
- **Snapshot apply failures**: If GET /operations/{operationId} returns a failed status during snapshot apply, surface immediately -- the target resource may be in an inconsistent state.
- **Empty person groups**: Flag any attempt to train or identify against a person group that has zero persons or persons with zero persisted faces.

## Playbook

### 1. Set Up Face Identification from Scratch

1. Create a person group: PUT /persongroups/{personGroupId} with a name and recognition model
2. Add persons: POST /persongroups/{personGroupId}/persons for each individual (save returned `personId`)
3. Add faces to each person: POST /persongroups/{personGroupId}/persons/{personId}/persistedfaces with image data (repeat for multiple angles)
4. Train the group: POST /persongroups/{personGroupId}/train
5. Poll training status: GET /persongroups/{personGroupId}/training until `status` is `succeeded`
6. Detect faces in a new image: POST /detect (save returned `faceId` values)
7. Identify: POST /identify with the faceIds and personGroupId

### 2. Find Similar Faces Using a Face List

1. Create a face list: PUT /facelists/{faceListId} with a name and recognition model
2. Add faces: POST /facelists/{faceListId}/persistedfaces for each reference image
3. Detect faces in a query image: POST /detect (save the `faceId`)
4. Find similar: POST /findsimilars with the faceId and faceListId
5. Review results sorted by confidence score

### 3. Verify Two Faces Match (1:1 Comparison)

1. Detect face A: POST /detect with the first image (save `faceId`)
2. Detect face B: POST /detect with the second image (save `faceId`)
3. Verify: POST /verify with both faceIds
4. Check `isIdentical` (boolean) and `confidence` (0-1) in the response

### 4. Migrate a Person Group to Another Subscription

1. Take a snapshot: POST /snapshots with the source personGroupId and target subscription IDs
2. Poll operation: GET /operations/{operationId} until complete
3. Apply snapshot in target subscription: POST /snapshots/{snapshotId}/apply with the target resource ID
4. Poll operation again: GET /operations/{operationId} until complete
5. Clean up: DELETE /snapshots/{snapshotId} when migration is confirmed

### 5. Scale Up: Migrate from PersonGroup to LargePersonGroup

1. Create a large person group: PUT /largepersongroups/{largePersonGroupId}
2. For each person in the original group: GET /persongroups/{personGroupId}/persons (paginate with `start`/`top`)
3. Recreate each person: POST /largepersongroups/{largePersonGroupId}/persons
4. For each person, list persisted faces: GET .../persons/{personId}/persistedfaces and re-add them to the large group
5. Train: POST /largepersongroups/{largePersonGroupId}/train
6. Poll: GET /largepersongroups/{largePersonGroupId}/training until `succeeded`
7. Update identification calls to use the new largePersonGroupId


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
