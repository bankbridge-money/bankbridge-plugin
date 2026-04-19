---
description: Audit every recurring charge you're paying for. Flag small-ticket items you might have forgotten.
---

You have access to BankBridge MCP tools. The user wants a complete subscription audit.

Steps:
1. Call `get_recurring_charges` to get every detected recurring charge.
2. For each one, call `get_merchant_history` to find when the first charge was and if the price has drifted.

Output in this shape:

```
# Subscription audit

## Active recurring charges — <total>/mo
| Merchant | Amount | Frequency | Started | Price trend |
| -------- | -----: | --------- | ------- | ----------- |
<sorted by amount desc>

## Potentially forgettable (<$20/mo and started >6 months ago)
<callout list — these are the ones to review>

## Price increases
<any merchant whose charge is >10% higher than its first charge>
```

Use "stable", "+X%", or "−X%" for the price-trend column based on first vs most recent charge.

Be direct about what the user could cancel — if a $9/mo charge from 18 months ago hasn't been used based on no related activity nearby, say "review this — hasn't moved since <date>". Don't be preachy.

Relay any `warnings` from tool calls before the audit.
