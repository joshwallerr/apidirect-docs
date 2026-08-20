# YouTube Channel Details

Get detailed information about a YouTube channel by channel ID, URL, or name/handle. Returns channel name, description, subscriber count, video count, total view count, country, creation date, verification status, external links, profile picture, and banner.

## Endpoint

```
GET /v1/youtube/channel
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

## Parameters

Provide exactly one of `id`, `url`, or `name`.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `id` | One required | YouTube channel ID (24 characters, starts with `UC`) |
| `url` | One required | Channel URL: `youtube.com/channel/...`, `youtube.com/@handle`, `/c/` or `/user/` forms |
| `name` | One required | Channel name or @handle (e.g. `@mkbhd` or `Linus Tech Tips`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `channel` | object | Channel data |
| `channel.channel_id` | string | YouTube channel ID |
| `channel.channel_name` | string | Channel name |
| `channel.description` | string | Channel description |
| `channel.subscriber_count` | string/null | Subscriber count (e.g., `"16.9M"`). `null` when hidden. |
| `channel.video_count` | string/null | Number of videos (e.g., `"7.8K"`) |
| `channel.view_count` | integer/null | Exact total channel views |
| `channel.country` | string | Channel country, or empty string when not shared |
| `channel.creation_date` | string | Channel creation date (`YYYY-MM-DD`) |
| `channel.verified` | boolean | Whether the channel is verified |
| `channel.has_business_email` | boolean | Whether the channel lists a business email |
| `channel.links` | array | External links from the channel's About page (`name`, `url`) |
| `channel.profile_pic_url` | string | URL to the highest resolution channel profile picture |
| `channel.banner` | string | URL to the highest resolution channel banner, or empty string when none |
| `channel.url` | string | Link to the channel |

If the channel does not exist, the endpoint returns a `404` with `code: "channel_not_found"`.

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/youtube/channel?id=UCXuqSBlHAE6Xw-yeJA0Tunw" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/youtube/channel",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"id": "UCXuqSBlHAE6Xw-yeJA0Tunw"}
)
print(response.json())
```

You can also pass a channel URL or a name/handle instead of an ID:

```bash
curl "https://apidirect.io/v1/youtube/channel?url=https://www.youtube.com/@mkbhd" \
  -H "X-API-Key: YOUR_API_KEY"

curl "https://apidirect.io/v1/youtube/channel?name=Linus%20Tech%20Tips" \
  -H "X-API-Key: YOUR_API_KEY"
```

## Example Response

```json
{
  "channel": {
    "channel_id": "UCXuqSBlHAE6Xw-yeJA0Tunw",
    "channel_name": "Linus Tech Tips",
    "description": "Linus Tech Tips is a passionate team of \"professionally curious\" experts in consumer technology and video production who aim to educate and entertain.",
    "subscriber_count": "16.9M",
    "video_count": "7.8K",
    "view_count": 9633982641,
    "country": "Canada",
    "creation_date": "2008-11-25",
    "verified": true,
    "has_business_email": true,
    "links": [
      {
        "name": "lttstore.com",
        "url": "https://lttstore.com"
      },
      {
        "name": "Twitter",
        "url": "https://twitter.com/LinusTech"
      }
    ],
    "profile_pic_url": "https://yt3.googleusercontent.com/.../photo.jpg",
    "banner": "https://yt3.googleusercontent.com/.../banner.jpg",
    "url": "https://youtube.com/channel/UCXuqSBlHAE6Xw-yeJA0Tunw"
  }
}
```
