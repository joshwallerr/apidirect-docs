# Reddit Comments

Search Reddit comments by keyword, optionally in one subreddit. Returns comment content, the comment, post and parent IDs, links to the comment and its post, subreddit, author, and publication date. Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/reddit/comments
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1) |
| `sort_by` | No | Sort order: `most_recent`, `relevance`, or `top` (default: `most_recent`) |
| `subreddit` | No | Only comments from this subreddit, with or without `r/` (e.g. `Python`). |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching comments |
| `posts[].comment_id` | string | Comment ID |
| `posts[].post_id` | string | ID of the post the comment is on |
| `posts[].parent_id` | string | ID of the comment it replies to, or the post ID for a top-level comment (empty when unavailable) |
| `posts[].comment_url` | string | Direct link to the comment |
| `posts[].title` | string | Comment title (format: `username on subreddit`) |
| `posts[].url` | string | Link for the parent post: its Reddit thread, or the article, image or video a link post shares |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Reddit username |
| `posts[].source` | string | `"Reddit (Comment)"` |
| `posts[].domain` | string | `"reddit.com"` |
| `posts[].subreddit` | string | Subreddit name |
| `posts[].snippet` | string | Comment content text |
| `posts[].type` | string | `"comment"` |
| `posts[].upvotes` | integer/null | Net upvotes on the comment. `null` if the score is hidden by the subreddit or unavailable. |
| `posts[].post_upvotes` | integer/null | Net upvotes on the parent post. `null` if unavailable. |
| `posts[].post_comments` | integer/null | Total comments on the parent post. `null` if unavailable. |
| `posts[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `posts[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `posts[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `posts[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `posts[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/comments?query=python&pages=2&sort_by=relevance" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/comments",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "python",
        "pages": 2,
        "sort_by": "relevance"
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "comment_id": "pfewxa0",
      "post_id": "1x3wfr5",
      "parent_id": "1x3wfr5",
      "comment_url": "https://www.reddit.com/r/TopCharacterTropes/comments/1x3wfr5/comment/pfewxa0/",
      "title": "practicalcabinet on TopCharacterTropes",
      "url": "https://www.reddit.com/gallery/1x3wfr5",
      "date": "2026-10-12 09:25:33",
      "author": "practicalcabinet",
      "source": "Reddit (Comment)",
      "domain": "reddit.com",
      "subreddit": "TopCharacterTropes",
      "snippet": "The Killer Rabbit of Caerbannog, from *Monty Python and the Holy Grail*, was actually played by a more common non-killer rabbit.\n\n![img](et5lcv7t80vh1)",
      "type": "comment",
      "upvotes": 2461,
      "post_upvotes": 12473,
      "post_comments": 1625,
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
  "pages": 2,
  "count": 44
}
```
