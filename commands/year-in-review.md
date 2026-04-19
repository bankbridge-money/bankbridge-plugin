---
description: Spotify Wrapped for your money — full-year cashflow, spending rank, top merchants, recurring tax, and a few fun stats.
---

You have access to BankBridge MCP tools. The user wants a full-year retrospective.

`$ARGUMENTS` is an optional year (e.g. `2025`). Default: most recently completed calendar year.

Steps:
1. Call `get_monthly_cashflow` for each month of the year. Sum income, expenses, net.
2. Call `get_spending_summary` with `group_by: "category"` for the full year.
3. Call `get_spending_summary` with `group_by: "merchant"` for the full year.
4. Call `get_recurring_charges`.
5. Call `list_holdings` and `list_investment_transactions` for the year (if any).

Output:

```
🎁 Year in review — <year>

## Cashflow
Total income:    $ X
Total expenses:  $ Y
Net:            ±$ Z
Best month:     <month> (+$X saved)
Worst month:    <month> (−$X)
Savings rate:   N%

## You spent the most on
1. <merchant>  $ X   (<N transactions>)
2. <merchant>  $ X
3. <merchant>  $ X
...
<top 10>

## By category
| Category | Total  | % of expenses |
| -------- | -----: | ------------: |
<rows, top 10>

## Subscription tax
You paid $ X / year in recurring charges:
  <merchant>  $ X / mo  (annual: $ Y)
  ...

## Fun stats
- Most expensive single day: <date> — $ X across N transactions
- Busiest spending day of week: <weekday> (avg $ X)
- Number of unique merchants: N
- Weirdest spend (single largest outlier): <merchant> $ X on <date>

## Investments (if connected)
Portfolio change: ±$ X  (±N%)
Dividends received: $ Y
Top mover: <ticker> (±N%)
```

Make it feel like a gift, not an audit. Be warm about the numbers. Don't shame; just report. Skip sections that don't apply (no investments → drop that section entirely).

Relay any `warnings` at the top.
