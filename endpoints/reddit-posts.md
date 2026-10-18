# Reddit Posts

Search Reddit posts by keyword. Returns each post's title, URL, subreddit, author, text, score, comment count, flair, and video and gallery links. Sort by newest, relevance, hot, top or most commented, narrow to a time window from the past hour to the past year or to one subreddit, and optionally include NSFW posts.

## Endpoint

```
GET /v1/reddit/posts
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `page` | No | Page number, 1-12 (default: 1). 20 posts per page |
| `sort_by` | No | Sort order: `most_recent`, `relevance`, `hot`, `top`, or `most_commented` (default: `most_recent`) |
| `posted_ago` | No | Only posts from this period: `1h`, `24h`, `7d`, `30d`, `12m`, or `all` (default: `all`). Works with every `sort_by`, e.g. `sort_by=relevance&posted_ago=24h` for the most relevant posts of the past day. |
| `subreddit` | No | Only posts from this subreddit, with or without `r/` (e.g. `Python`). |
| `include_nsfw` | No | Set to `true` to include posts marked NSFW (left out by default). |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Array of matching posts |
| `posts[].post_id` | string | Post ID (the base-36 ID in the post URL) |
| `posts[].title` | string | Post title |
| `posts[].url` | string | Direct link to the post |
| `posts[].date` | string | Publication date and time (UTC) |
| `posts[].author` | string | Author's Reddit username (`[deleted]` for a deleted account) |
| `posts[].author_url` | string | Link to the author's profile (empty for a deleted account) |
| `posts[].source` | string | `"Reddit"` |
| `posts[].domain` | string | `"reddit.com"` |
| `posts[].snippet` | string | Post text (the title for link, image and video posts) |
| `posts[].subreddit` | string | Subreddit name |
| `posts[].upvotes` | integer | Net upvotes (upvotes minus downvotes) |
| `posts[].upvote_ratio` | number | Fraction of votes that are upvotes, between 0 and 1 |
| `posts[].comments` | integer | Number of comments |
| `posts[].crossposts` | integer | Number of times the post has been crossposted |
| `posts[].flair` | string | Post flair text, or empty string |
| `posts[].link_url` | string | The URL a link, image or video post shares (empty for text posts) |
| `posts[].thumbnail` | string | Thumbnail image URL, or empty string |
| `posts[].is_video` | boolean | Whether the post is a Reddit-hosted video |
| `posts[].nsfw` | boolean | Whether the post is marked NSFW |
| `posts[].spoiler` | boolean | Whether the post is marked as a spoiler |
| `posts[].locked` | boolean | Whether the post is locked to new comments |
| `posts[].stickied` | boolean | Whether the post is pinned in its subreddit |
| `posts[].video_url` | string | MP4 file of a Reddit-hosted video, or empty string. It can be silent (Reddit stores most video sound separately), so use `video_hls_url` for video with sound. Reddit can expire video links, so use them soon after fetching |
| `posts[].video_hls_url` | string | HLS stream (with sound) of a Reddit-hosted video, or empty string. Reddit can expire this link too |
| `posts[].images` | array | Image URLs: every image of a gallery post, in order, or the image of an image post (empty otherwise) |
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
curl "https://apidirect.io/v1/reddit/posts?query=programming&page=1&sort_by=hot" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "programming",
        "page": 1,
        "sort_by": "hot"
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "post_id": "1x8r41q",
      "title": "Trauma Based Programming",
      "url": "https://www.reddit.com/r/Vaporwave/comments/1x8r41q/trauma_based_programming/",
      "date": "2026-10-18 01:48:31",
      "author": "planomania-",
      "author_url": "https://www.reddit.com/user/planomania-",
      "source": "Reddit",
      "domain": "reddit.com",
      "snippet": "Trauma Based Programming",
      "subreddit": "Vaporwave",
      "upvotes": 51,
      "upvote_ratio": 0.93,
      "comments": 5,
      "crossposts": 0,
      "flair": "Video",
      "link_url": "https://v.redd.it/j0e5l6pgs4wh1",
      "thumbnail": "https://external-preview.redd.it/cnYxMDNma2dzNHdoMegLt1Xvsyv80gIh_B9028HKtv_zyFY-Iep2LPcXiPLG.jpeg?width=140&height=107&format=jpg&auto=webp&s=e9624aebe61f11dbf2668c392ad42fe0118d9bd5",
      "is_video": true,
      "nsfw": false,
      "spoiler": false,
      "locked": false,
      "stickied": false,
      "video_url": "https://v.redd.it/j0e5l6pgs4wh1/CMAF_1080.mp4?source=fallback",
      "video_hls_url": "https://v.redd.it/j0e5l6pgs4wh1/HLSPlaylist.m3u8?a=1794925791%2CYzAxYjJlZGNlMGY1MjUxOTVhYjVjYjk3YWIwOTM5YTEzNTRhNzZhZmQ4OWYxNmQ3N2VmNThmNjA2MTAyYmU0OQ%3D%3D&v=1&f=sd",
      "images": [],
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
  "count": 20
}
```

## Notes

- To include posts marked NSFW, set `include_nsfw=true`.
