---
name: pos-terminal-management-api-deprecated
description: "POS Terminal Management API (deprecated) API skill. Use when working with POS Terminal Management API (deprecated) for assignTerminals, findTerminal, getStoresUnderAccount. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# POS Terminal Management API (deprecated)
API version: 1

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://postfmapi-test.adyen.com/postfmapi/terminal/v1

## Setup
1. Set Authorization header with your Bearer token
3. POST /assignTerminals -- create first assignTerminals

## Endpoints

5 endpoints across 5 groups. See references/api-spec.lap for full details.

### assignTerminals
| Method | Path | Description |
|--------|------|-------------|
| POST | /assignTerminals | Assign terminals |

### findTerminal
| Method | Path | Description |
|--------|------|-------------|
| POST | /findTerminal | Get the account or store of a terminal |

### getStoresUnderAccount
| Method | Path | Description |
|--------|------|-------------|
| POST | /getStoresUnderAccount | Get the stores of an account |

### getTerminalDetails
| Method | Path | Description |
|--------|------|-------------|
| POST | /getTerminalDetails | Get the details of a terminal |

### getTerminalsUnderAccount
| Method | Path | Description |
|--------|------|-------------|
| POST | /getTerminalsUnderAccount | Get the list of terminals |

## Enhanced Skill Content
## Question Mapping

- "Which account is this terminal assigned to?" -> POST /findTerminal
- "What are the details of terminal T123?" -> POST /getTerminalDetails
- "How do I assign terminals to a merchant?" -> POST /assignTerminals
- "What stores does this company account have?" -> POST /getStoresUnderAccount
- "List all terminals under my company account" -> POST /getTerminalsUnderAccount
- "Which terminals are in merchant inventory (unassigned to a store)?" -> POST /getTerminalsUnderAccount
- "What is the firmware version on a specific terminal?" -> POST /getTerminalDetails
- "Is this terminal online or offline?" -> POST /getTerminalDetails
- "Move terminals from one store to another" -> POST /assignTerminals
- "What terminals belong to a specific store?" -> POST /getTerminalsUnderAccount
- "What is the SIM status of a terminal?" -> POST /getTerminalDetails
- "When was the last transaction on this terminal?" -> POST /getTerminalDetails
- "How do I put terminals into merchant inventory?" -> POST /assignTerminals (with merchantInventory: true)
- "What is the address of a store linked to a terminal?" -> POST /getTerminalDetails

## Response Tips

- **assignTerminals**: `results` is a map keyed by terminal ID; check each entry for per-terminal success/failure rather than assuming bulk success.
- **findTerminal**: Returns a flat object; `merchantInventory: true` means the terminal is in holding inventory, not assigned to a store.
- **getStoresUnderAccount**: `stores` is an array of maps; filter by merchant account client-side if needed since the optional param narrows server-side.
- **getTerminalDetails**: Deeply nested `storeDetails.address` map; many fields are nullable (marked `?`) so guard against missing `ethernetIp`, `lastActivityDateTime`, `iccid`, and `simStatus`.
- **getTerminalsUnderAccount**: `inventoryTerminals` lists unassigned terminals separately from `merchantAccounts`, which is an array of maps each containing their own terminal lists.

## Anomaly Flags

- **Deprecated API**: This entire API is marked deprecated. Surface a warning on every call recommending migration to the replacement Management API.
- **Terminal inactivity**: If `lastActivityDateTime` or `lastTransactionDateTime` in getTerminalDetails is older than 7 days, flag the terminal as potentially offline or disconnected.
- **SIM status issues**: If `simStatus` is present and not "ACTIVATED" or similar active state, flag for connectivity investigation.
- **Firmware mismatch**: When querying multiple terminals, compare `firmwareVersion` values and flag outliers that may need updating.
- **Inventory drift**: If `merchantInventory: true` on findTerminal but the terminal was expected to be store-assigned, flag the discrepancy.
- **HTTP 422 errors**: Indicate validation failures (e.g., terminal ID format, nonexistent company account). Surface the specific field that failed rather than a generic error.
- **Rate limiting (401/403)**: Repeated auth failures may indicate key rotation is needed or permissions are misconfigured. Surface after 2+ consecutive failures.

## Playbook

### 1. Reassign a Terminal to a Different Store

1. Call POST /findTerminal with `{terminal: "TERMINAL_ID"}` to confirm current assignment.
2. Note the current `companyAccount`, `merchantAccount`, and `store` values.
3. Call POST /assignTerminals with the target `store`, same `companyAccount`, `merchantAccount`, and `terminals: ["TERMINAL_ID"]`.
4. Call POST /findTerminal again to verify the terminal now shows the new store.

### 2. Audit All Terminals Across an Account

1. Call POST /getTerminalsUnderAccount with `{companyAccount: "COMPANY"}` to get the full terminal list.
2. Note any entries in `inventoryTerminals` (unassigned terminals needing attention).
3. For each terminal of interest, call POST /getTerminalDetails with `{terminal: "ID"}` to check `terminalStatus`, `lastActivityDateTime`, and `firmwareVersion`.
4. Flag terminals with stale activity dates or mismatched firmware versions.

### 3. Onboard Terminals to a New Store

1. Call POST /getStoresUnderAccount with `{companyAccount: "COMPANY"}` to confirm the target store exists and note its store code.
2. Call POST /assignTerminals with `{companyAccount: "COMPANY", merchantAccount: "MERCHANT", store: "STORE_CODE", terminals: ["T1", "T2"]}`.
3. Inspect the `results` map in the response to verify each terminal was successfully assigned.
4. Call POST /getTerminalDetails for one terminal to confirm `store` and `storeDetails` reflect the new assignment.

### 4. Investigate a Disconnected Terminal

1. Call POST /findTerminal with `{terminal: "TERMINAL_ID"}` to locate the terminal's account and store.
2. Call POST /getTerminalDetails with `{terminal: "TERMINAL_ID"}` to inspect connectivity fields.
3. Check `terminalStatus`, `lastActivityDateTime`, `wifiIp`/`ethernetIp` (for network), `simStatus` (for cellular), and `firmwareVersion`.
4. If `dhcpEnabled` is true but IP fields are empty, flag a network configuration issue.
5. If `simStatus` indicates inactive, recommend SIM replacement or carrier check.

### 5. Move Terminals to Merchant Inventory

1. Call POST /getTerminalsUnderAccount with `{companyAccount: "COMPANY", store: "CURRENT_STORE"}` to list terminals currently at the store.
2. Call POST /assignTerminals with `{companyAccount: "COMPANY", merchantAccount: "MERCHANT", merchantInventory: true, terminals: ["T1", "T2"]}`.
3. Verify the `results` map confirms each terminal was moved to inventory.
4. Call POST /findTerminal for a sample terminal to confirm `merchantInventory: true` and `store` is cleared.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
