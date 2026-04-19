---
description: Last 7 days at a glance — total spend, biggest charges, and anything new or unusual.
---

You have access to BankBridge MCP tools. The user wants a weekly pulse.

`$ARGUMENTS` optionally specifies a reference week. Default: the last 7 calendar days ending today.

Steps:
1. Call `list_transactions` with `start_date: "<7 days ago>"`, `end_date: "<today>"`, `limit: 100`.
2. Compute: total out (positive amounts), total in (negative amounts), net, largest single expense.
3. Group by `category` via `get_spending_summary` with the same date range.
4. Flag any single transaction > 2× this week's average (loose "surprise" heuristic).

Output:

```
📆 Week of <start> – <end>

Total spent:   $ X
Total in:      $ Y
Net:          ±$ Z

Biggest single charge: <merchant> — $ X (<date>)

By category
  <cat>  $ X (N transactions)
  ...

Surprises (>2× avg daily)
  <date> <merchant> $ X
  ...
```

Skip the "Surprises" section if there are none. Stay brief — this is a check-in, not a deep report.

Relay any `warnings` above the summary.
