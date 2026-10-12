# Substack Note Details

Get a Substack Note by URL or ID, with its replies. Returns the note text, author, date, likes, replies and restacks, any quoted post or note, and the reply thread nested to any depth.

## Endpoint

```
GET /v1/substack/note
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

Provide exactly one of `url` or `note_id`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Note URL, e.g. `https://substack.com/@hamish/note/c-355659691` (max 500 characters). Provide either `url` or `note_id`. |
| `note_id` | One required | Numeric note ID, with or without the `c-` prefix. Provide either `url` or `note_id`. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per request to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `note` | object | The note |
| `note.note_id` | string | Note ID |
| `note.body` | string | Note text |
| `note.date` | string | Date and time posted (UTC) |
| `note.author` | string | Author's handle |
| `note.author_name` | string | Author's display name |
| `note.author_id` | string | Author's user ID |
| `note.author_url` | string | Link to the author's profile |
| `note.source` | string | `"Substack"` |
| `note.domain` | string | `"substack.com"` |
| `note.likes` | integer | Number of likes |
| `note.replies` | integer | Number of replies |
| `note.restacks` | integer | Number of restacks |
| `note.reactions` | object | Reaction counts by emoji |
| `note.author_pic_url` | string | Author's profile picture URL |
| `note.author_bestseller_tier` | integer | Author's bestseller badge tier: 0, 100, 1000 or 10000 |
| `note.lang` | string | Language code |
| `note.attachments` | array | Media and quoted items. Each has `type` (`image`, `video`, `link`, `post`, `note`, `publication`) and `url`, plus title or dimensions where relevant |
| `note.publication` | string | The author's primary publication |
| `note.url` | string | Direct link to the note |
| `note.sentiment` | object/null | Emotion analysis results. Only present when `get_sentiment=true`. Returns `null` if analysis fails. |
| `note.sentiment.emotions` | object | Plutchik emotion scores (0-100) for: `joy`, `trust`, `fear`, `surprise`, `sadness`, `disgust`, `anger`, `anticipation`. |
| `note.sentiment.dominant_emotion` | string | The emotion with the highest score. |
| `note.sentiment.emotional_intensity` | integer | Overall emotional intensity on a scale of 0-10. |
| `note.sentiment.polarity` | string | Overall sentiment polarity: `positive`, `negative`, or `neutral`. |
| `replies` | array | Replies to the note, each with the note fields plus `replies_list` (nested replies) |
| `count` | integer | Number of top-level replies returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/note?url=https%3A%2F%2Fsubstack.com%2F%40hamish%2Fnote%2Fc-355659691" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/note",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://substack.com/@hamish/note/c-355659691"}
)
print(response.json())
```

## Example Response

```json
{
  "count": 5,
  "note": {
    "attachments": [
      {
        "attachments": [
          {
            "post_id": "218085342",
            "publication": "On Substack",
            "title": "Model Behavior: George Saunders",
            "type": "post",
            "url": "https://on.substack.com/p/model-behavior-george-saunders"
          },
          {
            "duration": 44.6,
            "height": 1280,
            "type": "video",
            "url": "https://substack.com/api/v1/video/upload/c7e75333-51e0-4895-9c1c-597fbbdb5d11/src",
            "width": 720
          }
        ],
        "author": "arielleswedback",
        "author_name": "Arielle Swedback",
        "body": "@George Saunders spoke about Substack and our AI conversation yesterday on Late Night with Seth Meyers. Grateful to him for helping us see our way through",
        "note_id": "355302724",
        "type": "note",
        "url": "https://substack.com/@arielleswedback/note/c-355302724"
      }
    ],
    "author": "hamish",
    "author_bestseller_tier": 0,
    "author_id": "3567",
    "author_name": "Hamish McKenzie",
    "author_pic_url": "https://substack-post-media.s3.amazonaws.com/public/images/46d05a58-6aa7-4896-bd79-5972793b5d4f_1179x1179.jpeg",
    "author_url": "https://substack.com/@hamish",
    "body": "Still feels like a massive honor just for @George Saunders to be publishing on Substack, let alone be speaking of it on the big shows. ",
    "date": "2026-10-08 04:48:40",
    "domain": "substack.com",
    "lang": "en",
    "likes": 53,
    "note_id": "355659691",
    "publication": "Disjointed",
    "reactions": {
      "❤": 54
    },
    "replies": 5,
    "restacks": 3,
    "source": "Substack",
    "url": "https://substack.com/@hamish/note/c-355659691"
  },
  "replies": [
    {
      "attachments": [],
      "author_id": "1347124",
      "author_name": "Emma Gannon",
      "author_url": "https://substack.com/profile/1347124",
      "body": "v cool! Can’t wait to read your book Hamish 👓",
      "date": "2026-10-08 06:13:37",
      "domain": "substack.com",
      "lang": "en",
      "likes": 1,
      "note_id": "355689719",
      "publication": "The Hyphen by Emma Gannon",
      "replies": 0,
      "replies_list": [],
      "restacks": 0,
      "source": "Substack",
      "url": "https://substack.com/home/post/c-355689719"
    }
  ]
}
```
