# Instagram Comment Replies

Get the replies to an Instagram comment by post URL or shortcode and comment ID. Returns each reply's text, author, like count, and date. Supports pagination.

## Endpoint

```
GET /v1/instagram/comment/replies
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Instagram post or reel URL, e.g. `https://www.instagram.com/p/CxYQJO8xuC6/` (max 500 characters). Provide either `url` or `code`. |
| `code` | One required | The post's shortcode, e.g. `CxYQJO8xuC6`, or numeric media ID (max 50 characters). Provide either `url` or `code`. |
| `comment_id` | Yes | The comment's numeric ID, from the Post Comments endpoint (max 50 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `replies` | array | Array of replies, oldest first |
| `replies[].comment_id` | string | Unique comment ID |
| `replies[].text` | string | Comment text |
| `replies[].author` | string | Commenter's Instagram username |
| `replies[].author_name` | string | Commenter's display name |
| `replies[].author_id` | string | Commenter's Instagram user ID |
| `replies[].author_verified` | boolean | Whether the commenter is verified |
| `replies[].author_url` | string | Link to the commenter's profile |
| `replies[].author_profile_pic_url` | string | Commenter's profile picture URL |
| `replies[].likes` | integer | Number of likes |
| `replies[].reply_count` | integer | Number of replies |
| `replies[].is_pinned` | boolean | Whether the comment is pinned |
| `replies[].hashtags` | string[] | Hashtags used in the comment |
| `replies[].mentions` | string[] | Usernames mentioned in the comment |
| `replies[].date` | string | Publication date and time |
| `replies[].date_timestamp` | integer/null | Publication date as a Unix timestamp |
| `replies[].url` | string | Direct link to the comment (empty when the post was given by media ID) |
| `replies[].source` | string | `"Instagram"` |
| `replies[].domain` | string | `"instagram.com"` |
| `replies[].gif_url` | string/null | GIF URL for GIF comments (`null` otherwise) |
| `replies[].parent_comment_id` | string | ID of the top-level comment the thread belongs to |
| `replies[].replied_to_comment_id` | string | ID of the comment being replied to |
| `replies[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `replies[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `replies[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `replies[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `replies[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `comment_id` | string | The requested comment ID |
| `code` | string | The post's shortcode (or media ID, if that was passed) |
| `total` | integer | Total number of replies |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Number of replies returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/instagram/comment/replies?code=C3OqtMeRxrV&comment_id=18033049183828491" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/instagram/comment/replies",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "code": "C3OqtMeRxrV",
        "comment_id": "18033049183828491"
    }
)
print(response.json())
```

## Example Response

```json
{
  "replies": [
    {
      "comment_id": "18026563642931570",
      "text": "@instagram haha",
      "author": "omer.arincc",
      "author_name": "ÖmerArnc",
      "author_id": "52890574747",
      "author_verified": false,
      "author_url": "https://instagram.com/omer.arincc",
      "author_profile_pic_url": "https://scontent.cdninstagram.com/v/t51.89012-19/photo.jpg",
      "likes": 9,
      "reply_count": 0,
      "is_pinned": false,
      "hashtags": [],
      "mentions": [
        "instagram"
      ],
      "date": "2024-02-12 18:56:19",
      "date_timestamp": 1707759379,
      "url": "https://www.instagram.com/p/C3OqtMeRxrV/c/18033049183828491/r/18026563642931570/",
      "source": "Instagram",
      "domain": "instagram.com",
      "gif_url": null,
      "parent_comment_id": "18033049183828491",
      "replied_to_comment_id": "18033049183828491"
    }
  ],
  "comment_id": "18033049183828491",
  "code": "C3OqtMeRxrV",
  "total": 52,
  "pages": 1,
  "count": 9
}
```

## Notes

- Get `comment_id` from the [Post Comments](/docs/instagram-post-comments) endpoint. A comment with no replies returns an empty `replies` array.
- `parent_comment_id` is the top-level comment; `replied_to_comment_id` is the comment being answered, which may be another reply.
