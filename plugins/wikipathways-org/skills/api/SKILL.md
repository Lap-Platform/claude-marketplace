---
name: wikipathways-webservices
description: "WikiPathways Webservices API skill. Use when working with WikiPathways Webservices for listOrganisms, listPathways, getPathway. Covers 26 endpoints."
version: 1.0.0
generator: lapsh
---

# WikiPathways Webservices
API version: 1.0

## Auth
ApiKey auth in query

## Base URL
https://webservice.wikipathways.org/

## Setup
1. Set your API key in the appropriate header
2. GET /listOrganisms -- verify access
3. POST /createPathway -- create first createPathway

## Endpoints

26 endpoints across 26 groups. See references/api-spec.lap for full details.

### listOrganisms
| Method | Path | Description |
|--------|------|-------------|
| GET | /listOrganisms | listOrganisms |

### listPathways
| Method | Path | Description |
|--------|------|-------------|
| GET | /listPathways | listPathways |

### getPathway
| Method | Path | Description |
|--------|------|-------------|
| GET | /getPathway | getPathway |

### getPathwayInfo
| Method | Path | Description |
|--------|------|-------------|
| GET | /getPathwayInfo | getPathwayInfoGet some general info about the pathway, such as the name, species, without downloading the GPML. |

### getPathwayHistory
| Method | Path | Description |
|--------|------|-------------|
| GET | /getPathwayHistory | getPathwayHistoryGet the revision history of a pathway. |

### getRecentChanges
| Method | Path | Description |
|--------|------|-------------|
| GET | /getRecentChanges | getRecentChangesGet the recently changed pathways.<br>Note: the recent changes table only retains items for a limited time (2 months), so there is no guarantee that you will get all changes when the timestamp points to a date that is more than 2 months in the past. |

### login
| Method | Path | Description |
|--------|------|-------------|
| GET | /login | loginStart a logged in session, using an existing WikiPathways account. This function will return an authentication code that can be used to excecute methods that need authentication (e.g. updatePathway). |

### updatePathway
| Method | Path | Description |
|--------|------|-------------|
| GET | /updatePathway | updatePathwayUpdate a pathway on the wiki with the given GPML code.<br>Note: To create/modify pathways via the web service, you need to have an account with web service write permissions. Please contact us to request write access for the web service. |

### createPathway
| Method | Path | Description |
|--------|------|-------------|
| POST | /createPathway | createPathwayCreate a new pathway on the wiki with the given GPML code.<br>Note: To create/modify pathways via the web service, you need to have an account with web service write permissions. Please contact us to request write access for the web service. |

### findPathwaysByText
| Method | Path | Description |
|--------|------|-------------|
| GET | /findPathwaysByText | findPathwaysByText |

### findPathwaysByXref
| Method | Path | Description |
|--------|------|-------------|
| GET | /findPathwaysByXref | findPathwaysByXref |

### removeCurationTag
| Method | Path | Description |
|--------|------|-------------|
| GET | /removeCurationTag | removeCurationTagRemove a curation tag from a pathway. |

### saveCurationTag
| Method | Path | Description |
|--------|------|-------------|
| GET | /saveCurationTag | saveCurationTag |

### getCurationTags
| Method | Path | Description |
|--------|------|-------------|
| GET | /getCurationTags | getCurationTagsGet all curation tags for the given tag name. Use this method if you want to find all pathways that are tagged with a specific curation tag. |

### getCurationTagsByName
| Method | Path | Description |
|--------|------|-------------|
| GET | /getCurationTagsByName | getCurationTagsByNameGet all curation tags for the given tag name. Use this method if you want to find all pathways that are tagged with a specific curation tag. |

### getCurationTagHistory
| Method | Path | Description |
|--------|------|-------------|
| GET | /getCurationTagHistory | getCurationTagHistory |

### getColoredPathway
| Method | Path | Description |
|--------|------|-------------|
| GET | /getColoredPathway | getColoredPathwayGet a colored image version of the pathway. |

### findInteractions
| Method | Path | Description |
|--------|------|-------------|
| GET | /findInteractions | findInteractionsFind interactions defined in WikiPathways pathways. |

### getXrefList
| Method | Path | Description |
|--------|------|-------------|
| GET | /getXrefList | getXrefList |

### findPathwaysByLiterature
| Method | Path | Description |
|--------|------|-------------|
| GET | /findPathwaysByLiterature | findPathwaysByLiterature |

### saveOntologyTag
| Method | Path | Description |
|--------|------|-------------|
| GET | /saveOntologyTag | saveOntologyTag |

### removeOntologyTag
| Method | Path | Description |
|--------|------|-------------|
| GET | /removeOntologyTag | removeOntologyTag |

### getOntologyTermsByPathway
| Method | Path | Description |
|--------|------|-------------|
| GET | /getOntologyTermsByPathway | getOntologyTermsByPathway |

### getPathwaysByOntologyTerm
| Method | Path | Description |
|--------|------|-------------|
| GET | /getPathwaysByOntologyTerm | getPathwaysByOntologyTerm |

### getPathwaysByParentOntologyTerm
| Method | Path | Description |
|--------|------|-------------|
| GET | /getPathwaysByParentOntologyTerm | getPathwaysByParentOntologyTerm |

### getUserByOrcid
| Method | Path | Description |
|--------|------|-------------|
| GET | /getUserByOrcid | getUserByOrcid |

## Enhanced Skill Content
## Question Mapping

