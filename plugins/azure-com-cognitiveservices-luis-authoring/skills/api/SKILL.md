---
name: luis-authoring-client
description: "LUIS Authoring Client API skill. Use when working with LUIS Authoring Client for apps, azureaccounts, package. Covers 168 endpoints."
version: 1.0.0
generator: lapsh
---

# LUIS Authoring Client
API version: 3.0-preview

## Auth
ApiKey Ocp-Apim-Subscription-Key in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /apps/ -- verify access
3. POST /apps/{appId}/versions/{versionId}/phraselists -- create first phraselists

## Endpoints

168 endpoints across 3 groups. See references/api-spec.lap for full details.

### apps
| Method | Path | Description |
|--------|------|-------------|
| POST | /apps/{appId}/versions/{versionId}/phraselists | Creates a new phraselist feature in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/phraselists | Gets all the phraselist features in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/features | Gets all the extraction phraselist and pattern features in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/phraselists/{phraselistId} | Gets phraselist feature info in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/phraselists/{phraselistId} | Updates the phrases, the state and the name of the phraselist feature in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/phraselists/{phraselistId} | Deletes a phraselist feature from a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/example | Adds a labeled example utterance in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/examples | Adds a batch of labeled example utterances to a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/examples | Returns example utterances to be reviewed from a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/examples/{exampleId} | Deletes the labeled example utterances with the specified ID from a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/intents | Adds an intent to a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/intents | Gets information about the intent models in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/entities | Adds an entity extractor to a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/entities | Gets information about all the simple entity models in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/hierarchicalentities | Gets information about all the hierarchical entity models in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/compositeentities | Gets information about all the composite entity models in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/closedlists | Gets information about all the list entity models in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/closedlists | Adds a list entity model to a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/prebuilts | Adds a list of prebuilt entities to a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/prebuilts | Gets information about all the prebuilt entities in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/listprebuilts | Gets all the available prebuilt entities in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/models | Gets information about all the intent and entity models in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/models/{modelId}/examples | Gets the example utterances for the given intent or entity model in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/intents/{intentId} | Gets information about the intent model in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/intents/{intentId} | Updates the name of an intent in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/intents/{intentId} | Deletes an intent from a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/entities/{entityId} | Gets information about an entity model in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/entities/{entityId} | Deletes an entity or a child from a version of the application. |
| PATCH | /apps/{appId}/versions/{versionId}/entities/{entityId} | Updates the name of an entity extractor or the name and instanceOf model of a child entity extractor. |
| POST | /apps/{appId}/versions/{versionId}/intents/{intentId}/features | Adds a new feature relation to be used by the intent in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/intents/{intentId}/features | Gets the information of the features used by the intent in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/intents/{intentId}/features | Updates the information of the features used by the intent in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/intents/{intentId}/features | Deletes a relation from the feature relations used by the intent in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/entities/{entityId}/features | Adds a new feature relation to be used by the entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/entities/{entityId}/features | Gets the information of the features used by the entity in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/entities/{entityId}/features | Updates the information of the features used by the entity in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/entities/{entityId}/features | Deletes a relation from the feature relations used by the entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/hierarchicalentities/{hEntityId} | Gets information about a hierarchical entity in a version of the application. |
| PATCH | /apps/{appId}/versions/{versionId}/hierarchicalentities/{hEntityId} | Updates the name of a hierarchical entity model in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/hierarchicalentities/{hEntityId} | Deletes a hierarchical entity from a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/compositeentities/{cEntityId} | Gets information about a composite entity in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/compositeentities/{cEntityId} | Updates a composite entity in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/compositeentities/{cEntityId} | Deletes a composite entity from a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/closedlists/{clEntityId} | Gets information about a list entity in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/closedlists/{clEntityId} | Updates the list entity in a version of the application. |
| PATCH | /apps/{appId}/versions/{versionId}/closedlists/{clEntityId} | Adds a batch of sublists to an existing list entity in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/closedlists/{clEntityId} | Deletes a list entity model from a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/prebuilts/{prebuiltId} | Gets information about a prebuilt entity model in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/prebuilts/{prebuiltId} | Deletes a prebuilt entity extractor from a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/closedlists/{clEntityId}/sublists/{subListId} | Deletes a sublist of a specific list entity model from a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/closedlists/{clEntityId}/sublists/{subListId} | Updates one of the list entity's sublists in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/intents/{intentId}/suggest | Suggests example utterances that would improve the accuracy of the intent model in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/entities/{entityId}/suggest | Get suggested example utterances that would improve the accuracy of the entity model in a version of the application. |
| POST | /apps/ | Creates a new LUIS app. |
| GET | /apps/ | Lists all of the user's applications. |
| POST | /apps/import | Imports an application to LUIS, the application's structure is included in the request body. |
| GET | /apps/assistants | Gets the endpoint URLs for the prebuilt Cortana applications. |
| GET | /apps/domains | Gets the available application domains. |
| GET | /apps/usagescenarios | Gets the application available usage scenarios. |
| GET | /apps/cultures | Gets a list of supported cultures. Cultures are equivalent to the written language and locale. For example,"en-us" represents the U.S. variation of English. |
| GET | /apps/{appId}/querylogs | Gets the logs of the past month's endpoint queries for the application. |
| GET | /apps/{appId} | Gets the application info. |
| PUT | /apps/{appId} | Updates the name or description of the application. |
| DELETE | /apps/{appId} | Deletes an application. |
| POST | /apps/{appId}/versions/{versionId}/clone | Creates a new version from the selected version. |
| POST | /apps/{appId}/publish | Publishes a specific version of the application. |
| GET | /apps/{appId}/versions | Gets a list of versions for this application ID. |
| GET | /apps/{appId}/versions/{versionId}/ | Gets the version information such as date created, last modified date, endpoint URL, count of intents and entities, training and publishing status. |
| PUT | /apps/{appId}/versions/{versionId}/ | Updates the name or description of the application version. |
| DELETE | /apps/{appId}/versions/{versionId}/ | Deletes an application version. |
| GET | /apps/{appId}/versions/{versionId}/export | Exports a LUIS application to JSON format. |
| POST | /apps/{appId}/versions/{versionId}/train | Sends a training request for a version of a specified LUIS app. This POST request initiates a request asynchronously. To determine whether the training request is successful, submit a GET request to get training status. Note: The application version is not fully trained unless all the models (intents and entities) are trained successfully or are up to date. To verify training success, get the training status at least once after training is complete. |
| GET | /apps/{appId}/versions/{versionId}/train | Gets the training status of all models (intents and entities) for the specified LUIS app. You must call the train API to train the LUIS app before you call this API to get training status. "appID" specifies the LUIS app ID. "versionId" specifies the version number of the LUIS app. For example, "0.1". |
| POST | /apps/{appId}/versions/import | Imports a new version into a LUIS application. |
| GET | /apps/{appId}/settings | Get the application settings including 'UseAllTrainingData'. |
| PUT | /apps/{appId}/settings | Updates the application settings including 'UseAllTrainingData'. |
| GET | /apps/{appId}/publishsettings | Get the application publish settings including 'UseAllTrainingData'. |
| PUT | /apps/{appId}/publishsettings | Updates the application publish settings including 'UseAllTrainingData'. |
| DELETE | /apps/{appId}/versions/{versionId}/suggest | Deleted an unlabelled utterance in a version of the application. |
| GET | /apps/{appId}/endpoints | Returns the available endpoint deployment regions and URLs. |
| POST | /apps/{appId}/versions/{versionId}/closedlists/{clEntityId}/sublists | Adds a sublist to an existing list entity in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/customprebuiltdomains | Adds a customizable prebuilt domain along with all of its intent and entity models in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/customprebuiltintents | Adds a customizable prebuilt intent model to a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/customprebuiltintents | Gets information about customizable prebuilt intents added to a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/customprebuiltentities | Adds a prebuilt entity model to a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/customprebuiltentities | Gets all prebuilt entities used in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/customprebuiltmodels | Gets all prebuilt intent and entity model information used in a version of this application. |
| DELETE | /apps/{appId}/versions/{versionId}/customprebuiltdomains/{domainName} | Deletes a prebuilt domain's models in a version of the application. |
| GET | /apps/customprebuiltdomains | Gets all the available custom prebuilt domains for all cultures. |
| POST | /apps/customprebuiltdomains | Adds a prebuilt domain along with its intent and entity models as a new application. |
| GET | /apps/customprebuiltdomains/{culture} | Gets all the available prebuilt domains for a specific culture. |
| POST | /apps/{appId}/versions/{versionId}/entities/{entityId}/children | Creates a single child in an existing entity model hierarchy in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/hierarchicalentities/{hEntityId}/children/{hChildId} | Gets information about the child's model contained in an hierarchical entity child model in a version of the application. |
| PATCH | /apps/{appId}/versions/{versionId}/hierarchicalentities/{hEntityId}/children/{hChildId} | Renames a single child in an existing hierarchical entity model in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/hierarchicalentities/{hEntityId}/children/{hChildId} | Deletes a hierarchical entity extractor child in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/compositeentities/{cEntityId}/children | Creates a single child in an existing composite entity model in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/compositeentities/{cEntityId}/children/{cChildId} | Deletes a composite entity extractor child from a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/regexentities | Gets information about the regular expression entity models in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/regexentities | Adds a regular expression entity model to a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/patternanyentities | Get information about the Pattern.Any entity models in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/patternanyentities | Adds a pattern.any entity extractor to a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/entities/{entityId}/roles | Get all roles for an entity in a version of the application |
| POST | /apps/{appId}/versions/{versionId}/entities/{entityId}/roles | Create an entity role in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/prebuilts/{entityId}/roles | Get a prebuilt entity's roles in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/prebuilts/{entityId}/roles | Create a role for a prebuilt entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/closedlists/{entityId}/roles | Get all roles for a list entity in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/closedlists/{entityId}/roles | Create a role for a list entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/regexentities/{entityId}/roles | Get all roles for a regular expression entity in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/regexentities/{entityId}/roles | Create a role for an regular expression entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/compositeentities/{cEntityId}/roles | Get all roles for a composite entity in a version of the application |
| POST | /apps/{appId}/versions/{versionId}/compositeentities/{cEntityId}/roles | Create a role for a composite entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/patternanyentities/{entityId}/roles | Get all roles for a Pattern.any entity in a version of the application |
| POST | /apps/{appId}/versions/{versionId}/patternanyentities/{entityId}/roles | Create a role for an Pattern.any entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/hierarchicalentities/{hEntityId}/roles | Get all roles for a hierarchical entity in a version of the application |
| POST | /apps/{appId}/versions/{versionId}/hierarchicalentities/{hEntityId}/roles | Create a role for an hierarchical entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/customprebuiltentities/{entityId}/roles | Get all roles for a prebuilt entity in a version of the application |
| POST | /apps/{appId}/versions/{versionId}/customprebuiltentities/{entityId}/roles | Create a role for a prebuilt entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/patternanyentities/{entityId}/explicitlist | Get the explicit (exception) list of the pattern.any entity in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/patternanyentities/{entityId}/explicitlist | Add a new exception to the explicit list for the Pattern.Any entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/regexentities/{regexEntityId} | Gets information about a regular expression entity in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/regexentities/{regexEntityId} | Updates the regular expression entity in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/regexentities/{regexEntityId} | Deletes a regular expression entity from a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/patternanyentities/{entityId} | Gets information about the Pattern.Any model in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/patternanyentities/{entityId} | Updates the name and explicit (exception) list of a Pattern.Any entity model in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/patternanyentities/{entityId} | Deletes a Pattern.Any entity extractor from a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/entities/{entityId}/roles/{roleId} | Get one role for a given entity in a version of the application |
| PUT | /apps/{appId}/versions/{versionId}/entities/{entityId}/roles/{roleId} | Update a role for a given entity in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/entities/{entityId}/roles/{roleId} | Delete an entity role in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/prebuilts/{entityId}/roles/{roleId} | Get one role for a given prebuilt entity in a version of the application |
| PUT | /apps/{appId}/versions/{versionId}/prebuilts/{entityId}/roles/{roleId} | Update a role for a given prebuilt entity in a version of the application |
| DELETE | /apps/{appId}/versions/{versionId}/prebuilts/{entityId}/roles/{roleId} | Delete a role in a prebuilt entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/closedlists/{entityId}/roles/{roleId} | Get one role for a given list entity in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/closedlists/{entityId}/roles/{roleId} | Update a role for a given list entity in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/closedlists/{entityId}/roles/{roleId} | Delete a role for a given list entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/regexentities/{entityId}/roles/{roleId} | Get one role for a given regular expression entity in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/regexentities/{entityId}/roles/{roleId} | Update a role for a given regular expression entity in a version of the application |
| DELETE | /apps/{appId}/versions/{versionId}/regexentities/{entityId}/roles/{roleId} | Delete a role for a given regular expression in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/compositeentities/{cEntityId}/roles/{roleId} | Get one role for a given composite entity in a version of the application |
| PUT | /apps/{appId}/versions/{versionId}/compositeentities/{cEntityId}/roles/{roleId} | Update a role for a given composite entity in a version of the application |
| DELETE | /apps/{appId}/versions/{versionId}/compositeentities/{cEntityId}/roles/{roleId} | Delete a role for a given composite entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/patternanyentities/{entityId}/roles/{roleId} | Get one role for a given Pattern.any entity in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/patternanyentities/{entityId}/roles/{roleId} | Update a role for a given Pattern.any entity in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/patternanyentities/{entityId}/roles/{roleId} | Delete a role for a given Pattern.any entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/hierarchicalentities/{hEntityId}/roles/{roleId} | Get one role for a given hierarchical entity in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/hierarchicalentities/{hEntityId}/roles/{roleId} | Update a role for a given hierarchical entity in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/hierarchicalentities/{hEntityId}/roles/{roleId} | Delete a role for a given hierarchical role in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/customprebuiltentities/{entityId}/roles/{roleId} | Get one role for a given prebuilt entity in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/customprebuiltentities/{entityId}/roles/{roleId} | Update a role for a given prebuilt entity in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/customprebuiltentities/{entityId}/roles/{roleId} | Delete a role for a given prebuilt entity in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/patternanyentities/{entityId}/explicitlist/{itemId} | Get the explicit (exception) list of the pattern.any entity in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/patternanyentities/{entityId}/explicitlist/{itemId} | Updates an explicit (exception) list item for a Pattern.Any entity in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/patternanyentities/{entityId}/explicitlist/{itemId} | Delete an item from the explicit (exception) list for a Pattern.any entity in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/patternrule | Adds a pattern to a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/patternrules | Gets patterns in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/patternrules | Updates patterns in a version of the application. |
| POST | /apps/{appId}/versions/{versionId}/patternrules | Adds a batch of patterns in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/patternrules | Deletes a list of patterns in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/patternrules/{patternId} | Updates a pattern in a version of the application. |
| DELETE | /apps/{appId}/versions/{versionId}/patternrules/{patternId} | Deletes the pattern with the specified ID from a version of the application.. |
| GET | /apps/{appId}/versions/{versionId}/intents/{intentId}/patternrules | Returns patterns for the specific intent in a version of the application. |
| GET | /apps/{appId}/versions/{versionId}/settings | Gets the settings in a version of the application. |
| PUT | /apps/{appId}/versions/{versionId}/settings | Updates the settings in a version of the application. |
| POST | /apps/{appId}/azureaccounts | apps - Assign a LUIS Azure account to an application |
| GET | /apps/{appId}/azureaccounts | apps - Get LUIS Azure accounts assigned to the application |
| DELETE | /apps/{appId}/azureaccounts | apps - Removes an assigned LUIS Azure account from an application |

### azureaccounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /azureaccounts | user - Get LUIS Azure accounts |

### package
| Method | Path | Description |
|--------|------|-------------|
| GET | /package/{appId}/slot/{slotName}/gzip | package - Gets published LUIS application package in binary stream GZip format |
| GET | /package/{appId}/versions/{versionId}/gzip | package - Gets trained LUIS application package in binary stream GZip format |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new LUIS app?" -> POST /apps/
- "What LUIS apps do I have?" -> GET /apps/
- "How do I add a training utterance to my app?" -> POST /apps/{appId}/versions/{versionId}/example
- "How do I batch-add multiple utterances at once?" -> POST /apps/{appId}/versions/{versionId}/examples
- "How do I create a new intent?" -> POST /apps/{appId}/versions/{versionId}/intents
- "How do I train my LUIS app version?" -> POST /apps/{appId}/versions/{versionId}/train
- "Is my model done training?" -> GET /apps/{appId}/versions/{versionId}/train
- "How do I publish my app?" -> POST /apps/{appId}/publish
- "How do I export a version of my app?" -> GET /apps/{appId}/versions/{versionId}/export
- "How do I add a phrase list feature?" -> POST /apps/{appId}/versions/{versionId}/phraselists
- "What prebuilt entities are available for my culture?" -> GET /apps/{appId}/versions/{versionId}/listprebuilts
- "How do I clone an app version?" -> POST /apps/{appId}/versions/{versionId}/clone
- "How do I add a pattern rule for an intent?" -> POST /apps/{appId}/versions/{versionId}/patternrule
- "How do I get suggested utterances for an intent?" -> GET /apps/{appId}/versions/{versionId}/intents/{intentId}/suggest
- "How do I download a packaged model for offline use?" -> GET /package/{appId}/slot/{slotName}/gzip

