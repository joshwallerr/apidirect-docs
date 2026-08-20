# Batch Requests

Instead of looping an endpoint over a list of IDs, URLs or usernames, send up to 100 requests in a single call:

```
POST /v1/batch
```

Any mix of endpoints is allowed. Items run concurrently server-side (up to roughly half your per-endpoint concurrency limit at a time; the rest queue) and each returns its own status and body, in input order.

Batching is free — each item bills under its own endpoint at its normal rate, and consumes that endpoint's free tier, exactly as a direct call. Available over MCP as the `batch_requests` tool.

## Request Body

JSON object with a `requests` array of 1–100 items.

| Field | Required | Description |
|-----------|----------|-------------|
| `requests` | Yes | Array of 1–100 items to execute |
| `requests[].endpoint` | Yes | The `/v1` endpoint path to call (e.g. `/v1/twitter/user`). Every endpoint is supported except `/v1/web/ai-mode` |
| `requests[].params` | No | The same parameters the endpoint accepts when called directly. Values must be strings or numbers |
| `requests[].tag` | No | Optional label (max 100 characters) echoed back on the item's result |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `results` | array | Per-item results, in input order |
| `results[].index` | integer | Position of the item in the `requests` array |
| `results[].endpoint` | string | The endpoint the item called |
| `results[].tag` | string | The item's tag (when one was sent) |
| `results[].status` | integer | The item's HTTP status: 200 success; 4xx/5xx the endpoint's normal error; 0 the item was not attempted (failed, never billed) |
| `results[].body` | object | Exactly what the endpoint returns when called directly |
| `summary.total` | integer | Number of items in the batch |
| `summary.succeeded` | integer | Items that returned 2xx |
| `summary.failed` | integer | Items that did not succeed (failed items are never billed) |
| `summary.duration_ms` | integer | Total batch execution time |

## Example Request

### cURL

```bash
curl -X POST "https://apidirect.io/v1/batch" \
  -H "X-API-Key: YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"requests": [
    {"endpoint": "/v1/twitter/user", "params": {"username": "naval"}},
    {"endpoint": "/v1/twitter/user", "params": {"username": "paulg"}},
    {"endpoint": "/v1/instagram/user", "params": {"username": "instagram"}}
  ]}'
```

### Python

```python
import requests

response = requests.post(
    "https://apidirect.io/v1/batch",
    headers={"X-API-Key": "YOUR_API_KEY"},
    json={"requests": [
        {"endpoint": "/v1/twitter/user", "params": {"username": "naval"}},
        {"endpoint": "/v1/twitter/user", "params": {"username": "paulg"}},
        {"endpoint": "/v1/instagram/user", "params": {"username": "instagram"}},
    ]},
    timeout=780,
)
for item in response.json()["results"]:
    print(item["endpoint"], item["status"])
```

## Example Response

```json
{
  "results": [
    {
      "index": 0,
      "endpoint": "/v1/twitter/user",
      "status": 200,
      "body": {
        "user": {
          "name": "Naval",
          "username": "naval",
          "followers": 2100000
        }
      }
    },
    {
      "index": 1,
      "endpoint": "/v1/twitter/user",
      "status": 200,
      "body": { "user": { "name": "Paul Graham", "username": "paulg" } }
    },
    {
      "index": 2,
      "endpoint": "/v1/instagram/user",
      "status": 200,
      "body": { "user": { "username": "instagram" } }
    }
  ],
  "summary": {
    "total": 3,
    "succeeded": 3,
    "failed": 0,
    "duration_ms": 4200
  }
}
```

## Notes

- **Billing** — batching is free. Each item bills exactly like a direct call: same price, same free tier, same spending limits. Failed items are never billed.
- **Concurrency** — items run in parallel at up to roughly half your per-endpoint concurrency limit; the rest queue and start as slots free.
- **Isolation** — one item failing never affects the others. Each result is exactly what its endpoint would return directly, and rate-limited items are retried automatically.
- **Failed items** — any item that fails, including items the batch could not get to, returns an error body with a `code` and is never billed.