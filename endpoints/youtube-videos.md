# YouTube Videos

Search YouTube videos by keyword. Returns video title, URL, channel name, publication date, and description. Supports filtering by upload date and fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/youtube/posts
```

**Price:** $0.005 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |
| `upload_date` | No | Filter by upload date: `last_hour`, `today`, `this_week`, `this_month`, `this_year` |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching videos |
| `posts[].title` | string | Video title |
| `posts[].url` | string | Direct link to the video |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Channel name |
| `posts[].source` | string | `"YouTube"` |
| `posts[].snippet` | string | Video description text |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/youtube/posts?query=tutorial&pages=2&upload_date=this_week" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/youtube/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "tutorial",
        "pages": 2,
        "upload_date": "this_week"
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "title": "Tutorial Video Title",
      "url": "https://youtube.com/watch?v=...",
      "date": "2024-01-15 14:30:00",
      "author": "Channel Name",
      "source": "YouTube",
      "snippet": "Video description..."
    }
  ],
  "pages": 2,
  "count": 20
}
```
