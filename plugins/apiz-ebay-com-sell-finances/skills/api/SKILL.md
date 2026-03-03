---
name: finances-api
description: "Finances API skill. Use when working with Finances for payout, payout_summary, seller_funds_summary. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# Finances API
API version: v1.18.0

## Auth
OAuth2

## Base URL
https://apiz.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /payout -- verify access

## Endpoints

8 endpoints across 7 groups. See references/api-spec.lap for full details.

### payout
| Method | Path | Description |
|--------|------|-------------|
| GET | /payout/{payout_Id} | <div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> Due to EU &amp; UK Payments regulatory requirements, an additional security verification via Digital Signatures is required for certain API calls that are made on behalf of EU/UK sellers, including all <b>Finances API</b> methods. Please refer to <a href="/develop/guides/digital-signatures-for-apis " target="_blank">Digital Signatures for APIs</a> to learn more on the impacted APIs and the process to create signatures to be included in the HTTP payload.</p></div><br><span class="tablenote"><b>Note:</b>  The <b>Finances API</b> does not support <a href="https://www.ebay.com/sellercenter/ebay-for-business/multi-user-account-access" target="_blank">Team Access</a>. Financial information, such as payouts or transactions, is only returned for the user that makes the call. You cannot use any of the methods in this API to return financial information for another user.</span><br>This method retrieves details on a specific seller payout. The unique identifier of the payout is passed in as a path parameter at the end of the call URI. <br><br>The <b>getPayouts</b> method can be used to retrieve the unique identifier of a payout, or the user can check Seller Hub.<br><br>For split-payout cases, which are <b>only</b> available to sellers in mainland China, this method will return the <b>payoutPercentage</b> for the specified payout. This value indicates the current payout percentage allocated to a payment instrument. This method will also return the <b>convertedToCurrency</b> and <b>convertedToValue</b> response fields in CNY value. <br><br><span class="tablenote"><b>Note:</b> In split-payout cases, this method will only return details on an individual payout, also known as a true(actual) payoutid. If a user inputs a <b>payoutReference</b> id as a path parameter, the call will fail and the <b>404 not found</b> status code will be returned.<br>For more information on split payouts, see <a href="/api-docs/split-payout/playbook.html" target="_blank">Mainland China Split Payout Playbook</a>.</span> |
| GET | /payout | <div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> Due to EU &amp; UK Payments regulatory requirements, an additional security verification via Digital Signatures is required for certain API calls that are made on behalf of EU/UK sellers, including all <b>Finances API</b> methods. Please refer to <a href="/develop/guides/digital-signatures-for-apis " target="_blank">Digital Signatures for APIs</a> to learn more on the impacted APIs and the process to create signatures to be included in the HTTP payload.</p></div><br><span class="tablenote"><b>Note:</b>  The <b>Finances API</b> does not support <a href="https://www.ebay.com/sellercenter/ebay-for-business/multi-user-account-access" target="_blank">Team Access</a>. Financial information, such as payouts or transactions, is only returned for the user that makes the call. You cannot use any of the methods in this API to return financial information for another user.</span><br>This method is used to retrieve the details of one or more seller payouts. By using the <b>filter</b> query parameter, users can retrieve payouts processed within a specific date range, and/or they can retrieve payouts in a specific state.<br><br>There are also pagination and sort query parameters that allow users to control the payouts that are returned in the response.<br><br>If no payouts match the input criteria, an empty payload is returned.<br><br>For split-payout cases, which are <b>only</b> available to sellers in mainland China, this method will return the <b>payoutPercentage</b> for the specified payout. This value indicates the current payout percentage allocated to a payout instrument. This method will also return the <b>convertedToCurrency</b> and <b>convertedTo</b> response fields set to CNY value and the <b>payoutReference</b>, the unique identifier reference (not true payout). <br><br>By using the <b>filter</b> query parameter, users can retrieve the two true(actual) payouts associated with a <b>payoutReference</b>.<br><br><span class="tablenote"><b>Note:</b> For more information on split payouts, see <a href="/api-docs/split-payout/playbook.html" target="_blank">Mainland China Split Payout Playbook</a>.</span> <br><br><b>Note:</b> Only payouts less than 5 years in the past can be retrieved. |

