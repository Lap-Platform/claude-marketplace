---
name: openfec
description: "OpenFEC API skill. Use when working with OpenFEC for audit-case, audit-category, audit-primary-category. Covers 99 endpoints."
version: 1.0.0
generator: lapsh
---

# OpenFEC
API version: 1.0

## Auth
ApiKey X-Api-Key in header | ApiKey api_key in query | ApiKey api_key in query

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /v1/audit-case/ -- verify access

## Endpoints

99 endpoints across 25 groups. See references/api-spec.lap for full details.

### audit-case
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/audit-case/ | This endpoint contains Final Audit Reports approved by the Commission since inception. |

### audit-category
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/audit-category/ | This lists the options for the categories and subcategories available in the /audit-search/ endpoint. |

### audit-primary-category
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/audit-primary-category/ | This lists the options for the primary categories available in the /audit-search/ endpoint. |

### calendar-dates
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/calendar-dates/ | Combines the election and reporting dates with Commission meetings, conferences, outreach, Advisory Opinions, rules, litigation dates and other |
| GET | /v1/calendar-dates/export/ | Returns CSV or ICS for downloading directly into calendar applications like Google, Outlook or other applications. |

### candidate
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/candidate/{candidate_id}/ | This endpoint is useful for finding detailed information about a particular candidate. Use the |
| GET | /v1/candidate/{candidate_id}/committees/ | This endpoint is useful for finding detailed information about a particular committee or |
| GET | /v1/candidate/{candidate_id}/committees/history/ | Explore a filer's characteristics over time. This can be particularly useful if the committees change treasurers, designation, or `committee_type`. |
| GET | /v1/candidate/{candidate_id}/committees/history/{cycle}/ | Explore a filer's characteristics over time. This can be particularly useful if the committees change treasurers, designation, or `committee_type`. |
| GET | /v1/candidate/{candidate_id}/filings/ | All official records and reports filed by or delivered to the FEC. |
| GET | /v1/candidate/{candidate_id}/history/ | Find out a candidate's characteristics over time. This is particularly useful if the |
| GET | /v1/candidate/{candidate_id}/history/{cycle}/ | Find out a candidate's characteristics over time. This is particularly useful if the |
| GET | /v1/candidate/{candidate_id}/totals/ | This endpoint provides information about a committee's Form 3, Form 3X, or Form 3P financial reports, |

### candidates
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/candidates/ | Fetch basic information about candidates, and use parameters to filter results to the |
| GET | /v1/candidates/search/ | Fetch basic information about candidates and their principal committees. |
| GET | /v1/candidates/totals/ | Aggregated candidate receipts and disbursements grouped by cycle. |
| GET | /v1/candidates/totals/aggregates/ | Candidate total receipts and disbursements aggregated by `aggregate_by`. |

### committee
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/committee/{committee_id}/ | This endpoint is useful for finding detailed information about a particular committee or |
| GET | /v1/committee/{committee_id}/candidates/ | This endpoint is useful for finding detailed information about a particular candidate. Use the |
| GET | /v1/committee/{committee_id}/candidates/history/ | Find out a candidate's characteristics over time. This is particularly useful if the |
| GET | /v1/committee/{committee_id}/candidates/history/{cycle}/ | Find out a candidate's characteristics over time. This is particularly useful if the |
| GET | /v1/committee/{committee_id}/filings/ | All official records and reports filed by or delivered to the FEC. |
| GET | /v1/committee/{committee_id}/history/ | Explore a filer's characteristics over time. This can be particularly useful if the committees change treasurers, designation, or `committee_type`. |
| GET | /v1/committee/{committee_id}/history/{cycle}/ | Explore a filer's characteristics over time. This can be particularly useful if the committees change treasurers, designation, or `committee_type`. |
| GET | /v1/committee/{committee_id}/reports/ | Each report represents the summary information from Form 3, Form 3X and Form 3P. |
| GET | /v1/committee/{committee_id}/totals/ | This endpoint provides information about a committee's Form 3, Form 3X, or Form 3P financial reports, |

### committees
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/committees/ | Fetch basic information about committees and filers. Use parameters to filter for |

