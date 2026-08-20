# Instagram User Profile

Get the full profile for a single Instagram user by username or profile URL. Returns biography, follower / following counts, media count, category, external link, contact info, verification status, and "About this account" info (country the account is based in, join date, verification date, former usernames).

## Endpoint

```
GET /v1/instagram/user
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `username` or `url`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `username` | One required | Instagram username, with or without leading `@` (max 100 characters) |
| `url` | One required | Instagram profile URL, e.g. `https://instagram.com/natgeo` (max 500 characters) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `user` | object | Profile data |
| `user.username` | string | Instagram username |
| `user.full_name` | string | Display name |
| `user.user_id` | string | Instagram user ID |
| `user.biography` | string | Profile biography text |
| `user.follower_count` | integer | Number of followers |
| `user.following_count` | integer | Number of accounts followed |
| `user.media_count` | integer | Total number of posts |
| `user.is_verified` | boolean | Whether the user is verified (blue checkmark) |
| `user.is_private` | boolean | Whether the account is private |
| `user.is_business` | boolean | Whether the account is a business profile |
| `user.category` | string | Business / creator category, or empty string |
| `user.external_url` | string | External link displayed on the profile |
| `user.bio_links` | array | Additional bio link objects with `url` and `title` |
| `user.profile_pic_url` | string | URL to standard-resolution profile picture |
| `user.profile_pic_url_hd` | string | URL to high-resolution profile picture |
| `user.public_email` | string | Public contact email, or empty string |
| `user.public_phone_number` | string | Public contact phone number, or empty string |
| `user.account_based_in` | string | Country the account is based in, or empty string |
| `user.date_joined` | string | Month and year the account joined Instagram (e.g. `November 2010`), or empty string |
| `user.date_joined_timestamp` | integer/null | Unix timestamp of the join date |
| `user.date_verified` | string | Month and year the account was verified, or empty string |
| `user.date_verified_timestamp` | integer/null | Unix timestamp of the verification date |
| `user.former_usernames` | integer/null | Number of former usernames the account has used |
| `user.url` | string | Link to the profile |

The "About this account" fields come from Instagram's public transparency info. Instagram does not expose it for every account, so the string fields can be empty and the `integer/null` fields `null`.

If the username does not exist, the endpoint returns a `404` with `code: "not_found"`.

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/instagram/user?username=natgeo" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/instagram/user",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"username": "natgeo"}
)
print(response.json())
```

You can also pass a profile URL instead of a username:

```bash
curl "https://apidirect.io/v1/instagram/user?url=https://www.instagram.com/natgeo/" \
  -H "X-API-Key: YOUR_API_KEY"
```

## Example Response

```json
{
  "user": {
    "username": "natgeo",
    "full_name": "National Geographic",
    "user_id": "787132",
    "biography": "Step into wonder and find your inner explorer with National Geographic 🌎",
    "follower_count": 274777448,
    "following_count": 194,
    "media_count": 31593,
    "is_verified": true,
    "is_private": false,
    "is_business": true,
    "category": "",
    "external_url": "http://visitstore.bio/natgeo",
    "bio_links": [
      {
        "url": "http://visitstore.bio/natgeo",
        "title": ""
      }
    ],
    "profile_pic_url": "https://scontent.cdninstagram.com/.../photo.jpg",
    "profile_pic_url_hd": "https://scontent.cdninstagram.com/.../photo_hd.jpg",
    "public_email": "",
    "public_phone_number": "",
    "account_based_in": "United States",
    "date_joined": "November 2010",
    "date_joined_timestamp": 1288569600,
    "date_verified": "",
    "date_verified_timestamp": null,
    "former_usernames": 0,
    "url": "https://instagram.com/natgeo"
  }
}
```
