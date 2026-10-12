# Substack Trending Posts

Get the posts currently trending across all of Substack, as featured on its explore page. Returns each post's title, author, publication, publication date, engagement and paywall status.

## Endpoint

```
GET /v1/substack/trending
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Trending posts |
| `posts[].title` | string | Post title |
| `posts[].subtitle` | string | Post subtitle, empty when none |
| `posts[].url` | string | Direct link to the post |
| `posts[].date` | string | Publication date and time (UTC, YYYY-MM-DD HH:MM:SS) |
| `posts[].author` | string | Author's Substack handle (empty when the byline is the publication itself) |
| `posts[].author_name` | string | Author's display name |
| `posts[].author_id` | integer/null | Author's Substack user ID, null when the byline is the publication itself |
| `posts[].author_url` | string | Link to the author's profile |
| `posts[].source` | string | `"Substack"` |
| `posts[].domain` | string | `"substack.com"` |
| `posts[].snippet` | string | Post description or preview text |
| `posts[].likes` | integer | Number of likes (reactions) |
| `posts[].comments` | integer | Number of comments |
| `posts[].restacks` | integer | Number of restacks (shares to Notes) |
| `posts[].reactions` | object | Reaction counts by emoji, e.g. `{"❤": 284}` |
| `posts[].is_paid` | boolean | Whether the post is for paying subscribers only |
| `posts[].audience` | string | `everyone`, `only_paid` or `only_founding` |
| `posts[].type` | string | `newsletter`, `podcast`, `video` or `thread` |
| `posts[].wordcount` | integer | Word count of the full post |
| `posts[].lang` | string | Post language code (e.g. `en`) |
| `posts[].cover_image_url` | string | Cover image URL, empty when none |
| `posts[].podcast_url` | string | Audio file URL for podcast posts, empty otherwise |
| `posts[].podcast_duration` | number | Podcast length in seconds, 0 otherwise |
| `posts[].tags` | string[] | Post tags |
| `posts[].authors` | array | All credited authors (`username`, `name`, `user_id`, `url`); `author` is the first |
| `posts[].replies` | integer | Number of replies to comments |
| `posts[].audio_url` | string | Substack's narrated audio of the post (MP3), empty when none |
| `posts[].podcast_image_url` | string | Episode artwork for podcast posts, empty otherwise |
| `posts[].video_duration` | number | Video length in seconds for video posts, 0 otherwise |
| `posts[].publication` | string | Publication name |
| `posts[].publication_id` | integer/null | Publication ID (pass it as `publication_id` to the publication endpoints) |
| `posts[].publication_url` | string | Publication home URL |
| `posts[].slug` | string | Post URL slug |
| `posts[].post_id` | string | Post ID (pass it as `post_id` to the post endpoints) |
| `posts[].sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `posts[].sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `posts[].sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `posts[].sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `posts[].sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `count` | integer | Number of posts returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/trending" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/trending",
    headers={"X-API-Key": "YOUR_API_KEY"}
)
print(response.json())
```

## Example Response

```json
{
  "count": 7,
  "posts": [
    {
      "audience": "everyone",
      "audio_url": "",
      "author": "mattstoller",
      "author_id": "759128",
      "author_name": "Matt Stoller",
      "author_url": "https://substack.com/@mattstoller",
      "authors": [
        {
          "name": "Matt Stoller",
          "url": "https://substack.com/@mattstoller",
          "user_id": "759128",
          "username": "mattstoller"
        }
      ],
      "comments": 23,
      "cover_image_url": "https://substackcdn.com/image/fetch/$s_!uRXI!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F…",
      "date": "2026-10-10 19:18:47",
      "domain": "substack.com",
      "is_paid": false,
      "lang": "en",
      "likes": 172,
      "podcast_duration": 0,
      "podcast_image_url": "",
      "podcast_url": "",
      "post_id": "217288945",
      "publication": "BIG by Matt Stoller",
      "publication_id": "11524",
      "publication_url": "https://www.thebignewsletter.com",
      "reactions": {
        "❤": 172
      },
      "replies": 0,
      "restacks": 33,
      "slug": "how-pharma-middlemen-turned-the-federal",
      "snippet": "Everyone hates pharmacy benefit managers, or PBMs, the middlemen raising drug prices. So why did Trump FTC Chair Andrew Ferguson issue them a corporate pardon?",
      "source": "Substack",
      "subtitle": "Everyone hates pharmacy benefit managers, or PBMs, the middlemen raising drug prices. So why did Trump FTC Chair Andrew Ferguson issue them a corporate pardon?",
      "tags": [
        "pharmacy benefit managers"
      ],
      "title": "How Trump Enforcers are Sabotaging Efforts to Bring Down Drug Prices",
      "type": "newsletter",
      "url": "https://www.thebignewsletter.com/p/how-pharma-middlemen-turned-the-federal",
      "video_duration": 0,
      "wordcount": 2205
    }
  ]
}
```
