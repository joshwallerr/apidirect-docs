# Facebook Post Comments

Get comments on a Facebook post by post ID. Returns each comment's text, author details, reaction and reply counts, publication date, and any sticker, GIF, image, or video attachment. Supports fetching multiple pages in a single call.

## Endpoint

```
GET /v1/facebook/post/comments
```

**Price:** $0.008 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `post_id` | Yes | Facebook post ID (get from Page Posts, Group Posts, or Search Posts). Accepts both `pfbid` and numeric IDs. |
| `pages` | No | Number of pages to fetch (1-10, default 1). Billed per page. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `comments` | array | List of top-level comment objects |
| `comments[].comment_id` | string | Unique comment ID |
| `comments[].legacy_comment_id` | string | Numeric comment ID |
| `comments[].message` | string/null | Comment text content (null for sticker-only comments) |
| `comments[].date` | string | Human-readable date |
| `comments[].timestamp` | integer | Unix timestamp |
| `comments[].author_name` | string | Name of the comment author |
| `comments[].author_id` | string | Author's Facebook ID |
| `comments[].author_url` | string/null | URL to author's profile |
| `comments[].author_gender` | string | Author's gender when available (`MALE`, `FEMALE`, or `NEUTER`) |
| `comments[].author_profile_picture` | string | URL to author's profile picture |
| `comments[].replies_count` | integer | Number of replies to the comment |
| `comments[].reactions_count` | integer | Number of reactions on the comment |
| `comments[].is_sticker` | boolean | Whether the comment is a sticker |
| `comments[].sticker_url` | string/null | Sticker image URL, if the comment is a sticker |
| `comments[].is_gif` | boolean | Whether the comment is a GIF |
| `comments[].gif` | object/null | GIF attachment data, if any |
| `comments[].image` | object/null | Image attachment data, if any |
| `comments[].video` | object/null | Video attachment data, if any |
| `comments[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `comments[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `comments[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `comments[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `comments[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `count` | integer | Number of comments returned |
| `pages` | integer | Number of pages fetched |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/post/comments?post_id=pfbid02BzYRNmoznsZjci5FuztPUb9mKd9ameNVYSBweaBEvb8oEzSMjcs8nbXnMkYA5Benl" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/post/comments",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"post_id": "pfbid02BzYRNmoznsZjci5FuztPUb9mKd9ameNVYSBweaBEvb8oEzSMjcs8nbXnMkYA5Benl"}
)
print(response.json())
```

## Example Response

```json
{
  "comments": [
    {
      "comment_id": "Y29tbWVudDo5NDM5NDIxODExMTExMzZfMTIxNzA1OTI3NjU2OTgwNw==",
      "legacy_comment_id": "1217059276569807",
      "message": "Even the dog wants to dominate AI",
      "date": "2025-07-03 19:25:36",
      "timestamp": 1751570736,
      "author_name": "Gerson Stefano",
      "author_id": "100006584266587",
      "author_url": "https://www.facebook.com/Gerson.Stefano.48",
      "author_gender": "MALE",
      "author_profile_picture": "https://scontent.xx.fbcdn.net/v/t39.30808-1/462473244_..._n.jpg",
      "replies_count": 0,
      "reactions_count": 0,
      "is_sticker": false,
      "sticker_url": null,
      "is_gif": false,
      "gif": null,
      "image": null,
      "video": null
    }
  ],
  "count": 1,
  "pages": 1
}
```

## Notes

- Returns top-level comments only; each comment's `replies_count` shows how many replies it has.
- Each page returns up to ~10 comments. Billing is per page requested.
- A nonexistent or unavailable post returns an empty `comments` array, as does a post with no comments.
