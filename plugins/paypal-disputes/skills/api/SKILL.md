---
name: disputes
description: "Disputes API skill. Use when working with Disputes for customer. Covers 15 endpoints."
version: 1.0.0
generator: lapsh
---

# Disputes
API version: 1.11

## Auth
OAuth2

## Base URL
https://api-m.sandbox.paypal.com

## Setup
1. Configure auth: OAuth2
2. GET /v1/customer/disputes -- verify access
3. POST /v1/customer/disputes/{id}/provide-evidence -- create first provide-evidence

## Endpoints

15 endpoints across 1 groups. See references/api-spec.lap for full details.

### customer
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/customer/disputes | List disputes |
| GET | /v1/customer/disputes/{id} | Show dispute details |
| PATCH | /v1/customer/disputes/{id} | Partially update dispute |
| POST | /v1/customer/disputes/{id}/provide-evidence | Provide evidence |
| POST | /v1/customer/disputes/{id}/appeal | Appeal dispute |
| POST | /v1/customer/disputes/{id}/accept-claim | Accept claim |
| POST | /v1/customer/disputes/{id}/adjudicate | Settle dispute |
| POST | /v1/customer/disputes/{id}/require-evidence | Update dispute status |
| POST | /v1/customer/disputes/{id}/escalate | Escalate dispute to claim |
| POST | /v1/customer/disputes/{id}/send-message | Send message about dispute to other party |
| POST | /v1/customer/disputes/{id}/make-offer | Make offer to resolve dispute |
| POST | /v1/customer/disputes/{id}/accept-offer | Accept offer to resolve dispute |
| POST | /v1/customer/disputes/{id}/deny-offer | Deny offer to resolve dispute |
| POST | /v1/customer/disputes/{id}/acknowledge-return-item | Acknowledge returned item |
| POST | /v1/customer/disputes/{id}/provide-supporting-info | Provide supporting information for dispute |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my disputes?" -> GET /v1/customer/disputes
- "Show me dispute details for a specific case" -> GET /v1/customer/disputes/{id}
- "What disputes were opened in the last 30 days?" -> GET /v1/customer/disputes (use start_time filter)
- "How do I filter disputes by status?" -> GET /v1/customer/disputes (use dispute_state param)
- "How do I submit evidence for a dispute?" -> POST /v1/customer/disputes/{id}/provide-evidence
- "How do I accept a buyer's claim?" -> POST /v1/customer/disputes/{id}/accept-claim
- "How do I offer a refund to resolve a dispute?" -> POST /v1/customer/disputes/{id}/make-offer
- "How do I escalate a dispute to PayPal?" -> POST /v1/customer/disputes/{id}/escalate
- "How do I send a message to the other party in a dispute?" -> POST /v1/customer/disputes/{id}/send-message
- "How do I appeal a dispute decision?" -> POST /v1/customer/disputes/{id}/appeal
- "How do I accept or reject a settlement offer?" -> POST /v1/customer/disputes/{id}/accept-offer or POST /v1/customer/disputes/{id}/deny-offer
- "How do I confirm I received a returned item?" -> POST /v1/customer/disputes/{id}/acknowledge-return-item
- "How do I update dispute details?" -> PATCH /v1/customer/disputes/{id}
- "How do I adjudicate a dispute as a platform?" -> POST /v1/customer/disputes/{id}/adjudicate (requires adjudication_outcome: BUYER_FAVOR or SELLER_FAVOR)
- "How do I add supporting documents after filing?" -> POST /v1/customer/disputes/{id}/provide-supporting-info

## Response Tips

- **List endpoint**: Returns paginated `items` array with HATEOAS `links`; use `next_page_token` from links to page forward, default page size is 10 (max varies).
- **Detail endpoint**: Deeply nested object; `dispute_amount` and `dispute_outcome.amount_refunded` are `{currency_code, value}` maps. Check `allowed_response_options` to know which actions are currently valid.
- **Action endpoints**: Most return 200 with only `links` for next steps; PATCH may return 202 (accepted, processing) or 204 (no content). Follow returned links for updated state.
- **Error responses**: 400 indicates validation failure (bad ID format, missing required fields); 422 means the action is not allowed in the dispute's current state; 500 is a server error worth retrying.
- **Timestamps**: All datetime fields use `ppaas_date_time_v3` format (ISO 8601). Currency codes follow ISO 4217 via `ppaas_common_currency_code_v2`.

