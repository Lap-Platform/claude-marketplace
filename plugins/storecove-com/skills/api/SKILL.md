---
name: storecove-api
description: "Storecove API skill. Use when working with Storecove for invoice_submissions, document_submissions, legal_entities. Covers 37 endpoints."
version: 1.0.0
generator: lapsh
---

# Storecove API
API version: 2.0.1

## Auth
ApiKey Authorization in header

## Base URL
https://api.storecove.com/api/v2

## Setup
1. Set your API key in the appropriate header
2. GET /webhook_instances/ -- verify access
3. POST /invoice_submissions -- create first invoice_submissions

## Endpoints

37 endpoints across 8 groups. See references/api-spec.lap for full details.

### invoice_submissions
| Method | Path | Description |
|--------|------|-------------|
| GET | /invoice_submissions/{guid}/evidence | DEPRECATED. Get InvoiceSubmission Evidence |
| POST | /invoice_submissions | DEPRECATED. Submit a new invoice |
| POST | /invoice_submissions/preflight | DEPRECATED. Preflight an invoice recipient |

### document_submissions
| Method | Path | Description |
|--------|------|-------------|
| POST | /document_submissions | Submit a new document. |
| GET | /document_submissions/{guid}/evidence/{evidence_type} | Get DocumentSubmission Evidence |

### legal_entities
| Method | Path | Description |
|--------|------|-------------|
| POST | /legal_entities | Create a new LegalEntity |
| GET | /legal_entities/{id} | Get LegalEntity |
| DELETE | /legal_entities/{id} | Delete LegalEntity |
| PATCH | /legal_entities/{id} | Update LegalEntity |
| POST | /legal_entities/{legal_entity_id}/peppol_identifiers | Create a new PeppolIdentifier |
| DELETE | /legal_entities/{legal_entity_id}/peppol_identifiers/{superscheme}/{scheme}/{identifier} | Delete PeppolIdentifier |
| POST | /legal_entities/{legal_entity_id}/administrations | DEPRECATED. Create a new Administration |
| GET | /legal_entities/{legal_entity_id}/administrations/{id} | DEPRECATED. Get Administration |
| DELETE | /legal_entities/{legal_entity_id}/administrations/{id} | DEPRECATED. Delete Administration |
| PATCH | /legal_entities/{legal_entity_id}/administrations/{id} | DEPRECATED. Update Administration |
| POST | /legal_entities/{legal_entity_id}/additional_tax_identifiers | Create a new AdditionalTaxIdentifier |
| GET | /legal_entities/{legal_entity_id}/additional_tax_identifiers/{id} | Get AdditionalTaxIdentifier |
| DELETE | /legal_entities/{legal_entity_id}/additional_tax_identifiers/{id} | Delete AdditionalTaxIdentifier |
| PATCH | /legal_entities/{legal_entity_id}/additional_tax_identifiers/{id} | Update AdditionalTaxIdentifier |
| POST | /legal_entities/{legal_entity_id}/received_documents | Receive a new Document |

### purchase_invoices
| Method | Path | Description |
|--------|------|-------------|
| GET | /purchase_invoices/{guid} | DEPRECATED. Get Purchase invoice data as JSON |
| GET | /purchase_invoices/{guid}/{packaging} | DEPRECATED. Get Purchase invoice data in a selectable format |
| GET | /purchase_invoices/{guid}/{packaging}/{package_version} | DEPRECATED. Get Purchase invoice data as JSON with a Base64-encoded UBL string in the specified version |

### webhook_instances
| Method | Path | Description |
|--------|------|-------------|
| GET | /webhook_instances/ | GET a WebhookInstance |
| DELETE | /webhook_instances/{guid} | DELETE a WebhookInstance |

### discovery
| Method | Path | Description |
|--------|------|-------------|
| POST | /discovery/receives | Discover Network Participant Capabilites |
| POST | /discovery/exists | Discover Network Participant Existence |
| GET | /discovery/identifiers | Discover Country Identifiers ** EXPERIMENTAL |

