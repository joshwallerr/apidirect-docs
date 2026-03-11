# Facebook Page Photos

Get photos from a Facebook page by page ID. Returns photo IDs and image URLs. Supports fetching multiple pages in a single call.

## Endpoint

```
GET /v1/facebook/page/photos
```

**Price:** $0.008 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `page_id` | Yes | Facebook page ID (get from page details or page ID endpoint) |
| `pages` | No | Number of pages to fetch (1-10, default 1). Billed per page. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `photos` | array | List of photo objects |
| `photos[].photo_id` | string | Unique photo ID |
| `photos[].image_url` | string | URL to the image |
| `count` | integer | Number of photos returned |
| `pages` | integer | Number of pages fetched |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/page/photos?page_id=100064860875397" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/page/photos",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"page_id": "100064860875397"}
)
print(response.json())
```

## Example Response

```json
{
  "photos": [
    {
      "photo_id": "1442778724560810",
      "image_url": "https://scontent.xx.fbcdn.net/v/t39.30808-6/648337_..._n.jpg"
    },
    {
      "photo_id": "1442778694560813",
      "image_url": "https://scontent.xx.fbcdn.net/v/t39.30808-6/648291_..._n.jpg"
    }
  ],
  "count": 2,
  "pages": 1
}
```
