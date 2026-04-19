---
description: Broader suspicious-transaction finder — duplicates, unfamiliar merchants, unusual amounts, off-hours charges.
---

You have access to BankBridge MCP tools. The user wants a wider net than `/duplicate-check` — they're looking for anything suspicious.

`$ARGUMENTS` is an optional number of days to look back. Default: 30.

Steps:
1. Call `list_transactions` for the window.
2. Run FOUR checks in parallel:
   - **Duplicates**: same merchant + same amount within 48 hours.
   - **Amount outliers**: transactions > 3× the user's 90-day average transaction amount.
   - **Unfamiliar merchants**: transactions from merchants the user has <3 historical transactions with (use `get_merchant_history` per candidate to confirm).
   - **Off-hours**: transactions at 1am–5am local time, if timestamp resolution allows.

Output:

```
🛡 Suspicious activity — last N days

## Duplicates
<rows or "none">

## Amount outliers (>3× your typical transaction)
| Date | Merchant | Amount | Typical |
| ---- | -------- | -----: | ------: |
<rows>

## Unfamiliar merchants
| Date | Merchant | Amount | Prior history |
| ---- | -------- | -----: | ------------: |
<rows — "first ever" or "N prior charges" context>

## Off-hours (1am–5am)
<rows or omit section if empty>

## Verdict
<One sentence: "No red flags." | "Two items worth checking — see above." | "Multiple anomalies — take a minute.">
```

Tune sensitivity to avoid being the boy who cried wolf. A Tuesday $4.50 coffee shop repeat from a regular is NOT a duplicate even if the amount matches yesterday. Only include the "unfamiliar merchants" rows that are >$50 — sub-dollar prior-unknown charges are usually legit.

If BankBridge returns `warnings` about a connection needing reauth, surface that first — a stale feed is the most likely explanation for "weird" data.
