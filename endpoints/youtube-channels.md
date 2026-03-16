# YouTube Channels

Search YouTube channels by keyword. Returns channel name, description, subscriber count, and thumbnail. Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/youtube/channels
```

**Price:** $0.005 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `channels` | array | Array of matching channels |
| `channels[].channel_id` | string | YouTube channel ID |
| `channels[].title` | string | Channel name |
| `channels[].description` | string | Channel description |
| `channels[].subscriber_count` | string/null | Subscriber count (e.g., `"1.14K"`, `"6.44M"`) |
| `channels[].thumbnail` | string | URL to channel avatar |
| `channels[].url` | string | Link to the channel |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/youtube/channels?query=AI&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/youtube/channels",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "AI",
        "pages": 1
    }
)
print(response.json())
```

## Example Response

```json
{
  "channels": [
    {
      "channel_id": "UCLKPca3kwwd-B59HNr-_lvA",
      "title": "AI Engineer",
      "description": "Talks, workshops, events, and training for AI Engineers.",
      "subscriber_count": "377K",
      "thumbnail": "https://yt3.ggpht.com/.../photo.jpg",
      "url": "https://youtube.com/channel/UCLKPca3kwwd-B59HNr-_lvA"
    }
  ],
  "pages": 1,
  "count": 20
}
```
