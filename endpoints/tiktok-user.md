# TikTok User Profile

Get the full profile for a single TikTok user by username, user ID, or profile URL. Returns bio, bio link, follower / following counts, total likes, video count, verification status, join date, and linked Instagram, X/Twitter, and YouTube accounts.

## Endpoint

```
GET /v1/tiktok/user
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `username`, `user_id`, or `url`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | TikTok username, with or without leading `@` (max 100 characters) |
| `user_id` | One required | Numeric TikTok user ID, as returned by [Search Users](/docs/tiktok-users) |
| `url` | One required | TikTok profile URL, e.g. `https://www.tiktok.com/@tiktok` (max 500 characters) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `user` | object | Profile data |
| `user.username` | string | TikTok username (unique ID) |
| `user.nickname` | string | Display name |
| `user.user_id` | string | TikTok user ID |
| `user.sec_uid` | string | TikTok secondary user ID (secUid) |
| `user.bio` | string | Profile bio / signature |
| `user.bio_link` | string | Link displayed on the profile, or empty string |
| `user.verified` | boolean | Whether the user is verified |
| `user.is_private` | boolean | Whether the account is private |
| `user.followers` | integer | Number of followers |
| `user.following` | integer | Number of accounts followed |
| `user.likes` | integer | Total likes received |
| `user.video_count` | integer | Number of videos posted |
| `user.videos_liked` | integer | Number of videos the user has liked (0 when their liked list is private) |
| `user.avatar` | string | URL to profile picture |
| `user.avatar_hd` | string | URL to high-resolution profile picture |
| `user.date_joined` | string | Date and time the account was created |
| `user.date_joined_timestamp` | integer/null | Unix timestamp of the account creation date |
| `user.instagram_username` | string | Linked Instagram username, or empty string |
| `user.twitter_id` | string | Linked X/Twitter account ID, or empty string |
| `user.youtube_channel_id` | string | Linked YouTube channel ID, or empty string |
| `user.youtube_channel_title` | string | Linked YouTube channel name, or empty string |
| `user.url` | string | Link to the profile |

If the user does not exist, the endpoint returns a `404` with `code: "not_found"`.

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/tiktok/user?username=gordonramsayofficial" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/tiktok/user",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "gordonramsayofficial"}
)
print(response.json())
```

You can also pass a profile URL or a numeric user ID instead of a username:

```bash
curl "https://apidirect.io/v1/tiktok/user?url=https://www.tiktok.com/@gordonramsayofficial" \
  -H "X-API-Key: YOUR_API_KEY"
```

## Example Response

```json
{
  "user": {
    "username": "gordonramsayofficial",
    "nickname": "Gordon Ramsay",
    "user_id": "6747935906352907269",
    "sec_uid": "MS4wLjABAAAAv3zolJLlWp-WbKXqSZwVSflDdwcbjPADRG-dhb68k30dQjkFpkRs4HiMvWeeIyVv",
    "bio": "I cook sometimes too.....",
    "bio_link": "GordonRamsay.com/",
    "verified": true,
    "is_private": false,
    "followers": 40817126,
    "following": 573,
    "likes": 728577233,
    "video_count": 839,
    "videos_liked": 0,
    "avatar": "https://p19-common-sign.tiktokcdn-us.com/.../photo.webp",
    "avatar_hd": "https://p19-common-sign.tiktokcdn-us.com/.../photo_1080.webp",
    "date_joined": "2019-10-18 17:42:11",
    "date_joined_timestamp": 1571420531,
    "instagram_username": "",
    "twitter_id": "",
    "youtube_channel_id": "",
    "youtube_channel_title": "",
    "url": "https://www.tiktok.com/@gordonramsayofficial"
  }
}
```
