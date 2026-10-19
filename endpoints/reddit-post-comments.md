# Reddit Post Comments

Get the comments on a Reddit post, replies included, by URL or post ID. Comments come in thread order, each with its depth and parent ID, so you can rebuild the tree.

## Endpoint

```
GET /v1/reddit/post/comments
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Reddit post URL, e.g. `https://www.reddit.com/r/Python/comments/1wwv97o/my_python_magic_is_gone/` or `https://redd.it/1wwv97o` (max 500 characters). Provide exactly one of `url` or `post_id`. |
| `post_id` | One required | Reddit post ID, e.g. `1wwv97o` (a `t3_` prefix is accepted). Provide exactly one of `url` or `post_id`. |
| `sort_by` | No | Sort order: `top`, `best` (Reddit's default order), `most_recent`, `controversial`, `oldest`, or `qa` (Q&A) (default: `top`) |
| `pages` | No | Number of pages to fetch, 1-80 (default: 1). Each page returns up to 50 comments. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `comments` | array | The post's comments in thread order (each comment followed by its replies) |
| `comments[].comment_id` | string | Comment ID |
| `comments[].post_id` | string | ID of the post the comment is on |
| `comments[].parent_id` | string | ID of the parent comment, or the post ID for a top-level comment |
| `comments[].text` | string | Comment text (Markdown) |
| `comments[].author` | string | Commenter's Reddit username (`[deleted]` for a deleted account) |
| `comments[].author_url` | string | Link to the commenter's profile (empty for a deleted account) |
| `comments[].upvotes` | integer | Net upvotes |
| `comments[].date` | string | Publication date and time (UTC) |
| `comments[].url` | string | Direct link to the comment |
| `comments[].subreddit` | string | Subreddit name |
| `comments[].is_submitter` | boolean | Whether the commenter is the post's author |
| `comments[].stickied` | boolean | Whether a moderator pinned the comment |
| `comments[].edited` | boolean | Whether the comment has been edited |
| `comments[].source` | string | `"Reddit"` |
| `comments[].domain` | string | `"reddit.com"` |
| `comments[].depth` | integer | Nesting level: 0 for a top-level comment, 1 for a reply, and so on |
| `comments[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `comments[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `comments[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `comments[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `comments[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `post_id` | string | The post ID |
| `sort_by` | string | The sort order used |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of comments returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/post/comments?post_id=1wwv97o&sort_by=top&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/post/comments",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "post_id": "1wwv97o",
        "sort_by": "top",
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
      "comment_id": "pdo5esc",
      "post_id": "1wwv97o",
      "parent_id": "pdo3akk",
      "text": "It’s slightly different (worse) than that because incorporating AI properly can both speed you up -and- give a better final product. Whereas for the artist t...",
      "author": "SirPitchalot",
      "author_url": "https://www.reddit.com/user/SirPitchalot",
      "upvotes": 104,
      "date": "2026-10-03 19:38:31",
      "url": "https://www.reddit.com/r/Python/comments/1wwv97o/my_python_magic_is_gone/pdo5esc/",
      "subreddit": "Python",
      "is_submitter": false,
      "stickied": false,
      "edited": true,
      "source": "Reddit",
      "domain": "reddit.com",
      "depth": 1,
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
  "post_id": "1wwv97o",
  "sort_by": "top",
  "pages": 2,
  "count": 100
}
```
