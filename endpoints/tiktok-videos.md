# TikTok Videos

Search TikTok videos by keyword. Returns video title, URL, engagement metrics (plays, likes, comments, shares, downloads), author metadata, music info, and publication date. Supports filtering by time period and region, and fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/tiktok/videos
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |
| `region` | No | 2-letter region code (e.g. `us`, `gb`, `jp`) |
| `publish_time` | No | Time filter: `0`=ALL, `1`=24h, `7`=week, `30`=month, `90`=3months, `180`=6months (default: 0) |
| `sort_by` | No | Sort order: `relevance`, `most_recent`, `most_liked` (default: relevance) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `videos` | array | Array of matching TikTok videos |
| `videos[].title` | string | Video title/caption |
| `videos[].url` | string | Direct link to the video |
| `videos[].date` | string | Publication date and time |
| `videos[].author` | string | TikTok username |
| `videos[].source` | string | `"TikTok"` |
| `videos[].domain` | string | `"tiktok.com"` |
| `videos[].snippet` | string | Video caption text |
| `videos[].play_count` | integer | Number of plays/views |
| `videos[].likes` | integer | Number of likes |
| `videos[].comments` | integer | Number of comments |
| `videos[].shares` | integer | Number of shares |
| `videos[].downloads` | integer | Number of downloads |
| `videos[].duration` | integer | Video duration in seconds |
| `videos[].is_ad` | boolean | Whether the video is an ad |
| `videos[].author_name` | string | Author's display name |
| `videos[].author_avatar` | string | Author's avatar URL |
| `videos[].cover` | string | Video cover/thumbnail URL |
| `videos[].music_title` | string | Title of the music used |
| `videos[].music_author` | string | Author of the music used |
| `videos[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `videos[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `videos[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `videos[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `videos[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/videos?query=cooking&pages=2&region=us&sort_by=relevance" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/videos",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "cooking",
        "pages": 2,
        "region": "us",
        "sort_by": "relevance"
    }
)
print(response.json())
```

## Example Response

```json
{
  "videos": [
    {
      "title": "Easy pasta recipe you need to try #cooking #recipe",
      "url": "https://www.tiktok.com/@chefmike/video/7312345678901234567",
      "date": "2026-02-20 18:45:30",
      "author": "chefmike",
      "source": "TikTok",
      "domain": "tiktok.com",
      "snippet": "Easy pasta recipe you need to try #cooking #recipe",
      "play_count": 2450000,
      "likes": 185000,
      "comments": 3200,
      "shares": 12500,
      "downloads": 8400,
      "duration": 45,
      "is_ad": false,
      "author_name": "Chef Mike",
      "author_avatar": "https://p16-sign.tiktokcdn.com/...",
      "cover": "https://p16-sign.tiktokcdn.com/...",
      "music_title": "original sound",
      "music_author": "chefmike",
      "sentiment": {
        "emotions": {
          "joy": 40,
          "trust": 55,
          "fear": 0,
          "surprise": 10,
          "sadness": 0,
          "disgust": 0,
          "anger": 0,
          "anticipation": 30
        },
        "dominant_emotion": "trust",
        "emotional_intensity": 5,
        "polarity": "positive"
      }
    }
  ],
  "pages": 2,
  "count": 20
}
```
