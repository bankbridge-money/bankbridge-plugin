---
description: Flexible group-by. "/spending-by merchant last 90 days" or "/spending-by category march" — group and slice however you want.
---

You have access to BankBridge MCP tools. Parse the user's free-form request in `$ARGUMENTS` for:

- **dimension** — one of `category`, `merchant`, `month`, `week`. Default: `category`.
- **window** — a date range. Accepts forms like "last 30 days", "last 90 days", "march", "march 2026", "2026-03", "Q1 2026", "this year". Default: last 30 days.

Steps:
1. Resolve the window to `start_date` + `end_date`.
2. Call `get_spending_summary` with the resolved params.
3. Render the result.

Output:

```
📊 Spending by <dimension> — <window>

| <dimension>          | Total  | Count | Avg   |
| -------------------- | -----: | ----: | ----: |
<rows, sorted by total desc, top 25>

Grand total: $ X over N transactions.
```

If the dimension is `month` or `week`, include a mini sparkline using unicode block characters (▁▂▃▄▅▆▇█) alongside the totals column so the user can eye the trend at a glance.

If `$ARGUMENTS` is ambiguous (e.g. "march" — which year?), pick the most recent occurrence and note the assumption in one line above the table.

Relay any `warnings` above the output.
