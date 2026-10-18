# Reddit Post Details

Get one Reddit post by URL or post ID. Returns the title, text, author, subreddit, score, upvote ratio, comment and crosspost counts, flair, video and gallery links, and NSFW/spoiler/locked flags.

## Endpoint

```
GET /v1/reddit/post
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Reddit post URL, e.g. `https://www.reddit.com/r/Python/comments/1wwv97o/my_python_magic_is_gone/` or `https://redd.it/1wwv97o` (max 500 characters). Provide exactly one of `url` or `post_id`. |
| `post_id` | One required | Reddit post ID, e.g. `1wwv97o` (a `t3_` prefix is accepted). Provide exactly one of `url` or `post_id`. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to the post. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `post` | object | The post |
| `post.post_id` | string | Post ID (the base-36 ID in the post URL) |
| `post.title` | string | Post title |
| `post.url` | string | Direct link to the post |
| `post.date` | string | Publication date and time (UTC) |
| `post.author` | string | Author's Reddit username (`[deleted]` for a deleted account) |
| `post.author_url` | string | Link to the author's profile (empty for a deleted account) |
| `post.source` | string | `"Reddit"` |
| `post.domain` | string | `"reddit.com"` |
| `post.snippet` | string | Post text (the title for link, image and video posts) |
| `post.subreddit` | string | Subreddit name |
| `post.upvotes` | integer | Net upvotes (upvotes minus downvotes) |
| `post.upvote_ratio` | number | Fraction of votes that are upvotes, between 0 and 1 |
| `post.comments` | integer | Number of comments |
| `post.crossposts` | integer | Number of times the post has been crossposted |
| `post.flair` | string | Post flair text, or empty string |
| `post.link_url` | string | The URL a link, image or video post shares (empty for text posts) |
| `post.thumbnail` | string | Thumbnail image URL, or empty string |
| `post.is_video` | boolean | Whether the post is a Reddit-hosted video |
| `post.nsfw` | boolean | Whether the post is marked NSFW |
| `post.spoiler` | boolean | Whether the post is marked as a spoiler |
| `post.locked` | boolean | Whether the post is locked to new comments |
| `post.stickied` | boolean | Whether the post is pinned in its subreddit |
| `post.video_url` | string | MP4 file of a Reddit-hosted video, or empty string. It can be silent (Reddit stores most video sound separately), so use `video_hls_url` for video with sound. Reddit can expire video links, so use them soon after fetching |
| `post.video_hls_url` | string | HLS stream (with sound) of a Reddit-hosted video, or empty string. Reddit can expire this link too |
| `post.images` | array | Image URLs: every image of a gallery post, in order, or the image of an image post (empty otherwise) |
| `post.sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `post.sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `post.sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `post.sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `post.sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/post?url=https://www.reddit.com/r/Python/comments/1wwv97o/my_python_magic_is_gone/" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/post",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "url": "https://www.reddit.com/r/Python/comments/1wwv97o/my_python_magic_is_gone/"
    }
)
print(response.json())
```

## Example Response

```json
{
  "post": {
    "post_id": "1wwv97o",
    "title": "My Python magic is gone",
    "url": "https://www.reddit.com/r/Python/comments/1wwv97o/my_python_magic_is_gone/",
    "date": "2026-10-03 19:08:43",
    "author": "RedYad2",
    "author_url": "https://www.reddit.com/user/RedYad2",
    "source": "Reddit",
    "domain": "reddit.com",
    "snippet": "I've been coding for a long time, and I've been developing with Python for years.\n\nI loved coding, always loved it. I started many years ago because I wanted...",
    "subreddit": "Python",
    "upvotes": 876,
    "upvote_ratio": 0.89,
    "comments": 309,
    "crossposts": 0,
    "flair": "Discussion",
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
}
```
