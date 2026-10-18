# Reddit User Posts

Get a Reddit user's submitted posts by username or profile URL, sorted by newest, hot, top or controversial, with a time window for top and controversial. Returns the same post fields as Post Details, 25 per page.

## Endpoint

```
GET /v1/reddit/user/posts
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | Reddit username, with or without `u/` (3-20 characters). Provide exactly one of `username` or `url`. |
| `url` | One required | Reddit profile URL, e.g. `https://www.reddit.com/user/spez` (max 500 characters). Provide exactly one of `username` or `url`. |
| `sort_by` | No | Sort order: `most_recent`, `hot`, `top`, or `controversial` (default: `most_recent`) |
| `posted_ago` | No | Time window for `sort_by=top` or `sort_by=controversial`: `1h`, `24h`, `7d`, `30d`, `12m`, or `all` (default: `all`). Rejected with any other `sort_by`. |
| `pages` | No | Number of pages to fetch, 1-40 (default: 1). Each page returns up to 25 posts. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | The user's posts |
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
| `username` | string | The username |
| `sort_by` | string | The sort order used |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of posts returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/user/posts?username=GallowBoob&sort_by=most_recent&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/user/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "username": "GallowBoob",
        "sort_by": "most_recent",
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
      "post_id": "fgghrs",
      "title": "‪Everything in balance.‬ ‪Except karma ⬆️‬⬆️⬆️",
      "url": "https://www.reddit.com/user/GallowBoob/comments/fgghrs/everything_in_balance_except_karma/",
      "date": "2020-03-10 16:27:45",
      "author": "GallowBoob",
      "author_url": "https://www.reddit.com/user/GallowBoob",
      "source": "Reddit",
      "domain": "reddit.com",
      "snippet": "‪Everything in balance.‬ ‪Except karma ⬆️‬⬆️⬆️",
      "subreddit": "u_GallowBoob",
      "upvotes": 7949,
      "upvote_ratio": 0.94,
      "comments": 66,
      "crossposts": 6,
      "flair": "",
      "link_url": "https://i.redd.it/41i4qishgvl41.jpg",
      "thumbnail": "https://b.thumbs.redditmedia.com/I4852BZ7_GtmRUfZQki5aAefmUmWDKtd_1Ymqr9UT1I.jpg",
      "is_video": false,
      "nsfw": false,
      "spoiler": false,
      "locked": true,
      "stickied": true,
      "video_url": "",
      "video_hls_url": "",
      "images": [
        "https://i.redd.it/41i4qishgvl41.jpg"
      ],
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
  "username": "GallowBoob",
  "sort_by": "most_recent",
  "pages": 2,
  "count": 50
}
```

## Notes

- Some profiles show only part of their history to logged-out visitors; those return what Reddit shows.
