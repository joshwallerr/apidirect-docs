# LinkedIn Company Details

Get detailed information about a LinkedIn company page by URL. Returns company name, description, employee count, locations, specialities, website, industry, headquarters, similar companies, and more.

## Endpoint

```
GET /v1/linkedin/company
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | Yes | LinkedIn company page URL (max 500 characters) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Company name |
| `company_id` | integer | LinkedIn company ID |
| `url` | string | Company page URL |
| `universal_name` | string | URL-friendly company identifier |
| `description` | string | Company description |
| `tagline` | string | Company tagline |
| `website` | string | Company website URL |
| `industry` | string | Industry category |
| `followers` | integer | Number of LinkedIn followers |
| `employees` | integer | Employee count |
| `employee_range` | string | Employee count range (e.g. "201-500") |
| `founded_year` | integer | Year the company was founded |
| `hashtag` | string | Company hashtag |
| `specialities` | array | Array of company specialities/skills |
| `headquarters` | object | Headquarters location (city, country, region, postal_code, address) |
| `locations` | array | Array of all office locations |
| `logo` | string | Company logo image URL |
| `cover_image` | string | Company cover image URL |
| `call_to_action` | object | Call-to-action button (text, url) |
| `similar_companies` | array | Array of similar companies (name, url, industry, followers, logo) |
| `showcases` | array | Array of affiliated showcase pages (name, url, followers) |
| `source` | string | `"LinkedIn"` |
| `domain` | string | `"linkedin.com"` |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/linkedin/company?url=https://www.linkedin.com/company/visualsoft-uk-ltd" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/linkedin/company",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "url": "https://www.linkedin.com/company/visualsoft-uk-ltd"
    }
)
print(response.json())
```

## Example Response

```json
{
  "name": "Visualsoft | Shopify Plus Partner | Full Service Agency",
  "company_id": 478635,
  "url": "https://www.linkedin.com/company/visualsoft-uk-ltd/",
  "universal_name": "visualsoft-uk-ltd",
  "description": "We deliver the Shopify stores, in-store tech...",
  "tagline": "We deliver the Shopify stores...",
  "website": "http://www.visualsoft.co.uk",
  "industry": "Software Development",
  "followers": 16391,
  "employees": 269,
  "employee_range": "201-500",
  "founded_year": 1998,
  "hashtag": "#digitalmarketing",
  "specialities": ["eCommerce", "Web Design", "SEO", "PPC"],
  "headquarters": {
    "city": "Stockton-on-Tees",
    "country": "GB",
    "region": "Cleveland",
    "postal_code": "TS17 6QY",
    "address": "Visualsoft House"
  },
  "locations": [
    {
      "city": "Newcastle upon Tyne",
      "country": "GB",
      "region": "England",
      "postal_code": "NE1 6EF",
      "address": "71 Grey Street",
      "description": "Newcastle Office",
      "is_headquarters": false
    }
  ],
  "logo": "https://media.licdn.com/...",
  "cover_image": "https://media.licdn.com/...",
  "call_to_action": {
    "text": "Visit website",
    "url": "http://www.visualsoft.co.uk"
  },
  "similar_companies": [
    {
      "name": "Shopify",
      "url": "https://www.linkedin.com/company/shopify/",
      "industry": "Software Development",
      "followers": 1067167,
      "logo": "https://media.licdn.com/..."
    }
  ],
  "showcases": [
    {
      "name": "Visualsoft SEO",
      "url": "https://www.linkedin.com/showcase/visualsoft-seo/",
      "followers": 63
    }
  ],
  "source": "LinkedIn",
  "domain": "linkedin.com"
}
```
