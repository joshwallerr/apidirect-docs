# Bluesky Post Likes

Get the users who liked a Bluesky post, newest first. Returns handle, display name, DID, bio, verification status, profile picture, join date, and the time of the like for each user.

## Endpoint

```
GET /v1/bluesky/post/likes
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
| `likes` | array | Array of users who liked the post, newest first |
| `likes[].username` | string | Bluesky handle |
| `likes[].full_name` | string | Display name |
| `likes[].user_id` | string | DID (permanent account ID) |
| `likes[].biography` | string | Profile description |
| `likes[].is_verified` | boolean | Whether the account is verified |
| `likes[].profile_pic_url` | string | URL to profile picture |
| `likes[].date_joined` | string | Account creation date and time |
| `likes[].url` | string | Link to the profile |
| `likes[].liked_at` | string | When the user liked the post |
| `post_id` | string | The post's AT URI |
| `total` | integer | The post's total like count |
| `pages` | integer | Number of pages returned |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/bluesky/post/likes?url=https%3A%2F%2Fbsky.app%2Fprofile%2Fbsky.app%2Fpost%2F3l6oveex3ii2l&pages=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/bluesky/post/likes",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://bsky.app/profile/bsky.app/post/3l6oveex3ii2l", "pages": 1}
)
print(response.json())
```

## Example Response

```json
{
  "likes": [
    {
      "username": "js2k9.bsky.social",
      "full_name": "JS_2K9",
      "user_id": "did:plc:yqsdfrzxn6ocmtu53euptrnp",
      "biography": "Bluesky account of JS_2K9.\n(Made back in July)",
      "is_verified": false,
      "profile_pic_url": "https://cdn.bsky.app/img/avatar/plain/did:plc:yqsdfrzxn6ocmtu53euptrnp/bafkreianv47vz3ryjbwfifrihesvdkusyqiif3a3mbmxwq5jt5vbw5dfiq",
      "date_joined": "2026-07-16 04:26:07",
      "url": "https://bsky.app/profile/js2k9.bsky.social",
      "liked_at": "2026-09-16 04:21:54"
    }
  ],
  "post_id": "at://did:plc:z72i7hdynmk6r22z27h6tvur/app.bsky.feed.post/3l6oveex3ii2l",
  "total": 63685,
  "pages": 1,
  "count": 50
}
```
