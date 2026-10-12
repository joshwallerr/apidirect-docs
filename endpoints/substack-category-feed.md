# Substack Category Feed

Get a Substack category's feed: the posts and notes Substack shows for the topic, top, newest or posts only. Each item is tagged note or post. Supports fetching multiple pages in a single API call.

## Endpoint

```
GET /v1/substack/category/feed
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `category` | Yes | Category ID or slug, e.g. `4` or `technology`. See [Category IDs](/docs/substack-category-ids) |
| `sort_by` | No | Sort order: `top`, `most_recent`, `posts` (default: `top`) |
| `pages` | No | Number of pages to fetch, 1-250 (default: 1). Each page returns about 11 items; you are billed per page returned. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `items` | array | Array of feed items |
| `items[].type` | string | note or post |
| `items[].note_id` | string | Note ID |
| `items[].body` | string | Note text |
| `items[].date` | string | Date and time posted (UTC) |
| `items[].author` | string | Author's handle |
| `items[].author_name` | string | Author's display name |
| `items[].author_id` | string | Author's user ID |
| `items[].author_url` | string | Link to the author's profile |
| `items[].source` | string | "Substack" |
| `items[].domain` | string | "substack.com" |
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
| `items[].post_type` | string | For post items: newsletter, podcast, video or thread; post items otherwise carry the post fields documented on [User Posts](/docs/substack-user-posts)  |
| `category` | object | The category (category_id, name) |
| `sort_by` | string | The sort order used |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of items returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/category/feed?category=technology&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/category/feed",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"category": "technology", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "category": {
    "category_id": 4,
    "name": "Technology"
  },
  "count": 10,
  "items": [
    {
      "attachments": [],
      "author": "sifuyik",
      "author_bestseller_tier": 0,
      "author_id": "73134922",
      "author_name": "Sifu Yik Chan",
      "author_pic_url": "",
      "author_url": "https://substack.com/@sifuyik",
      "body": "50 legendary websites that feel like the internet’s hidden toolbox 🧰\n\n1. http://unpaywall.org — Free research papers\n\n2.…",
      "date": "2026-09-23 04:15:17",
      "domain": "substack.com",
      "lang": "en",
      "likes": 16089,
      "note_id": "343671380",
      "publication": "Sifu Yik's Substack",
      "reactions": {
        "❤": 16089
      },
      "replies": 89,
      "restacks": 4337,
      "source": "Substack",
      "type": "note",
      "url": "https://substack.com/@sifuyik/note/c-343671380"
    },
    {
      "audience": "everyone",
      "audio_url": "",
      "author": "chrisarmitage1",
      "author_id": "370292293",
      "author_name": "Christopher Armitage",
      "author_url": "https://substack.com/@chrisarmitage1",
      "authors": [
        {
          "name": "Christopher Armitage",
          "url": "https://substack.com/@chrisarmitage1",
          "user_id": "370292293",
          "username": "chrisarmitage1"
        }
      ],
      "comments": 87,
      "cover_image_url": "https://substackcdn.com/image/fetch/$s_!skDu!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.…",
      "date": "2026-10-11 22:08:52",
      "domain": "substack.com",
      "is_paid": false,
      "lang": "en",
      "likes": 700,
      "podcast_duration": 0,
      "podcast_image_url": "",
      "podcast_url": "",
      "post_id": "219921886",
      "post_type": "newsletter",
      "publication": "The Existentialist Republic",
      "publication_id": "5818316",
      "publication_url": "https://cmarmitage.substack.com",
      "reactions": {
        "❤": 700
      },
      "replies": 0,
      "restacks": 306,
      "slug": "ukraine-is-successfully-bombing-the",
      "snippet": "Yandex answers 70% of Russian searches, and Ukraine hit three of its five data centers in four days.",
      "source": "Substack",
      "subtitle": "Yandex answers 70% of Russian searches, and Ukraine hit three of its five data centers in four days.",
      "tags": [
        "Christopher Armitage ",
        "campaign",
        "American fascism",
        "activism",
        "ukraine"
      ],
      "title": "Ukraine is Successfully Bombing the Heart of Russia’s Online Disinformation Machine.",
      "type": "post",
      "url": "https://cmarmitage.substack.com/p/ukraine-is-successfully-bombing-the",
      "video_duration": 0,
      "wordcount": 1573
    }
  ],
  "pages": 1,
  "sort_by": "top"
}
```