## Anomaly Flags

- **State mismatch**: Surface when an action returns 422 -- the dispute's lifecycle stage does not permit the requested operation. Fetch dispute details to confirm current status before retrying.
- **Empty allowed_response_options**: When retrieving dispute details, flag if `allowed_response_options` is empty or missing -- this means no further actions are available (dispute may be closed or awaiting the other party).
- **Response deadline approaching**: Proactively warn when `seller_response_due_date` or `buyer_response_due_date` is within 48 hours -- missing a deadline can result in automatic resolution against the non-responding party.
- **Unexpected 500 errors**: PayPal sandbox can be intermittent; flag repeated 500s and suggest retrying with exponential backoff or switching to a different sandbox environment.
- **Offer type constraints**: When making an offer, flag if `offer_type` is REFUND_WITH_RETURN but no `return_shipping_address` is provided -- this will likely fail or create an incomplete resolution.
- **Dispute amount vs offer amount**: Surface when `offer_amount` in a make-offer call differs significantly from `dispute_amount` -- the buyer may reject low offers, and overpayment is irreversible.

## Playbook

### 1. Investigate and Respond to a New Dispute

1. Call `GET /v1/customer/disputes?dispute_state=OPEN&page_size=20` to list open disputes.
2. For each dispute, call `GET /v1/customer/disputes/{id}` to get full details.
3. Review `reason`, `disputed_transactions`, and `extensions` to understand the claim.
4. Check `allowed_response_options` to see what actions are available.
5. Check `seller_response_due_date` to know your deadline.
6. Decide on action: provide evidence, accept claim, or make an offer.

### 2. Contest a Dispute with Evidence

1. Call `GET /v1/customer/disputes/{id}` to review claim details and confirm status allows evidence submission.
2. Call `POST /v1/customer/disputes/{id}/provide-evidence` with supporting documents (tracking info, receipts, correspondence).
3. If the initial evidence is insufficient and the case is decided against you, call `POST /v1/customer/disputes/{id}/appeal` to reopen.
4. Optionally call `POST /v1/customer/disputes/{id}/provide-supporting-info` to add supplementary materials.
5. Call `POST /v1/customer/disputes/{id}/escalate` if the buyer is unresponsive and you want PayPal to intervene.

### 3. Resolve a Dispute with a Partial Refund Offer

1. Call `GET /v1/customer/disputes/{id}` and note `dispute_amount` and `refund_details.allowed_refund_amount`.
2. Call `POST /v1/customer/disputes/{id}/make-offer` with `offer_type: REFUND`, a `note` explaining the rationale, and `offer_amount` set to your proposed refund.
3. Monitor via `GET /v1/customer/disputes/{id}` -- check `offer.history` for buyer response.
4. If the buyer counters, evaluate and either accept via `POST /v1/customer/disputes/{id}/accept-offer` or deny via `POST /v1/customer/disputes/{id}/deny-offer` with a reason.

### 4. Handle a Return-and-Refund Flow

1. Call `POST /v1/customer/disputes/{id}/make-offer` with `offer_type: REFUND_WITH_RETURN` and provide `return_shipping_address`.
2. Wait for the buyer to ship the item back (monitor via `GET /v1/customer/disputes/{id}` messages).
3. Once the item arrives, call `POST /v1/customer/disputes/{id}/acknowledge-return-item` to confirm receipt.
4. The refund processes automatically after acknowledgment. Verify final state with `GET /v1/customer/disputes/{id}`.

### 5. Monitor and Triage Disputes in Bulk

1. Call `GET /v1/customer/disputes?page_size=10` to get the first page of disputes.
2. Follow `links` with `rel: next` using `next_page_token` to iterate through all pages.
3. Filter by `update_time_after` and `update_time_before` to scope to a specific date range.
4. For each dispute, check `status` and `seller_response_due_date` to prioritize urgent cases.
5. Use `POST /v1/customer/disputes/{id}/send-message` to communicate with buyers on lower-priority disputes while focusing manual review on high-value or near-deadline cases.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