- "What organisms are available in WikiPathways?" -> GET /listOrganisms
- "Show me all pathways for Homo sapiens" -> GET /listPathways
- "Download the GPML for pathway WP554" -> GET /getPathway
- "What is the description and revision of pathway WP100?" -> GET /getPathwayInfo
- "What changes were made to pathway WP554 since January 2024?" -> GET /getPathwayHistory
- "What pathways were updated in the last week?" -> GET /getRecentChanges
- "Find pathways related to apoptosis" -> GET /findPathwaysByText
- "Which pathways reference gene BRCA1 by cross-reference ID?" -> GET /findPathwaysByXref
- "Find pathways cited in a specific PubMed paper" -> GET /findPathwaysByLiterature
- "What interactions involve TP53?" -> GET /findInteractions
- "Get all cross-references for pathway WP554 using Ensembl codes" -> GET /getXrefList
- "What curation tags are on pathway WP100?" -> GET /getCurationTags
- "Which pathways have the 'Curation:AnalysisCollection' tag?" -> GET /getCurationTagsByName
- "What ontology terms are associated with pathway WP554?" -> GET /getOntologyTermsByPathway
- "Find pathways annotated with a specific ontology term" -> GET /getPathwaysByOntologyTerm
- "Look up a WikiPathways user by their ORCID" -> GET /getUserByOrcid

## Response Tips

- **Listing endpoints** (listOrganisms, listPathways): Returns flat arrays; no pagination -- full result set in one call. Filter client-side or use the `organism`/`species` param where available.
- **Pathway detail** (getPathway, getPathwayInfo): Returns nested objects with GPML (XML) content embedded as a string field. Parse GPML separately if you need graph structure.
- **Search endpoints** (findPathwaysByText, findPathwaysByXref, findPathwaysByLiterature, findInteractions): Results are arrays of pathway summaries with score/relevance info. Empty queries return empty arrays, not errors.
- **History/changes** (getPathwayHistory, getRecentChanges, getCurationTagHistory): Requires a `timestamp` parameter (typically UNIX epoch or ISO string). Returns chronological change records.
- **Write operations** (updatePathway, createPathway, saveCurationTag, saveOntologyTag): Require `auth` token from login plus `username`. Successful writes return the new revision number.
- **Colored pathway** (getColoredPathway): Returns binary image data (SVG/PNG per `fileType` param), not JSON. Handle as a file download.
- **All endpoints**: Append `format=json` to get JSON responses; default format may be XML.

## Anomaly Flags

- **Auth token expiry**: The `login` endpoint returns a short-lived token. Surface a warning if write operations return auth errors -- the agent should re-authenticate automatically.
- **Missing format parameter**: Responses default to XML. If the agent receives XML unexpectedly, flag that `format=json` was not included and retry.
- **Empty search results**: If `findPathwaysByText` or `findPathwaysByXref` returns zero results, suggest broadening the query or checking organism/species filters.
- **Stale revision on update**: If `updatePathway` fails, it likely means the `revision` parameter is outdated. Flag a revision conflict and suggest fetching the latest revision first.
- **Deprecated pathways**: If `getPathwayInfo` returns a pathway marked as deleted or redirected, surface this to the user before proceeding with further operations.
- **Rate limiting**: WikiPathways is a community resource. If responses slow down or return 429/503 status codes, flag rate limiting and back off automatically.
- **GPML size**: Large pathways can return multi-MB GPML payloads from `getPathway`. Flag when response size is unusually large.

## Playbook

### 1. Search and Download a Pathway

1. Call `GET /listOrganisms` to confirm the target organism name
2. Call `GET /findPathwaysByText?query=apoptosis&species=Homo sapiens&format=json` to find matching pathways
3. Pick the best match from results and note the `pwId`
4. Call `GET /getPathwayInfo?pwId=WP554&format=json` to review metadata
5. Call `GET /getPathway?pwId=WP554&format=json` to download the full GPML content

### 2. Cross-Reference Lookup for a Gene

1. Call `GET /findPathwaysByXref?ids=ENSG00000141510&codes=En&format=json` to find pathways containing the gene
2. For each returned pathway, call `GET /getXrefList?pwId={pwId}&code=L&format=json` to get Entrez Gene cross-references
3. Optionally call `GET /getOntologyTermsByPathway?pwId={pwId}&format=json` to see associated biological terms

### 3. Annotate a Pathway with Curation and Ontology Tags

1. Call `GET /login?name={user}&pass={pass}&format=json` to obtain an auth token
2. Call `GET /getPathwayInfo?pwId={pwId}&format=json` to get the current revision number
3. Call `GET /saveCurationTag?pwId={pwId}&tagName=Curation:AnalysisCollection&text=Reviewed&revision={rev}&auth={token}&username={user}&format=json`
4. Call `GET /saveOntologyTag?pwId={pwId}&term=apoptotic+process&termId=GO:0006915&auth={token}&user={user}&format=json`
5. Verify by calling `GET /getCurationTags?pwId={pwId}&format=json` and `GET /getOntologyTermsByPathway?pwId={pwId}&format=json`

### 4. Monitor Recent Pathway Changes

1. Compute a UNIX timestamp for the desired lookback window (e.g., 7 days ago)
2. Call `GET /getRecentChanges?timestamp={ts}&format=json` to get all recent edits
3. For each changed pathway of interest, call `GET /getPathwayHistory?pwId={pwId}&timestamp={ts}&format=json` for detailed revision history
4. Optionally call `GET /getCurationTagHistory?pwId={pwId}&timestamp={ts}&format=json` to check if curation status changed

### 5. Generate a Highlighted Pathway Image

1. Call `GET /getPathway?pwId={pwId}&format=json` to retrieve the GPML and identify graph element IDs
2. Select the `graphId` values for nodes to highlight and choose hex colors (e.g., `#FF0000`)
3. Call `GET /getColoredPathway?pwId={pwId}&revision={rev}&graphId={id}&color={hex}&fileType=svg` to get the colored image
4. Save the binary response as an SVG or PNG file for review


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
