---
description: Portfolio health check — total value, gain/loss, concentration, and any single position > 20% of portfolio.
---

You have access to BankBridge MCP tools. The user wants to know if their portfolio is concentrated or diversified.

Steps:
1. Call `list_holdings`. If the result is empty or `warnings` say no investments connected, stop and tell the user to connect a brokerage account.
2. For each holding, compute: current value, cost basis, unrealized gain/loss ($ and %), and % of total portfolio.
3. Flag any position > 20% of the total portfolio as concentration risk.
4. Call `list_investment_transactions` with `limit: 20` to get recent activity.

Output:

```
📈 Portfolio health

Total value:      $ X
Total cost basis: $ Y
Unrealized P/L:   ±$ Z  (±N%)

Positions
| Ticker | Qty   | Value  | Cost   | Δ $    | Δ %   | % of portfolio |
| ------ | ----: | -----: | -----: | -----: | ----: | -------------: |
<rows, sorted by value desc>

⚠ Concentration risk (>20% of portfolio)
- <ticker>: X%  (consider diversifying)

Recent activity (last 20)
  <date>  <type>  <ticker>  qty <n>  $ <amount>
  ...
```

If no positions are >20%, replace the concentration section with a one-liner: "Your most concentrated position is <ticker> at N% — within typical single-stock thresholds."

Don't give investment advice beyond pointing out concentration math. If the user asks "should I sell?", decline and suggest they speak with a fiduciary.

Relay any `warnings` above the report.
