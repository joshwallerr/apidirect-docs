# Facebook Search Pages

Search for Facebook pages by keyword. Returns page name, URL, profile image, and verification status.

## Endpoint

```
GET /v1/facebook/pages
```

**Price:** $0.008 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch (1-10, default 1). Billed per page. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `results` | array | Array of matching Facebook pages |
| `results[].name` | string | Page display name |
| `results[].facebook_id` | string | Unique numeric page identifier |
| `results[].url` | string | Direct link to the page |
| `results[].profile_url` | string | Profile URL of the page |
| `results[].image_url` | string | URL of the page's profile image |
| `results[].is_verified` | boolean | Whether the page is verified |
| `count` | integer | Number of results returned |
| `pages` | integer | Number of pages fetched |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/pages?query=nike" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/pages",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "nike"
    }
)
print(response.json())
```

## Example Response

```json
{
  "results": [
    {
      "name": "Nike",
      "facebook_id": "15087023444",
      "url": "https://www.facebook.com/nike",
      "profile_url": "https://www.facebook.com/nike",
      "image_url": "https://scontent.fxxx.fbcdn.net/v/t39.30808-1/nike_logo.jpg",
      "is_verified": true
    },
    {
      "name": "Nike Running",
      "facebook_id": "116784541498",
      "url": "https://www.facebook.com/nikerunning",
      "profile_url": "https://www.facebook.com/nikerunning",
      "image_url": "https://scontent.fxxx.fbcdn.net/v/t39.30808-1/nike_running_logo.jpg",
      "is_verified": true
    },
    {
      "name": "Nike Skateboarding",
      "facebook_id": "391740174562",
      "url": "https://www.facebook.com/nikeskateboarding",
      "profile_url": "https://www.facebook.com/nikeskateboarding",
      "image_url": "https://scontent.fxxx.fbcdn.net/v/t39.30808-1/nike_sb_logo.jpg",
      "is_verified": false
    }
  ],
  "count": 3,
  "pages": 1
}
```
