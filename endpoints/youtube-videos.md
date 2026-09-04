# YouTube Videos

Search YouTube videos by keyword. Returns video title, URL, channel name, publication date, description, view count, video length, thumbnail, and more. Supports filtering by upload date and fetching multiple pages in a single API call.

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
| `pages` | No | Number of pages to fetch, 1-20 (default: 1) |
| `upload_date` | No | Filter by upload date: `last_hour`, `today`, `this_week`, `this_month`, `this_year` |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching videos |
| `posts[].title` | string | Video title |
| `posts[].url` | string | Direct link to the video |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Channel name |
| `posts[].source` | string | `"YouTube"` or `"YouTube Shorts"` |
| `posts[].domain` | string | `"youtube.com"` |
| `posts[].snippet` | string | Video description text |
| `posts[].views` | integer/null | Number of views (`null` when unavailable) |
| `posts[].video_length` | string/null | Video duration (e.g., `"14:45"`). `null` for Shorts. |
| `posts[].video_id` | string | YouTube video ID |
| `posts[].channel_id` | string | YouTube channel ID |
| `posts[].is_live` | boolean/null | Whether the video is live content |
| `posts[].type` | string | Video type (e.g., `"NORMAL"`) |
| `posts[].keywords` | string[] | Video keywords/tags |
| `posts[].thumbnail` | string | URL to the highest resolution thumbnail |
| `posts[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `posts[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `posts[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `posts[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `posts[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
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
      "url": "https://youtube.com/watch?v=dQw4w9WgXcQ",
      "date": "2024-01-15 14:30:00",
      "author": "Channel Name",
      "source": "YouTube",
      "domain": "youtube.com",
      "snippet": "Video description...",
      "views": 86979,
      "video_length": "14:45",
      "video_id": "dQw4w9WgXcQ",
      "channel_id": "UCeMcDx6-rOq_RlKSPehk2tQ",
      "is_live": null,
      "type": "NORMAL",
      "keywords": [],
      "thumbnail": "https://i.ytimg.com/vi/dQw4w9WgXcQ/hq720.jpg",
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