## Response Tips

- **App listing/search (GET /apps/, GET /apps/{appId}/versions):** Results support `skip` and `take` pagination params -- default page size varies, always pass both to paginate reliably.
- **Batch utterance upload (POST /examples):** Can return 201 (all succeeded) or 207 (partial success) -- inspect per-item results in the response array for individual errors.
- **Training (POST then GET /train):** POST returns 202 (accepted, async); poll GET /train until all model statuses show "Success" or "UpToDate" -- do not assume training is instant.
- **Publish (POST /publish):** Can return 201 or 207 -- a 207 means some slots/regions failed; check each region's status in the response body.
- **Entity/intent CRUD:** GET single-resource endpoints return flat objects; list endpoints return arrays. IDs are GUIDs returned on creation (201 body).
- **Roles and features:** Nested under their parent entity path; responses are arrays of role/feature-relation objects keyed by role or feature ID.
- **Azure accounts:** Require both `Authorization` (user token) and optionally `ArmToken` -- these are separate from the `Ocp-Apim-Subscription-Key` header used for all other endpoints.

## Anomaly Flags

- **207 Multi-Status on publish or batch examples:** Surface immediately -- partial failures mean some items succeeded and others did not; the agent should list which items failed and why.
- **Training status stuck or regressed:** If polling GET /train returns statuses other than "Success" or "UpToDate" (e.g., "Fail", "InProgress" for extended periods), flag to the user with the specific model name and status.
- **Hierarchical and composite entities (deprecated):** These entity types are legacy in LUIS v3; if a user creates or modifies them, warn that Microsoft recommends migrating to machine-learned entities with children instead.
- **Missing `Ocp-Apim-Subscription-Key`:** Any 401 should prompt the agent to verify the API key header is set, since all 168 endpoints require it.
- **Large skip/take values:** If a user requests `take` values over 500 for list endpoints, flag that the API may silently cap results or degrade performance.
- **Force-delete of an app (DELETE /apps/{appId} with `force=true`):** Warn that this bypasses safety checks and permanently removes the app and all versions.
- **Version import conflicts:** POST /apps/{appId}/versions/import with an existing `versionId` will fail -- surface a suggestion to use a new version ID or clone first.

