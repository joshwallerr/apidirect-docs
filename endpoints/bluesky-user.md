# Bluesky User Profile

Get a Bluesky user's full profile by handle, DID, or profile URL. Returns display name, bio, follower/following/post counts, verification status, profile picture and banner, join date, and the pinned post.

## Endpoint

```
GET /v1/bluesky/user
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

Provide exactly one of `username` or `url`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | Bluesky handle, e.g. `bsky.app`, with or without leading `@`, or the account's DID (max 100 characters). Provide either `username` or `url`. |
| `url` | One required | Bluesky profile URL, e.g. `https://bsky.app/profile/bsky.app` (max 500 characters). Provide either `username` or `url`. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `user` | object | Profile data |
| `user.username` | string | Bluesky handle |
| `user.full_name` | string | Display name |
| `user.user_id` | string | DID (permanent account ID) |
| `user.biography` | string | Profile description |
| `user.follower_count` | integer | Number of followers |
| `user.following_count` | integer | Number of accounts followed |
| `user.post_count` | integer | Total posts |
| `user.list_count` | integer | Number of lists the account has created |
| `user.feed_count` | integer | Number of custom feeds the account publishes |
| `user.starter_pack_count` | integer | Number of starter packs the account has created |
| `user.is_verified` | boolean | Whether the account is verified |
| `user.is_labeler` | boolean | Whether the account is a moderation labeler service |
| `user.profile_pic_url` | string | URL to profile picture |
| `user.profile_banner_url` | string | URL to profile banner, or empty string |
| `user.date_joined` | string | Account creation date and time |
| `user.date_joined_timestamp` | integer/null | Unix timestamp of the account creation date |
| `user.pinned_post_id` | string | `post_id` of the pinned post, or empty string |
| `user.url` | string | Link to the profile |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/bluesky/user?username=bsky.app" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/bluesky/user",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "bsky.app"}
)
print(response.json())
```

## Example Response

```json
{
  "user": {
    "username": "bsky.app",
    "full_name": "Bluesky",
    "user_id": "did:plc:z72i7hdynmk6r22z27h6tvur",
    "biography": "official Bluesky account (check username👆)\n\nBugs, feature requests, feedback: support@bsky.app",
    "follower_count": 34923372,
    "following_count": 15,
    "post_count": 863,
    "list_count": 18,
    "feed_count": 7,
    "starter_pack_count": 15,
    "is_verified": false,
    "is_labeler": false,
    "profile_pic_url": "https://cdn.bsky.app/img/avatar/plain/did:plc:z72i7hdynmk6r22z27h6tvur/bafkreihwihm6kpd6zuwhhlro75p5qks5qtrcu55jp3gddbfjsieiv7wuka",
    "profile_banner_url": "https://cdn.bsky.app/img/banner/plain/did:plc:z72i7hdynmk6r22z27h6tvur/bafkreichzyovokfzmymz36p5jibbjrhsur6n7hjnzxrpbt5jaydp2szvna",
    "date_joined": "2023-04-12 04:53:57",
    "date_joined_timestamp": 1681275237,
    "pinned_post_id": "at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6oveex3ii2l",
    "url": "https://bsky.app/profile/bsky.app"
  }
}
```
