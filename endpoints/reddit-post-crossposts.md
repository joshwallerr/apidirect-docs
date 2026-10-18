# Reddit Post Crossposts

Get the other submissions of a Reddit post's link across Reddit: crossposts and reposts of the same URL, with each one's subreddit, author, score and comment count.

## Endpoint

```
GET /v1/reddit/post/crossposts
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Reddit post URL, e.g. `https://www.reddit.com/r/Python/comments/1wwv97o/my_python_magic_is_gone/` or `https://redd.it/1wwv97o` (max 500 characters). Provide exactly one of `url` or `post_id`. |
| `post_id` | One required | Reddit post ID, e.g. `1wwv97o` (a `t3_` prefix is accepted). Provide exactly one of `url` or `post_id`. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Crossposts and reposts of the post's link |
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
| `post_id` | string | The original post's ID |
| `count` | integer | Number of posts returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/post/crossposts?post_id=z1c9z" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/post/crossposts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "post_id": "z1c9z"
    }
)
print(response.json())
```

## Example Response

```json
{
  "posts": [
    {
      "post_id": "x0hiil",
      "title": "President Obama does a Reddit AMA [10YA - Aug 29]",
      "url": "https://www.reddit.com/r/TenYearsAgo/comments/x0hiil/president_obama_does_a_reddit_ama_10ya_aug_29/",
      "date": "2022-08-29 06:25:55",
      "author": "MonsieurA",
      "author_url": "https://www.reddit.com/user/MonsieurA",
      "source": "Reddit",
      "domain": "reddit.com",
      "snippet": "President Obama does a Reddit AMA [10YA - Aug 29]",
      "subreddit": "TenYearsAgo",
      "upvotes": 27,
      "upvote_ratio": 0.91,
      "comments": 4,
      "crossposts": 0,
      "flair": "Technology & Internet",
      "link_url": "https://www.reddit.com/r/IAmA/comments/z1c9z/i_am_barack_obama_president_of_the_united_states/",
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
  "post_id": "z1c9z",
  "count": 13
}
```