## Playbook

### 1. Create an App, Add Intents and Utterances, Then Train and Publish

1. POST /apps/ with `{ name, culture, description }` -- save the returned `appId`
2. Note the default version (usually "0.1") or POST /apps/{appId}/versions/{versionId}/clone to create a working version
3. POST /apps/{appId}/versions/{versionId}/intents with `{ name: "OrderFood" }` -- save the `intentId`
4. POST /apps/{appId}/versions/{versionId}/examples with an array of labeled utterances referencing the intent
5. Check for 207 partial failures in the response; fix and re-submit any failed utterances
6. POST /apps/{appId}/versions/{versionId}/train to kick off training
7. Poll GET /apps/{appId}/versions/{versionId}/train until all models report "Success"
8. POST /apps/{appId}/publish with `{ versionId, isStaging: false }` to deploy to production slot

### 2. Add Entities with Roles and Phrase List Features

1. POST /apps/{appId}/versions/{versionId}/entities with `{ name: "Location" }` -- save `entityId`
2. POST /apps/{appId}/versions/{versionId}/entities/{entityId}/roles with `{ name: "Origin" }`
3. POST /apps/{appId}/versions/{versionId}/entities/{entityId}/roles with `{ name: "Destination" }`
4. POST /apps/{appId}/versions/{versionId}/phraselists with `{ name: "CityNames", phrases: "Seattle,Portland,Vancouver", isExchangeable: true }`
5. POST /apps/{appId}/versions/{versionId}/entities/{entityId}/features to link the phrase list as a feature for the entity
6. Retrain and republish (see Playbook 1, steps 6-8)

