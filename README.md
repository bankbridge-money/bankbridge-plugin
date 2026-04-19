# BankBridge for Claude Code

> **Your bank accounts, transactions, and investments — in plain English, right inside Claude Code.**

Ask Claude things like *"how much did I spend on restaurants last month?"* or *"find any subscriptions I've forgotten about"* or *"draft a budget from my actual last 3 months"* — and get real answers from your real data.

One account. Every bank you use. Works with Claude Code, Claude Desktop, Claude.ai, ChatGPT, Cursor, Copilot, Gemini, Codex, and everything else that speaks MCP.

---

## Install

```shell
/plugin marketplace add bankbridge-money/bankbridge-plugin
/plugin install bankbridge
```

When prompted, paste your API token from [**bankbridge.money/dashboard**](https://bankbridge.money/dashboard). It&rsquo;s pre-filled and copy-ready on your dashboard — just hit the big Copy button.

You&rsquo;ll need:
- **A BankBridge account** — [sign up](https://bankbridge.money) ($5/mo per connected bank)
- **At least one bank connected** — linked via Plaid on the dashboard in ~30 seconds

That&rsquo;s it. The plugin handles the rest.

---

## 19 slash commands, included

Type `/` in any Claude Code session to find them. Each wraps a multi-step flow with an opinionated output shape, so you don&rsquo;t have to hand-craft the prompt.

### 💨 Quick lookups — fastest path from install to first result

| Command | What it does |
|---------|--------------|
| `/balances` | Snapshot of every account, rolling total, credit utilization. |
| `/weekly-review` | Last 7 days at a glance: total spend, biggest charges, surprises. |

### 📊 Spending analysis — group and slice

| Command | What it does |
|---------|--------------|
| `/spending-by` | Flexible group-by. Slice by category, merchant, month, or week for any window. |
| `/compare-months` | Side-by-side month comparison with category deltas and callouts. |
| `/category-deep-dive` | Zoom into one category — every transaction, top merchants, cadence, outliers. |

### 💰 Cashflow & budgeting — real numbers only

| Command | What it does |
|---------|--------------|
| `/monthly-check` | One-page monthly report — cashflow, top categories, merchants, subscriptions. |
| `/cashflow-trend` | Multi-month income vs expenses table with trend takeaways. |
| `/budget-draft` | Draft a realistic budget from your actual last 3 months of spending. |

### 📈 Investments — if you have a brokerage connected

| Command | What it does |
|---------|--------------|
| `/portfolio-health` | Total value, gain/loss, concentration check, positions >20% flagged. |
| `/dividends` | YTD dividends received by ticker with run-rate. |

### 📉 Charts & exports — agents that can run code can save files

| Command | What it does |
|---------|--------------|
| `/monthly-chart` | Bar chart of income vs expenses for the last N months. Writes `cashflow.png`. |
| `/category-pie` | Pie chart of spending by category. Writes `spending-pie.png`. |
| `/tax-prep` | Exports a full year of transactions + category totals to CSV. |

### 🛡 Detective work — peace of mind

| Command | What it does |
|---------|--------------|
| `/subscriptions` | Every recurring charge, sorted, with age and price-drift flags. |
| `/price-creep` | Subscriptions whose price increased — catch Netflix hikes before your card does. |
| `/duplicate-check` | Same-merchant, same-amount charges within 48 hours, plus outliers. |
| `/fraud-check` | Wider net: unfamiliar merchants, amount outliers, off-hours charges. |

### 📝 Reports — shareable, archivable, email-worthy

| Command | What it does |
|---------|--------------|
| `/monthly-report` | Polished narrative report for a given month. |
| `/year-in-review` | Spotify Wrapped for your money. |

---

## Example prompts (no command required)

Claude Code picks the right MCP tools automatically when you ask in plain English. Copy any of these:

**Every-day check-ins**
> How much did I spend this week?

> List my last 20 transactions over $50.

> What's my current cashflow this month?

**Spending analysis**
> Break down my March spending by category, biggest first. Show as a markdown table.

> Who are my top 10 merchants by spend in the last 90 days?

> Compare my restaurant spending in March vs January 2026 — am I trending up?

**Subscription audits**
> List every recurring charge I have. Which ones are the smallest — can I cancel any?

> Has any subscription raised its price in the last 12 months?

**Investments**
> Show my current holdings sorted by gain/loss with percentages.

> How much have I received in dividends this year?

> What percentage of my portfolio is in my single biggest position?

**Visualizations (agents with code execution)**
> Make a bar chart of my monthly cashflow for the last 6 months. Save as cashflow.png.

> Export my March transactions to CSV.

> Build me a one-page markdown report for last month.

**Detective work**
> Find any transactions that look unusual or duplicated this month.

> Which 5 merchants have I spent the most on this year?

> Find recurring charges under $20/mo that I might have forgotten about.

---

## Under the hood — 12 MCP tools

Claude Code picks these automatically based on your question. You never have to name them, but here&rsquo;s what&rsquo;s available:

| Tool | Purpose |
|------|---------|
| `list_accounts` | All connected bank accounts with current balances |
| `get_account` | Detail lookup for one account by id |
| `list_transactions` | Filter by date range, amount, category, account, pending flag |
| `search_transactions` | Substring match on merchant name + description |
| `get_spending_summary` | Group spending by category / merchant / month / week |
| `get_recurring_charges` | Detected subscriptions with merchant, amount, frequency |
| `get_monthly_cashflow` | Income vs expenses for a given month, top sources |
| `get_merchant_history` | Full charge history for a merchant with stats |
| `list_categories` | Plaid categories present in your data |
| `list_holdings` | Current investment positions with gain/loss |
| `list_investment_transactions` | Buys, sells, dividends, fees |
| `connect_bank` | Deep-link into a bank-connect flow when no banks are connected |

All **read-only**. BankBridge literally can&rsquo;t move money, change passwords, or make trades.

---

## Privacy & security

Your transactions live at your bank. **We never store them.**

| | |
|---|---|
| **We don&rsquo;t keep your data** | Every question your agent asks live-fetches in real time. No transaction cache. No query log. |
| **Read-only access** | We can see your transactions. We can&rsquo;t move money. |
| **Bank-grade encryption** | AES-256-GCM for access tokens at rest. TLS 1.3 for everything else. |
| **Revocable in seconds** | Cancel or delete your account anytime — your bank access is revoked and deleted from our servers within seconds. |
| **Trusted banking rails** | Same infrastructure Venmo and Robinhood rely on. |

No mainstream competitor can say "we never store your transactions" — most cache your financial history server-side for speed. BankBridge re-fetches on every question instead. Slightly slower, dramatically more private.

Full privacy policy → [bankbridge.money/privacy](https://bankbridge.money/privacy)

---

## Pricing

**$5/month per connected bank.** First bank unlocks the service. Each additional bank adds $5/mo, prorated when you connect it. Cancel anytime, access ends at the end of your billing period.

No free tier, no freemium, no trial. Just $5 per bank — it&rsquo;s fair, predictable, and means we&rsquo;re never tempted to monetize your data. We&rsquo;re a real subscription business.

---

## Get started

<p align="center">
  <a href="https://bankbridge.money">
    <strong>→ Sign up at bankbridge.money</strong>
  </a>
</p>

1. Create an account (magic-link email, no password).
2. Click **Subscribe — $5/mo**. Any major card works.
3. Connect a bank via Plaid in ~30 seconds.
4. Copy your API token from the dashboard.
5. `/plugin install bankbridge` in Claude Code, paste the token.
6. Ask your first question.

End-to-end: about 90 seconds. Most of that is the bank authentication flow.

---

## Not using Claude Code?

BankBridge works everywhere MCP works:

- **Claude Desktop** — download the signed `.mcpb` bundle, double-click to install
- **Claude.ai web / mobile / Cowork** — add a Custom Connector, OAuth auto-discovers
- **ChatGPT** — Developer Mode → Import remote MCP
- **Cursor, Copilot, Windsurf, Continue, Cline, Zed** — paste a `mcp.json` snippet
- **Gemini CLI / Code Assist / Vertex AI** — add to `~/.gemini/settings.json`
- **Codex CLI / Codex Cloud / OpenAI Responses API / AgentKit** — native integration
- **Anything that speaks MCP** — plain HTTP with Bearer auth

[Full integration guides →](https://bankbridge.money/docs)

---

## Support & community

- **Docs:** [bankbridge.money/docs](https://bankbridge.money/docs)
- **Issues (this plugin):** [github.com/bankbridge-money/bankbridge-plugin/issues](https://github.com/bankbridge-money/bankbridge-plugin/issues)
- **Sales + everything else:** [support@bankbridge.money](mailto:support@bankbridge.money)

---

<p align="center">
  <sub>Built by <a href="https://greatwork.company">Great Work LLC</a>. Powered by Plaid. Not a bank, not a broker — just a bridge.</sub>
</p>
