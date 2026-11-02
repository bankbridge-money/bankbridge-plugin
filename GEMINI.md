# BankBridge

BankBridge is a remote MCP server (`https://bankbridge.money/api/mcp`) that gives you read-only access to the user's connected US bank, credit card and brokerage accounts. Every tool call fetches live data from the bank. Nothing can move money, pay a bill or place a trade.

## Setup

- The first time, the user runs `/mcp auth bankbridge` inside Gemini CLI and signs in at bankbridge.money in the browser. No API key is needed.
- If a result says `setup_required` or has a NO_CONNECTIONS notice, show the user the link in the result. It finishes the subscription or connects a bank. Pricing is $5 a month per connected bank, or $50 a year.
- Full setup guide: https://bankbridge.money/docs/gemini-cli

## Which tool for which question

| Question | Tool |
|---|---|
| Balances, account list, credit utilization | `list_accounts`, `get_account` |
| "How much did I spend on X?" | `get_spending_summary` (group by category, merchant, month or week) |
| Find a specific charge or merchant | `search_transactions`, then `get_merchant_history` |
| Subscriptions and bills | `get_recurring_charges` |
| "Am I making more than I spend?" | `get_monthly_cashflow` (one call per month, `month: "YYYY-MM"`) |
| Raw transactions with filters | `list_transactions` (date range, amount, category, account; paginate with `offset`) |
| Category names to filter by | `list_categories` |
| Portfolio, gains, dividends | `list_holdings`, `list_investment_transactions` |
| Add another bank | `connect_bank` (returns a link for the user) |

## Reading the data correctly

- Amounts are dollars. Positive = money leaving the account (spending). Negative = money coming in (income, refunds).
- Credit card payments from checking are not new spending: the purchases already appear on the card. Leave them out of spending totals.
- Transfers between the user's own accounts are not spending. Transfers to other people (rent to a landlord, for example) are.
- Account ids can change when a bank is reconnected. Start a session with `list_accounts` instead of reusing old ids.
- Every result has a `warnings` array. If it is not empty, tell the user (for example, a bank that needs reconnecting, with its reconnect link) and say the totals cover only the banks that answered.