### 3. Review and Improve Model Using Suggested Utterances

1. GET /apps/{appId}/versions/{versionId}/intents to list all intents and their IDs
2. For each intent of interest, GET /apps/{appId}/versions/{versionId}/intents/{intentId}/suggest with `take=20`
3. Review suggested utterances; label and correct entity annotations as needed
4. POST /apps/{appId}/versions/{versionId}/examples with the accepted suggestions
5. DELETE /apps/{appId}/versions/{versionId}/suggest for any utterance you want to dismiss from the suggestion pool
6. Retrain and republish

### 4. Export, Clone, and Manage Versions

1. GET /apps/{appId}/versions to list all versions with training/publish status
2. GET /apps/{appId}/versions/{versionId}/export to download the full version as JSON (backup)
3. POST /apps/{appId}/versions/{versionId}/clone with `{ version: "0.2" }` to create an experimental branch
4. Make changes on version "0.2" (add intents, entities, utterances)
5. Train and test version "0.2"; if satisfied, publish it
6. Optionally DELETE /apps/{appId}/versions/{oldVersionId}/ to clean up obsolete versions

### 5. Set Up Pattern Rules for Intent Recognition

1. GET /apps/{appId}/versions/{versionId}/intents to find the target `intentId`
2. POST /apps/{appId}/versions/{versionId}/patternrule with `{ pattern: "book a flight to {Location}", intent: "BookFlight" }`
3. To bulk-add patterns: POST /apps/{appId}/versions/{versionId}/patternrules with an array of pattern objects
4. GET /apps/{appId}/versions/{versionId}/intents/{intentId}/patternrules to verify patterns are attached
5. Retrain and republish; test with utterances matching the pattern structure


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
