# API Keys

API keys are used to authenticate your requests. Manage them from the [API Keys](https://apidirect.io/dashboard/keys) page in your dashboard.

## Creating a Key

1. Go to [Dashboard > API Keys](https://apidirect.io/dashboard/keys)
2. Click "Create API Key"
3. Copy your new key immediately — the full key is only shown once

Your key will look like:

```
ak_live_7f3a9b2c1d4e5f6a8b9c0d1e2f3a4b5c
```

## Key Limits

Each account can have up to **10 API keys**. All keys share the same account balance, usage limits, and spending limits.

## Revoking a Key

Revoking a key disables it immediately. Revoked keys can be re-enabled later from the dashboard. Use this to temporarily disable a key without deleting it.

## Deleting a Key

Deleting a key permanently removes it. This cannot be undone. Any application using the deleted key will start receiving `401` errors.

## Best Practices

**Use separate keys for different applications** - This makes it easy to revoke access for a specific app without affecting others.

**Never commit keys to source control** - Store your API key in environment variables or a secrets manager. Don't hard-code it in your application.

**Rotate keys periodically** - Create a new key, update your application, then delete the old key.

**Revoke unused keys** - If a key is no longer in use, revoke or delete it to reduce your attack surface.

## Using Your Key

Pass your API key in the `X-API-Key` header:

```bash
curl "https://apidirect.io/v1/reddit/posts?query=test" \
  -H "X-API-Key: ak_live_7f3a9b2c1d4e5f6a8b9c0d1e2f3a4b5c"
```

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/posts",
    headers={"X-API-Key": "ak_live_7f3a9b2c1d4e5f6a8b9c0d1e2f3a4b5c"},
    params={"query": "test"}
)
```