### payout_summary
| Method | Path | Description |
|--------|------|-------------|
| GET | /payout_summary | <div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> Due to EU &amp; UK Payments regulatory requirements, an additional security verification via Digital Signatures is required for certain API calls that are made on behalf of EU/UK sellers, including all <b>Finances API</b> methods. Please refer to <a href="/develop/guides/digital-signatures-for-apis " target="_blank">Digital Signatures for APIs</a> to learn more on the impacted APIs and the process to create signatures to be included in the HTTP payload.</p></div><br><span class="tablenote"><b>Note:</b>  The <b>Finances API</b> does not support <a href="https://www.ebay.com/sellercenter/ebay-for-business/multi-user-account-access" target="_blank">Team Access</a>. Financial information, such as payouts or transactions, is only returned for the user that makes the call. You cannot use any of the methods in this API to return financial information for another user.</span><br>This method is used to retrieve cumulative values for payouts in a particular state, or all states. The metadata in the response includes total payouts, the total number of monetary transactions (sales, refunds, credits) associated with those payouts, and the total dollar value of all payouts.<br><br>If the <b>filter</b> query parameter is used to filter by payout status, only one payout status value may be used. If the <b>filter</b> query parameter is not used to filter by a specific payout status, cumulative values for payouts in all states are returned.<br><br>The user can also use the <b>filter</b> query parameter to specify a date range, and then only payouts that were processed within that date range are considered. <br><br><b>Note:</b> getPayoutSummary will only return data on payouts that occurred less than five years in the past. |

### seller_funds_summary
| Method | Path | Description |
|--------|------|-------------|
| GET | /seller_funds_summary | <div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> Due to EU &amp; UK Payments regulatory requirements, an additional security verification via Digital Signatures is required for certain API calls that are made on behalf of EU/UK sellers, including all <b>Finances API</b> methods. Please refer to <a href="/develop/guides/digital-signatures-for-apis " target="_blank">Digital Signatures for APIs</a> to learn more on the impacted APIs and the process to create signatures to be included in the HTTP payload.</p></div><br><span class="tablenote"><b>Note:</b>  The <b>Finances API</b> does not support <a href="https://www.ebay.com/sellercenter/ebay-for-business/multi-user-account-access" target="_blank">Team Access</a>. Financial information, such as payouts or transactions, is only returned for the user that makes the call. You cannot use any of the methods in this API to return financial information for another user.</span><br>This method retrieves all pending funds that have not yet been distibuted through a seller payout.<br><br>There are no input parameters for this method. The response payload includes available funds, funds being processed, funds on hold, and also an aggregate count of all three of these categories.<br><br>If there are no funds that are pending, on hold, or being processed for the seller's account, no response payload is returned, and an http status code of <code>204 - No Content</code> is returned instead. |

