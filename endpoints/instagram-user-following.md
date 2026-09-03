# Instagram User Following

Get the accounts a user follows by username or profile URL. Returns username, full name, user ID, verification status, and profile picture for each account. Supports pagination and an optional keyword search.

## Endpoint

```
GET /v1/instagram/user/following
```

**Price:** $0.006 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | Instagram username, with or without leading `@` (max 100 characters). Provide either `username` or `url`. |
| `url` | One required | Instagram profile URL, e.g. `https://instagram.com/natgeo` (max 500 characters). Provide either `username` or `url`. |
| `pages` | No | Number of pages to fetch, 1-20 (default: 1). Each page returns up to 50 accounts. |
| `query` | No | Search the following list by username or name (max 100 characters). Returns up to 50 matches in a single request; `pages` is ignored. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `following` | array | Array of followed-account profiles |
| `following[].username` | string | Instagram username |
| `following[].full_name` | string | Display name |
| `following[].user_id` | string | Instagram user ID |
| `following[].is_verified` | boolean | Whether the user is verified (blue checkmark) |
| `following[].is_private` | boolean | Whether the account is private |
| `following[].profile_pic_url` | string | URL to profile picture |
| `following[].url` | string | Link to the profile |
| `username` | string | The requested username |
| `query` | string | The search keyword (only when `query` was passed) |
| `pages` | integer | Number of pages fetched |
| `count` | integer | Total results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/instagram/user/following?username=natgeo&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/instagram/user/following",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "username": "natgeo",
        "pages": 2
    }
)
print(response.json())
```

## Example Response

```json
{
  "following": [
    {
      "username": "marcuswestbergphotography",
      "full_name": "Photographer & Storyteller",
      "user_id": "364094780",
      "is_verified": false,
      "is_private": false,
      "profile_pic_url": "https://scontent.cdninstagram.com/v/t51.2885-19/photo.jpg",
      "url": "https://instagram.com/marcuswestbergphotography"
    }
  ],
  "username": "natgeo",
  "pages": 2,
  "count": 100
}
```

## Notes

- Each page returns up to 50 accounts; you are billed per page requested. Instagram serves at most 1,000 accounts per call.
- With `query`, the endpoint returns up to 50 matching accounts in one request and bills one page.
- A private account returns `403` with code `private_account`. A username that does not exist returns `404` with code `not_found`.
