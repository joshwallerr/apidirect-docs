# Search Substack Notes

Search Substack Notes by keyword. Returns each note's text, author, date, engagement (likes, replies, restacks) and any quoted post or note, newest first or top first. Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/substack/notes
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `sort_by` | No | Sort order: `most_recent`, `top` (default: `most_recent`) |
| `pages` | No | Number of pages to fetch, 1-250 (default: 1). Each page returns about 5 notes; you are billed per page returned. |
| `get_sentiment` | No | Set to `true` to add AI emotion analysis (Plutchik's Wheel) to each result. Adds +$0.001 per page to the cost. Returns emotion scores, dominant emotion, intensity, and polarity. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `notes` | array | Array of matching notes |
| `notes[].note_id` | string | Note ID |
| `notes[].body` | string | Note text |
| `notes[].date` | string | Date and time posted (UTC) |
| `notes[].author` | string | Author's handle |
| `notes[].author_name` | string | Author's display name |
| `notes[].author_id` | string | Author's user ID |
| `notes[].author_url` | string | Link to the author's profile |
| `notes[].source` | string | "Substack" |
| `notes[].domain` | string | "substack.com" |
| `notes[].likes` | integer | Number of likes |
| `notes[].replies` | integer | Number of replies |
| `notes[].restacks` | integer | Number of restacks |
| `notes[].reactions` | object | Reaction counts by emoji |
| `notes[].author_pic_url` | string | Author's profile picture URL |
| `notes[].author_bestseller_tier` | integer | Author's bestseller badge tier: 0, 100, 1000 or 10000 |
| `notes[].lang` | string | Language code |
| `notes[].attachments` | array | Media and quoted items. Each has `type` (`image`, `video`, `link`, `post`, `note`, `publication`) and `url`, plus title or dimensions where relevant |
| `notes[].publication` | string | The author's primary publication |
| `notes[].url` | string | Direct link to the note |
| `query` | string | The search keyword |
| `sort_by` | string | The sort order used |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of notes returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/notes?query=claude%20code&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/notes",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "claude code", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "count": 9,
  "notes": [
    {
      "attachments": [
        {
          "height": 3000,
          "type": "image",
          "url": "https://substack-post-media.s3.amazonaws.com/public/images/3b20c7ab-894d-4fac-8c71-a770e65b2cd3_2400x3000.webp",
          "width": 2400
        }
      ],
      "author": "aakashgupta",
      "author_bestseller_tier": 0,
      "author_id": "4429439",
      "author_name": "Aakash Gupta",
      "author_pic_url": "",
      "author_url": "https://substack.com/@aakashgupta",
      "body": "Claude Code is the best way to use AI.\n\nHere's your complete guide:\n\n1. Stop working in chat windows\n\nOpen terminal in y…",
      "date": "2026-10-12 05:00:03",
      "domain": "substack.com",
      "lang": "en",
      "likes": 1,
      "note_id": "358840474",
      "publication": "Product Growth",
      "reactions": {
        "❤": 1
      },
      "replies": 0,
      "restacks": 0,
      "source": "Substack",
      "url": "https://substack.com/@aakashgupta/note/c-358840474"
    }
  ],
  "pages": 1,
  "query": "claude code",
  "sort_by": "most_recent"
}
```
