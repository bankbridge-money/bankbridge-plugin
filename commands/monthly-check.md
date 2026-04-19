---
description: Full monthly financial review — cashflow, top spending, subscriptions, investment delta.
---

You have access to BankBridge MCP tools. The user has asked for a monthly financial check.

If the user hasn't specified a month, use the current month. Accept input like "March 2026" or "2026-03" as `$ARGUMENTS`.

Build a one-page markdown report in this structure:

```
# Monthly check — <Month Year>

## Cashflow
<income, expenses, net, savings rate>

## Top 5 spending categories
<markdown table, biggest first>

## Top 10 merchants
<markdown table, biggest first>

## Recurring charges
<list every one with amount, frequency, total monthly impact>

## Investment delta (if any brokerage is connected)
<total value, gain/loss since last month if derivable, top mover>
```

Steps:
1. Call `get_monthly_cashflow` with `month: "<YYYY-MM>"` → top of the report
2. Call `get_spending_summary` with `group_by: "category"` → top 5 table
3. Call `get_spending_summary` with `group_by: "merchant"` → top 10 table
4. Call `get_recurring_charges` → the subscriptions section
5. Call `list_holdings` → if non-empty, add the investments section; otherwise omit

If any tool returns a `warnings` array, **relay each warning to the user verbatim at the top of your response** before the report. Never silently drop warnings.

Keep numbers in plain dollars with 2 decimals. Prefix negatives with `−`. No prose filler — the report is the deliverable.