### communication_costs
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/communication_costs/ | 52 U.S.C. 30118 allows "communications by a corporation to its stockholders and executive or administrative personnel and their families or by a labor organization to its members and their families on any subject," including the express advocacy of the election or defeat of any Federal candidate.  The costs of such communications must be reported to the Federal Election Commission under certain circumstances. |
| GET | /v1/communication_costs/aggregates/ | Communication cost aggregated by candidate ID and committee ID. |
| GET | /v1/communication_costs/by_candidate/ | Communication cost aggregated by candidate ID and committee ID. |
| GET | /v1/communication_costs/totals/by_candidate/ | Total communications costs aggregated across committees on supported or opposed candidates by cycle or candidate election year. |

### efile
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/efile/filings/ | Basic information about electronic files coming into the FEC, posted as they are received. |
| GET | /v1/efile/form1/ | Basic information about electronic files coming into the FEC, posted as they are received. |
| GET | /v1/efile/form2/ | Basic information about electronic files coming into the FEC, posted as they are received. |
| GET | /v1/efile/reports/house-senate/ | Key financial data reported periodically by committees as they are reported. This feed includes summary |
| GET | /v1/efile/reports/pac-party/ | Key financial data reported periodically by committees as they are reported. This feed includes summary |
| GET | /v1/efile/reports/presidential/ | Key financial data reported periodically by committees as they are reported. This feed includes summary |

### election-dates
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/election-dates/ | FEC election dates since 1995. |

### electioneering
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/electioneering/ | An electioneering communication is any broadcast, cable or satellite communication that fulfills each of the following conditions: |
| GET | /v1/electioneering/aggregates/ | Electioneering communications costs aggregates |
| GET | /v1/electioneering/by_candidate/ | Electioneering costs aggregated by candidate |
| GET | /v1/electioneering/totals/by_candidate/ | Total electioneering communications spent on candidates by cycle |

### elections
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/elections/ | Look at the top-level financial information for all candidates running for the same |
| GET | /v1/elections/search/ | List elections by cycle, office, state, and district. |
| GET | /v1/elections/summary/ | List elections by cycle, office, state, and district. |

### filings
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/filings/ | All official records and reports filed by or delivered to the FEC. |

### legal
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/legal/docs/{doc_type}/{no} | Search legal documents by type and number |
| GET | /v1/legal/search/ | Search legal documents by document type, or across all document types using keywords, parameter values and ranges. |

### names
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/names/audit_candidates/ | Search for candidates or committees by name. If you're looking for information on a |
| GET | /v1/names/audit_committees/ | Search for candidates or committees by name. If you're looking for information on a |
| GET | /v1/names/candidates/ | Search for candidates or committees by name. If you're looking for information on a |
| GET | /v1/names/committees/ | Search for candidates or committees by name. If you're looking for information on a |

### national_party
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/national_party/schedule_a/ | This endpoint includes national party committee account receipts for presidential nominating conventions, |
| GET | /v1/national_party/schedule_b/ | This endpoint includes national party committee account disbursements for presidential nominating conventions, |
| GET | /v1/national_party/totals/ | This endpoint includes national party committee account total receipts and total disbursements for |

### operations-log
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/operations-log/ | The Operations log contains details of each report loaded into the database. It is primarily |

### presidential
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/presidential/contributions/by_candidate/ | Net receipts per candidate. |
| GET | /v1/presidential/contributions/by_size/ | Contribution receipts by size per candidate. |
| GET | /v1/presidential/contributions/by_state/ | Contribution receipts by state per candidate. |
| GET | /v1/presidential/coverage_end_date/ | Coverage end date per candidate. |
| GET | /v1/presidential/financial_summary/ | Financial summary per candidate. |

### rad-analyst
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/rad-analyst/ | Use this endpoint to look up the RAD Analyst for a committee. |

### reporting-dates
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/reporting-dates/ | FEC election dates since 1995. |

### reports
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/reports/{entity_type}/ | Each report represents the summary information from Form 3, Form 3X and Form 3P. |

