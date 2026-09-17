# Bluesky Post Reposts

Get the users who reposted a Bluesky post, newest first. Returns handle, display name, DID, bio, verification status, profile picture, and join date for each user.

## Endpoint

```
GET /v1/bluesky/post/reposts
```

**Price:** $0.003 per page
**Free tier:** 50 requests/month

Provide exactly one of `url` or `post_id`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Bluesky post URL, e.g. `https://bsky.app/profile/bsky.app/post/3l6oveex3ii2l` (max 500 characters). Provide either `url` or `post_id`. |
| `post_id` | One required | The post's AT URI as returned in `post_id`, e.g. `at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6oveex3ii2l` (max 200 characters). Provide either `url` or `post_id`. |
| `pages` | No | Number of pages to fetch, 1-20 (default: 1). Each page returns up to 50 accounts; you are billed per page returned. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `reposts` | array | Array of users who reposted the post, newest first |
| `reposts[].username` | string | Bluesky handle |
| `reposts[].full_name` | string | Display name |
| `reposts[].user_id` | string | DID (permanent account ID) |
| `reposts[].biography` | string | Profile description |
| `reposts[].is_verified` | boolean | Whether the account is verified |
| `reposts[].profile_pic_url` | string | URL to profile picture |
| `reposts[].date_joined` | string | Account creation date and time |
| `reposts[].url` | string | Link to the profile |
| `post_id` | string | The post's AT URI |
| `total` | integer | The post's total repost count |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/bluesky/post/reposts?url=https%3A%2F%2Fbsky.app%2Fprofile%2Fbsky.app%2Fpost%2F3l6oveex3ii2l&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/bluesky/post/reposts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://bsky.app/profile/bsky.app/post/3l6oveex3ii2l", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "reposts": [
    {
      "username": "sykhotic.bsky.social",
      "full_name": "Hunter/Hubris (XIV 7.x Spoilers)",
      "user_id": "did:plc:zzwq6jhjnv4irlwhl5okzdut",
      "biography": "They/He | 30s | 🔞 (18+) | Furry\nExtremely part-time Let's Player. Canadian. Severely addicted to FFXIV (Hubris Tymbaent/Bozica Tirasch - Faerie, Aethe…",
      "is_verified": false,
      "profile_pic_url": "https://cdn.bsky.app/img/avatar/plain/did:plc:zzwq6jhjnv4irlwhl5okzdut/bafkreifcg4l3q5spoia4tdwxrdkrmuzcem3ymzllpykff7jtnps6tcejam",
      "date_joined": "2023-08-03 15:59:32",
      "url": "https://bsky.app/profile/sykhotic.bsky.social"
    }
  ],
  "post_id": "at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6oveex3ii2l",
  "total": 9530,
  "pages": 1,
  "count": 50
}
```
