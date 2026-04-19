---
description: Multi-month cashflow trend — income, expenses, net, savings rate as a table + quick-read takeaways.
---

You have access to BankBridge MCP tools. Give the user a trend view of their income vs expenses over time.

`$ARGUMENTS` is the number of months to include. Default: 6. Accepts 3–24.

Steps:
1. For each of the last N months, call `get_monthly_cashflow` with `month: "<YYYY-MM>"`.
2. Compute monthly savings rate = (income − expenses) / income. Treat zero income months as N/A.
3. Compute the average income, average expenses, average net over the window.

Output:

```
📈 Cashflow — last N months

| Month    | Income  | Expenses | Net   | Savings rate |
| -------- | ------: | -------: | ----: | -----------: |
| 2026-03  | $ 8,420 | $ 6,315  | +2,105|          25% |
| ...

Averages  $<avg income>  $<avg expenses>  ±<avg net>   <avg rate>%

🔍 Takeaways
- <e.g. "Expenses have crept up 12% over the window.">
- <e.g. "Your most profitable month was 2026-01 (savings rate 31%).">
- <e.g. "Savings rate is trending ↓ over the last 3 months.">
```

Keep the takeaways tight — at most 3. Only flag a trend if it's directionally consistent over at least 3 months. Avoid advice; stick to observations.

Relay any `warnings` above the trend.
