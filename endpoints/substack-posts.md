# Search Substack Posts

Search Substack posts by keyword across every publication. Returns post title, subtitle, author, publication, publication date, engagement (likes, comments, restacks), paywall status, word count, cover image and tags, plus the publications related to the query. Supports a time window from the past day to the past year.

## Endpoint

```
GET /v1/substack/posts
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `page` | No | Page number, 1-101 (default: 1). 16-20 posts per page |
| `posted_ago` | No | Only posts from this period: `24h`, `7d`, `30d`, or `12m` (default: all time) |
| `language` | No | Two-letter language code, e.g. `es`, to rank posts in that language first |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching posts, most relevant first |
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
| `publications` | array | Publications related to the query, each with the publication fields documented on [Publication Details](/docs/substack-publication) |
| `query` | string | The search keyword |
| `page` | integer | Current page number |
| `has_next_page` | boolean | Whether another page exists |
| `count` | integer | Number of posts returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/posts?query=claude%20code&page=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "claude code", "page": 1}
)
print(response.json())
```

## Example Response

```json
{
  "count": 18,
  "has_next_page": true,
  "page": 1,
  "posts": [
    {
      "audience": "everyone",
      "audio_url": "",
      "author": "lonharris",
      "author_id": "380063648",
      "author_name": "Lon Harris",
      "author_url": "https://substack.com/@lonharris",
      "authors": [
        {
          "name": "Lon Harris",
          "url": "https://substack.com/@lonharris",
          "user_id": "380063648",
          "username": "lonharris"
        }
      ],
      "comments": 0,
      "cover_image_url": "https://substackcdn.com/image/youtube/w_728,c_limit/yUuFvL1lK4k",
      "date": "2026-10-06 18:23:35",
      "domain": "substack.com",
      "is_paid": false,
      "lang": "en",
      "likes": 7,
      "podcast_duration": 0,
      "podcast_image_url": "",
      "podcast_url": "",
      "post_id": "219138700",
      "publication": "This Week in AI",
      "publication_id": "6195110",
      "publication_url": "https://www.thisweekinai.ai",
      "reactions": {
        "❤": 7
      },
      "replies": 0,
      "restacks": 1,
      "slug": "build-custom-claude-code-features",
      "snippet": "No more filing feature requests with Anthropic. Just tell Claude what you want.",
      "source": "Substack",
      "subtitle": "No more filing feature requests with Anthropic. Just tell Claude what you want.",
      "tags": [
        "Demo"
      ],
      "title": "Build custom Claude Code features in Claude Code",
      "type": "newsletter",
      "url": "https://www.thisweekinai.ai/p/build-custom-claude-code-features",
      "video_duration": 0,
      "wordcount": 686
    }
  ],
  "publications": [
    {
      "author": "thisweekininc",
      "author_id": "544240277",
      "author_name": "This Week In",
      "author_pic_url": "",
      "author_url": "https://substack.com/@thisweekininc",
      "bestseller_tier": 0,
      "cover_image_url": "https://substack-post-media.s3.amazonaws.com/public/images/daa90518-9a2f-4ae3-9068-88b7c4d53b14_1280x1280.png",
      "created_at": "2025-09-04 15:56:00",
      "custom_domain": "www.thisweekinai.ai",
      "description": "Essential briefing on AI news and trends for researchers, founders, and the enterprises betting on them. New episodes every Thursday, fresh posts daily.",
      "domain": "substack.com",
      "first_post_date": "2025-10-28 01:00:12",
      "founding_plan_name": "",
      "has_chat": true,
      "has_podcast": true,
      "has_recommendations": true,
      "is_bestseller": false,
      "language": "en",
      "logo_url": "https://substackcdn.com/image/fetch/$s_!JY4r!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F…",
      "logo_url_wide": "",
      "name": "This Week in AI",
      "paid_enabled": true,
      "paid_subscriber_band": "",
      "paid_subscriber_floor": 0,
      "plans": [
        {
          "amount": 10.0,
          "currency": "USD",
          "interval": "month"
        }
      ],
      "podcast": null,
      "publication_id": "6195110",
      "ranking_detail": "Launched a year ago",
      "sections": [],
      "source": "Substack",
      "subdomain": "twiai",
      "subscriber_count": 9000,
      "subscriber_count_label": "9.6K+",
      "twitter_handle": "",
      "type": "newsletter",
      "url": "https://www.thisweekinai.ai"
    }
  ],
  "query": "claude code"
}
```