### transaction
| Method | Path | Description |
|--------|------|-------------|
| GET | /transaction | <div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> Due to EU &amp; UK Payments regulatory requirements, an additional security verification via Digital Signatures is required for certain API calls that are made on behalf of EU/UK sellers, including all <b>Finances API</b> methods. Please refer to <a href="/develop/guides/digital-signatures-for-apis " target="_blank">Digital Signatures for APIs</a> to learn more on the impacted APIs and the process to create signatures to be included in the HTTP payload.</p></div><br><span class="tablenote"><b>Note:</b>  The <b>Finances API</b> does not support <a href="https://www.ebay.com/sellercenter/ebay-for-business/multi-user-account-access" target="_blank">Team Access</a>. Financial information, such as payouts or transactions, is only returned for the user that makes the call. You cannot use any of the methods in this API to return financial information for another user.</span><br>The <b>getTransactions</b> method allows a seller to retrieve information about one or more of their monetary transactions.<br><br><span class="tablenote"><b>Note:</b> For a complete list of transaction types, refer to <a href="/api-docs/sell/finances/types/pay:TransactionTypeEnum " target="_blank ">TransactionTypeEnum</a>.</span><br>Numerous input filters are available which can be used individually or combined to refine the data that are returned. For example:<ul><li><code>SALE</code> transactions for August 15, 2022;</li><li><code>RETURN</code> transactions for the month of January, 2021;</li><li>Transactions currently in a <code>transactionStatus</code> equal to <code>FUNDS_ON_HOLD</code>.</li></ul>Refer to the <a href="#uri.filter ">filter</a> field for additional information about each filter and its use.<br><br>Pagination and sort query parameters are also provided that allow users to further control how monetary transactions are displayed in the response.<br><br>If no monetary transactions match the input criteria, an http status code of <em>204 No Content</em> is returned with no response payload. <br><br><b>Note:</b> Only monetary transactions that have occurred within the last five years can be retrieved. |

### transaction_summary
| Method | Path | Description |
|--------|------|-------------|
| GET | /transaction_summary | <div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> Due to EU &amp; UK Payments regulatory requirements, an additional security verification via Digital Signatures is required for certain API calls that are made on behalf of EU/UK sellers, including all <b>Finances API</b> methods. Please refer to <a href="/develop/guides/digital-signatures-for-apis " target="_blank">Digital Signatures for APIs</a> to learn more on the impacted APIs and the process to create signatures to be included in the HTTP payload.</p></div><<br><span class="tablenote"><b>Note:</b>  The <b>Finances API</b> does not support <a href="https://www.ebay.com/sellercenter/ebay-for-business/multi-user-account-access" target="_blank">Team Access</a>. Financial information, such as payouts or transactions, is only returned for the user that makes the call. You cannot use any of the methods in this API to return financial information for another user.</span><br>The <b>getTransactionSummary</b> method retrieves cumulative information for monetary transactions. If applicable, the number of payments with a <code>transactionStatus</code> equal to <code>FUNDS_ON_HOLD</code> and the total monetary amount of these on-hold payments are also returned.<br><br><span class="tablenote"><b>Note:</b> For a complete list of transaction types, refer to <a href="/api-docs/sell/finances/types/pay:TransactionTypeEnum " target="_blank ">TransactionTypeEnum</a>.</span><br>Refer to the <a href="#uri.filter ">filter</a> field for additional information about each filter and its use.<br><br><span class="tablenote"><b>Note:</b> Unless a <code>transactionType</code> filter is used to retrieve a specific type of transaction (e.g., <code>SALE</code>, <code>REFUND</code>, etc.,) the <a href="#response.creditCount">creditCount</a> and <a href="#response.creditAmount">creditAmount</a> response fields both include <i>order sales</i> and <i>seller credits</i> information. That is, the <b>count</b> and <b>value</b> fields do not distinguish between these two types monetary transactions.</span> <br><br><b>Note:</b> getTransactionSummary will only return data on transactions that occurred less than five years in the past. |

### transfer
| Method | Path | Description |
|--------|------|-------------|
| GET | /transfer/{transfer_Id} | <div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> Due to EU &amp; UK Payments regulatory requirements, an additional security verification via Digital Signatures is required for certain API calls that are made on behalf of EU/UK sellers, including all <b>Finances API</b> methods. Please refer to <a href="/develop/guides/digital-signatures-for-apis " target="_blank">Digital Signatures for APIs</a> to learn more on the impacted APIs and the process to create signatures to be included in the HTTP payload.</p></div><br><span class="tablenote"><b>Note:</b>  The <b>Finances API</b> does not support <a href="https://www.ebay.com/sellercenter/ebay-for-business/multi-user-account-access" target="_blank">Team Access</a>. Financial information, such as payouts or transactions, is only returned for the user that makes the call. You cannot use any of the methods in this API to return financial information for another user.</span><br>This method retrieves detailed information regarding a <code>TRANSFER</code> transaction type. A <code>TRANSFER</code> is a  monetary transaction type that involves a seller transferring money to eBay for reimbursement of one or more charges. For example, when a seller reimburses eBay for a buyer refund.<br><br>If an ID is passed into the URI that is an identifier for another transaction type, this call will return an http status code of <code>404 Not found</code>. |

