# BankBridge for Claude Code

Give Claude Code read-only access to your bank accounts, transactions, and investment holdings. Ask anything about your money in plain English.

## Install

```
/plugin marketplace add bankbridge-money/bankbridge-plugin
/plugin install bankbridge
```

When prompted, paste your API token from [bankbridge.money/dashboard](https://bankbridge.money/dashboard). It starts with `bbk_`.

## What you can ask

- "How much did I spend on restaurants last month?"
- "List every subscription I'm paying for."
- "What's my cashflow for this month?"
- "How are my investments doing?"
- "Show me all my Netflix charges."

Twelve tools across accounts, transactions, spending, subscriptions, cashflow, investments, and bank-connect. Your agent picks the right one.

## Slash commands

Once installed, type `/` in Claude Code and look for these. Each one wraps a multi-step flow so you don't have to write the prompt:

| Command | What it does |
|---------|--------------|
| `/monthly-check` | Full monthly review — cashflow, top categories, top merchants, subscriptions, investment delta. |
| `/budget-draft` | Drafts a realistic budget from your actual last 3 months of spending. |
| `/subscriptions` | Audit of every recurring charge, flagged by age + price drift. |
| `/duplicate-check` | Finds possible duplicate charges or statistical outliers in recent activity. |
| `/monthly-chart` | Writes a bar chart of cashflow over the last N months to `cashflow.png`. |
| `/tax-prep` | Exports a year's worth of transactions + category totals to CSV. |

All commands pass through your agent's natural language — you can follow up, redirect, or ask for the output in a different shape.

## Requires

An active [BankBridge](https://bankbridge.money) subscription ($5/mo per connected bank) with at least one bank connected.
