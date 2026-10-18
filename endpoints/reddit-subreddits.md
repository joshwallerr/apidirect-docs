# Reddit Search Subreddits

Search subreddits by keyword. Returns each community's name, title, member count, description, creation date, type and icon, 25 per page.

## Endpoint

```
GET /v1/reddit/subreddits
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-10 (default: 1). Each page returns up to 25 subreddits. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `subreddits` | array | Matching subreddits |
| `subreddits[].name` | string | Subreddit name |
| `subreddits[].subreddit_id` | string | Subreddit ID |
| `subreddits[].title` | string | Subreddit title |
| `subreddits[].description` | string | Short public description |
| `subreddits[].url` | string | Link to the subreddit |
| `subreddits[].subscribers` | integer | Number of members |
| `subreddits[].created_at` | string | Creation date and time (UTC) |
| `subreddits[].nsfw` | boolean | Whether the subreddit is marked NSFW |
| `subreddits[].type` | string | Community type, e.g. `public` or `restricted` |
| `subreddits[].icon` | string | Community icon URL, or empty string |
| `subreddits[].language` | string | Language code, e.g. `en` |
| `query` | string | The search keyword |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of subreddits returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/subreddits?query=python&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/subreddits",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "python",
        "pages": 1
    }
)
print(response.json())
```

## Example Response

```json
{
  "subreddits": [
    {
      "name": "Python",
      "subreddit_id": "2qh0y",
      "title": "Python",
      "description": "The largest Python community for Reddit! Stay up to date with the latest news, packages, and meta information relating to the Python programming language. \n-...",
      "url": "https://www.reddit.com/r/Python/",
      "subscribers": 1518060,
      "created_at": "2008-01-25 03:14:39",
      "nsfw": false,
      "type": "public",
      "icon": "https://styles.redditmedia.com/t5_2qh0y/styles/communityIcon_lctik80p96tg1.png?width=256&s=6d91fcc92d9f08c5ba30096d43a555ddd0edbc7d",
      "language": "en"
    }
  ],
  "query": "python",
  "pages": 1,
  "count": 25
}
```
