# Forum Posts

Search forum posts across discussion boards, Q&A sites, and community forums. Returns post title, URL, source domain, and content snippet. Supports filtering by time period and country.

## Endpoint

```
GET /v1/forums/posts
```

**Price:** $0.008 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `page` | No | Page number for pagination (default: 1) |
| `time` | No | Time filter: `any`, `hour`, `day`, `week`, `month`, `year` (default: `any`) |
| `country` | No | ISO 3166-1 alpha-2 country code (e.g., `US`, `GB`, `DE`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching forum posts |
| `posts[].position` | integer | Result ranking position |
| `posts[].rank` | integer | Result rank value |
| `posts[].title` | string | Post or thread title |
| `posts[].url` | string | Direct link to the post |
| `posts[].source` | string | Source name or forum domain |
| `posts[].domain` | string | Forum domain name |
| `posts[].snippet` | string | Post content preview |
| `page` | integer | Current page number |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/forums/posts?query=programming&time=week&country=US" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/forums/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "programming",
        "time": "week",
        "country": "US"
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "position": 1,
      "rank": 1,
      "title": "Discussion about programming",
      "url": "https://forum.example.com/thread/...",
      "source": "forum.example.com",
      "domain": "forum.example.com",
      "snippet": "Forum post content..."
    }
  ],
  "page": 1,
  "count": 10
}
```