### billing_activity
| Method | Path | Description |
|--------|------|-------------|
| GET | /billing_activity | <div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> Due to EU &amp; UK Payments regulatory requirements, an additional security verification via Digital Signatures is required for certain API calls that are made on behalf of EU/UK sellers, including all <b>Finances API</b> methods. Please refer to <a href="/develop/guides/digital-signatures-for-apis " target="_blank">Digital Signatures for APIs</a> to learn more on the impacted APIs and the process to create signatures to be included in the HTTP payload.</p></div><br><span class="tablenote"><b>Note:</b>  The <b>Finances API</b> does not support <a href="https://www.ebay.com/sellercenter/ebay-for-business/multi-user-account-access" target="_blank">Team Access</a>. Financial information, such as payouts or transactions, is only returned for the user that makes the call. You cannot use any of the methods in this API to return financial information for another user.</span><br>This method retrieves filtered billing activities of the seller. Returned results are filtered through query parameters such as date range, activity ID, listing ID, or order ID. Sorting and pagination features help organize and navigate returned activities efficiently. |

## Enhanced Skill Content
## Question Mapping

- "What are my recent payouts?" -> GET /payout
- "Show me details for a specific payout" -> GET /payout/{payout_Id}
- "What is the status of my last payout?" -> GET /payout/{payout_Id}
- "How much have I been paid out this month?" -> GET /payout_summary
- "How many transactions were included in my payouts?" -> GET /payout_summary
- "What funds do I have available for payout?" -> GET /seller_funds_summary
- "How much money is currently on hold?" -> GET /seller_funds_summary
- "Show me my recent sales transactions" -> GET /transaction
- "How many refunds have I issued this month?" -> GET /transaction_summary
- "What are my total dispute amounts?" -> GET /transaction_summary
- "Break down my fees, refunds, and adjustments" -> GET /transaction_summary
- "Show details of a specific fund transfer" -> GET /transfer/{transfer_Id}
- "What are my billing charges from eBay?" -> GET /billing_activity
- "List payouts sorted by date for the US marketplace" -> GET /payout
- "What shipping label costs have I incurred?" -> GET /transaction_summary

## Response Tips

- **Payout/Transaction lists**: Paginated via `limit`, `offset`, `next`, `prev`, and `total` -- follow `next` URL to page forward; a 204 means no results exist (not an error).
- **Payout details**: The `amount` vs `totalAmount` distinction matters -- `amount` is the net payout, `totalAmount` is pre-fee; check `totalFee` and `totalFeeDetails` for fee breakdown.
- **Summaries (payout/transaction)**: Return aggregate counts and amounts, not individual records -- use `filter` to scope by date range or status before calling.
- **Money fields**: All amounts use a nested structure with `currency`/`value` plus optional `convertedFrom*` and `exchangeRate` fields for cross-currency sellers; always read `currency` to know the denomination.
- **Transfer details**: Deeply nested -- `transferDetail.balanceAdjustment.adjustmentAmount` and `transferDetail.charges[]` require drilling into sub-objects.
- **Billing activity**: Uses `count` (items in current page) and `total` (all matching records) -- do not confuse the two when calculating remaining pages.

## Anomaly Flags

