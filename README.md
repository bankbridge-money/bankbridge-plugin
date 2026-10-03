# BankBridge for Claude

> **Your bank accounts, transactions, and investments, in plain English, right inside Claude.**

[![Add to Claude](https://img.shields.io/badge/Claude-Add_connector-D97757?style=flat-square&logo=claude&logoColor=white)](https://claude.ai/directory/connectors/bankbridge)
[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=bankbridge&config=eyJ1cmwiOiJodHRwczovL2JhbmticmlkZ2UubW9uZXkvYXBpL21jcCJ9)
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect/mcp/install?name=bankbridge&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fbankbridge.money%2Fapi%2Fmcp%22%7D)
[![Install in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Install_server-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=bankbridge&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fbankbridge.money%2Fapi%2Fmcp%22%7D)

Ask Claude things like *"how much did I spend on restaurants last month?"* or *"find any subscriptions I've forgotten about"* or *"draft a budget from my actual last 3 months"* and get real answers from your real data.

One account. Every bank you use. Works with Claude Code, Claude Desktop, Claude.ai, ChatGPT, Cursor, Copilot, Gemini, Codex, and everything else that speaks MCP. Read-only, US banks.

---

## Install

### Claude.ai, Claude Desktop, Claude mobile, Cowork

BankBridge is in the [Claude Connectors Directory](https://claude.ai/directory/connectors/bankbridge). Open the listing, click **Connect**, sign in to BankBridge. No key to paste. Connectors sync across every Claude app, and Claude Code picks them up too.

### Claude Code (plugin, with 19 slash commands)

```shell
/plugin marketplace add bankbridge-money/bankbridge-plugin
/plugin install bankbridge
```

When prompted, paste your API token from [**bankbridge.money/dashboard**](https://bankbridge.money/dashboard?ref=github). It&rsquo;s pre-filled and copy-ready on your dashboard.

Prefer no plugin and no key? One command, then `/mcp` to sign in through your browser:

```shell
claude mcp add --scope user --transport http bankbridge https://bankbridge.money/api/mcp
```

### Cursor, VS Code (Copilot)

Use the **Add to Cursor** or **Install in VS Code** badge above. The editor asks you to confirm, then opens the BankBridge sign-in page in your browser. No key to paste.

### Gemini CLI, Codex CLI

```shell
gemini mcp add --scope user --transport http bankbridge https://bankbridge.money/api/mcp
codex mcp add bankbridge --url https://bankbridge.money/api/mcp
```

Both discover BankBridge&rsquo;s OAuth sign-in automatically (Gemini: run `/mcp auth bankbridge`; Codex opens the browser on its own).

### Everything else

Server URL: `https://bankbridge.money/api/mcp` (Streamable HTTP). Auth: OAuth 2.1 with Dynamic Client Registration, or `Authorization: Bearer bbk_...` with a key from your dashboard. Step-by-step guides for each agent: [bankbridge.money/docs](https://bankbridge.money/docs?ref=github).

You&rsquo;ll need:
- **A BankBridge account**: [sign up](https://bankbridge.money/?ref=github) ($5/mo or $50/yr per connected bank), or try the demo with sample data from the sign-in screen, no signup
- **At least one bank connected**: linked on the dashboard in ~30 seconds

---

## 19 slash commands, included

Type `/` in any Claude Code session to find them. Each wraps a multi-step flow with an opinionated output shape, so you don&rsquo;t have to hand-craft the prompt.

> **Also in Claude iOS / Android / Desktop / Cowork.** The same 19 commands are exposed as MCP prompts, so they appear under the **+** button in the chat input bar. One tap fills the full prompt. In Cursor, ChatGPT, and other MCP clients, they show up in whatever prompt-picker UI that client provides.

### 💨 Quick lookups: fastest path from install to first result

| Command | What it does |
|---------|--------------|
| `/balances` | Snapshot of every account, rolling total, credit utilization. |
| `/weekly-review` | Last 7 days at a glance: total spend, biggest charges, surprises. |

### 📊 Spending analysis: group and slice

| Command | What it does |
|---------|--------------|
| `/spending-by` | Flexible group-by. Slice by category, merchant, month, or week for any window. |
| `/compare-months` | Side-by-side month comparison with category deltas and callouts. |
| `/category-deep-dive` | Zoom into one category: every transaction, top merchants, cadence, outliers. |

### 💰 Cashflow & budgeting: real numbers only

| Command | What it does |
|---------|--------------|
| `/monthly-check` | One-page monthly report: cashflow, top categories, merchants, subscriptions. |
| `/cashflow-trend` | Multi-month income vs expenses table with trend takeaways. |
| `/budget-draft` | Draft a realistic budget from your actual last 3 months of spending. |

### 📈 Investments: if you have a brokerage connected

| Command | What it does |
|---------|--------------|
| `/portfolio-health` | Total value, gain/loss, concentration check, positions >20% flagged. |
| `/dividends` | YTD dividends received by ticker with run-rate. |

### 📉 Charts & exports: agents that can run code can save files

| Command | What it does |
|---------|--------------|
| `/monthly-chart` | Bar chart of income vs expenses for the last N months. Writes `cashflow.png`. |
| `/category-pie` | Pie chart of spending by category. Writes `spending-pie.png`. |
| `/tax-prep` | Exports a full year of transactions + category totals to CSV. |

### 🛡 Detective work: peace of mind

| Command | What it does |
|---------|--------------|
| `/subscriptions` | Every recurring charge, sorted, with age and price-drift flags. |
| `/price-creep` | Subscriptions whose price increased. Catch Netflix hikes before your card does. |
| `/duplicate-check` | Same-merchant, same-amount charges within 48 hours, plus outliers. |
| `/fraud-check` | Wider net: unfamiliar merchants, amount outliers, off-hours charges. |

### 📝 Reports: shareable, archivable, email-worthy

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

> Compare my restaurant spending in March vs January 2026. Am I trending up?

**Subscription audits**
> List every recurring charge I have. Which ones are the smallest? Can I cancel any?

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

## Under the hood: 12 MCP tools

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
| `list_categories` | Spending categories present in your data |
| `list_holdings` | Current investment positions with gain/loss |
| `list_investment_transactions` | Buys, sells, dividends, fees |
| `connect_bank` | Deep-link into a bank-connect flow when no banks are connected |

All **read-only**. BankBridge literally can&rsquo;t move money, change passwords, or make trades.

---

## Privacy & security

Your transactions never touch our servers. **We never store them.**

| | |
|---|---|
| **We don&rsquo;t keep your data** | Every question your agent asks live-fetches in real time. No transaction cache, and no record of what you asked or what came back. |
| **Read-only access** | Your agent can read balances and transactions. Nothing can move money, pay a bill, or change your accounts. |
| **Bank-grade encryption** | AES-256-GCM for access tokens at rest. HTTPS everywhere. |
| **Revocable right away** | Disconnect a bank or delete your account anytime, and the connection is revoked and deleted right away. |
| **Trusted banking rails** | Same infrastructure Venmo and Robinhood rely on. |

BankBridge re-fetches on every question instead of caching your financial history. Details: [bankbridge.money/security](https://bankbridge.money/security?ref=github).

Full privacy policy → [bankbridge.money/privacy](https://bankbridge.money/privacy?ref=github)

---

## Pricing

**$5/month per connected bank, or $50/year per bank.** First bank unlocks the service. Each additional bank adds $5/mo, prorated when you connect it. Cancel anytime, access ends at the end of your billing period.

No free tier, no freemium, no trial. Just $5 per bank. It&rsquo;s fair, predictable, and means we&rsquo;re never tempted to monetize your data. We&rsquo;re a real subscription business.

---

## Get started

<p align="center">
  <a href="https://bankbridge.money/?ref=github">
    <strong>→ Sign up at bankbridge.money</strong>
  </a>
</p>

1. Create an account (magic-link email, no password).
2. Click **Subscribe** ($5/mo or $50/yr per bank). Any major card works.
3. Connect a bank in ~30 seconds.
4. Copy your API token from the dashboard.
5. `/plugin install bankbridge` in Claude Code, paste the token.
6. Ask your first question.

End-to-end: about 90 seconds. Most of that is the bank authentication flow.

---

## Support & community

- **Docs:** [bankbridge.money/docs](https://bankbridge.money/docs?ref=github)
- **Issues (this plugin):** [github.com/bankbridge-money/bankbridge-plugin/issues](https://github.com/bankbridge-money/bankbridge-plugin/issues)
- **Sales + everything else:** [hello@greatwork.company](mailto:hello@greatwork.company)

---

<p align="center">
  <sub>Built by <a href="https://greatwork.company">Great Work LLC</a>. Not a bank, not a broker. Just a bridge.</sub>
</p>
