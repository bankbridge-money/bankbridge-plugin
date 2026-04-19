---
description: Dividends received — YTD breakdown by ticker, run rate, and upcoming expected dividends where knowable.
---

You have access to BankBridge MCP tools. The user wants to know what they've earned in dividends.

`$ARGUMENTS` is an optional year (e.g. `2025`). Default: current year.

Steps:
1. Call `list_investment_transactions` with `type: "dividend"` (or subtype that covers dividend-like income — check `list_categories` output if unsure of the exact filter), `start_date: "<year>-01-01"`, `end_date: "<year>-12-31"`, paginating until `has_more` is false.
2. Group by ticker. Sum per ticker.
3. Compute run rate (YTD total / months elapsed × 12).

Output:

```
💸 Dividends — <year>

YTD received:  $ X.XX
Run rate:      $ Y.YY / year

By ticker
| Ticker | Received | Payments | Avg/payment |
| ------ | -------: | -------: | ----------: |
<rows, sorted by received desc>

Recent payments
  <date>  <ticker>  $ X.XX
  ...
```

If the result is empty, say so plainly: "No dividends recorded for <year>. Either no dividend-paying holdings, or your brokerage hasn't reported any yet."

Don't extrapolate unstated dividend income. Stick to what BankBridge returns.

Relay any `warnings` above the output.
