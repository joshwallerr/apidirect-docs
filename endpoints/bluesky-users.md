# Bluesky Users

Search Bluesky users by keyword. Matches handles, display names, and bios. Returns handle, display name, DID, bio, verification status, profile picture, and join date for each account.

## Endpoint

```
GET /v1/bluesky/users
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch, 1-20 (default: 1). Each page returns up to 50 users; you are billed per page returned. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `users` | array | Array of matching users |
| `users[].username` | string | Bluesky handle |
| `users[].full_name` | string | Display name |
| `users[].user_id` | string | DID (permanent account ID) |
| `users[].biography` | string | Profile description |
| `users[].is_verified` | boolean | Whether the account is verified |
| `users[].profile_pic_url` | string | URL to profile picture |
| `users[].date_joined` | string | Account creation date and time |
| `users[].url` | string | Link to the profile |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/bluesky/users?query=anthropic&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/bluesky/users",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "anthropic", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "users": [
    {
      "username": "anthropic.com",
      "full_name": "Anthropic",
      "user_id": "did:plc:7xblllgnpqtiotu62pic747n",
      "biography": "We're an Al safety and research company that builds reliable, interpretable, and steerable Al systems. Talk to our Al assistant Claude at Claude.ai.",
      "is_verified": false,
      "profile_pic_url": "https://cdn.bsky.app/img/avatar/plain/did:plc:7xblllgnpqtiotu62pic747n/bafkreifymuozievn7kgdpqlqmbhycgcmzg2zytdtsks5diw4ost34iybjm",
      "date_joined": "2024-11-19 19:33:47",
      "url": "https://bsky.app/profile/anthropic.com"
    }
  ],
  "pages": 1,
  "count": 50
}
```

## Notes

- A keyword with no matching accounts returns an empty list with `count: 0`.
- Follower, following, and post counts are not part of search results; use [User Profile](/docs/bluesky-user) for them.
