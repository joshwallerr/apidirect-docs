# Substack Publication Posts

Get a publication's posts, newest first, top or most discussed, or search them by keyword. Returns post title, author, publication date, engagement, paywall status, word count and tags.

## Endpoint

```
GET /v1/substack/publication/posts
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `publication` | Yes | Publication subdomain (`lenny`), host (`lenny.substack.com`, `www.lennysnewsletter.com`) or any URL on it (max 500 characters) |
| `query` | No | Only posts matching this keyword or phrase (max 500 characters), most relevant first. `sort_by` is ignored when `query` is set |
| `sort_by` | No | Sort order: `most_recent`, `top`, `discussions` (default: `most_recent`) |
| `podcasts_only` | No | Set to `true` to return only podcast episodes, the publication's podcast feed. Works with the `most_recent` archive only |
| `page` | No | Page number (default: 1). 20 posts per page |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of the publication's posts |
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
| `publication` | object/null | The publication (`publication_id`, `name`, `subdomain`, `url`, `logo_url`) |
| `publication_url` | string | Publication home URL |
| `sort_by` | string | The sort order used (`relevance` when `query` is set) |
| `query` | string/null | The keyword filter used, null when none |
| `podcasts_only` | boolean | Whether only podcast episodes were requested |
| `page` | integer | Current page number |
| `has_next_page` | boolean | Whether another page exists |
| `count` | integer | Number of posts returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/publication/posts?publication=lenny&sort_by=most_recent&page=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/publication/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"publication": "lenny", "sort_by": "most_recent", "page": 1}
)
print(response.json())
```

## Example Response

```json
{
  "count": 20,
  "has_next_page": true,
  "page": 1,
  "podcasts_only": false,
  "posts": [
    {
      "audience": "only_paid",
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
      "comments": 25,
      "cover_image_url": "https://substackcdn.com/image/fetch/$s_!ByeN!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F…",
      "date": "2025-10-14 13:03:49",
      "domain": "substack.com",
      "is_paid": true,
      "lang": "en",
      "likes": 839,
      "podcast_duration": 0,
      "podcast_image_url": "",
      "podcast_url": "",
      "post_id": "175662739",
      "publication": "Lenny's Newsletter",
      "publication_id": "10845",
      "publication_url": "https://www.lennysnewsletter.com",
      "reactions": {
        "❤": 839
      },
      "replies": 0,
      "restacks": 65,
      "slug": "everyone-should-be-using-claude-code",
      "snippet": "How to get started, and 50 ways non-technical people are using Claude Code in their work and life",
      "source": "Substack",
      "subtitle": "How to get started, and 50 ways non-technical people are using Claude Code in their work and life",
      "tags": [
        "AI"
      ],
      "title": "Everyone should be using Claude Code more",
      "type": "newsletter",
      "url": "https://www.lennysnewsletter.com/p/everyone-should-be-using-claude-code",
      "video_duration": 0,
      "wordcount": 2958
    }
  ],
  "publication": {
    "logo_url": "https://substackcdn.com/image/fetch/$s_!8MSN!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F…",
    "name": "Lenny's Newsletter",
    "publication_id": "10845",
    "subdomain": "lenny",
    "url": "https://www.lennysnewsletter.com"
  },
  "publication_url": "https://www.lennysnewsletter.com",
  "query": null,
  "sort_by": "top"
}
```
