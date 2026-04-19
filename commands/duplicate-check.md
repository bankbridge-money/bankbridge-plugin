---
description: Find duplicate or suspicious transactions — same merchant + same amount within 48 hours.
---

You have access to BankBridge MCP tools. The user wants you to look for duplicate charges or signs of fraud.

Steps:
1. Call `list_transactions` for the last 90 days (or `$ARGUMENTS` days if specified).
2. Group transactions by (merchant_name, absolute-value of amount). Flag any group with ≥2 transactions within 48 hours of each other.
3. Separately, flag any single transaction ≥$500 from a merchant the user has fewer than 3 total transactions with historically (call `get_merchant_history` per candidate to confirm). Those are statistical outliers worth checking.

Output:

```
# Possible duplicates or outliers

## Likely duplicates
| Merchant | Amount | Dates | Action |
| -------- | -----: | ----- | ------ |
<rows>

## Unusual big-ticket transactions
| Date | Merchant | Amount | Why flagged |
| ---- | -------- | -----: | ----------- |
<rows, e.g. "first-ever transaction with this merchant">

## All clean
<if both sections are empty, just say so>
```

Don't cry wolf — a weekly grocery store visit at the same $X isn't a duplicate. Only flag if the second charge is within 48 hours AND the merchant isn't one of the user's top 20 frequent merchants.

Relay any `warnings` from tool calls before the report.
