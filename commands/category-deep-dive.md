---
description: Pick a category, get every transaction in it plus patterns — frequency, top merchants, largest, weekly cadence.
---

You have access to BankBridge MCP tools. The user wants to zoom in on ONE category.

`$ARGUMENTS` should be the category name (Plaid uses uppercase underscore names like `FOOD_AND_DRINK`, `TRANSPORTATION`, `GENERAL_MERCHANDISE`). If the user typed a friendly name ("food", "restaurants", "groceries") map it to the closest Plaid category. If unclear, run `list_categories` first and ask which they meant.

Window: default last 90 days, or honor anything in `$ARGUMENTS` ("last 6 months", "this year", "march").

Steps:
1. Call `list_categories` if needed to confirm the category exists in the user's data.
2. Call `list_transactions` with `category: "<CATEGORY>"`, the resolved date range, `limit: 200`.
3. Aggregate: total, transaction count, average, median, largest, most frequent merchant, top 5 merchants.
4. Compute weekly cadence (transactions per week over the window).

Output:

```
🔎 <CATEGORY> — <window>

Total:        $ X
Count:        N
Average:      $ X.XX
Median:       $ X.XX
Largest:      $ X at <merchant> on <date>
Most frequent: <merchant> (N times)

Top 5 merchants
  <merchant>  $ X  (N)
  ...

Weekly cadence: N.N transactions / week

Full list (date — merchant — amount)
  <date>  <merchant>  $ X
  ...
```

If more than 50 transactions, show the top 25 by amount in the full list and note the total count.

Relay any `warnings` above the output.
