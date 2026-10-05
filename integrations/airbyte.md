# Airbyte

Load API Direct data into your warehouse with our [Airbyte](https://airbyte.com) source connector. Social posts, reviews, news and web results land as tables in BigQuery, Snowflake, Postgres or any other Airbyte destination, on a schedule, with no code. It works on Airbyte Cloud and self-hosted Airbyte.

## Install

1. Download [`manifest.yaml`](https://apidirect.io/airbyte/manifest.yaml).
2. In Airbyte, open **Builder → New custom connector → Import a YAML manifest** and upload the file.
3. Click **Publish**. **API Direct** now appears under **Sources → New source**.

## Set up a source

1. Copy your API key from the [API Keys](https://apidirect.io/dashboard/keys) page (it starts with `ak_live_`).
2. Create an **API Direct** source and paste the key.
3. Enter your **Search terms**. Each search stream runs once per term.
4. Optionally, list the accounts, pages, posts or products to track under **Accounts to monitor** and **Posts, products, places and categories to look up**.
5. Click **Set up source**, pick a destination, choose your streams and set a schedule.

## Good to know

- **Cost:** each stream bills one request per search term (or listed item) per page, per sync, at the endpoint's normal [price](/docs/pricing). Enable only the streams you need.
- **Incremental sync:** streams with a publication date only sync records published since the last sync.
- **Errors:** an invalid key or empty balance fails the sync with a clear message; an account or post that doesn't exist is skipped.
