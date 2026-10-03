# Installing BankBridge for Cline

BankBridge is a **remote, hosted MCP server** — you don't run it locally. You point Cline at `https://bankbridge.money/api/mcp` with a Bearer token, and every tool call live-fetches from the user's bank.

## Prerequisites

Before installing, the user must:

1. **Have a BankBridge account.** Sign up at [bankbridge.money](https://bankbridge.money) — magic-link login, no password.
2. **Have an active subscription.** $5/mo per connected bank. Subscribe from the dashboard (any major card).
3. **Have at least one bank connected.** Click "Connect a bank" on the dashboard — Plaid Link handles the OAuth flow (~30 seconds per bank).
4. **Have an API token.** Copy it from [bankbridge.money/dashboard/settings](https://bankbridge.money/dashboard/settings). The token starts with `bbk_`.

If any of the above is missing, tell the user to do those steps first, then come back and re-run install. Do not attempt to work around this — BankBridge cannot function without a valid, active-subscription API token attached to at least one connected bank.

## Installation

Add this block to the user's Cline MCP settings (`cline_mcp_settings.json`):

```json
{
  "mcpServers": {
    "bankbridge": {
      "type": "streamableHttp",
      "url": "https://bankbridge.money/api/mcp",
      "headers": {
        "Authorization": "Bearer <PASTE_THE_bbk_TOKEN_HERE>"
      }
    }
  }
}
```

Replace `<PASTE_THE_bbk_TOKEN_HERE>` with the token the user copied from their dashboard. It starts with `bbk_` followed by a long random suffix.

**Ask the user for their token before writing the config.** Never invent or guess a token; a wrong token returns `401 unauthorized` on every call and the whole install looks broken.

## Verify

After Cline reloads MCP servers, ask the model to run the `list_accounts` tool. A successful call returns a JSON array of the user's connected bank accounts (masked account numbers, balances, types). If it returns an error, check:

- `401 Unauthorized` → the Bearer token is wrong or the subscription lapsed. Regenerate at `/dashboard/settings`.
- `402 Payment Required` → subscription is `past_due` or `canceled`. Reactivate at `/dashboard`.
- `no banks connected` warning → user needs to connect at least one bank before any tool returns data.

## About the tools

BankBridge exposes 12 tools total. Categories:

**Accounts & transactions.**
- `list_accounts` — balances + types for every connected account
- `get_account` — detail lookup by id
- `list_transactions` — filter by date / amount / category / account (paginated)
- `search_transactions` — substring match on name + merchant_name

**Analysis.**
- `get_spending_summary` — group by category / merchant / month / week
- `get_recurring_charges` — detect subscriptions
- `get_monthly_cashflow` — income vs expenses for a given `YYYY-MM`
- `get_merchant_history` — every charge for a merchant + aggregate stats
- `list_categories` — Plaid categories present in the user's data

**Investments.**
- `list_holdings` — current positions with gain/loss
- `list_investment_transactions` — buys, sells, dividends, fees

**Utility.**
- `connect_bank` — deep-link into a bank-connect flow when no banks are connected

All tools are **read-only.** BankBridge literally cannot move money, place trades, or change credentials.

## Data & privacy notes to relay to the user

- BankBridge caches **zero** financial data. Every tool call live-fetches from the bank. Query latency reflects that (~500ms–2s per call).
- Amount convention: **positive amounts = money leaving the account (expenses); negative = money entering (income/refunds).** This is Plaid's convention.
- If a tool response contains a `warnings` array, relay every warning verbatim — it means a bank is disconnected or rate-limited and the answer is partial.

## Troubleshooting

If Cline can't reach `https://bankbridge.money/api/mcp`:
- Check the user's network isn't blocking outbound HTTPS to `bankbridge.money`.
- The endpoint speaks **Streamable HTTP** (single POST, chunked responses). Legacy SSE clients won't work.
- If a request hangs > 30 seconds, retry once; if it still hangs, tell the user to check [bankbridge.money](https://bankbridge.money) or email `hello@greatwork.company`.

## Uninstall

Remove the `bankbridge` block from `cline_mcp_settings.json`. This does **not** cancel the paid subscription — for that, go to `bankbridge.money/dashboard` → Billing → Cancel.
