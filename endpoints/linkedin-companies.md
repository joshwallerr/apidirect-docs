# LinkedIn Companies

Search LinkedIn companies by keyword. Returns company name, description, industry, location, follower count, logo, and direct link. Supports pagination with 10 results per page.

## Endpoint

```
GET /v1/linkedin/companies
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `page` | No | Page number, 1-100 (default: 1). Each page returns 10 results. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `companies` | array | Array of matching companies |
| `companies[].name` | string | Company name |
| `companies[].company_id` | string | LinkedIn company ID |
| `companies[].description` | string | Company summary / tagline |
| `companies[].subtitle` | string | Industry and location (e.g., "Software Development - San Francisco") |
| `companies[].followers` | string | Follower count (e.g., "2M followers") |
| `companies[].logo` | string | URL to company logo |
| `companies[].url` | string | Link to the LinkedIn company page |
| `page` | integer | Current page number |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/linkedin/companies?query=AI&page=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/linkedin/companies",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "AI", "page": 1}
)
print(response.json())
```

## Example Response

```json
{
  "companies": [
    {
      "name": "AI For Enterprise",
      "company_id": "69206356",
      "description": "Become better at AI in just 1 minute a day.",
      "subtitle": "Business Content - San Francisco",
      "followers": "2M followers",
      "logo": "https://media.licdn.com/dms/image/.../company-logo.jpg",
      "url": "https://www.linkedin.com/company/aiforenterprise/"
    }
  ],
  "page": 1,
  "count": 10
}
```
