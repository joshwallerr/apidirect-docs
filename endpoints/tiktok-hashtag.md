# TikTok Hashtag Details

Get a hashtag's details by name, numeric hashtag ID, or hashtag URL. Returns its ID, video count, total views, description, and cover image.

## Endpoint

```
GET /v1/tiktok/hashtag
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `name`, `hashtag_id`, or `url`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `name` | One required | Hashtag name, with or without leading `#` (max 100 characters). |
| `hashtag_id` | One required | Numeric hashtag ID, as returned by [Search Hashtags](/docs/tiktok-hashtags). |
| `url` | One required | TikTok hashtag URL, e.g. `https://www.tiktok.com/tag/cooking` (max 500 characters). |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `hashtag` | object | Hashtag data |
| `hashtag.hashtag_id` | string | Numeric hashtag ID |
| `hashtag.name` | string | Hashtag name, without the # |
| `hashtag.description` | string | Hashtag description, or empty string |
| `hashtag.video_count` | integer | Number of videos using the hashtag |
| `hashtag.views` | integer | Total views across the hashtag's videos |
| `hashtag.is_commerce` | boolean | Whether TikTok flags the hashtag as commercial |
| `hashtag.cover` | string | Cover image URL, or empty string |
| `hashtag.url` | string | Link to the hashtag page |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/hashtag?name=cooking" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/hashtag",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"name": "cooking"}
)
print(response.json())
```

## Example Response

```json
{
  "hashtag": {
    "hashtag_id": "18973",
    "name": "cooking",
    "description": "",
    "video_count": 19318490,
    "views": 555119436497,
    "is_commerce": false,
    "cover": "https://p16-common-sign.tiktokcdn.com/.../cover.jpeg",
    "url": "https://www.tiktok.com/tag/cooking"
  }
}
```
