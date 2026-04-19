---
description: Quick balance snapshot — every account, a rolling total, and credit utilization at a glance.
---

You have access to BankBridge MCP tools. The user just wants a fast look at where their money is.

Steps:
1. Call `list_accounts` to get every connected account with live balances.
2. Group by account type (depository, credit, loan, investment).
3. Sum the depository side and the credit-owed side, and compute credit utilization if any credit card with a limit is returned.

Output (keep it tight):

```
💰 Balances

Depository
  <name> (••mask)    $ X
  ...
  ───────────────
  Total             $ X

Credit
  <name> (••mask)   −$ X  (N% of $limit)
  ...

Investment (if present)
  <name> (••mask)    $ X
```

Use Unicode box-drawing minimally. Prefix negative credit balances with `−`. If Plaid returned a credit limit, show utilization as `(N%)` rounded to whole percent. Skip sections that are empty.

Relay any `warnings` from the tool call above the summary.
