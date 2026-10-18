# Reddit Subreddit Details

Get a subreddit's details by name or URL. Returns member count, weekly visitors and contributions, description and sidebar, creation date, type, NSFW and quarantine flags, icon and banner, and whether it is private or banned.

## Endpoint

```
GET /v1/reddit/subreddit
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `subreddit` | One required | Subreddit name, with or without `r/`, e.g. `Python`. Provide exactly one of `subreddit` or `url`. |
| `url` | One required | Subreddit URL, e.g. `https://www.reddit.com/r/Python/` (max 500 characters). Provide exactly one of `subreddit` or `url`. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `subreddit` | object | The subreddit |
| `subreddit.name` | string | Subreddit name |
| `subreddit.subreddit_id` | string | Subreddit ID |
| `subreddit.title` | string | Subreddit title |
| `subreddit.description` | string | Short public description |
| `subreddit.sidebar` | string | Full sidebar text (Markdown) |
| `subreddit.url` | string | Link to the subreddit |
| `subreddit.subscribers` | integer/null | Number of members (null when Reddit hides it) |
| `subreddit.weekly_active_users` | integer/null | Unique visitors in the past week (null when unavailable) |
| `subreddit.weekly_contributions` | integer/null | Posts and comments in the past week (null when unavailable) |
| `subreddit.created_at` | string | Creation date and time (UTC) |
| `subreddit.type` | string | Community type: `public`, `restricted`, `private`, `archived`, `employees_only`, `gold_only` or `user` (empty when unavailable) |
| `subreddit.status` | string | `active`, or why the community can't be browsed: `private`, `gold_only`, `banned` or `quarantined` |
| `subreddit.nsfw` | boolean | Whether the subreddit is marked NSFW |
| `subreddit.quarantined` | boolean | Whether the subreddit is quarantined |
| `subreddit.icon` | string | Community icon URL, or empty string |
| `subreddit.banner` | string | Banner image URL, or empty string |
| `subreddit.language` | string | Language code, e.g. `en` |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/reddit/subreddit?subreddit=Python" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/reddit/subreddit",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "subreddit": "Python"
    }
)
print(response.json())
```

## Example Response

```json
{
  "subreddit": {
    "name": "Python",
    "subreddit_id": "2qh0y",
    "title": "Python",
    "description": "The largest Python community for Reddit! Stay up to date with the latest news, packages, and meta information relating to the Python programming language. \n-...",
    "sidebar": "####[The Python Discord](https://discord.gg/python)\n\nNews about the dynamic, interpreted, interactive, object-oriented, extensible programming language Pytho...",
    "url": "https://www.reddit.com/r/Python/",
    "subscribers": 1518060,
    "weekly_active_users": 118064,
    "weekly_contributions": 737,
    "created_at": "2008-01-25 03:14:39",
    "type": "public",
    "status": "active",
    "nsfw": false,
    "quarantined": false,
    "icon": "https://styles.redditmedia.com/t5_2qh0y/styles/communityIcon_lctik80p96tg1.png?width=64&frame=1&auto=webp&s=92baaacc951d52b5071629852df033d53cafa5ec",
    "banner": "https://styles.redditmedia.com/t5_2qh0y/styles/bannerBackgroundImage_cd73kiu1502d1.png?frame=1&auto=webp&s=cb043cb4ba040265a97554d8debbeb2ed419db16",
    "language": "en"
  }
}
```

## Notes

- `weekly_active_users` and `weekly_contributions` are null for private and banned communities.
