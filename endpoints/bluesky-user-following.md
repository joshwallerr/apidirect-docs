# Bluesky User Following

Get the accounts a Bluesky user follows, newest first. Returns handle, display name, DID, bio, verification status, profile picture, and join date for each account.

## Endpoint

```
GET /v1/bluesky/user/following
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
| `following` | array | Array of followed profiles, newest first |
| `following[].username` | string | Bluesky handle |
| `following[].full_name` | string | Display name |
| `following[].user_id` | string | DID (permanent account ID) |
| `following[].biography` | string | Profile description |
| `following[].is_verified` | boolean | Whether the account is verified |
| `following[].profile_pic_url` | string | URL to profile picture |
| `following[].date_joined` | string | Account creation date and time |
| `following[].url` | string | Link to the profile |
| `username` | string | The requested handle or DID |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/bluesky/user/following?username=pfrazee.com&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/bluesky/user/following",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "pfrazee.com", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "following": [
    {
      "username": "wired.sister.haus",
      "full_name": "evil_sister.rb",
      "user_id": "did:plc:m6stoaqv4ocgbn4icbwj7chp",
      "biography": "dream sender",
      "is_verified": false,
      "profile_pic_url": "https://cdn.bsky.app/img/avatar/plain/did:plc:m6stoaqv4ocgbn4icbwj7chp/bafkreifzlrytu464rba7tkbted4qzw5ovz6z5bxk2r26uctjespgz5dul4",
      "date_joined": "2026-04-14 23:30:04",
      "url": "https://bsky.app/profile/wired.sister.haus"
    }
  ],
  "username": "pfrazee.com",
  "pages": 1,
  "count": 50
}
```
