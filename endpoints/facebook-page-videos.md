# Facebook Page Videos

Get videos from a Facebook page. Requires the delegate_page_id which can be obtained from the page details endpoint. Returns video metadata and play counts. Supports fetching multiple pages in a single call.

## Endpoint

```
GET /v1/facebook/page/videos
```

**Price:** $0.008 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `delegate_page_id` | Yes | Delegate page ID (get from the page details endpoint `delegate_page_id` field) |
| `pages` | No | Number of pages to fetch (1-10, default 1). Billed per page. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `videos` | array | List of video objects |
| `videos[].video_id` | string | Unique video ID |
| `videos[].url` | string | URL to the video on Facebook |
| `videos[].description` | string | Video description |
| `videos[].thumbnail` | string | URL to the video thumbnail image |
| `videos[].play_count` | integer | Number of video plays |
| `videos[].date` | string | Formatted date (YYYY-MM-DD HH:MM:SS) |
| `videos[].timestamp` | integer | Unix timestamp |
| `count` | integer | Number of videos returned |
| `pages` | integer | Number of pages fetched |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/page/videos?delegate_page_id=20531316728" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/page/videos",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"delegate_page_id": "20531316728"}
)
print(response.json())
```

## Example Response

```json
{
  "videos": [
    {
      "video_id": "1312587094016698",
      "url": "https://www.facebook.com/watch/?v=1312587094016698",
      "description": "Welcome to K-Ville, Duke University's legendary tent city where students camp out for weeks just to score basketball tickets.",
      "thumbnail": "https://scontent.xx.fbcdn.net/v/t15.5256-10/646502_..._n.jpg",
      "play_count": 1096104,
      "date": "2026-03-07 17:21:49",
      "timestamp": 1772904109
    },
    {
      "video_id": "1610049803578776",
      "url": "https://www.facebook.com/watch/?v=1610049803578776",
      "description": "No mascots were harmed during the making of this prank.",
      "thumbnail": "https://scontent.xx.fbcdn.net/v/t15.5256-10/644973_..._n.jpg",
      "play_count": 631559,
      "date": "2026-03-05 21:51:45",
      "timestamp": 1772747505
    }
  ],
  "count": 2,
  "pages": 1
}
```
