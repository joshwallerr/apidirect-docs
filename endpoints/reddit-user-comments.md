# Reddit User Comments

Get a Reddit user's comments by username or profile URL, sorted by newest, hot, top or controversial, with a time window for top and controversial. Returns each comment's text, score, date and subreddit, plus the post it was left on. 25 per page.

## Endpoint

```
GET /v1/reddit/user/comments
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | Reddit username, with or without `u/` (3-20 characters). Provide exactly one of `username` or `url`. |
| `url` | One required | Reddit profile URL, e.g. `https://www.reddit.com/user/spez` (max 500 characters). Provide exactly one of `username` or `url`. |
| `sort_by` | No | Sort order: `most_recent`, `hot`, `top`, or `controversial` (default: `most_recent`) |
| `posted_ago` | No | Time window for `sort_by=top` or `sort_by=controversial`: `1h`, `24h`, `7d`, `30d`, `12m`, or `all` (default: `all`). Rejected with any other `sort_by`. |
| `pages` | No | Number of pages to fetch, 1-40 (default: 1). Each page returns up to 25 comments. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `comments` | array | The user's comments |
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
| `comments[].post_title` | string | Title of the post the comment is on (when available) |
| `comments[].post_url` | string | Link to the post the comment is on |
| `comments[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `comments[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `comments[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `comments[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `comments[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `username` | string | The username |
| `sort_by` | string | The sort order used |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of comments returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/user/comments?username=spez&sort_by=most_recent&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/user/comments",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "username": "spez",
        "sort_by": "most_recent",
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
      "comment_id": "p1wosm9",
      "post_id": "1vgbkge",
      "parent_id": "p1wd2fi",
      "text": "That was the thinking. Otherwise it would be easier to just replicate the UI. ",
      "author": "spez",
      "author_url": "https://www.reddit.com/user/spez",
      "upvotes": 14,
      "date": "2026-08-05 18:31:50",
      "url": "https://www.reddit.com/r/u_spez/comments/1vgbkge/modernizing_reddits_infrastructure_with_you/p1wosm9/",
      "subreddit": "u_spez",
      "is_submitter": true,
      "stickied": false,
      "edited": false,
      "source": "Reddit",
      "domain": "reddit.com",
      "post_title": "Modernizing Reddit’s infrastructure with you",
      "post_url": "https://www.reddit.com/r/u_spez/comments/1vgbkge/modernizing_reddits_infrastructure_with_you/",
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
  "username": "spez",
  "sort_by": "most_recent",
  "pages": 2,
  "count": 50
}
```
