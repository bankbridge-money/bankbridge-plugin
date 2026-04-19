---
description: Full written markdown report for a given month — narrative, not just tables. Meant for sharing or archiving.
---

You have access to BankBridge MCP tools. The user wants a polished, narrative-style monthly report.

`$ARGUMENTS` is the month (e.g. "2026-03" or "march 2026"). Default: most recently completed month.

This is the longer, prose-friendly cousin of `/monthly-check`. Use it when someone wants to save a file or email it.

Steps:
1. Call `get_monthly_cashflow`, `get_spending_summary` (by category and by merchant), `get_recurring_charges`, and `list_holdings` (if connected).
2. Write a narrative report, not just tables.

Output structure:

```
# <Month Year> — Financial report

## The headline
<1–2 sentence summary of the month: profitable, tight, big purchase, etc. Lead with the most salient number.>

## Cashflow
<Income, expenses, net — as a table. Follow with 1 paragraph contextualizing: how this compared to typical, any outlier inflows/outflows.>

## Where the money went
<Top 5 categories as a table, followed by 2–3 sentences of narrative pointing out what stood out — a category that spiked, a category that was quiet, etc.>

## Top merchants
<Top 10 as a table. 1–2 sentences on any pattern (e.g. "coffee spend was dominated by Blue Bottle, 14 visits").>

## Recurring charges
<Total monthly recurring + list every recurring charge. 1 sentence on anything that changed vs last month.>

## Investments (if connected)
<Portfolio value, change over the month, top mover, any notable trades.>

## What to watch
<2–3 bullets of things the user might want to pay attention to next month. Not advice — observations: "Food spend was 28% higher than February. Worth watching in April.">
```

Tone: calm, factual, warm. Like a good CFO email. No hype, no emoji (save that for /year-in-review). Numbers get commas and 2-decimal formatting.

Offer to save to `report-<year>-<month>.md` if the user asks — don't save unless asked.

Relay any `warnings` above the report.