### received_documents
| Method | Path | Description |
|--------|------|-------------|
| GET | /received_documents/{guid}/{format} | Get a new ReceivedDocument |

### api
| Method | Path | Description |
|--------|------|-------------|
| POST | /api/v2/legal_entities/{legal_entity_id}/c5/iras/email/activate | Request a new C5 Email Activation |
| POST | /api/v2/legal_entities/{legal_entity_id}/c5/iras/email/deactivate | Request a new C5 Email Deactivation |
| PUT | /api/v2/legal_entities/{legal_entity_id}/c5/iras/email/cancel | Cancel a C5 email activation or deactivation |
| POST | /api/v2/legal_entities/{legal_entity_id}/c5/iras/redirect/activate | Request a new C5 Redirect Activation |
| POST | /api/v2/legal_entities/{legal_entity_id}/c5/iras/redirect/deactivate | Request a new C5 Redirect Deactivation |
| PUT | /api/v2/legal_entities/{legal_entity_id}/c5/iras/redirect/cancel | Cancel a C5 redirect activation or deactivation |
| POST | /api/v2/legal_entities/{legal_entity_id}/c5_activation/activate | DEPRECATED. Request a new C5 Activation |
| POST | /api/v2/legal_entities/{legal_entity_id}/c5_deactivation/deactivate | DEPRECATED. Request a new C5 Deactivation |

## Enhanced Skill Content
## Question Mapping

- "How do I send an invoice to a customer?" -> POST /invoice_submissions
- "Can I check if a recipient can receive invoices before sending?" -> POST /invoice_submissions/preflight
- "How do I get proof that an invoice was delivered?" -> GET /invoice_submissions/{guid}/evidence
- "How do I submit a raw document (UBL, CII) instead of using the invoice model?" -> POST /document_submissions
- "How do I retrieve a purchase invoice I received?" -> GET /purchase_invoices/{guid}
- "How do I download a received invoice in a specific format like UBL or CII?" -> GET /purchase_invoices/{guid}/{packaging}
- "How do I register a new legal entity for sending or receiving invoices?" -> POST /legal_entities
- "How do I add a PEPPOL identifier to my legal entity so it can receive e-invoices?" -> POST /legal_entities/{legal_entity_id}/peppol_identifiers
- "How do I look up whether a trading partner exists on a network like PEPPOL?" -> POST /discovery/exists
- "What document types can a recipient accept?" -> POST /discovery/receives
- "What identifier schemes are supported for discovery?" -> GET /discovery/identifiers
- "How do I list pending webhook deliveries?" -> GET /webhook_instances/
- "How do I delete a failed or stale webhook instance?" -> DELETE /webhook_instances/{guid}
- "How do I activate Singapore IRAS e-invoicing via email for a legal entity?" -> POST /api/v2/legal_entities/{legal_entity_id}/c5/iras/email/activate
- "How do I remove a legal entity and all its identifiers?" -> DELETE /legal_entities/{id}

## Response Tips

- **Invoice/document submissions**: 200 returns a `guid` -- store it immediately; you need it for evidence retrieval and tracking. 422 means validation failed; inspect the `errors` array for field-level detail.
- **Legal entities & sub-resources** (PEPPOL identifiers, administrations, tax identifiers): 200 returns the full updated object. 204 on DELETE means success with no body. 404 usually means the parent entity ID is wrong, not just the child.
- **Purchase invoices**: The `{packaging}` and `{package_version}` path segments control output format (e.g., UBL 2.1 vs CII). The response content type changes accordingly (XML vs JSON).
- **Discovery**: `receives` and `exists` both take a `discoverable_participant` body and return capability or boolean results. A 422 means the identifier scheme or value is invalid.
- **Webhook instances**: 200 returns a list; 204 means the list is empty (no pending instances). This is unusual -- check status code before parsing body.
- **C5/IRAS endpoints**: 204 means the activation/deactivation was accepted. 422 errors here often indicate the legal entity is not eligible for the requested tax authority integration.

