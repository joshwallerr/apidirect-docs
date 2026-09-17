# Bluesky User Followers

Get the followers of a Bluesky user, newest first. Returns handle, display name, DID, bio, verification status, profile picture, and join date for each follower.

## Endpoint

```
GET /v1/bluesky/user/followers
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

Provide exactly one of `username` or `url`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | Bluesky handle, e.g. `bsky.app`, with or without leading `@`, or the account's DID (max 100 characters). Provide either `username` or `url`. |
| `url` | One required | Bluesky profile URL, e.g. `https://bsky.app/profile/bsky.app` (max 500 characters). Provide either `username` or `url`. |
| `pages` | No | Number of pages to fetch, 1-20 (default: 1). Each page returns up to 50 accounts; you are billed per page returned. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `followers` | array | Array of follower profiles, newest first |
| `followers[].username` | string | Bluesky handle |
| `followers[].full_name` | string | Display name |
| `followers[].user_id` | string | DID (permanent account ID) |
| `followers[].biography` | string | Profile description |
| `followers[].is_verified` | boolean | Whether the account is verified |
| `followers[].profile_pic_url` | string | URL to profile picture |
| `followers[].date_joined` | string | Account creation date and time |
| `followers[].url` | string | Link to the profile |
| `username` | string | The requested handle or DID |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/bluesky/user/followers?username=bsky.app&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/bluesky/user/followers",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "bsky.app", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "followers": [
    {
      "username": "useforgekit.bsky.social",
      "full_name": "ForgeKit",
      "user_id": "did:plc:fmtj42jmivqv5ffhhniuflov",
      "biography": "Screenshot & PDF API without Puppeteer. One credit pool for screenshots, PDFs, OG images, QR, link previews. Agent-ready (MCP). https://useforgekit.de…",
      "is_verified": false,
      "profile_pic_url": "https://cdn.bsky.app/img/avatar/plain/did:plc:fmtj42jmivqv5ffhhniuflov/bafkreiflnuwjcrdi36s3h63xqgrn6gumysxuhl7g4fyg5poc7mqegqhp2u",
      "date_joined": "2026-09-03 00:11:18",
      "url": "https://bsky.app/profile/useforgekit.bsky.social"
    }
  ],
  "username": "bsky.app",
  "pages": 1,
  "count": 50
}
```
