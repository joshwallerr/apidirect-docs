# Instagram Post Comments

Get the comments on an Instagram post or reel by URL or shortcode. Returns each comment's text, author, like and reply counts, and date. Supports sorting by popular or recent, and pagination.

## Endpoint

```
GET /v1/instagram/post/comments
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Instagram post or reel URL, e.g. `https://www.instagram.com/p/CxYQJO8xuC6/` (max 500 characters). Provide either `url` or `code`. |
| `code` | One required | The post's shortcode, e.g. `CxYQJO8xuC6`, or numeric media ID (max 50 characters). Provide either `url` or `code`. |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1). Each page returns up to 15 comments. |
| `sort_by` | No | Sort order: `popular` or `recent` (default: `popular`) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `comments` | array | Array of top-level comments |
| `comments[].comment_id` | string | Unique comment ID |
| `comments[].text` | string | Comment text |
| `comments[].author` | string | Commenter's Instagram username |
| `comments[].author_name` | string | Commenter's display name |
| `comments[].author_id` | string | Commenter's Instagram user ID |
| `comments[].author_verified` | boolean | Whether the commenter is verified |
| `comments[].author_url` | string | Link to the commenter's profile |
| `comments[].author_profile_pic_url` | string | Commenter's profile picture URL |
| `comments[].likes` | integer | Number of likes |
| `comments[].reply_count` | integer | Number of replies |
| `comments[].is_pinned` | boolean | Whether the comment is pinned |
| `comments[].hashtags` | string[] | Hashtags used in the comment |
| `comments[].mentions` | string[] | Usernames mentioned in the comment |
| `comments[].date` | string | Publication date and time |
| `comments[].date_timestamp` | integer/null | Publication date as a Unix timestamp |
| `comments[].url` | string | Direct link to the comment (empty when the post was given by media ID) |
| `comments[].source` | string | `"Instagram"` |
| `comments[].domain` | string | `"instagram.com"` |
| `comments[].gif_url` | string/null | GIF URL for GIF comments (`null` otherwise) |
| `comments[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `comments[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `comments[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `comments[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `comments[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `code` | string | The post's shortcode (or media ID, if that was passed) |
| `total` | integer | Total number of comments on the post |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Number of comments returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/instagram/post/comments?code=CxYQJO8xuC6&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/instagram/post/comments",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "code": "CxYQJO8xuC6",
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
      "comment_id": "18058799162049620",
      "text": "Nice post!",
      "author": "garcia99.r",
      "author_name": "Robert Garcia",
      "author_id": "72771312829",
      "author_verified": false,
      "author_url": "https://instagram.com/garcia99.r",
      "author_profile_pic_url": "https://scontent.cdninstagram.com/v/t51.89012-19/photo.jpg",
      "likes": 23,
      "reply_count": 0,
      "is_pinned": false,
      "hashtags": [],
      "mentions": [],
      "date": "2025-03-09 13:20:14",
      "date_timestamp": 1741524014,
      "url": "https://www.instagram.com/p/CxYQJO8xuC6/c/18058799162049620/",
      "source": "Instagram",
      "domain": "instagram.com",
      "gif_url": null
    }
  ],
  "code": "CxYQJO8xuC6",
  "total": 4006,
  "pages": 2,
  "count": 23
}
```

## Notes

- Returns top-level comments only. Use `comment_id` with the [Comment Replies](/docs/instagram-comment-replies) endpoint to get a comment's replies.
- Each page returns up to 15 comments; you are billed per page requested. `sort_by=popular` includes pinned comments.