## Anomaly Flags

- **422 on invoice submission**: Surface the full validation error list -- these often contain multiple issues that need fixing before retry.
- **404 on legal entity sub-resources**: Flag when a legal_entity_id returns 404 -- the entity may have been deleted, which cascades to all PEPPOL identifiers, administrations, and tax identifiers.
- **Preflight rejection**: If `/invoice_submissions/preflight` returns a negative result, alert the user before they attempt the actual submission -- it will fail.
- **Webhook 204 vs 200**: The dual return codes (200 with data, 204 empty) are non-standard. Flag if code assumes a body is always present.
- **Evidence 404**: If evidence is not yet available for a submitted invoice, it may still be processing. Surface this with a suggestion to retry after a delay.
- **PEPPOL identifier deletion path complexity**: The DELETE requires four path segments (legal_entity_id, superscheme, scheme, identifier). Flag if any segment looks malformed or URL-encoded incorrectly.
- **C5 activation without prior legal entity setup**: Flag if a user attempts IRAS activation on a legal entity that lacks required fields (tax identifiers, administrations).
- **401/403 on any endpoint**: Distinguish between missing API key (401) and insufficient permissions (403) -- the fix is different for each.

## Playbook

### 1. Send Your First Invoice

1. Create a legal entity: `POST /legal_entities` with company details (name, address, tax number).
2. Run a preflight check: `POST /invoice_submissions/preflight` with the recipient's identifier to confirm deliverability.
3. Submit the invoice: `POST /invoice_submissions` with the full `invoice_submission` object including line items, tax, and recipient.
4. Store the returned `guid` from the submission response.
5. Retrieve delivery evidence: `GET /invoice_submissions/{guid}/evidence` (may require polling if processing is async).

### 2. Register for PEPPOL e-Invoicing

1. Create or retrieve your legal entity: `POST /legal_entities` or `GET /legal_entities/{id}`.
2. Add a PEPPOL identifier: `POST /legal_entities/{legal_entity_id}/peppol_identifiers` with scheme and identifier (e.g., `0106` for Dutch KvK).
3. Set up an administration: `POST /legal_entities/{legal_entity_id}/administrations` to configure how received invoices are handled.
4. Verify discoverability: `POST /discovery/exists` with your own identifier to confirm registration on the network.

### 3. Retrieve and Process Received Invoices

1. Receive a webhook notification indicating a new purchase invoice (configure webhooks separately).
2. Fetch the invoice: `GET /purchase_invoices/{guid}` for the default JSON representation.
3. If you need a specific format: `GET /purchase_invoices/{guid}/{packaging}` (e.g., `ubl` or `cii`).
4. For a pinned version: `GET /purchase_invoices/{guid}/{packaging}/{package_version}`.
5. Clear the webhook instance: `DELETE /webhook_instances/{guid}` after successful processing.

### 4. Activate Singapore IRAS InvoiceNow

1. Ensure your legal entity exists: `GET /legal_entities/{id}` and verify it has a Singapore tax identifier.
2. Add an additional tax identifier if needed: `POST /legal_entities/{legal_entity_id}/additional_tax_identifiers`.
3. Choose delivery method and activate:
   - Email: `POST /api/v2/legal_entities/{legal_entity_id}/c5/iras/email/activate`
   - Redirect: `POST /api/v2/legal_entities/{legal_entity_id}/c5/iras/redirect/activate`
4. To deactivate later, use the corresponding `/deactivate` endpoint.
5. To cancel a pending activation/deactivation: `PUT .../cancel` with the cancellation request body.

### 5. Discover Trading Partner Capabilities

1. Get the list of supported identifier schemes: `GET /discovery/identifiers`.
2. Check if the partner exists on the network: `POST /discovery/exists` with their identifier (scheme + value).
3. If they exist, check what they can receive: `POST /discovery/receives` with the same identifier.
4. Use the capabilities response to determine which document types and profiles to use when submitting invoices.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
