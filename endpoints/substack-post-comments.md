# Substack Post Comments

Get the full comment thread of a Substack post, nested. Returns every comment with text, author, date, likes, replies and restacks, replies nested under their parent to any depth, sorted by relevance, newest first or oldest first.

## Endpoint

```
GET /v1/substack/post/comments
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

Provide exactly one of `url`, `post_id`, or `publication` together with `slug`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Post URL, e.g. `https://www.lennysnewsletter.com/p/all-of-the-lenny-and-friends-summit` (max 500 characters). Provide `url`, `post_id`, or `publication` and `slug`. |
| `post_id` | One required | Numeric post ID, as returned in `post_id`. Provide `url`, `post_id`, or `publication` and `slug`. |
| `publication` | One required | Publication subdomain, host or URL, used together with `slug`. |
| `slug` | One required | Post URL slug, e.g. `all-of-the-lenny-and-friends-summit`, used together with `publication`. |
| `sort_by` | No | Sort order: `relevance` (best first), `most_recent`, `oldest` (default: `relevance`) |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `comments` | array | Top-level comments in the requested order |
| `comments[].comment_id` | string | Comment ID |
| `comments[].body` | string | Comment text |
| `comments[].date` | string | Date and time posted (UTC) |
| `comments[].author` | string | Commenter's handle |
| `comments[].author_name` | string | Commenter's display name |
| `comments[].author_id` | string | Commenter's user ID |
| `comments[].author_url` | string | Link to the commenter's profile |
| `comments[].likes` | integer | Number of likes |
| `comments[].replies` | integer | Number of replies |
| `comments[].restacks` | integer | Number of restacks |
| `comments[].is_author` | boolean | Whether the commenter wrote the post |
| `comments[].is_pinned` | boolean | Whether the comment is pinned |
| `comments[].author_pic_url` | string | Author's profile picture URL |
| `comments[].reactions` | object | Reaction counts by emoji |
| `comments[].liked_by` | array | Names of the first people who liked the comment |
| `comments[].status` | string | `published`, or Substack's removal status |
| `comments[].url` | string | Direct link to the comment |
| `comments[].children` | array | Replies, each with the same fields (nested to any depth) |
| `comments[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `comments[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `comments[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `comments[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `comments[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `post_id` | string | The post's ID |
| `post_url` | string | The post's URL |
| `sort_by` | string | The sort order used |
| `total` | integer | The post's comment count |
| `count` | integer | Number of comments returned, including nested replies |
| `truncated` | boolean | True when a very large thread was cut at the response size limit (whole top-level comments are dropped from the end) |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/post/comments?url=https%3A%2F%2Fwww.lennysnewsletter.com%2Fp%2Fhow-duolingo-reignited-user-growth" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/post/comments",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://www.lennysnewsletter.com/p/how-duolingo-reignited-user-growth"}
)
print(response.json())
```

## Example Response

```json
{
  "comments": [
    {
      "author": "fullstackresearcher",
      "author_id": "8067246",
      "author_name": "Daniel Kyne",
      "author_pic_url": "https://bucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com/public/images/69f08c0f-8d66-4b63-8d88-97af005d6bab_2126x2126.png",
      "author_url": "https://substack.com/@fullstackresearcher",
      "body": "Nothing beats real life examples (especially including failures) in deep detail like this! 🙏",
      "children": [
        {
          "author": "jorgemazal1",
          "author_id": "25411757",
          "author_name": "Jorge Mazal",
          "author_url": "https://substack.com/@jorgemazal1",
          "body": "Thank you Daniel!",
          "children": [],
          "comment_id": "13190378",
          "date": "2023-02-28 21:45:14",
          "is_author": true,
          "is_pinned": false,
          "likes": 5,
          "replies": 0,
          "restacks": 0,
          "url": "https://www.lennysnewsletter.com/p/how-duolingo-reignited-user-growth/comment/13190378"
        }
      ],
      "comment_id": "13180393",
      "date": "2023-02-28 16:40:12",
      "is_author": false,
      "is_pinned": false,
      "liked_by": [
        "Lenny Rachitsky"
      ],
      "likes": 49,
      "reactions": {
        "❤": 49
      },
      "replies": 1,
      "restacks": 0,
      "status": "published",
      "url": "https://www.lennysnewsletter.com/p/how-duolingo-reignited-user-growth/comment/13180393"
    }
  ],
  "count": 79,
  "post_id": "104096876",
  "post_url": "https://www.lennysnewsletter.com/p/how-duolingo-reignited-user-growth",
  "sort_by": "relevance",
  "total": 78,
  "truncated": false
}
```
