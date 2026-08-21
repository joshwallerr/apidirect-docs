# n8n

Use API Direct in your [n8n](https://n8n.io) workflows with our community node — search social media, news, and the web as a native workflow step, no code required.

The node is published on npm as [`n8n-nodes-apidirect`](https://www.npmjs.com/package/n8n-nodes-apidirect) and covers 58 operations across Twitter/X, Facebook, Instagram, TikTok, YouTube, Reddit, Threads, Truth Social, and Google (web search, AI Mode, news, forums, and Maps/Places).

## Install

On self-hosted n8n (version 1.94 or later):

1. Open **Settings → Community nodes**.
2. Click **Install a community node**.
3. Enter `n8n-nodes-apidirect`, tick the acknowledgement, and click **Install**.

The **API Direct** node then appears in the nodes panel like any built-in node.

## Set up credentials

1. Get your API key from the [API Keys](https://apidirect.io/dashboard/keys) page — new accounts include $5 of free credit plus [50 free requests per endpoint per month](/docs/pricing).
2. In n8n, add the API Direct node to a workflow and choose **Create new credential**.
3. Paste your key (starts with `ak_live_`) and save.

n8n tests the connection automatically — you should see **"Connection tested successfully"**.

## Usage

Pick a **Resource** (the platform) and an **Operation**, fill in the required fields, and execute. Optional parameters — page counts, sort order, date filters, [sentiment analysis](/docs/pricing#emotion-analysis) — live under **Additional Fields → Add Field**.

List operations return one n8n item per result (20 tweets become 20 items), so you can feed results straight into filters, spreadsheets, Slack messages, or any other node. Detail operations return a single item.

A few things worth knowing:

- **Pagination** uses `Page` or `Pages` fields rather than cursors. Where the API fetches multiple pages server-side in one call, each page is billed as one request — the field description tells you when that applies. See [Pagination](/docs/pagination).
- **Pricing** is pay-as-you-go, $0.002–$0.01 per request — each operation's description shows its price. No subscriptions. See [Pricing](/docs/pricing).
- **Search operations** support [boolean search syntax](/docs/boolean-search).

## Use with AI Agents

The node is flagged as an AI Agent tool. Attach **API Direct** to an n8n AI Agent as a tool, and the agent can search any platform on demand — ask it *"What are people saying about our brand on Twitter this week?"* and it will pick the operation, run the search, and summarize the results.

## Troubleshooting

**"Authorization failed - please check your credentials"** — Double-check your API key in the [dashboard](https://apidirect.io/dashboard/keys). Keys start with `ak_live_`.

**"Payment required"** — Your credit balance is empty and the endpoint's free-tier allowance is used up. Top up on the [billing page](https://apidirect.io/dashboard/billing).

**"Service unavailable"** — The endpoint is temporarily suspended; check the [status page](https://apidirect.io/status).

**Node not in the panel after install** — Refresh the browser tab; on older n8n versions, restart the instance.
