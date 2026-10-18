# Reddit Subreddit Posts

Get a subreddit's posts by name or URL, sorted hot, new, top, rising or controversial, with Reddit's time windows for top and controversial. Returns the same post fields as Post Details, 25 per page.

## Endpoint

```
GET /v1/reddit/subreddit/posts
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `subreddit` | One required | Subreddit name, with or without `r/`, e.g. `Python`. Provide exactly one of `subreddit` or `url`. |
| `url` | One required | Subreddit URL, e.g. `https://www.reddit.com/r/Python/` (max 500 characters). Provide exactly one of `subreddit` or `url`. |
| `sort_by` | No | Sort order: `hot`, `most_recent`, `top`, `rising`, or `controversial` (default: `hot`) |
| `posted_ago` | No | Time window for `sort_by=top` or `sort_by=controversial`: `1h`, `24h`, `7d`, `30d`, `12m`, or `all` (default: `24h`, Reddit's own default). Rejected with any other `sort_by`. |
| `flair` | No | Only posts with exactly this flair, e.g. `Hiring` (max 64 characters, not case-sensitive). |
| `pages` | No | Number of pages to fetch, 1-40 (default: 1). Each page returns up to 25 posts. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | The subreddit's posts |
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
| `subreddit` | string | The subreddit name |
| `sort_by` | string | The sort order used |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of posts returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/subreddit/posts?subreddit=AskReddit&sort_by=top&posted_ago=7d&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/subreddit/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "subreddit": "AskReddit",
        "sort_by": "top",
        "posted_ago": "7d",
        "pages": 2
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "post_id": "1x3uinu",
      "title": "What previously glorified careers are struggling now?",
      "url": "https://www.reddit.com/r/AskReddit/comments/1x3uinu/what_previously_glorified_careers_are_struggling/",
      "date": "2026-10-12 06:28:49",
      "author": "JAMIEISSLEEPWOKEN",
      "author_url": "https://www.reddit.com/user/JAMIEISSLEEPWOKEN",
      "source": "Reddit",
      "domain": "reddit.com",
      "snippet": "What previously glorified careers are struggling now?",
      "subreddit": "AskReddit",
      "upvotes": 10146,
      "upvote_ratio": 0.96,
      "comments": 5366,
      "crossposts": 6,
      "flair": "",
      "link_url": "",
      "thumbnail": "",
      "is_video": false,
      "nsfw": false,
      "spoiler": false,
      "locked": false,
      "stickied": false,
      "video_url": "",
      "video_hls_url": "",
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
  "subreddit": "AskReddit",
  "sort_by": "top",
  "pages": 2,
  "count": 50
}
```

## Notes

- An unknown subreddit returns an empty `posts` list; a private or banned one returns 404 `not_found`.
