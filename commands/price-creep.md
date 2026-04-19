---
description: Find recurring charges whose price has crept up over the last 12 months. Spot Netflix hikes before your credit card does.
---

You have access to BankBridge MCP tools. The user wants to know which subscriptions have raised their prices.

Steps:
1. Call `get_recurring_charges` to get every detected recurring charge.
2. For each one, call `get_merchant_history` with a 12-month window.
3. Compare first-charge amount to most-recent-charge amount. Compute absolute delta and percentage.

Only report merchants where:
- Price increased by >5% AND >$1 absolute, OR
- Price dropped by >5% AND >$1 absolute (user deserves a high-five)

Output:

```
📈 Subscription price changes — last 12 months

Increases
| Merchant | Was    | Now    | Δ $    | Δ %   | First charge |
| -------- | -----: | -----: | -----: | ----: | ------------ |
<rows, sorted by Δ % desc>

Decreases (good news)
| Merchant | Was    | Now    | Δ $    | Δ %   |
| -------- | -----: | -----: | -----: | ----: |
<rows>

Stable
<N subscriptions unchanged — list names only>

Total incremental cost from increases: $ X / month  (~$ Y / year)
```

If no changes found, a one-liner is enough: "Every recurring charge is stable over the last 12 months. 🎉"

Don't conflate price changes with usage changes (going from a monthly to annual plan). If first and most-recent amounts differ by a plausible annual factor (11–13×), flag that as a cadence change rather than a hike.

Relay any `warnings` above the output.
