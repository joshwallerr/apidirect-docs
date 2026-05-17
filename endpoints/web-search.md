# Web Search

Search the web and get Google organic search results in real time. Returns title, URL, snippet, source and domain for each result. Supports country/language targeting, time filters, city-level geo, and an optional Google AI Overview.

## Endpoint

```
GET /v1/web/search
```

**Price:** $0.004 per page (+$0.002 flat per request when `include_ai_overview=true`)
**Free tier:** 50 requests/month

A "page" is 10 results. Each page you request consumes one billable request, so `pages=3` is billed as 3 requests.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters). Supports Google advanced operators (`site:`, `inurl:`, `intitle:`, etc.) |
| `pages` | No | Number of result pages to fetch, 1-10 (default: 1). 10 results per page |
| `country` | No | 2-letter ISO 3166-1 alpha-2 country code (default: `us`) |
| `language` | No | 2-letter ISO 639-1 language code (default: `en`) |
| `time` | No | Time filter: `any`, `hour`, `day`, `week`, `month`, `year` (default: `any`) |
| `location` | No | City-level geo location (e.g. `London,England,United Kingdom`) |
| `device` | No | `desktop` or `mobile` (default: `desktop`) |
| `include_ai_overview` | No | When `true`, include Google AI Overview if available. Adds $0.002 flat to the request, regardless of how many pages you request |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `results` | array | Array of organic search results across all requested pages |
| `results[].position` | integer | Position on the result page |
| `results[].rank` | integer | Overall rank across the merged result set |
| `results[].title` | string | Result title |
| `results[].url` | string | Result URL |
| `results[].snippet` | string | Result snippet |
| `results[].source` | string | Result source name |
| `results[].domain` | string | Result domain |
| `results[].displayed_link` | string | Breadcrumb-style URL as displayed in the SERP |
| `pages` | integer | Number of pages requested |
| `count` | integer | Total results returned |
| `ai_overview` | object \| null | AI Overview content (only present when `include_ai_overview=true`). May be `null` if no overview was generated for this query |
| `ai_overview.text_parts` | array | Ordered list of overview parts (`paragraph`, `heading`, `list`, etc.) |
| `ai_overview.reference_links` | array | Citation links backing the overview |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/web/search?query=how%20to%20build%20a%20website&pages=2&country=us&language=en" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/web/search",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "how to build a website",
        "pages": 2,
        "country": "us",
        "language": "en",
        "include_ai_overview": "true"
    }
)
print(response.json())
```

## Example Response

```json
{
  "results": [
    {
      "position": 1,
      "rank": 1,
      "title": "Website Builder - Create a Free Website",
      "url": "https://www.canva.com/website-builder/",
      "snippet": "Design and launch a professional, one-of-a-kind website in minutes...",
      "source": "Canva",
      "domain": "canva.com",
      "displayed_link": "https://www.canva.com › website-builder"
    },
    {
      "position": 2,
      "rank": 2,
      "title": "Wix.com: Website Builder - Create a Free Website In Minutes",
      "url": "https://www.wix.com/",
      "snippet": "Get everything you need to create your website, your way...",
      "source": "Wix",
      "domain": "wix.com",
      "displayed_link": "https://www.wix.com"
    }
  ],
  "pages": 2,
  "count": 20,
  "ai_overview": {
    "text_parts": [
      {
        "type": "paragraph",
        "text": "Building a website involves choosing a platform, designing pages, and publishing. Most modern builders offer drag-and-drop interfaces..."
      }
    ],
    "reference_links": [
      {
        "title": "How to Create a Website From Scratch",
        "link": "https://www.wix.com/blog/how-to-build-website-from-scratch-guide",
        "source": "Wix"
      }
    ]
  }
}
```

## Notes

- `pages` is a count, not a page number. `pages=3` returns the first 30 results merged into a single `results` array.
- AI Overviews are only returned when Google generates one for the query. Even with `include_ai_overview=true`, expect `ai_overview` to be `null` for some queries. The $0.002 surcharge applies whenever the flag is set.
- Use the `location` parameter to simulate searches from a specific city. Common formats include `City,State,Country` (e.g., `New York,New York,United States`).
