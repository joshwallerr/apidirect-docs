# Truth Social User Posts

Get a user's recent posts (their feed) by username. Returns post text, engagement metrics (replies, reposts, likes), media attachments, hashtags, and reply status. Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/truthsocial/user/posts
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | Yes | Truth Social username, with or without leading `@` (max 100 characters). |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1). Each page returns up to 20 posts. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of the user's recent posts |
| `posts[].title` | string | Post title (format: `@username on Truth Social`) |
| `posts[].url` | string | Direct link to the post |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Truth Social username |
| `posts[].source` | string | `"Truth Social"` |
| `posts[].domain` | string | `"truthsocial.com"` |
| `posts[].snippet` | string | Post text with formatting removed |
| `posts[].likes` | integer | Number of likes |
| `posts[].replies` | integer | Number of replies |
| `posts[].reposts` | integer | Number of reposts |
| `posts[].post_id` | string | Truth Social post ID |
| `posts[].content_html` | string | Original post body as HTML, with links and mentions preserved |
| `posts[].media` | array | Media attachments, each with `media_id`, `type` (e.g. `image`, `video`), `url`, and `description` |
| `posts[].hashtags` | string[] | Hashtags used in the post |
| `posts[].language` | string | Detected language code (empty when not detected) |
| `posts[].visibility` | string | Post visibility (e.g. `public`) |
| `posts[].sensitive` | boolean | Whether the post is marked sensitive |
| `posts[].spoiler_text` | string | Content warning text (empty when none) |
| `posts[].sponsored` | boolean | Whether the post is sponsored |
| `posts[].is_reply` | boolean | Whether the post is a reply to another post |
| `posts[].in_reply_to_id` | string | ID of the post being replied to (empty when not a reply) |
| `posts[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `posts[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `posts[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `posts[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `posts[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `username` | string | The username the feed was fetched for |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/truthsocial/user/posts?username=realDonaldTrump&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/truthsocial/user/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "username": "realDonaldTrump",
        "pages": 2
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "title": "@realDonaldTrump on Truth Social",
      "url": "https://truthsocial.com/@realDonaldTrump/117043133534824966",
      "date": "2026-08-05 13:28:05",
      "author": "realDonaldTrump",
      "source": "Truth Social",
      "domain": "truthsocial.com",
      "snippet": "Thank you for your attention to this matter! President DJT",
      "likes": 5514,
      "replies": 567,
      "reposts": 1399,
      "post_id": "117043133534824966",
      "content_html": "<p>Thank you for your attention to this matter! President DJT</p>",
      "media": [
        {
          "media_id": "117041192378469520",
          "type": "video",
          "url": "https://static-assets-1.truthsocial.com/media_attachments/files/117/041/192/original/9cbc020383d40cd5.mp4",
          "description": ""
        }
      ],
      "hashtags": [],
      "language": "en",
      "visibility": "public",
      "sensitive": false,
      "spoiler_text": "",
      "sponsored": false,
      "is_reply": false,
      "in_reply_to_id": ""
    }
  ],
  "username": "realDonaldTrump",
  "pages": 2,
  "count": 40
}
```

## Notes

- Posts are returned newest first, up to 20 per page. Use `pages` (1-10) to fetch more in a single call; you are billed per page requested.
- A user's feed can include their original posts and their replies. Use `is_reply` to distinguish them.
- `snippet` is the post text with formatting stripped. Use `content_html` when you need the original links and mentions.
