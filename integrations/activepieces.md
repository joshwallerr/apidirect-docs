# Activepieces

Use API Direct in your [Activepieces](https://www.activepieces.com) flows with our official piece — search social media, news, reviews and the web as a native flow step, no code required.

The piece is published on npm as [`@apidirect/piece-api-direct`](https://www.npmjs.com/package/@apidirect/piece-api-direct) and covers 92 actions across Twitter/X, Facebook, Instagram, TikTok, YouTube, Reddit, Threads, Truth Social, Bluesky, Amazon, Trustpilot, and Google (web search, AI Mode, news, forums, and Maps/Places).

## Install

On a self-hosted Activepieces instance (0.36 or later):

1. Open **Settings → Pieces** and click **Install Piece**.
2. Choose **npm** as the source and enter `@apidirect/piece-api-direct`.
3. Click **Install**. The **API Direct** piece appears in the builder's piece list once the download finishes.

Activepieces Cloud only ships pieces from the main Activepieces repository, which is not accepting outside contributions at the moment, so the piece is self-hosted only for now.

## Set up a connection

1. Get your API key from the [API Keys](https://apidirect.io/dashboard/keys) page — new accounts include $5 of free credit plus [50 free requests per endpoint per month](/docs/pricing).
2. In a flow, add an **API Direct** step, pick an action, and click **Create connection**.
3. Paste your key (starts with `ak_live_`) and save.

Activepieces checks the key against our cheapest endpoint (`/v1/time`, $0.001) before saving the connection.

## Usage

Pick an action (one per endpoint, named after the platform: **Search Twitter Posts**, **Instagram User Profile**, **Trustpilot Company Reviews**), fill in the required fields, and test the step. Secondary options — page counts and [sentiment analysis](/docs/pricing#emotion-analysis) — live in the step's **Advanced** section.

Each action returns the API response exactly as documented on its endpoint page, and ships with an output schema, so the data selector shows the result fields by name. To process a list of results one by one, pass the list (for example `posts`) to a **Loop** step.

A few things worth knowing:

- **Pagination** uses `Page` or `Pages` fields rather than cursors. Where the API fetches multiple pages server-side in one call, each page is billed as one request — the field description tells you when that applies. See [Pagination](/docs/pagination).
- **Pricing** is pay-as-you-go, $0.003–$0.01 per request — each action's description shows its price. No subscriptions. See [Pricing](/docs/pricing).
- **Search actions** support [boolean search syntax](/docs/boolean-search).
- **Custom API Call** covers endpoints or parameters the piece does not expose yet: it sends your API key automatically to any path under `https://apidirect.io/v1`.

## Use with AI agents

Every action carries the metadata Activepieces agents and its MCP server read, so you can hand the API Direct piece to an agent and ask it *"What are people saying about our brand on Twitter this week?"* — it picks the action, runs the search, and summarizes the results.

## Troubleshooting

**"API Direct returned 401 (invalid_api_key)"** — Double-check your API key in the [dashboard](https://apidirect.io/dashboard/keys). Keys start with `ak_live_`.

**"API Direct returned 402 (payment_required)"** — Your credit balance is empty and the endpoint's free-tier allowance is used up. Top up on the [billing page](https://apidirect.io/dashboard/billing).

**"API Direct returned 503 (endpoint_suspended)"** — The endpoint is temporarily suspended; check the [status page](https://apidirect.io/status).

**"Provide at least one of: username, url"** — The action accepts several ways to identify the same thing (a username or a profile URL, a post URL or a post ID); fill in one of them.

**Piece not in the builder after install** — Refresh the browser tab; on older Activepieces versions, restart the instance.
