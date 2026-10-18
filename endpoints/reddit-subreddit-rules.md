# Reddit Subreddit Rules

Get a subreddit's rules by name or URL, in the order the subreddit lists them, with what each rule covers and the report reason moderators use.

## Endpoint

```
GET /v1/reddit/subreddit/rules
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `subreddit` | One required | Subreddit name, with or without `r/`, e.g. `Python`. Provide exactly one of `subreddit` or `url`. |
| `url` | One required | Subreddit URL, e.g. `https://www.reddit.com/r/Python/` (max 500 characters). Provide exactly one of `subreddit` or `url`. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `rules` | array | The subreddit's rules, in order |
| `rules[].priority` | integer | Position in the rules list, starting at 0 |
| `rules[].title` | string | Rule title |
| `rules[].description` | string | Rule text (Markdown) |
| `rules[].applies_to` | string | What the rule covers: `link` (posts), `comment` or `all` |
| `rules[].violation_reason` | string | Reason shown when content is reported under the rule |
| `rules[].created_at` | string | When the rule was added (UTC) |
| `subreddit` | string | The subreddit name |
| `count` | integer | Number of rules returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/subreddit/rules?subreddit=Python" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/subreddit/rules",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "subreddit": "Python"
    }
)
print(response.json())
```

## Example Response

```json
{
  "rules": [
    {
      "priority": 0,
      "title": "No showcase posts",
      "description": "Due to an increase of showcases featuring AI content such as working with multiple AI models or wrappers around APIs, this is no longer allowed. Please post...",
      "applies_to": "link",
      "violation_reason": "No showcase posts",
      "created_at": "2024-08-03 05:47:33"
    }
  ],
  "subreddit": "Python",
  "count": 11
}
```

## Notes

- An unknown subreddit returns an empty `rules` list; a private or banned one returns 404 `not_found`.
