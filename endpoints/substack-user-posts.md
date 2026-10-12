# Substack User Posts

Get an author's posts across all their publications, newest first. Returns post title, publication, publication date, engagement, paywall status, word count and tags. Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/substack/user/posts
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

Provide exactly one of `username`, `user_id` or `url`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | Substack handle, e.g. `lenny`, with or without a leading `@` (max 100 characters). Provide one of `username`, `user_id` or `url`. |
| `user_id` | One required | Numeric Substack user ID, as returned in `user_id`. Provide one of `username`, `user_id` or `url`. |
| `url` | One required | Profile URL, e.g. `https://substack.com/@lenny` (max 500 characters). Provide one of `username`, `user_id` or `url`. |
| `pages` | No | Number of pages to fetch, 1-60 (default: 1). Each page returns up to 50 posts; you are billed per page returned. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of the author's posts, newest first |
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
| `username` | string | The author's handle |
| `user_id` | string | The author's user ID |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of posts returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/user/posts?username=lenny&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/user/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "lenny", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "count": 100,
  "pages": 2,
  "posts": [
    {
      "audience": "only_paid",
      "audio_url": "",
      "author": "kiyani",
      "author_id": "3667529",
      "author_name": "Kiyani",
      "author_url": "https://substack.com/@kiyani",
      "authors": [
        {
          "name": "Kiyani",
          "url": "https://substack.com/@kiyani",
          "user_id": "3667529",
          "username": "kiyani"
        }
      ],
      "comments": 0,
      "cover_image_url": "https://substackcdn.com/image/fetch/$s_!KxHU!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F…",
      "date": "2026-10-10 13:01:38",
      "domain": "substack.com",
      "is_paid": true,
      "lang": "en",
      "likes": 10,
      "podcast_duration": 0,
      "podcast_image_url": "",
      "podcast_url": "",
      "post_id": "219527894",
      "publication": "Lenny's Newsletter",
      "publication_id": "10845",
      "publication_url": "https://www.lennysnewsletter.com",
      "reactions": {
        "❤": 10
      },
      "replies": 0,
      "restacks": 0,
      "slug": "community-wisdom-community-wisdom",
      "snippet": "Community Wisdom 301",
      "source": "Substack",
      "subtitle": "Community Wisdom 301",
      "tags": [],
      "title": "🧠 Community Wisdom: Community Wisdom Top Contributors Summer Class 2026 + ML recommendation systems, getting back into product after being fired, deciding wh…",
      "type": "newsletter",
      "url": "https://www.lennysnewsletter.com/p/community-wisdom-community-wisdom",
      "video_duration": 0,
      "wordcount": 8056
    }
  ],
  "user_id": "1849774",
  "username": "lenny"
}
```