### schedules
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/schedules/schedule_a/ | This description is for both ​`/schedules​/schedule_a​/` and ​ `/schedules​/schedule_a​/{sub_id}​/`. |
| GET | /v1/schedules/schedule_a/by_employer/ | This endpoint provides itemized individual contributions received by a committee, aggregated by the contributor’s employer name. If you are interested in our “is_individual” methodology, review the [methodology page](https://www.fec.gov/campaign-finance-data/about-campaign-finance-data/methodology). Unitemized individual contributions are not included. |
| GET | /v1/schedules/schedule_a/by_occupation/ | This endpoint provides itemized individual contributions received by a committee, aggregated by the contributor’s occupation. If you are interested in our “is_individual” methodology, review the [methodology page](https://www.fec.gov/campaign-finance-data/about-campaign-finance-data/methodology). Unitemized individual contributions are not included. |
| GET | /v1/schedules/schedule_a/by_size/ | This endpoint provides individual contributions received by a committee, aggregated by size: |
| GET | /v1/schedules/schedule_a/by_size/by_candidate/ | This endpoint provides itemized individual contributions received by a committee, aggregated by size of contribution and candidate. If you are interested in our “is_individual” methodology, review the [methodology page](https://www.fec.gov/campaign-finance-data/about-campaign-finance-data/methodology). Unitemized individual contributions are not included. |
| GET | /v1/schedules/schedule_a/by_state/ | This endpoint provides itemized individual contributions received by a committee, aggregated by the contributor’s state. If you are interested in our “is_individual” methodology, review the [methodology page](https://www.fec.gov/campaign-finance-data/about-campaign-finance-data/methodology). Unitemized individual contributions are not included. |
| GET | /v1/schedules/schedule_a/by_state/by_candidate/ | This endpoint provides itemized individual contributions received by a committee, aggregated by contributor’s state and candidate. If you are interested in our “is_individual” methodology, review the [methodology page](https://www.fec.gov/campaign-finance-data/about-campaign-finance-data/methodology). Unitemized individual contributions are not included. |
| GET | /v1/schedules/schedule_a/by_state/by_candidate/totals/ | Itemized individual contributions aggregated by contributor’s state, candidate, committee type and cycle. If you are interested in our “is_individual” methodology, review the [methodology page](https://www.fec.gov/campaign-finance-data/about-campaign-finance-data/methodology). Unitemized individual contributions are not included. |
| GET | /v1/schedules/schedule_a/by_state/totals/ | This endpoint provides itemized individual contributions received by a committee, aggregated by contributor’s state, committee type and cycle. If you are interested in our “is_individual” methodology, review the [methodology page](https://www.fec.gov/campaign-finance-data/about-campaign-finance-data/methodology). Unitemized individual contributions are not included. |
| GET | /v1/schedules/schedule_a/by_zip/ | This endpoint provides itemized individual contributions received by a committee, aggregated by the contributor’s ZIP code. If you are interested in our “is_individual” methodology, review the [methodology page](https://www.fec.gov/campaign-finance-data/about-campaign-finance-data/methodology). Unitemized individual contributions are not included. |
| GET | /v1/schedules/schedule_a/efile/ | Efiling endpoints provide real-time campaign finance data received from electronic filers. Efiling endpoints only contain the most recent four months of data and don't contain the processed and coded data that you can find on other endpoints. |
| GET | /v1/schedules/schedule_a/{sub_id}/ | This description is for both ​`/schedules​/schedule_a​/` and ​ `/schedules​/schedule_a​/{sub_id}​/`. |
| GET | /v1/schedules/schedule_a_form5/ | FEC FORM 5 Receipts |
| GET | /v1/schedules/schedule_b/ | Schedule B filings describe itemized disbursements. This data |
| GET | /v1/schedules/schedule_b/by_purpose/ | Schedule B disbursements aggregated by disbursement purpose category. To avoid double counting, |
| GET | /v1/schedules/schedule_b/by_recipient/ | Schedule B disbursements aggregated by recipient name. To avoid double counting, |
| GET | /v1/schedules/schedule_b/by_recipient_id/ | Schedule B disbursements aggregated by recipient committee ID, if applicable. |
| GET | /v1/schedules/schedule_b/efile/ | Efiling endpoints provide real-time campaign finance data received from electronic filers. Efiling endpoints only contain the most recent four months of data and don't contain the processed and coded data that you can find on other endpoints. |
| GET | /v1/schedules/schedule_b/{sub_id}/ | Schedule B filings describe itemized disbursements. This data |
| GET | /v1/schedules/schedule_c/ | Schedule C shows all loans, endorsements and loan guarantees a committee |
| GET | /v1/schedules/schedule_c/{sub_id}/ | Schedule C shows all loans, endorsements and loan guarantees a committee |
| GET | /v1/schedules/schedule_d/ | Schedule D, it shows debts and obligations owed to or by the committee that are |
| GET | /v1/schedules/schedule_d/{sub_id}/ | Schedule D, it shows debts and obligations owed to or by the committee that are |
| GET | /v1/schedules/schedule_e/ | Schedule E covers the line item expenditures for independent expenditures. For example, if a super PAC |
| GET | /v1/schedules/schedule_e/by_candidate/ | Schedule E receipts aggregated by recipient candidate. To avoid double |
| GET | /v1/schedules/schedule_e/efile/ | Efiling endpoints provide real-time campaign finance data received from electronic filers. Efiling endpoints only contain the most recent four months of data and don't contain the processed and coded data that you can find on other endpoints. |
| GET | /v1/schedules/schedule_e/totals/by_candidate/ | Total independent expenditure on supported or opposed candidates by cycle or candidate election year. |
| GET | /v1/schedules/schedule_f/ | Schedule F, it shows all special expenditures a national or state party committee |
| GET | /v1/schedules/schedule_f/{sub_id}/ | Schedule F, it shows all special expenditures a national or state party committee |
| GET | /v1/schedules/schedule_h4/ | Schedule H4 filings describe disbursements for allocated federal/nonfederal activity. This data |
| GET | /v1/schedules/schedule_h4/efile/ | Efiling endpoints provide real-time campaign finance data received from electronic filers. Efiling endpoints only contain the most recent four months of data and don't contain the processed and coded data that you can find on other endpoints. |

### state-election-office
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/state-election-office/ | State laws and procedures govern elections for state or local offices as well as |

### totals
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/totals/by_entity/ | Provides cumulative receipt totals by entity type, over a two year cycle. Totals are adjusted to avoid double counting. |
| GET | /v1/totals/inaugural_committees/by_contributor/ | This endpoint provides information about an inaugural committee's Form 13 report of donations accepted. |
| GET | /v1/totals/{entity_type}/ | This endpoint provides information about a committee's Form 3, Form 3X, or Form 3P financial reports, |

## Enhanced Skill Content
## Question Mapping

- "Who is candidate P00009423?" -> GET /v1/candidate/{candidate_id}/
- "What committees support a specific candidate?" -> GET /v1/candidate/{candidate_id}/committees/
- "How much money has a candidate raised this cycle?" -> GET /v1/candidate/{candidate_id}/totals/
- "Search for all Senate candidates in Texas" -> GET /v1/candidates/search/?office=S&state=TX
- "What are the top donors to a committee by employer?" -> GET /v1/schedules/schedule_a/by_employer/
- "Show me independent expenditures against a candidate" -> GET /v1/schedules/schedule_e/by_candidate/
- "When is the next FEC filing deadline?" -> GET /v1/reporting-dates/
- "What elections are happening in 2026?" -> GET /v1/elections/search/?cycle=2026
- "Find all electioneering communications by a committee" -> GET /v1/electioneering/?committee_id={id}
- "How much did a presidential candidate raise by state?" -> GET /v1/presidential/contributions/by_state/
- "Look up an advisory opinion by number" -> GET /v1/legal/docs/{doc_type}/{no}
- "Which RAD analyst is assigned to a committee?" -> GET /v1/rad-analyst/?committee_id={id}
- "Show me a committee's disbursements to a specific recipient" -> GET /v1/schedules/schedule_b/by_recipient/
- "What upcoming FEC calendar events are there?" -> GET /v1/calendar-dates/?min_start_date={today}
- "Get the state election office contact info for Ohio" -> GET /v1/state-election-office/?state=OH

## Response Tips

- **Paginated lists** (candidates, committees, schedules): All return `page`, `per_page`, `pages`, and `count` at the top level; iterate with `page` param, default `per_page` is 20, max typically 100.
- **Schedule A/B/E cursor pagination**: These use `last_index`, `last_contribution_receipt_date`, or `last_disbursement_date` instead of page numbers; pass the last record's values to fetch the next batch.
- **Candidate/committee lookups**: Single-entity responses nest the record inside a `results` array even for one item; always index `results[0]`.
- **Financial totals**: Amounts are in raw cents or dollars depending on endpoint; compare `receipts` vs `disbursements` fields, not `total` fields which may aggregate differently.
- **Legal search**: Returns `total_all`, `total_murs`, `total_adrs`, `total_advisory_opinions` alongside `docs`; use `from_hit` + `hits_returned` for offset pagination rather than `page`.
- **Error responses**: 400s return `message` with human-readable validation errors; 404s on path-param lookups mean the ID does not exist in FEC data.
- **History endpoints**: Return one record per cycle; the most recent cycle is not always the current one if the candidate/committee was inactive.

## Anomaly Flags

- **Rate limiting**: OpenFEC enforces hourly rate limits per API key. Surface warnings when response headers indicate approaching the cap (typically 1,000 requests/hour for demo keys, higher for registered keys). Recommend the user apply for a higher-tier key if they hit limits during bulk operations.
- **Stale coverage dates**: Presidential and committee financial summaries have a `coverage_end_date` that may lag weeks behind the current date. Flag when the latest coverage end date is more than 60 days old, as the data may not reflect recent filings.
- **Amended filings**: Many endpoints return amended and superseded filings by default. If `is_amended: true` appears in results without `most_recent: true` filtering, warn that the user may be looking at outdated data.
- **Empty results for valid IDs**: A candidate or committee ID that returns zero results for totals/history likely means the entity has not yet filed for the requested cycle. Surface this rather than silently returning nothing.
- **Two-year transaction period mismatches**: Schedule A/B queries default to the current two-year period. If the user asks about a past election cycle but omits `two_year_transaction_period`, flag that results will only cover the default period.
- **Null sort behavior**: Endpoints with `sort_hide_null` and `sort_null_only` can silently filter out records. Flag when these are set, as they reduce result counts in non-obvious ways.

## Playbook

### 1. Research a Candidate's Full Financial Profile

1. Search for the candidate: `GET /v1/candidates/search/?q={name}`
2. Note the `candidate_id` from results (format: `P00000000`, `H0XX00000`, or `S0XX00000`)
3. Get candidate details and history: `GET /v1/candidate/{candidate_id}/history/`
4. Pull financial totals: `GET /v1/candidate/{candidate_id}/totals/?cycle={cycle}`
5. List their committees: `GET /v1/candidate/{candidate_id}/committees/`
6. For each committee, pull receipts: `GET /v1/committee/{committee_id}/reports/`
7. Summarize: compare `receipts`, `disbursements`, and `cash_on_hand_end_period`

### 2. Trace Donations to a Committee

1. Look up the committee: `GET /v1/committees/?q={name}`
2. Get aggregate receipts by size: `GET /v1/schedules/schedule_a/by_size/?committee_id={id}&cycle={cycle}`
3. Get top employers: `GET /v1/schedules/schedule_a/by_employer/?committee_id={id}&cycle={cycle}`
4. Get geographic breakdown: `GET /v1/schedules/schedule_a/by_state/?committee_id={id}&cycle={cycle}`
5. For individual transaction detail, paginate through: `GET /v1/schedules/schedule_a/?committee_id={id}&two_year_transaction_period={period}` using `last_index` cursor

### 3. Track Independent Expenditures in a Race

1. Identify the election: `GET /v1/elections/search/?state={st}&office={office}&cycle={cycle}`
2. Get IE totals by candidate: `GET /v1/schedules/schedule_e/totals/by_candidate/?candidate_id={id}&cycle={cycle}`
3. See which committees are spending: `GET /v1/schedules/schedule_e/by_candidate/?candidate_id={id}&cycle={cycle}`
4. For real-time e-filed IEs: `GET /v1/schedules/schedule_e/efile/?candidate_id={id}&most_recent=true`
5. Cross-reference with electioneering communications: `GET /v1/electioneering/by_candidate/?candidate_id={id}&cycle={cycle}`

### 4. Monitor Upcoming Deadlines and Filings

1. Check reporting deadlines: `GET /v1/reporting-dates/?min_due_date={today}&sort=due_date`
2. Pull FEC calendar events: `GET /v1/calendar-dates/?min_start_date={today}&sort=start_date`
3. Check election dates: `GET /v1/election-dates/?min_election_date={today}&sort=election_date`
4. For a specific committee, see recent filings: `GET /v1/committee/{committee_id}/filings/?most_recent=true&sort=-receipt_date`
5. Check e-filed filings for the latest submissions: `GET /v1/efile/filings/?committee_id={id}&sort=-receipt_date`

### 5. Audit and Compliance Lookup

1. Search audit cases: `GET /v1/audit-case/?candidate_id={id}` or `?committee_id={id}`
2. Get audit categories for context: `GET /v1/audit-category/`
3. Get primary categories: `GET /v1/audit-primary-category/`
4. Search legal documents (MURs, advisory opinions): `GET /v1/legal/search/?q={query}&type=murs`
5. Retrieve a specific legal document: `GET /v1/legal/docs/{doc_type}/{no}`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
