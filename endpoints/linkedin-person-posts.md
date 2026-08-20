# LinkedIn Person Posts

Get the recent posts authored by a LinkedIn person (their profile feed) by profile URL or public slug. Returns post content, engagement metrics (likes, comments, shares, reaction breakdowns), author info, images, videos, and articles.

## Endpoint

```
GET /v1/linkedin/person/posts
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | Yes | LinkedIn profile URL or public slug — e.g. `https://www.linkedin.com/in/williamhgates` or just `williamhgates` (max 500 characters) |
| `page` | No | Page number, 1-5 (default: 1). 20 posts per page — returns up to ~100 of the person's most recent posts. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of the person's posts |
| `posts[].url` | string | Post URL |
| `posts[].text` | string | Full post text content |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Author name |
| `posts[].author_description` | string | Author headline (e.g. job title or follower count) |
| `posts[].author_image` | string | Author profile image URL |
| `posts[].author_url` | string | Author profile URL |
| `posts[].likes` | integer | Total number of reactions |
| `posts[].comments` | integer | Number of comments |
| `posts[].shares` | integer | Number of reposts/shares |
| `posts[].reactions` | object | Breakdown of reaction types and counts |
| `posts[].is_repost` | boolean | Whether the post is a repost or quote-reshare |
| `posts[].images` | array | Array of image URLs |
| `posts[].video` | object/null | Video content with `thumbnail` and `duration` (ms) |
| `posts[].article` | object/null | Shared article with `title`, `subtitle`, `url`, `description` |
| `posts[].urn` | string | LinkedIn post URN identifier |
| `posts[].source` | string | `"LinkedIn"` |
| `posts[].domain` | string | `"linkedin.com"` |
| `posts[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `posts[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `posts[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `posts[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `posts[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `page` | integer | Current page number |
| `count` | integer | Number of posts returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/linkedin/person/posts?url=williamhgates&page=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/linkedin/person/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "url": "williamhgates",
        "page": 1
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "url": "https://www.linkedin.com/posts/williamhgates_activity-7474530647273934848-VLxg",
      "text": "I got involved in global health back in 1997...",
      "date": "2026-06-21 18:36:16",
      "author": "Bill Gates",
      "author_description": "Chair, Gates Foundation and Founder, Breakthrough Energy",
      "author_image": "https://media.licdn.com/dms/image/...",
      "author_url": "https://www.linkedin.com/in/williamhgates",
      "likes": 3706,
      "comments": 368,
      "shares": 28,
      "reactions": {
        "like": 3290,
        "appreciation": 145,
        "empathy": 168
      },
      "is_repost": false,
      "images": [],
      "video": {
        "thumbnail": "https://media.licdn.com/dms/image/...",
        "duration": 83600
      },
      "article": null,
      "urn": "urn:li:activity:7474530647273934848"
    }
  ],
  "page": 1,
  "count": 20
}
```
