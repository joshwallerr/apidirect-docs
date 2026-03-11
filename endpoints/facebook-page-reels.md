# Facebook Page Reels

Get reels from a Facebook page. Requires the reels_page_id which can be obtained from the page details endpoint. Returns reel metadata and engagement metrics. Supports fetching multiple pages in a single call.

## Endpoint

```
GET /v1/facebook/page/reels
```

**Price:** $0.008 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `reels_page_id` | Yes | Reels page ID (get from the page details endpoint `reels_page_id` field) |
| `pages` | No | Number of pages to fetch (1-10, default 1). Billed per page. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `reels` | array | List of reel objects |
| `reels[].video_id` | string | Unique video ID |
| `reels[].post_id` | string | Associated post ID |
| `reels[].url` | string | URL to the reel on Facebook |
| `reels[].description` | string | Reel description / caption |
| `reels[].date` | string | Human-readable date |
| `reels[].timestamp` | integer | Unix timestamp |
| `reels[].length_in_seconds` | number | Duration of the reel in seconds |
| `reels[].play_count` | integer | Number of plays |
| `reels[].comments_count` | integer | Number of comments |
| `reels[].reactions_count` | integer | Total number of reactions |
| `reels[].reshare_count` | integer | Number of shares |
| `reels[].author_name` | string | Name of the reel author |
| `reels[].author_url` | string | URL to the author's profile |
| `reels[].thumbnail` | string | URL to the reel thumbnail image |
| `count` | integer | Number of reels returned |
| `pages` | integer | Number of pages fetched |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/page/reels?reels_page_id=YXBwX2NvbGxlY3Rpb246cGZiaWQwcTlLYm..." \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
# First, get the reels_page_id from the page details endpoint
details = requests.get(
    "https://apidirect.io/v1/facebook/page",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://www.facebook.com/facebook"}
).json()

reels_page_id = details["page"]["reels_page_id"]

response = requests.get(
    "https://apidirect.io/v1/facebook/page/reels",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"reels_page_id": reels_page_id}
)
print(response.json())
```

## Example Response

```json
{
  "reels": [
    {
      "video_id": "894523017483261",
      "post_id": "894523017483261_100064860875397",
      "url": "https://www.facebook.com/reel/894523017483261",
      "description": "What happens when you bring people together? Amazing things.",
      "date": "2025-12-08 16:45:00",
      "timestamp": 1733676300,
      "length_in_seconds": 28.4,
      "play_count": 1842093,
      "comments_count": 4312,
      "reactions_count": 67481,
      "reshare_count": 12094,
      "author_name": "Facebook",
      "author_url": "https://www.facebook.com/facebook",
      "thumbnail": "https://scontent.xx.fbcdn.net/v/t15.5256-10/894523_..._n.jpg"
    },
    {
      "video_id": "851749203847192",
      "post_id": "851749203847192_100064860875397",
      "url": "https://www.facebook.com/reel/851749203847192",
      "description": "3 features you probably didn't know about",
      "date": "2025-11-29 12:00:00",
      "timestamp": 1732881600,
      "length_in_seconds": 15.7,
      "play_count": 934571,
      "comments_count": 1829,
      "reactions_count": 42318,
      "reshare_count": 7203,
      "author_name": "Facebook",
      "author_url": "https://www.facebook.com/facebook",
      "thumbnail": "https://scontent.xx.fbcdn.net/v/t15.5256-10/851749_..._n.jpg"
    }
  ],
  "count": 2,
  "pages": 1
}
```
