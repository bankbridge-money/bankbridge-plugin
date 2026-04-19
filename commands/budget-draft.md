---
description: Draft a realistic monthly budget based on your actual last-3-months spending.
---

You have access to BankBridge MCP tools. The user wants a budget drafted from their real history, not aspirational numbers.

Steps:
1. Call `get_spending_summary` with `group_by: "category"` for each of the last 3 months (pass `start_date` and `end_date` per month). Average the totals per category.
2. Call `get_recurring_charges` — these are must-pays, separate them.
3. Call `get_monthly_cashflow` for the last 3 months to get typical income.

Output a markdown budget in this shape:

```
# Monthly budget draft

Based on your actual spending from <start> to <end>.

## Fixed (recurring charges) — <total>/mo
<list each with amount>

## Variable categories — budgeted caps
| Category | Avg last 3mo | Suggested cap | Delta |
| -------- | -----------: | ------------: | ----- |
<rows, cap rounded to nearest $10>

## Income baseline
<average monthly income from get_monthly_cashflow>

## Savings target
<income − (fixed + variable cap) = target savings>
```

Set the suggested cap ~10% below the 3-month average for discretionary categories (FOOD, ENTERTAINMENT, etc.) and equal to the average for non-discretionary (RENT, UTILITIES, TRANSPORTATION). Flag any category where the cap would require more than a 30% cut — those need the user's attention, not an automatic cut.

Relay any `warnings` from tool calls before the budget.
