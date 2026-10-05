# Clay

Use API Direct inside your [Clay](https://www.clay.com) tables: enrich every row with live data from LinkedIn, X/Twitter, Reddit, YouTube, Instagram, TikTok, Facebook, Threads, Bluesky, Truth Social, Google Maps, Amazon, Trustpilot, news, forums and web search, through Clay's built-in **HTTP API** column. No Clay integration to install and no code: paste the endpoint, pick your saved API key, point a parameter at a column, and run.

There are three ways in, and they stack:

- **HTTP API columns** run one API Direct request per row and write the response into your table. Every endpoint has a ready-made recipe at [apidirect.io/clay/templates.json](/clay/templates.json), and the common ones are spelled out below.
- **AI columns** can call API Direct through its [MCP server](/docs/mcp-claude-desktop), so a Claygent or **Use AI** step can research a row ("what has this company posted on LinkedIn this month?") with real data instead of a web crawl.
- **Clay skills** for coding agents (Claude Code, Codex, Cursor) that combine API Direct signals with your Clay enrichments. They are in the [API Direct agent kit](https://github.com/apidirect/agent-kit/tree/main/clay-skills) and on the Clay Skills Marketplace.

## Before you start

1. Get your API key from the [API Keys](https://apidirect.io/dashboard/keys?utm_source=clay) page. New accounts include $5 of free credit plus [50 free requests per endpoint per month](/docs/pricing). Keys start with `ak_live_`.
2. In Clay, open any table, click **Add column → HTTP API**, click **Select header account → Add account**, and save one header:

   | Key | Value |
   |---|---|
   | `X-API-Key` | `ak_live_…` (your key) |

   Name the account **API Direct**. Clay encrypts it at workspace level and every HTTP API column can reuse it, so your key never sits in a table cell. You can manage it later under **Settings → Connections**.

## Add an HTTP API column

Take the LinkedIn profile endpoint as the example. Your table has a column of LinkedIn profile URLs called **LinkedIn URL**.

1. **Add column → HTTP API.**
2. **Method:** `GET`.
3. **Endpoint URL:** `https://apidirect.io/v1/linkedin/person`.
4. **Headers:** choose the **API Direct** header account.
5. **Query string parameters:** one row, key `url`, value `/LinkedIn URL` (type `/` in the value field and pick the column).
6. **Field paths to return:** `full_name`, `headline`, `location`, `followers`, `open_to_work`, `experience`. Leave this empty to keep the whole response.
7. Run the column on one row, check the response, then run the table.

Every API Direct endpoint follows the same recipe: the endpoint page tells you the method and path, each **parameter** becomes a query string parameter, and each **response field** is a field path. Search endpoints take a `query` parameter (your keyword or boolean expression) instead of an identifier.

Once a column works, open its configuration panel and **save it as a template** so the next table only needs the column reference changed.

## Recipes

Each recipe is an HTTP API column with method `GET`, the **API Direct** header account, and the parameters below. Column names are placeholders: use `/` to pick your own.

| What you want | Endpoint URL | Query string parameters | Field paths to return |
|---|---|---|---|
| Enrich a person from their LinkedIn URL | `https://apidirect.io/v1/linkedin/person` | `url` = `/LinkedIn URL` | `full_name`, `headline`, `location`, `followers`, `experience` |
| A person's recent LinkedIn posts | `https://apidirect.io/v1/linkedin/person/posts` | `url` = `/LinkedIn URL` | `posts` |
| Enrich a company from its LinkedIn page | `https://apidirect.io/v1/linkedin/company` | `url` = `/Company LinkedIn URL` | `name`, `industry`, `employees`, `employee_range`, `headquarters`, `website`, `description` |
| A company's recent LinkedIn posts | `https://apidirect.io/v1/linkedin/company/posts` | `url` = `/Company LinkedIn URL` | `posts` |
| Posts that mention a company, with sentiment | `https://apidirect.io/v1/linkedin/posts` | `mentions_company` = `/LinkedIn Company ID`, `get_sentiment` = `true`, `posted_ago` = `30d` | `posts` |
| Open roles a company is hiring for | `https://apidirect.io/v1/linkedin/jobs` | `query` = `/Role`, `company_ids` = `/LinkedIn Company ID`, `posted_ago` = `30d` | `jobs`, `count` |
| X/Twitter profile and follower count | `https://apidirect.io/v1/twitter/user` | `username` = `/Twitter Handle` | `user.name`, `user.description`, `user.followers_count`, `user.verified`, `user.url` |
| What people say about a brand on X this week | `https://apidirect.io/v1/twitter/posts` | `query` = `/Brand`, `posted_ago` = `7d`, `sort_by` = `most_recent`, `get_sentiment` = `true` | `posts`, `count` |
| Reddit threads about a topic or product | `https://apidirect.io/v1/reddit/posts` | `query` = `/Keyword`, `sort_by` = `most_recent`, `get_sentiment` = `true` | `posts` |
| News about an account | `https://apidirect.io/v1/news/articles` | `query` = `/Company Name`, `time_published` = `7d`, `limit` = `10` | `articles` |
| Find a local business on Google Maps | `https://apidirect.io/v1/places/search` | `query` = `/Business + City`, `pages` = `1` | `places` |
| Contacts and details of a Google Maps place | `https://apidirect.io/v1/places/details` | `place_id` = `/Place ID` | `place.name`, `place.website`, `place.phone_number`, `place.rating`, `place.review_count`, `place.emails_and_contacts` |
| A place's worst reviews | `https://apidirect.io/v1/places/reviews` | `place_id` = `/Place ID`, `sort_by` = `lowest_ranking`, `get_sentiment` = `true` | `reviews` |
| Trustpilot reviews of a company | `https://apidirect.io/v1/trustpilot/company/reviews` | `domain` = `/Company Domain`, `sort_by` = `newest`, `get_sentiment` = `true` | `company`, `reviews` |
| Instagram profile with public email | `https://apidirect.io/v1/instagram/user` | `username` = `/Instagram Handle` | `user.full_name`, `user.follower_count`, `user.biography`, `user.public_email`, `user.external_url` |
| TikTok profile | `https://apidirect.io/v1/tiktok/user` | `username` = `/TikTok Handle` | `user.nickname`, `user.followers`, `user.bio`, `user.url` |
| YouTube channel stats | `https://apidirect.io/v1/youtube/channel` | `url` = `/YouTube Channel URL` | `channel.channel_name`, `channel.subscriber_count`, `channel.description` |
| Web search with Google's AI overview | `https://apidirect.io/v1/web/search` | `query` = `/Question`, `include_ai_overview` = `true` | `ai_overview`, `results` |
| Ask Google AI Mode a question about a row | `https://apidirect.io/v1/web/ai-mode` | `prompt` = `/Prompt` | `reply_parts`, `reference_links` |
| Amazon product by ASIN | `https://apidirect.io/v1/amazon/product` | `asin` = `/ASIN` | `product.title`, `product.price`, `product.rating`, `product.num_ratings` |

Two patterns cover most other tables:

- **Resolve, then enrich.** Search endpoints return the identifier the detail endpoints need. A column calling `/v1/linkedin/companies` with `query` = `/Company Name` returns `companies[].company_id` and `companies[].url`; the next column passes `url` to `/v1/linkedin/company` or `mentions_company` to `/v1/linkedin/posts`. Google Maps works the same way: `/v1/places/search` gives `places[].place_id`, which feeds details and reviews.
- **Search per row.** Put the row's own value in `query`: the company name for news, the brand for X and Reddit, the product for Amazon. On Reddit, X, forums, LinkedIn and Bluesky the query accepts that platform's [boolean syntax](/docs/boolean-search), so a formula column can build `"Acme" AND (cancel OR switching)` for `/v1/reddit/posts` and feed it in; every other search treats operators as plain words.

## Every endpoint, as a template

[apidirect.io/clay/templates.json](/clay/templates.json) lists every endpoint as a Clay column recipe, generated from the [OpenAPI spec](https://apidirect.io/openapi.json) so it is always current. Each entry has:

```json
{
  "id": "linkedinPersonDetails",
  "name": "LinkedIn Person Profile",
  "platform": "LinkedIn",
  "method": "GET",
  "url": "https://apidirect.io/v1/linkedin/person",
  "header_account": "API Direct",
  "query_parameters": [
    {"key": "url", "value": "/LinkedIn Profile URL", "required": true, "example": "reidhoffman"}
  ],
  "response": {"shape": "object", "field_paths": ["full_name", "headline", "location"]},
  "price": "$0.006 per request",
  "free_tier": "50 requests/month",
  "docs": "https://apidirect.io/docs/linkedin-person"
}
```

`query_parameters` carries every parameter the endpoint accepts, with the row's identifier already written as a column reference and the optional filters left blank. `response.shape` is `list` when the endpoint returns a page of results under `response.list_key`, and `object` for a single profile, post or place.

## Working with lists

Search and listing endpoints return an array (`posts`, `jobs`, `reviews`, `places`) and a `count`. Three ways to use one inside Clay:

- **Keep it as JSON** (field path `posts`) and let a **Use AI** or formula column summarise, classify or count it. This is the cheapest option: one request per row, whatever the number of results.
- **Pick fields from the first results** with indexed paths such as `posts[0].snippet` and `posts[0].url` (Clay also accepts `posts.0.snippet`), which turn into plain cells.
- **Fan out to rows** with Clay's **Send Table Data** action (the replacement for the deprecated Write to Table) on the array field when every result needs its own row (one row per job posting, per review, per complaint).

Where an endpoint takes `pages`, each page is billed as one request; start with `pages` = `1` and raise it only on tables that need depth. See [Pagination](/docs/pagination).

## AI columns through the MCP server

Clay's AI steps can use your own [MCP](https://modelcontextprotocol.io) servers as tools when you bring your own model key (Clay documents this under the **Use AI** action and the Claygent builder). Connecting API Direct's server gives a Claygent or **Use AI** column all 100+ endpoints at once, with the model choosing the call.

1. In Clay, add your own model key under the AI provider settings, then open the Claygent builder (or a **Use AI** column running on that key) and choose to connect an MCP server. Workspace admins can require approval before a new MCP server is added, so an admin may need to accept it.
2. Name it **API Direct** and set the server URL to `https://apidirect.io/mcp`. Put the key from step 1 in the server's API key or authorization field; the server accepts it as a bearer token. If there is no such field, use `https://apidirect.io/mcp?token=YOUR_API_KEY` as the URL instead.
3. Save and enable the server as a tool, then write a prompt that names it, for example *"Use API Direct to fetch the latest 10 LinkedIn posts by {{Company LinkedIn URL}} and list the three themes they talk about most."*

Every MCP tool is read-only and billed at its endpoint price; the tool descriptions carry the price, so the model can keep a run cheap. The server also exposes the [skills library](https://github.com/apidirect/agent-kit#skills) as prompts, so *"run the Competitor Conquest Radar for Acme"* works from an AI column too.

## Clay skills

Skills are plain-language playbooks a coding agent follows. The API Direct agent kit ships a set written to Clay's skill contract, each pairing an API Direct signal with the enrichments your Clay workspace already has:

| Skill | What it does |
|---|---|
| [Competitor complaint prospects](https://github.com/apidirect/agent-kit/tree/main/clay-skills/competitor-complaint-prospects) | People publicly complaining about a competitor on LinkedIn, X and Reddit, resolved to profiles and work emails |
| [Hiring-signal accounts](https://github.com/apidirect/agent-kit/tree/main/clay-skills/hiring-signal-accounts) | Companies hiring for a role that implies they need you, ranked by posting volume, with the budget owner named |
| [Just-funded accounts](https://github.com/apidirect/agent-kit/tree/main/clay-skills/just-funded-accounts) | This week's raises in a sector, resolved to the company page and the buyer persona before the window closes |
| [Local leads from reviews](https://github.com/apidirect/agent-kit/tree/main/clay-skills/local-leads-from-reviews) | Local businesses in a category and city with their contact details and the complaint themes from their one-star reviews |
| [Pre-call account brief](https://github.com/apidirect/agent-kit/tree/main/clay-skills/pre-call-account-brief) | A one-page, cited brief on an account from its posts, its executives' posts, news and reviews |
| [Creator contact sheet](https://github.com/apidirect/agent-kit/tree/main/clay-skills/creator-contact-sheet) | Niche creators on Instagram, TikTok, YouTube and X with the public email or link from their bios |

Install them with the kit (in Claude Code, `/plugin marketplace add apidirect/agent-kit` then `/plugin install api-direct@api-direct`; elsewhere, `npx skills add apidirect/agent-kit`), or from the [Clay Skills Marketplace](https://marketplace.clay.com). Each skill asks for its inputs, prices every paid step, and stops for approval before spending credits or writing anywhere.

## Pricing and limits

- API Direct is pay-as-you-go, $0.002–$0.01 per request depending on the endpoint; each recipe above shows its price in `templates.json` and on the endpoint page. There are no subscriptions. See [Pricing](/docs/pricing).
- Every endpoint has a free tier of 50 requests per month (20 for Places Search, Place Reviews and Place Photos), so a small table runs for free.
- `get_sentiment=true` adds AI emotion analysis to posts and reviews for $0.001 per request on top of the endpoint price (per page on multi-page endpoints).
- Clay runs HTTP API columns in parallel, and API Direct allows 10 in-flight requests per endpoint per account (see [Rate limits](/docs/rate-limits)). Set the column's **Rate limiting** option to about 5 requests per second; a `429` means lower it.
- Google AI Mode can take over a minute to answer. Raise the column's timeout in its optional settings for that endpoint.

## Troubleshooting

**401 `invalid_api_key`** — The header account is missing or holds the wrong key. Check it under **Settings → Connections**; keys start with `ak_live_`.

**402 `payment_required`** — Your credit balance is empty and the endpoint's free-tier allowance is used up. Top up on the [billing page](https://apidirect.io/dashboard/billing).

**400 "Provide at least one of: username, url"** — The endpoint accepts several identifiers; send exactly one of them as a query string parameter.

**429 `concurrency_limit_exceeded`** — More than 10 requests to one endpoint were in flight. Lower the column's rate limit or run fewer columns on that endpoint at once.

**503 `endpoint_suspended`** — The endpoint is temporarily suspended; check the [status page](https://apidirect.io/status).

**Empty `posts` or `count: 0`** — The search ran and found nothing. Widen `posted_ago`, drop a filter, or check the query on the endpoint page's examples before raising `pages`.

**Column references come back literally** — A value like `/LinkedIn URL` typed as text is sent as text. Delete it and type `/` to insert the column from the picker.
