# Substack Post Details

Get a Substack post by URL, ID, or publication and slug. Returns the full body as HTML and plain text (the free preview for paid posts), title, subtitle, author, publication, publication date, engagement, paywall status, word count, cover image, podcast audio and tags.

## Endpoint

```
GET /v1/substack/post
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
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `post` | object | Post data |
| `post.title` | string | Post title |
| `post.subtitle` | string | Post subtitle, empty when none |
| `post.url` | string | Direct link to the post |
| `post.date` | string | Publication date and time (UTC, YYYY-MM-DD HH:MM:SS) |
| `post.author` | string | Author's Substack handle (empty when the byline is the publication itself) |
| `post.author_name` | string | Author's display name |
| `post.author_id` | integer/null | Author's Substack user ID, null when the byline is the publication itself |
| `post.author_url` | string | Link to the author's profile |
| `post.source` | string | `"Substack"` |
| `post.domain` | string | `"substack.com"` |
| `post.snippet` | string | Post description or preview text |
| `post.likes` | integer | Number of likes (reactions) |
| `post.comments` | integer | Number of comments |
| `post.restacks` | integer | Number of restacks (shares to Notes) |
| `post.reactions` | object | Reaction counts by emoji, e.g. `{"❤": 284}` |
| `post.is_paid` | boolean | Whether the post is for paying subscribers only |
| `post.audience` | string | `everyone`, `only_paid` or `only_founding` |
| `post.type` | string | `newsletter`, `podcast`, `video` or `thread` |
| `post.wordcount` | integer | Word count of the full post |
| `post.lang` | string | Post language code (e.g. `en`) |
| `post.cover_image_url` | string | Cover image URL, empty when none |
| `post.podcast_url` | string | Audio file URL for podcast posts, empty otherwise |
| `post.podcast_duration` | number | Podcast length in seconds, 0 otherwise |
| `post.tags` | string[] | Post tags |
| `post.authors` | array | All credited authors (`username`, `name`, `user_id`, `url`); `author` is the first |
| `post.replies` | integer | Number of replies to comments |
| `post.audio_url` | string | Substack's narrated audio of the post (MP3), empty when none |
| `post.podcast_image_url` | string | Episode artwork for podcast posts, empty otherwise |
| `post.video_duration` | number | Video length in seconds for video posts, 0 otherwise |
| `post.publication` | string | Publication name |
| `post.publication_id` | integer/null | Publication ID (pass it as `publication_id` to the publication endpoints) |
| `post.publication_url` | string | Publication home URL |
| `post.slug` | string | Post URL slug |
| `post.post_id` | string | Post ID (pass it as `post_id` to the post endpoints) |
| `post.body_html` | string | Full post HTML for free posts; the free preview Substack shows non-subscribers for paid posts |
| `post.body_text` | string | Plain text of `body_html` |
| `post.body_is_preview` | boolean | Whether `body_html` is the paywall preview rather than the full post |
| `post.updated_at` | string | Last edit date and time (UTC) |
| `post.previous_post_slug` | string | Slug of the previous post on the publication, empty when none |
| `post.next_post_slug` | string | Slug of the next post on the publication, empty when none |
| `post.publication_details` | object/null | The publication (`publication_id`, `name`, `subdomain`, `url`, `logo_url`) |
| `post.sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `post.sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `post.sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `post.sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `post.sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/post?url=https%3A%2F%2Fwww.lennysnewsletter.com%2Fp%2Fall-of-the-lenny-and-friends-summit" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/post",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://www.lennysnewsletter.com/p/all-of-the-lenny-and-friends-summit"}
)
print(response.json())
```

## Example Response

```json
{
  "post": {
    "audience": "everyone",
    "audio_url": "",
    "author": "lenny",
    "author_id": "1849774",
    "author_name": "Lenny Rachitsky",
    "author_url": "https://substack.com/@lenny",
    "authors": [
      {
        "name": "Lenny Rachitsky",
        "url": "https://substack.com/@lenny",
        "user_id": "1849774",
        "username": "lenny"
      }
    ],
    "body_html": "<p><em>👋 Hey there, I’m Lenny. Each week, I share deeply researched product, growth, and career advice. For more: <a href=\"https://www.lennysjobs.com/\">Lenny…",
    "body_is_preview": false,
    "body_text": "👋 Hey there, I’m Lenny. Each week, I share deeply researched product, growth, and career advice. For more: Lenny’s Jobs | Lennybot | Become an AI-Native Buil…",
    "comments": 7,
    "cover_image_url": "https://substack-post-media.s3.amazonaws.com/public/images/9fed347c-0e02-4190-a590-1236719b99de_9213x6142.jpeg",
    "date": "2026-09-29 13:15:57",
    "domain": "substack.com",
    "is_paid": false,
    "lang": "en",
    "likes": 285,
    "next_post_slug": "",
    "podcast_duration": 0,
    "podcast_image_url": "",
    "podcast_url": "",
    "post_id": "215694124",
    "previous_post_slug": "",
    "publication": "Lenny's Newsletter",
    "publication_details": {
      "logo_url": "https://substack-post-media.s3.amazonaws.com/public/images/441213db-4824-4e48-9d28-a3a18952cbfc_592x592.png",
      "name": "Lenny's Newsletter",
      "publication_id": "10845",
      "subdomain": "lenny",
      "url": "https://www.lennysnewsletter.com"
    },
    "publication_id": "10845",
    "publication_url": "https://www.lennysnewsletter.com",
    "reactions": {
      "❤": 285
    },
    "replies": 0,
    "restacks": 5,
    "slug": "all-of-the-lenny-and-friends-summit",
    "snippet": "Plus, some reflections and takeaways from the day",
    "source": "Substack",
    "subtitle": "Plus, some reflections and takeaways from the day",
    "tags": [],
    "title": "All of the Lenny & Friends Summit talks are now online!",
    "type": "newsletter",
    "updated_at": "2026-09-29 16:23:45",
    "url": "https://www.lennysnewsletter.com/p/all-of-the-lenny-and-friends-summit",
    "video_duration": 0,
    "wordcount": 1276
  }
}
```
