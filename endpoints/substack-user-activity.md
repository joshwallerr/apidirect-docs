# Substack User Activity

Get an author's public activity feed: their Notes and the posts they publish or restack, newest first, or only their notes, posts, replies, restacks or likes. Each item is tagged note, post or comment and says what the author did with it. Notes carry text, engagement and any quoted post or note.

## Endpoint

```
GET /v1/substack/user/activity
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

Provide exactly one of `username`, `user_id` or `url`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | Substack handle, e.g. `lenny`, with or without a leading `@` (max 100 characters). Provide one of `username`, `user_id` or `url`. |
| `user_id` | One required | Numeric Substack user ID, as returned in `user_id`. Provide one of `username`, `user_id` or `url`. |
| `url` | One required | Profile URL, e.g. `https://substack.com/@lenny` (max 500 characters). Provide one of `username`, `user_id` or `url`. |
| `type` | No | Only one kind of activity: `note`, `post`, `reply`, `restack`, `like` (default: notes, posts and restacks) |
| `pages` | No | Number of pages to fetch, 1-250 (default: 1). Each page returns 12 items; you are billed per page returned. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `items` | array | Array of activity items, newest first |
| `items[].type` | string | `note`, `post` or `comment` (a reply on a post or note) |
| `items[].activity` | string | What the author did with it: `note`, `post`, `reply`, `restack` or `like` |
| `items[].note_id` | string | Note ID |
| `items[].body` | string | Note text |
| `items[].date` | string | Date and time posted (UTC) |
| `items[].author` | string | Author's handle |
| `items[].author_name` | string | Author's display name |
| `items[].author_id` | string | Author's user ID |
| `items[].author_url` | string | Link to the author's profile |
| `items[].source` | string | `"Substack"` |
| `items[].domain` | string | `"substack.com"` |
| `items[].likes` | integer | Number of likes |
| `items[].replies` | integer | Number of replies |
| `items[].restacks` | integer | Number of restacks |
| `items[].reactions` | object | Reaction counts by emoji |
| `items[].author_pic_url` | string | Author's profile picture URL |
| `items[].author_bestseller_tier` | integer | Author's bestseller badge tier: 0, 100, 1000 or 10000 |
| `items[].lang` | string | Language code |
| `items[].attachments` | array | Media and quoted items. Each has `type` (`image`, `video`, `link`, `post`, `note`, `publication`) and `url`, plus title or dimensions where relevant |
| `items[].publication` | string | The author's primary publication |
| `items[].url` | string | Direct link to the note |
| `items[].post_type` | string | For `post` items: `newsletter`, `podcast`, `video` or `thread`; post items otherwise carry the post fields documented on [User Posts](/docs/substack-user-posts) |
| `username` | string | The author's handle |
| `user_id` | string | The author's user ID |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of items returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/user/activity?username=hamish&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/user/activity",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "hamish", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "count": 24,
  "items": [
    {
      "activity": "note",
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
      "author_pic_url": "",
      "author_url": "https://substack.com/@hamish",
      "body": "Still feels like a massive honor just for @George Saunders to be publishing on Substack, let alone be speaking of it on the big shows. ",
      "date": "2026-10-08 04:48:40",
      "domain": "substack.com",
      "lang": "en",
      "likes": 53,
      "note_id": "355659691",
      "publication": "Disjointed",
      "reactions": {
        "❤": 53
      },
      "replies": 5,
      "restacks": 3,
      "source": "Substack",
      "type": "note",
      "url": "https://substack.com/@hamish/note/c-355659691"
    }
  ],
  "pages": 2,
  "user_id": "3567",
  "username": "hamish"
}
```
