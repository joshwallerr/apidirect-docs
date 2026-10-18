# Reddit Trending Posts

Get the posts trending across Reddit (r/popular, or r/all), worldwide or in one country, sorted hot, new, top, rising or controversial. Returns the same post fields as Post Details, 25 per page.

## Endpoint

```
GET /v1/reddit/trending
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `sort_by` | No | Sort order: `hot`, `most_recent`, `top`, `rising`, or `controversial` (default: `hot`) |
| `posted_ago` | No | Time window for `sort_by=top` or `sort_by=controversial`: `1h`, `24h`, `7d`, `30d`, `12m`, or `all` (default: `24h`). Rejected with any other `sort_by`. |
| `feed` | No | `popular` (r/popular: the most active posts in public, non-NSFW communities) or `all` (r/all: every community) (default: `popular`) |
| `country` | No | One country's r/popular, as on reddit.com: `AR`, `AU`, `BG`, `CA`, `CL`, `CO`, `CZ`, `DE`, `ES`, `FI`, `FR`, `GB`, `GR`, `HR`, `HU`, `IE`, `IN`, `IS`, `IT`, `JP`, `MX`, `MY`, `NZ`, `PH`, `PL`, `PR`, `PT`, `RO`, `RS`, `SE`, `SG`, `TH`, `TR`, `TW` or `US` (default: worldwide). Only with `feed=popular`. |
| `pages` | No | Number of pages to fetch, 1-20 (default: 1). Each page returns up to 25 posts. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `posts` | array | Trending posts |
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
| `sort_by` | string | The sort order used |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of posts returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/trending?sort_by=hot&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/trending",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "sort_by": "hot",
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
      "post_id": "1x91fou",
      "title": "Tommy asked a question. Abdul El-Sayed answered and no one physically harmed Tommy.",
      "url": "https://www.reddit.com/r/BlackPeopleofReddit/comments/1x91fou/tommy_asked_a_question_abdul_elsayed_answered_and/",
      "date": "2026-10-18 11:58:02",
      "author": "Damiana1111",
      "author_url": "https://www.reddit.com/user/Damiana1111",
      "source": "Reddit",
      "domain": "reddit.com",
      "snippet": "**\"Answer the question, Tommy. Everybody knows the answer to it.\"**",
      "subreddit": "BlackPeopleofReddit",
      "upvotes": 12357,
      "upvote_ratio": 0.98,
      "comments": 871,
      "crossposts": 11,
      "flair": "Politics",
      "link_url": "https://v.redd.it/2krz9t3ht7wh1",
      "thumbnail": "https://external-preview.redd.it/MDU3ZnhwMmh0N3doMVwiL369t9IGvDaBgYRPof2vTwA6JFUwNQ-nlvrN4aju.png?width=140&height=140&crop=1:1,smart&format=jpg&auto=webp&s=dd43b4c3a370f0dbcf009a0de277bacdbd839ccc",
      "is_video": true,
      "nsfw": false,
      "spoiler": false,
      "locked": false,
      "stickied": false,
      "video_url": "https://v.redd.it/2krz9t3ht7wh1/CMAF_480.mp4?source=fallback",
      "video_hls_url": "https://v.redd.it/2krz9t3ht7wh1/HLSPlaylist.m3u8?a=1794925761%2COGE5NGZlNjIxNzhkYmE4Y2ZiMzU1MDU3NmIzNDViMGJjNzZjZWU5MTkyMjEzYWMxM2EwM2Y4N2JiOWQ3ZTdjZQ%3D%3D&v=1&f=sd",
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
  "sort_by": "hot",
  "pages": 2,
  "count": 50
}
```
