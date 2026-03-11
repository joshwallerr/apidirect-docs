# Twitter Trends

Get the current trending topics for a specific location on Twitter/X. Returns trend names, search queries, and tweet volumes where available.

## Endpoint

```
GET /v1/twitter/trends
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `woeid` | Yes | Where On Earth ID for the location. Use `1` for Worldwide. |

## WOEID Locations

Download the full list of 467 available locations with their WOEID values:

**[Download twitter-trends-locations.json](https://apidirect.io/static/twitter-trends-locations.json)**

Common WOEIDs:

| Location | WOEID |
|----------|-------|
| Worldwide | `1` |
| United States | `23424977` |
| United Kingdom | `23424975` |
| Canada | `23424775` |
| Australia | `23424748` |
| India | `23424848` |
| Japan | `23424856` |
| Germany | `23424829` |
| France | `23424819` |
| Brazil | `23424768` |
| New York | `2459115` |
| Los Angeles | `2442047` |
| London | `44418` |
| Tokyo | `1118370` |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `trends` | array | Array of trending topics |
| `trends[].name` | string | Trend name or hashtag |
| `trends[].query` | string | URL-encoded search query |
| `trends[].tweet_volume` | integer/null | Estimated tweet volume (null when unavailable) |
| `trends[].url` | string | Twitter search URL for this trend |
| `location` | string | Name of the location |
| `woeid` | integer | WOEID used |
| `as_of` | string | Timestamp of when trends were captured |
| `count` | integer | Number of trends returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/twitter/trends?woeid=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/twitter/trends",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"woeid": 1}
)
print(response.json())
```

## Example Response

```json
{
  "trends": [
    {
      "name": "#TrendingTopic",
      "query": "%23TrendingTopic",
      "tweet_volume": 125000,
      "url": "http://twitter.com/search?q=%23TrendingTopic"
    },
    {
      "name": "Breaking News",
      "query": "%22Breaking+News%22",
      "tweet_volume": null,
      "url": "http://twitter.com/search?q=%22Breaking+News%22"
    }
  ],
  "location": "Worldwide",
  "woeid": 1,
  "as_of": "2026-03-05T01:23:37Z",
  "count": 50
}
```
