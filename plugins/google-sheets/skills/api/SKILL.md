---
name: google-sheets-api
description: "Google Sheets API skill. Use when working with Google Sheets for spreadsheets. Covers 17 endpoints."
version: 1.0.0
generator: lapsh
---

# Google Sheets API
API version: v4

## Auth
OAuth2 | OAuth2

## Base URL
https://sheets.googleapis.com/

## Setup
1. Configure auth: OAuth2 | OAuth2
2. GET /v4/spreadsheets/{spreadsheetId}/values:batchGet -- verify access
3. POST /v4/spreadsheets -- create first spreadsheets

## Endpoints

17 endpoints across 1 groups. See references/api-spec.lap for full details.

### spreadsheets
| Method | Path | Description |
|--------|------|-------------|
| POST | /v4/spreadsheets | Creates a spreadsheet, returning the newly created spreadsheet. |
| GET | /v4/spreadsheets/{spreadsheetId} | Returns the spreadsheet at the given ID. The caller must specify the spreadsheet ID. By default, data within grids is not returned. You can include grid data in one of 2 ways: * Specify a [field mask](https://developers.google.com/sheets/api/guides/field-masks) listing your desired fields using the `fields` URL parameter in HTTP * Set the includeGridData URL parameter to true. If a field mask is set, the `includeGridData` parameter is ignored For large spreadsheets, as a best practice, retrieve only the specific spreadsheet fields that you want. To retrieve only subsets of spreadsheet data, use the ranges URL parameter. Ranges are specified using [A1 notation](/sheets/api/guides/concepts#cell). You can define a single cell (for example, `A1`) or multiple cells (for example, `A1:D5`). You can also get cells from other sheets within the same spreadsheet (for example, `Sheet2!A1:C4`) or retrieve multiple ranges at once (for example, `?ranges=A1:D5&ranges=Sheet2!A1:C4`). Limiting the range returns only the portions of the spreadsheet that intersect the requested ranges. |
| GET | /v4/spreadsheets/{spreadsheetId}/developerMetadata/{metadataId} | Returns the developer metadata with the specified ID. The caller must specify the spreadsheet ID and the developer metadata's unique metadataId. |
| POST | /v4/spreadsheets/{spreadsheetId}/developerMetadata:search | Returns all developer metadata matching the specified DataFilter. If the provided DataFilter represents a DeveloperMetadataLookup object, this will return all DeveloperMetadata entries selected by it. If the DataFilter represents a location in a spreadsheet, this will return all developer metadata associated with locations intersecting that region. |
| POST | /v4/spreadsheets/{spreadsheetId}/sheets/{sheetId}:copyTo | Copies a single sheet from a spreadsheet to another spreadsheet. Returns the properties of the newly created sheet. |
| GET | /v4/spreadsheets/{spreadsheetId}/values/{range} | Returns a range of values from a spreadsheet. The caller must specify the spreadsheet ID and a range. |
| PUT | /v4/spreadsheets/{spreadsheetId}/values/{range} | Sets values in a range of a spreadsheet. The caller must specify the spreadsheet ID, range, and a valueInputOption. |
| POST | /v4/spreadsheets/{spreadsheetId}/values/{range}:append | Appends values to a spreadsheet. The input range is used to search for existing data and find a "table" within that range. Values will be appended to the next row of the table, starting with the first column of the table. See the [guide](/sheets/api/guides/values#appending_values) and [sample code](/sheets/api/samples/writing#append_values) for specific details of how tables are detected and data is appended. The caller must specify the spreadsheet ID, range, and a valueInputOption. The `valueInputOption` only controls how the input data will be added to the sheet (column-wise or row-wise), it does not influence what cell the data starts being written to. |
| POST | /v4/spreadsheets/{spreadsheetId}/values/{range}:clear | Clears values from a spreadsheet. The caller must specify the spreadsheet ID and range. Only values are cleared -- all other properties of the cell (such as formatting, data validation, etc..) are kept. |
| POST | /v4/spreadsheets/{spreadsheetId}/values:batchClear | Clears one or more ranges of values from a spreadsheet. The caller must specify the spreadsheet ID and one or more ranges. Only values are cleared -- all other properties of the cell (such as formatting and data validation) are kept. |
| POST | /v4/spreadsheets/{spreadsheetId}/values:batchClearByDataFilter | Clears one or more ranges of values from a spreadsheet. The caller must specify the spreadsheet ID and one or more DataFilters. Ranges matching any of the specified data filters will be cleared. Only values are cleared -- all other properties of the cell (such as formatting, data validation, etc..) are kept. |
| GET | /v4/spreadsheets/{spreadsheetId}/values:batchGet | Returns one or more ranges of values from a spreadsheet. The caller must specify the spreadsheet ID and one or more ranges. |
| POST | /v4/spreadsheets/{spreadsheetId}/values:batchGetByDataFilter | Returns one or more ranges of values that match the specified data filters. The caller must specify the spreadsheet ID and one or more DataFilters. Ranges that match any of the data filters in the request will be returned. |
| POST | /v4/spreadsheets/{spreadsheetId}/values:batchUpdate | Sets values in one or more ranges of a spreadsheet. The caller must specify the spreadsheet ID, a valueInputOption, and one or more ValueRanges. |
| POST | /v4/spreadsheets/{spreadsheetId}/values:batchUpdateByDataFilter | Sets values in one or more ranges of a spreadsheet. The caller must specify the spreadsheet ID, a valueInputOption, and one or more DataFilterValueRanges. |
| POST | /v4/spreadsheets/{spreadsheetId}:batchUpdate | Applies one or more updates to the spreadsheet. Each request is validated before being applied. If any request is not valid then the entire request will fail and nothing will be applied. Some requests have replies to give you some information about how they are applied. The replies will mirror the requests. For example, if you applied 4 updates and the 3rd one had a reply, then the response will have 2 empty replies, the actual reply, and another empty reply, in that order. Due to the collaborative nature of spreadsheets, it is not guaranteed that the spreadsheet will reflect exactly your changes after this completes, however it is guaranteed that the updates in the request will be applied together atomically. Your changes may be altered with respect to collaborator changes. If there are no collaborators, the spreadsheet should reflect your changes. |
| POST | /v4/spreadsheets/{spreadsheetId}:getByDataFilter | Returns the spreadsheet at the given ID. The caller must specify the spreadsheet ID. This method differs from GetSpreadsheet in that it allows selecting which subsets of spreadsheet data to return by specifying a dataFilters parameter. Multiple DataFilters can be specified. Specifying one or more data filters returns the portions of the spreadsheet that intersect ranges matched by any of the filters. By default, data within grids is not returned. You can include grid data one of 2 ways: * Specify a [field mask](https://developers.google.com/sheets/api/guides/field-masks) listing your desired fields using the `fields` URL parameter in HTTP * Set the includeGridData parameter to true. If a field mask is set, the `includeGridData` parameter is ignored For large spreadsheets, as a best practice, retrieve only the specific spreadsheet fields that you want. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new spreadsheet?" -> POST /v4/spreadsheets
- "How do I read data from a sheet?" -> GET /v4/spreadsheets/{spreadsheetId}/values/{range}
- "How do I write data to a range?" -> PUT /v4/spreadsheets/{spreadsheetId}/values/{range}
- "How do I append rows to a table?" -> POST /v4/spreadsheets/{spreadsheetId}/values/{range}:append
- "How do I clear a range of cells?" -> POST /v4/spreadsheets/{spreadsheetId}/values/{range}:clear
- "How do I read multiple ranges at once?" -> GET /v4/spreadsheets/{spreadsheetId}/values:batchGet
- "How do I update multiple ranges in one call?" -> POST /v4/spreadsheets/{spreadsheetId}/values:batchUpdate
- "How do I get spreadsheet metadata (title, sheets, properties)?" -> GET /v4/spreadsheets/{spreadsheetId}
- "How do I add a sheet, merge cells, or format cells?" -> POST /v4/spreadsheets/{spreadsheetId}:batchUpdate
- "How do I copy a sheet to another spreadsheet?" -> POST /v4/spreadsheets/{spreadsheetId}/sheets/{sheetId}:copyTo
- "How do I find and replace text across sheets?" -> POST /v4/spreadsheets/{spreadsheetId}:batchUpdate (findReplace request)
- "How do I delete rows or columns?" -> POST /v4/spreadsheets/{spreadsheetId}:batchUpdate (deleteDimension request)
- "How do I look up developer metadata by ID?" -> GET /v4/spreadsheets/{spreadsheetId}/developerMetadata/{metadataId}
- "How do I search for developer metadata by key or value?" -> POST /v4/spreadsheets/{spreadsheetId}/developerMetadata:search
- "How do I get spreadsheet data filtered by developer metadata?" -> POST /v4/spreadsheets/{spreadsheetId}:getByDataFilter

## Response Tips

- **Values endpoints** (GET/PUT/append/clear): Response wraps cell data in `values: [[any]]` -- each inner array is one row (or column if `majorDimension=COLUMNS`). Empty trailing cells are omitted, so rows may have unequal lengths.
- **batchGet/batchUpdate**: Results are in `valueRanges[]` or `responses[]` arrays, matched positionally to the input ranges/data arrays. Check `totalUpdatedCells` and per-range counts to confirm all writes landed.
- **Spreadsheet metadata** (GET /spreadsheets, :getByDataFilter): The `sheets[]` array contains full sheet definitions. Grid data is only included when `includeGridData=true` or specific `ranges` are requested -- omit these to keep responses small.
- **batchUpdate (structural)**: The `replies[]` array maps 1:1 to `requests[]`. Many reply objects are empty `{}`; meaningful ones (addSheet, duplicateSheet, findReplace) contain the created/modified resource.
- **Errors**: Google returns `{ error: { code, message, status } }`. Common codes: 400 (bad range syntax like `Sheet1!A:` or invalid sheetId), 403 (missing OAuth scope), 404 (spreadsheet not found or not shared), 429 (rate limit).

## Anomaly Flags

- **429 Too Many Requests**: Surface immediately. Google Sheets enforces per-user and per-project quotas (default 60 read requests/min, 60 write requests/min per user). Back off exponentially.
- **403 with "insufficientPermissions"**: The OAuth token is missing the required scope. Read operations need `spreadsheets.readonly`; writes need `spreadsheets`. Flag this before retrying.
- **Empty `values` array or missing `values` key**: The requested range exists but contains no data. Surface this -- the user may have the wrong range or sheet name.
- **`updatedCells: 0` after a write**: The write succeeded technically but changed nothing. Likely a range mismatch or empty data payload -- flag for user review.
- **`includeGridData` on large sheets**: Responses can exceed 10MB and cause timeouts. Warn when this flag is true without narrowing `ranges`.
- **Mismatched `majorDimension`**: If the user sends data as rows but sets `majorDimension=COLUMNS` (or vice versa), data will be transposed silently. Flag any mismatch between data shape and dimension setting.
- **`valueInputOption` not set on writes**: Defaults to `INPUT_VALUE_OPTION_UNSPECIFIED` which may reject the request. Always surface when this is missing from PUT/append/batchUpdate calls.

## Playbook

### 1. Create a spreadsheet and populate it with data

1. POST /v4/spreadsheets with `{ properties: { title: "My Sheet" } }` to create the spreadsheet.
2. Extract `spreadsheetId` from the response.
3. PUT /v4/spreadsheets/{spreadsheetId}/values/Sheet1!A1 with `valueInputOption=USER_ENTERED` and `values: [["Name","Score"],["Alice",95],["Bob",87]]`.
4. Verify `updatedCells` in the response matches expected count (6 in this example).

### 2. Read, modify, and write back data

1. GET /v4/spreadsheets/{spreadsheetId}/values/Sheet1!A1:Z1000 with `valueRenderOption=UNFORMATTED_VALUE` to get raw numbers.
2. Process the `values[][]` array in your application (filter, compute, transform).
3. PUT /v4/spreadsheets/{spreadsheetId}/values/Sheet1!A1 with the modified `values` and `valueInputOption=RAW`.
4. Check `updatedRows` and `updatedCells` to confirm the write.

### 3. Batch-read multiple named ranges

1. GET /v4/spreadsheets/{spreadsheetId} (no `includeGridData`) to discover sheet names and named ranges.
2. GET /v4/spreadsheets/{spreadsheetId}/values:batchGet with `ranges=["Sheet1!A1:B10","Sheet2!C5:D20","MyNamedRange"]`.
3. Iterate over `valueRanges[]` -- each entry has its own `range` and `values`.

### 4. Format cells and add a chart via batchUpdate

1. POST /v4/spreadsheets/{spreadsheetId}:batchUpdate with a `requests` array containing:
   - `repeatCell` to set bold headers and number formats on a range.
   - `updateBorders` to add borders around the data area.
   - `addChart` with a chart spec referencing the data range.
2. Set `includeSpreadsheetInResponse: true` if you need the updated spreadsheet state.
3. Check `replies[]` -- the `addChart` reply returns the new `chartId` for future modifications.

### 5. Append rows to a growing log/table

1. POST /v4/spreadsheets/{spreadsheetId}/values/Sheet1!A:E:append with `valueInputOption=USER_ENTERED` and `insertDataOption=INSERT_ROWS`.
2. Send `values: [["2026-03-03","event_login","user_42",1,""]]` in the body.
3. The response `tableRange` tells you where existing data ended; `updates.updatedRange` shows where new rows landed.
4. Repeat as new events arrive -- the API auto-detects the table boundary and appends below it.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
