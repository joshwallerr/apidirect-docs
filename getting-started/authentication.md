# Authentication

All API requests require authentication using an API key passed in the `X-API-Key` header.

## The X-API-Key Header

Include your API key in every request:

```bash
curl "https://apidirect.io/v1/reddit/posts?query=test" \
  -H "X-API-Key: ak_live_abc123..."
```

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/posts",
    headers={"X-API-Key": "ak_live_abc123..."},
    params={"query": "test"}
)
```

## Key Format

API keys follow the format `ak_live_` followed by a random string. For example:

```
ak_live_7f3a9b2c1d4e5f6a8b9c0d1e2f3a4b5c
```

## Managing Keys

You can create and manage API keys from your [dashboard](https://apidirect.io/dashboard/keys):

- **Create** up to 10 keys per account
- **Revoke** a key to immediately disable it (can be re-enabled later)
- **Delete** a key to permanently remove it

See [API Keys](../account/api-keys.md) for more details on key management.

## Error Responses

If authentication fails, you'll receive one of these responses:

**Missing API key** (no header provided):

```json
{
  "error": "Missing API key",
  "code": "missing_api_key"
}
```
Status: `401`

**Invalid API key** (key not found or deleted):

```json
{
  "error": "Invalid API key",
  "code": "invalid_api_key"
}
```
Status: `401`

**Account blocked** (payment failure):

```json
{
  "error": "Account blocked due to payment failure. Please update your payment method.",
  "code": "account_blocked"
}
```
Status: `403`
