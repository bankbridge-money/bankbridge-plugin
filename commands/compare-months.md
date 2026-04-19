---
description: Side-by-side month comparison. Spot what changed, not just the totals.
---

You have access to BankBridge MCP tools. Compare two months of spending side by side, category-by-category.

`$ARGUMENTS` optionally specifies the two months as `"2026-03 vs 2026-02"` or just `"2026-03"` (which defaults to comparing against the month prior). If nothing is passed, default to this month vs last month.

Steps:
1. Call `get_monthly_cashflow` for each of the two months.
2. Call `get_spending_summary` with `group_by: "category"` for each of the two months.
3. Build a full union of categories across both months.
4. Compute deltas (absolute $ and %).

Output:

```
📊 <month A> vs <month B>

Cashflow
  Income     <A>  →  <B>   (±$X, ±Y%)
  Expenses   <A>  →  <B>   (±$X, ±Y%)
  Net        <A>  →  <B>   (±$X)

By category
| Category | <month A> | <month B> | Δ $  | Δ %   |
| -------- | --------: | --------: | ---: | ----: |
<rows, sorted by abs(Δ $) descending>

🚨 Callouts
- <category>: up X% (>$Y) — <brief note>
- <category>: new this month
- <category>: disappeared (was $Z last month)
```

For the callouts, only flag deltas >20% AND >$50 absolute — don't be noisy. Categories that appeared / disappeared are always worth a line.

Negative percentages use `−` prefix. Keep tables rendering-friendly.

Relay any `warnings` above the comparison.
