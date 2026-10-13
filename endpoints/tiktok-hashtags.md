# Search TikTok Hashtags

Search TikTok hashtags by keyword. Returns each hashtag's ID, name, video count, total views, and cover image, 30 per page.

## Endpoint

```
GET /v1/tiktok/hashtags
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-1000 (default: 1). Each page returns up to 30 hashtags. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `hashtags` | array | Array of matching hashtags, most relevant first |
| `hashtags[].hashtag_id` | string | Numeric hashtag ID |
| `hashtags[].name` | string | Hashtag name, without the # |
| `hashtags[].description` | string | Hashtag description, or empty string |
| `hashtags[].video_count` | integer | Number of videos using the hashtag |
| `hashtags[].views` | integer | Total views across the hashtag's videos |
| `hashtags[].is_commerce` | boolean | Whether TikTok flags the hashtag as commercial |
| `hashtags[].cover` | string | Cover image URL, or empty string |
| `hashtags[].url` | string | Link to the hashtag page |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/hashtags?query=cooking&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/hashtags",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "cooking",
        "pages": 2
    }
)
print(response.json())
```

## Example Response

```json
{
  "hashtags": [
    {
      "hashtag_id": "18973",
      "name": "cooking",
      "description": "",
      "video_count": 19318490,
      "views": 555119436497,
      "is_commerce": false,
      "cover": "https://p16-common-sign.tiktokcdn.com/.../cover.jpeg",
      "url": "https://www.tiktok.com/tag/cooking"
    },
    {
      "hashtag_id": "8620710",
      "name": "cookingtips",
      "description": "",
      "video_count": 622053,
      "views": 12157160228,
      "is_commerce": false,
      "cover": "https://p16-common-sign.tiktokcdn.com/.../cover.jpeg",
      "url": "https://www.tiktok.com/tag/cookingtips"
    }
  ],
  "pages": 2,
  "count": 60
}
```
