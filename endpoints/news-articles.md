# News Articles

Search news articles from thousands of sources worldwide. Returns article title, URL, snippet, author, source, and publication date. Supports filtering by time period, source, country, and language.

## Endpoint

```
GET /v1/news/articles
```

**Price:** $0.008 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `limit` | No | Number of results to return, 1-100 (default: 10) |
| `time_published` | No | Time filter: `anytime`, `1h`, `1d`, `7d`, `1m`, `1y` (default: `anytime`) |
| `source` | No | Filter by news source (e.g., `bbc.com`) |
| `country` | No | 2-letter country code (default: `us`) |
| `language` | No | 2-letter language code (default: `en`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `articles` | array | Array of matching news articles |
| `articles[].title` | string | Article headline |
| `articles[].url` | string | Direct link to the article |
| `articles[].snippet` | string | Article content preview |
| `articles[].photo_url` | string | Article photo URL |
| `articles[].thumbnail_url` | string | Article thumbnail URL |
| `articles[].published_datetime_utc` | string | Publication date and time in UTC |
| `articles[].authors` | array | List of author names |
| `articles[].source_url` | string | News source URL |
| `articles[].source_name` | string | News source name |
| `articles[].source_favicon_url` | string | News source favicon URL |
| `articles[].domain` | string | Article domain name |
| `limit` | integer | Requested result limit |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/news/articles?query=artificial%20intelligence&limit=10&time_published=1d&country=us&language=en" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/news/articles",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "artificial intelligence",
        "limit": 10,
        "time_published": "1d",
        "country": "us",
        "language": "en"
    }
)
print(response.json())
```

## Example Response

```json
{
  "articles": [
    {
      "title": "New AI Breakthrough Changes the Industry",
      "url": "https://example.com/article/ai-breakthrough",
      "snippet": "Researchers have announced a major advancement in artificial intelligence...",
      "photo_url": "https://example.com/images/ai-photo.jpg",
      "thumbnail_url": "https://example.com/images/ai-thumb.jpg",
      "published_datetime_utc": "2025-01-15 14:30:00",
      "authors": ["Jane Smith", "John Doe"],
      "source_url": "https://example.com",
      "source_name": "Example News",
      "source_favicon_url": "https://example.com/favicon.ico",
      "domain": "example.com"
    }
  ],
  "limit": 10,
  "count": 1
}
```