- **Payout status not `SUCCEEDED`**: Surface any payout where `payoutStatus` is `FAILED`, `REVERSED`, or `BLOCKED` -- these need seller attention.
- **Funds on hold increasing**: If `seller_funds_summary.fundsOnHold` is a significant portion of `totalFunds`, warn the seller about potential account restrictions.
- **High dispute amounts**: When `transaction_summary.disputeCount` is non-zero or `disputeAmount` is rising, flag for seller review.
- **Currency conversion active**: When `exchangeRate` is present and non-trivial, alert that cross-currency conversion fees may apply.
- **204 No Content responses**: These indicate zero results for the query period -- surface this clearly rather than showing an empty state silently.
- **Loan repayment entries**: Non-zero `loanRepaymentAmount` or `loanRepaymentCount` in transaction summaries should be called out since these reduce available funds.
- **Pagination truncation**: If `total` significantly exceeds `limit`, warn that results are partial and offer to fetch remaining pages.

## Playbook

### 1. Daily Payout Reconciliation

1. Call `GET /seller_funds_summary` with the marketplace header to get current available, on-hold, and processing funds.
2. Call `GET /payout?filter=payoutDate:[{today}..{today}]&sort=payoutDate` to list today's payouts.
3. For each payout, call `GET /payout/{payout_Id}` to verify the `payoutStatus` is `SUCCEEDED` and review `totalFee`.
4. Call `GET /payout_summary?filter=payoutDate:[{today}..{today}]` to cross-check aggregate totals against individual payouts.
5. Flag any payout where `payoutStatus` is not `SUCCEEDED` for follow-up.

### 2. Monthly Financial Summary

1. Call `GET /transaction_summary?filter=transactionDate:[{monthStart}..{monthEnd}]` to get a full breakdown of sales, refunds, disputes, fees, and adjustments.
2. Call `GET /payout_summary?filter=payoutDate:[{monthStart}..{monthEnd}]` to get total payouts and transaction counts.
3. Compare `creditAmount` (sales) against `refundAmount` and `disputeAmount` to calculate net revenue.
4. Review `nonSaleChargeAmount` and `shippingLabelAmount` for operational costs.
5. Call `GET /billing_activity?filter=transactionDate:[{monthStart}..{monthEnd}]` for eBay-specific billing charges.

### 3. Investigating a Missing Payout

1. Call `GET /payout?filter=payoutStatus:{RETRYABLE_FAILURE|TERMINAL_FAILURE}&sort=-payoutDate` to find failed payouts.
2. For each failed payout, call `GET /payout/{payout_Id}` and read `payoutStatusDescription` and `payoutMemo` for the failure reason.
3. Check `payoutInstrument` to confirm bank account details (last four digits, instrument type).
4. Check `lastAttemptedPayoutDate` versus `payoutDate` to see if retries occurred.
5. Call `GET /seller_funds_summary` to verify the funds are still available and not stuck on hold.

### 4. Dispute and Refund Tracking

1. Call `GET /transaction_summary?filter=transactionDate:[{start}..{end}]` and examine `disputeCount`, `disputeAmount`, `refundCount`, and `refundAmount`.
2. If counts are elevated, call `GET /transaction?filter=transactionType:{DISPUTE}&sort=-transactionDate` to list individual dispute transactions.
3. Page through results using `next` until all disputes are retrieved.
4. Cross-reference dispute transactions with order IDs for resolution tracking.

### 5. Transfer and Balance Adjustment Review

1. Call `GET /transaction?filter=transactionType:{TRANSFER}&sort=-transactionDate` to find recent transfers.
2. For each transfer of interest, call `GET /transfer/{transfer_Id}` to get full details.
3. Review `fundingSource` to understand the transfer origin (credit card charge, bank debit, etc.).
4. Check `transferDetail.balanceAdjustment` for any balance corrections applied.
5. Sum `transferDetail.charges[]` via `totalChargeNetAmount` to understand associated fees.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
