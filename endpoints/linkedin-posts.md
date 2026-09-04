# LinkedIn Posts

Search LinkedIn posts and articles by keyword. Returns post content, author, publication date, engagement metrics (likes, comments, shares, reactions), and attached content (images, articles, videos, job listings) for each result.

## Endpoint

```
GET /v1/linkedin/posts
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Conditional | Search keyword (max 500 characters). Required unless at least one filter (e.g. `author`) is provided. |
| `page` | No | Page number, 1-25 (default: 1). 20 posts per page |
| `sort_by` | No | Sort order: `most_recent` or `relevance` (default: `most_recent`) |
| `author` | No | Filter to posts authored by a specific person. Accepts a profile URL, public slug (e.g. `williamhgates`), or member URN — resolved automatically. Comma-separate for multiple. |
| `mentions_member` | No | Filter to posts that mention a specific person (profile URL, slug, or member URN). |
| `from_company` | No | Filter to posts authored by a company page. Numeric LinkedIn company ID (get it from the [Company Details](/docs/linkedin-company) endpoint). Comma-separate for multiple. |
| `author_company` | No | Filter to posts written by people who work at a company. Numeric company ID. |
| `mentions_company` | No | Filter to posts that mention a company. Numeric company ID. |
| `author_title` | No | Filter by the author's job title as free text (e.g. `CEO`). |
| `author_industry` | No | Filter by the author's industry. Numeric LinkedIn industry ID(s), comma-separated. Advanced. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching posts |
| `posts[].title` | string | Post title (format: `@author on LinkedIn`) |
| `posts[].url` | string | Direct link to the post |
| `posts[].date` | string | Publication date and time |
| `posts[].author` | string | Author name |
| `posts[].source` | string | `"LinkedIn"` |
| `posts[].domain` | string | `"linkedin.com"` |
| `posts[].snippet` | string | Post content text |
| `posts[].urn` | string | LinkedIn post URN identifier |
| `posts[].likes` | integer | Number of likes |
| `posts[].comments` | integer | Number of comments |
| `posts[].shares` | integer | Number of shares |
| `posts[].reactions` | object | Reaction type breakdown (e.g. `{"like": 2, "appreciation": 1}`) |
| `posts[].images` | array | Image URLs attached to the post |
| `posts[].article` | object/null | Shared article with `title`, `subtitle`, `url`, `description` |
| `posts[].video` | object/null | Video content with `thumbnail` and `duration` (ms) |
| `posts[].job` | object/null | Job listing with `title`, `subtitle`, `url`, `description` |
| `posts[].has_content_entities` | boolean | `true` if the post has attached content (image, article, video, or job). Posts with `has_content_entities: false` may be reposts — use the Post Details endpoint to check. |
| `posts[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `posts[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `posts[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `posts[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `posts[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `page` | integer | Current page number |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/linkedin/posts?query=artificial%20intelligence&page=1&sort_by=most_recent" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/linkedin/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "artificial intelligence",
        "page": 1,
        "sort_by": "most_recent"
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "title": "@John Doe on LinkedIn",
      "url": "https://linkedin.com/posts/...",
      "date": "2024-01-15 14:30:00",
      "author": "John Doe",
      "source": "LinkedIn",
      "domain": "linkedin.com",
      "snippet": "Exciting developments in artificial intelligence...",
      "urn": "urn:li:activity:7444854690124652545",
      "likes": 12,
      "comments": 3,
      "shares": 1,
      "reactions": {
        "like": 10,
        "appreciation": 2
      },
      "images": [
        "https://media.licdn.com/dms/image/..."
      ],
      "article": null,
      "video": null,
      "job": null,
      "has_content_entities": true,
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
  "page": 1,
  "count": 10
}
```
