---
name: deal-api
description: "Deal API skill. Use when working with Deal for deal_item, event, event_item. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Deal API
API version: v1.3.0

## Auth
OAuth2

## Base URL
https://api.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /deal_item -- verify access

## Endpoints

4 endpoints across 3 groups. See references/api-spec.lap for full details.

### deal_item
| Method | Path | Description |
|--------|------|-------------|
| GET | /deal_item | This method retrieves a paginated set of deal items. The result set contains all deal items associated with the specified search criteria and marketplace ID.<h3>Restrictions</h3>This method can return a maximum of 10,000 items. For a list of supported sites and other restrictions, see <a href="/api-docs/buy/browse/overview.html#API" target="_blank">API Restrictions</a>.<br><br><span class="tablenote"><b>eBay Partner Network: </b> In order to receive a commission for your sales, you must use the URL returned in the <code>itemAffiliateWebUrl</code> field to forward your buyer to the ebay.com site.</span> |

### event
| Method | Path | Description |
|--------|------|-------------|
| GET | /event/{event_id} | This method retrieves the details for an eBay event. The result set contains detailed information associated with the specified event ID, such as applicable coupons, start and end dates, and event terms.<h3><b>Restrictions </b></h3>This method can return a maximum of 10,000 items. For a list of supported sites and other restrictions, see <a href="/api-docs/buy/browse/overview.html#API" target="_blank">API Restrictions</a>.<br><br><span class="tablenote"><b>eBay Partner Network: </b> In order to receive a commission for your sales, you must use the URL returned in the <code>itemAffiliateWebUrl</code> field to forward your buyer to the ebay.com site. </span> |
| GET | /event | This method returns paginated results containing all eBay events for the specified marketplace.<h3><b>Restrictions </b></h3>This method can return a maximum of 10,000 items. For a list of supported sites and other restrictions, see <a href="/api-docs/buy/browse/overview.html#API" target="_blank ">API Restrictions</a>.<br><br><span class="tablenote"><b>eBay Partner Network: </b> In order to receive a commission for your sales, you must use the URL returned in the <code>itemAffiliateWebUrl</code> field to forward your buyer to the ebay.com site. </span> |

### event_item
| Method | Path | Description |
|--------|------|-------------|
| GET | /event_item | This method returns a paginated set of event items. The result set contains all event items associated with the specified search criteria and marketplace ID.<h3><b>Restrictions </b></h3>This method can return a maximum of 10,000 items. For a list of supported sites and other restrictions, see <a href="/api-docs/buy/browse/overview.html#API" target="_blank ">API Restrictions</a>.<br><br><span class="tablenote"><b>eBay Partner Network: </b> In order to receive a commission for your sales, you must use the URL returned in the <code>itemAffiliateWebUrl</code> field to forward your buyer to the ebay.com site. </span> |

## Enhanced Skill Content
## Question Mapping

- "What deals are available right now?" -> GET /deal_item
- "Show me deals in a specific category" -> GET /deal_item (with category_ids)
- "What deals can I get with commission?" -> GET /deal_item (with commissionable=true)
- "Are there deals that ship to Germany?" -> GET /deal_item (with delivery_country=DE)
- "What events are running on eBay?" -> GET /event
- "Tell me about a specific event" -> GET /event/{event_id}
- "When does event X start and end?" -> GET /event/{event_id}
- "What coupons apply to this event?" -> GET /event/{event_id}
- "What items are in a specific event?" -> GET /event_item (with event_ids)
- "Show me event items in Electronics" -> GET /event_item (with event_ids + category_ids)
- "How many total deals are available?" -> GET /deal_item (check total in response)
- "What's the affiliate link for this event?" -> GET /event/{event_id} (read eventAffiliateWebUrl)
- "What are the terms and conditions for an event?" -> GET /event/{event_id} (read terms.fullText)
- "List the next page of deal items" -> GET /deal_item (with offset incremented by limit)

## Response Tips

- **Deal items / Event items:** Paginated lists -- use `next`/`prev` URLs for navigation; `total` gives full count; actual items are in `dealItems` or `eventItems` arrays of maps.
- **Single event:** Flat object with nested `terms` (has `fullText` and `summary`) and `images`/`applicableCoupons` as arrays of maps; dates are strings (ISO 8601).
- **Event list:** Same pagination pattern as deal items; events are in the `events` array.
- **Errors:** 400 = bad request (invalid marketplace ID, malformed params); 403 = auth/scope issue; 404 = event not found (only on single event lookup); 500 = retry after brief delay.

## Anomaly Flags

- **Missing marketplace header:** All endpoints require `X-EBAY-C-MARKETPLACE-ID` -- surface a clear error if omitted, since every call will 400 without it.
- **Empty result sets:** If `total` is 0, flag that no deals/events/items matched -- the filters or marketplace may be too narrow.
- **Pagination exhaustion:** If `next` is absent or null, the agent should note there are no more pages rather than attempting another fetch.
- **403 on valid requests:** Likely an OAuth scope issue -- surface that the token may lack the `deals` scope or has expired.
- **Large offsets with zero results:** If offset exceeds total, the API may return empty arrays silently -- flag the mismatch.
- **Event date windows:** If `endDate` is in the past, flag that the event has expired and items may no longer be available at deal prices.
- **Commissionable filter gotcha:** The `commissionable` param is a string, not boolean -- surface if the caller passes a non-string value.

## Playbook

### 1. Browse All Current Deals in a Marketplace

1. Call `GET /deal_item` with `X-EBAY-C-MARKETPLACE-ID` set (e.g., `EBAY_US`).
2. Read `dealItems` array and `total` from the response.
3. If `next` is present, follow it to fetch subsequent pages.
4. Repeat until `next` is null or absent.

### 2. Explore a Specific Event and Its Items

1. Call `GET /event` with the marketplace header to list active events.
2. Pick an event and note its `eventId`.
3. Call `GET /event/{event_id}` with that ID to get full details, coupons, terms, and dates.
4. Call `GET /event_item` with `event_ids` set to the same ID to list items in that event.
5. Page through results using `offset` and `limit` if `total` exceeds one page.

### 3. Find Commissionable Deals by Category

1. Call `GET /deal_item` with `commissionable=true` and `category_ids` set to the desired eBay category ID(s).
2. Include the marketplace header.
3. Review returned `dealItems` for affiliate-eligible listings.
4. Use pagination (`next`/`offset`) to scan all matching deals.

### 4. Check Event Eligibility by Delivery Country

1. Call `GET /event` to discover active events.
2. For a chosen event, call `GET /event_item` with the `event_ids` and `delivery_country` set to the target country code (e.g., `US`, `DE`, `GB`).
3. If `total` is 0, the event has no items deliverable to that country -- try a different event or country.
4. Otherwise, page through `eventItems` to review eligible products.

### 5. Build an Event Digest with Coupons

1. Call `GET /event` to list all current events; page through if needed.
2. For each event, call `GET /event/{event_id}` to retrieve `title`, `description`, `startDate`, `endDate`, and `applicableCoupons`.
3. Filter to events where `applicableCoupons` is non-empty.
4. Compile a summary with event title, date range, coupon details, and `eventAffiliateWebUrl` for linking.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
