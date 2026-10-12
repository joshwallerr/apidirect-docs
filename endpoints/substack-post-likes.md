# Substack Post Likes

Get the people who liked a Substack post. Returns up to 100 profiles with display name, user ID, profile picture, bestseller tier and primary publication, plus the post's total like count.

## Endpoint

```
GET /v1/substack/post/likes
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

Provide exactly one of `url`, `post_id`, or `publication` together with `slug`.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | One required | Post URL, e.g. `https://www.lennysnewsletter.com/p/all-of-the-lenny-and-friends-summit` (max 500 characters). Provide `url`, `post_id`, or `publication` and `slug`. |
| `post_id` | One required | Numeric post ID, as returned in `post_id`. Provide `url`, `post_id`, or `publication` and `slug`. |
| `publication` | One required | Publication subdomain, host or URL, used together with `slug`. |
| `slug` | One required | Post URL slug, e.g. `all-of-the-lenny-and-friends-summit`, used together with `publication`. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `likes` | array | People who liked the post (up to 100) |
| `likes[].full_name` | string | Display name |
| `likes[].user_id` | string | User ID (pass it as `user_id` to the user endpoints) |
| `likes[].profile_pic_url` | string | Profile picture URL |
| `likes[].bestseller_tier` | integer | Bestseller badge tier, 0 when none |
| `likes[].is_bestseller` | boolean | Whether the person carries a bestseller badge |
| `likes[].primary_publication` | object/null | Their main publication (`publication_id`, `name`, `subdomain`, `url`, `logo_url`), or null |
| `likes[].url` | string | Link to the profile (by ID) |
| `post_id` | string | The post's ID |
| `post_url` | string | The post's URL |
| `total` | integer | The post's total like count |
| `count` | integer | Number of profiles returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/substack/post/likes?url=https%3A%2F%2Fwww.lennysnewsletter.com%2Fp%2Fall-of-the-lenny-and-friends-summit" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/substack/post/likes",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://www.lennysnewsletter.com/p/all-of-the-lenny-and-friends-summit"}
)
print(response.json())
```

## Example Response

```json
{
  "count": 100,
  "likes": [
    {
      "bestseller_tier": 0,
      "full_name": "Christopher L Ross",
      "is_bestseller": false,
      "primary_publication": {
        "logo_url": "",
        "name": "Christopher L Ross",
        "publication_id": "8445348",
        "subdomain": "christopherlross782652",
        "url": "https://christopherlross782652.substack.com"
      },
      "profile_pic_url": "https://substack-post-media.s3.amazonaws.com/public/images/795aab44-1e19-40ff-a4f3-14d22be4346f_144x144.png",
      "url": "https://substack.com/profile/106335682",
      "user_id": "106335682"
    }
  ],
  "post_id": "215694124",
  "post_url": "https://www.lennysnewsletter.com/p/all-of-the-lenny-and-friends-summit",
  "total": 285
}
```
