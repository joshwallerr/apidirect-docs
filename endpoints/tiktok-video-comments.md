# TikTok Video Comments

Get the top-level comments on a video, in TikTok's default order, by video URL or numeric video ID. Returns each comment's text, author, like and reply counts, and date, 50 per page.

## Endpoint

```
GET /v1/tiktok/video/comments
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `url` or `video_id`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | TikTok video URL, e.g. `https://www.tiktok.com/@tiktok/video/7516594811734854943` (max 500 characters). Short links are accepted. |
| `video_id` | One required | Numeric TikTok video ID: the number at the end of a video URL. |
| `pages` | No | Number of pages to fetch, 1-1000 (default: 1). Each page returns up to 50 comments. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `comments` | array | Array of top-level comments, in TikTok's default order |
| `comments[].comment_id` | string | Unique comment ID |
| `comments[].video_id` | string | ID of the video the comment is on |
| `comments[].text` | string | Comment text |
| `comments[].images` | string[] | Image URLs attached to the comment; usually empty |
| `comments[].likes` | integer | Number of likes |
| `comments[].date` | string | Publication date and time |
| `comments[].date_timestamp` | integer/null | Publication date as a Unix timestamp |
| `comments[].author` | string | Commenter's TikTok username |
| `comments[].author_name` | string | Commenter's display name |
| `comments[].author_id` | string | Commenter's numeric user ID |
| `comments[].author_avatar` | string | Commenter's avatar URL |
| `comments[].author_url` | string | Link to the commenter's profile |
| `comments[].author_verified` | boolean | Whether the commenter is verified |
| `comments[].author_bio` | string | Commenter's profile bio |
| `comments[].author_region` | string | 2-letter region code of the commenter |
| `comments[].source` | string | `"TikTok"` |
| `comments[].domain` | string | `"tiktok.com"` |
| `comments[].reply_count` | integer | Number of replies to the comment |
| `comments[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `comments[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `comments[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `comments[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `comments[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `video_id` | string | The video's numeric ID |
| `total` | integer | Total number of comments on the video, as reported by TikTok |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

TikTok exposes roughly the first 450 comments of a video, however large `total` is. Use `comment_id` with [Comment Replies](/docs/tiktok-comment-replies) to get a comment's thread.

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/video/comments?url=https://www.tiktok.com/@tiktok/video/7516594811734854943&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/video/comments",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "url": "https://www.tiktok.com/@tiktok/video/7516594811734854943",
        "pages": 2
    }
)
print(response.json())
```

## Example Response

```json
{
  "comments": [
    {
      "comment_id": "7516998696283505430",
      "video_id": "7516594811734854943",
      "text": "Bring back the symphony trend rn",
      "images": [],
      "likes": 11379,
      "date": "2025-06-17 19:14:14",
      "date_timestamp": 1750187654,
      "author": "izzy_0104",
      "author_name": "Izzy",
      "author_id": "80504510963429376",
      "author_avatar": "https://p19-common-sign.tiktokcdn-us.com/.../avatar.jpeg",
      "author_url": "https://www.tiktok.com/@izzy_0104",
      "author_verified": false,
      "author_bio": "19",
      "author_region": "GB",
      "source": "TikTok",
      "domain": "tiktok.com",
      "reply_count": 6
    }
  ],
  "video_id": "7516594811734854943",
  "total": 4368,
  "pages": 2,
  "count": 100
}
```
