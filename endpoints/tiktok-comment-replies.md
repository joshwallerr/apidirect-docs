# TikTok Comment Replies

Get the replies to one comment (its thread) by video URL or numeric video ID plus the comment ID. Returns each reply's text, author, like count, and date, about 50 per page.

## Endpoint

```
GET /v1/tiktok/comment/replies
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `url` or `video_id`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | TikTok video URL, e.g. `https://www.tiktok.com/@tiktok/video/7516594811734854943` (max 500 characters). Short links are accepted. |
| `video_id` | One required | Numeric TikTok video ID: the number at the end of a video URL. |
| `comment_id` | Yes | Numeric ID of the comment, as returned by [Video Comments](/docs/tiktok-video-comments) |
| `pages` | No | Number of pages to fetch, 1-1000 (default: 1). Each page returns up to 50 replies. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `replies` | array | Array of replies to the comment |
| `replies[].comment_id` | string | Unique comment ID |
| `replies[].video_id` | string | ID of the video the comment is on |
| `replies[].text` | string | Comment text |
| `replies[].images` | string[] | Image URLs attached to the comment; usually empty |
| `replies[].likes` | integer | Number of likes |
| `replies[].date` | string | Publication date and time |
| `replies[].date_timestamp` | integer/null | Publication date as a Unix timestamp |
| `replies[].author` | string | Commenter's TikTok username |
| `replies[].author_name` | string | Commenter's display name |
| `replies[].author_id` | string | Commenter's numeric user ID |
| `replies[].author_avatar` | string | Commenter's avatar URL |
| `replies[].author_url` | string | Link to the commenter's profile |
| `replies[].author_verified` | boolean | Whether the commenter is verified |
| `replies[].author_bio` | string | Commenter's profile bio |
| `replies[].author_region` | string | 2-letter region code of the commenter |
| `replies[].source` | string | `"TikTok"` |
| `replies[].domain` | string | `"tiktok.com"` |
| `replies[].parent_comment_id` | string | ID of the comment the reply belongs to |
| `replies[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `replies[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `replies[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `replies[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `replies[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `comment_id` | string | The requested comment ID |
| `video_id` | string | The video's numeric ID |
| `total` | integer | Total number of replies to the comment |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/comment/replies?url=https://www.tiktok.com/@tiktok/video/7516594811734854943&comment_id=7516700694288876344" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/comment/replies",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "url": "https://www.tiktok.com/@tiktok/video/7516594811734854943",
        "comment_id": "7516700694288876344"
    }
)
print(response.json())
```

## Example Response

```json
{
  "replies": [
    {
      "comment_id": "7517173688660394774",
      "video_id": "7516594811734854943",
      "text": "Nooooo",
      "images": [],
      "likes": 183,
      "date": "2025-06-18 06:33:27",
      "date_timestamp": 1750228407,
      "author": "kirstie_x1",
      "author_name": "kirstie_x1",
      "author_id": "6945571097887015941",
      "author_avatar": "https://p19-common-sign.tiktokcdn-us.com/.../avatar.jpeg",
      "author_url": "https://www.tiktok.com/@kirstie_x1",
      "author_verified": false,
      "author_bio": "Kirstie; 33",
      "author_region": "GB",
      "source": "TikTok",
      "domain": "tiktok.com",
      "parent_comment_id": "7516700694288876344"
    }
  ],
  "comment_id": "7516700694288876344",
  "video_id": "7516594811734854943",
  "total": 39,
  "pages": 1,
  "count": 39
}
```
