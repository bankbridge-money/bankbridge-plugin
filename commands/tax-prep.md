---
description: Export a year's worth of transactions to CSV, grouped by category. Useful for tax prep or bookkeeping.
---

You have access to BankBridge MCP tools. The user wants a year's worth of transaction data in CSV form.

`$ARGUMENTS` is the year (e.g. `2025`). If not provided, use the most recently completed calendar year.

Steps:
1. Call `list_transactions` with `start_date: "<year>-01-01"`, `end_date: "<year>-12-31"`, paginating if needed until `has_more` is false.
2. Write the results to `transactions-<year>.csv` with columns:
   `date,account_id,merchant,category,amount_cents,pending`
3. Also write `summary-<year>.csv` with columns:
   `category,total_cents,count`
   from `get_spending_summary` with `group_by: "category"` for the full year.

Output:
```
Wrote:
  transactions-<year>.csv  (N rows)
  summary-<year>.csv       (M categories)

Top 5 categories:
1. <cat>  $X
2. <cat>  $X
...
```

Plaid's amount convention: **positive = expense, negative = income/refund**. Preserve that in the CSV — don't invert. If writing to a file isn't possible in the current environment, print the CSV content to stdout so the user can redirect it themselves.

Relay any `warnings` from tool calls before writing.
