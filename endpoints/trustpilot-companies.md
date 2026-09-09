# Trustpilot Company Search

Search Trustpilot companies by name or keyword. Returns 10 matches per page, plus the categories that match the query.

## Endpoint

```
GET /v1/trustpilot/companies
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

Each page returns up to 10 companies.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Company name or keyword (max 500 characters) |
| `page` | No | Page number, 1-500 (default: 1). Each page returns up to 10 results |
| `min_rating` | No | Only companies with at least this TrustScore: 3, 4, 4.5 |
| `min_review_count` | No | Only companies with at least this many reviews: 25, 50, 100, 250, 500 |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `companies` | array | Array of matching companies |
| `companies[].business_unit_id` | string | Trustpilot business unit ID |
| `companies[].name` | string | Company display name |
| `companies[].domain` | string | Company website domain — pass to [Company Reviews](/docs/trustpilot-company-reviews) as `domain` |
| `companies[].website` | string \| null | Company website URL |
| `companies[].url` | string | Trustpilot review page URL |
| `companies[].logo` | string \| null | Company logo URL |
| `companies[].rating` | number \| null | TrustScore, 1.0-5.0 (Trustpilot's weighted score, favours recent reviews) |
| `companies[].stars` | number \| null | TrustScore rounded to the nearest half star (display value) |
| `companies[].review_count` | integer \| null | Total number of reviews |
| `companies[].categories` | array | Categories the company is listed in: `category_id`, `name`, `is_primary` |
| `companies[].city` | string \| null | City |
| `companies[].country` | string \| null | Country name (e.g. `United States`) |
| `companies[].address` | string \| null | Street address |
| `companies[].zipcode` | string \| null | Postal code |
| `companies[].is_recommended` | boolean \| null | Whether Trustpilot recommends the company within its categories |
| `count` | integer | Number of companies returned |
| `page` | integer | Current page number |
| `total_pages` | integer \| null | Total pages available for this query |
| `total_results` | integer \| null | Total matching companies |
| `query` | string | Echo of the search query |
| `categories` | array | Categories matching the query: `category_id`, `name` — pass to [Category Companies](/docs/trustpilot-category-companies) |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/trustpilot/companies?query=amazon" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/trustpilot/companies",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "amazon"}
)
print(response.json())
```

## Example Response

```json
{
  "companies": [
    {
      "business_unit_id": "46ad346800006400050092d0",
      "name": "Amazon",
      "domain": "www.amazon.com",
      "website": "https://www.amazon.com",
      "url": "https://www.trustpilot.com/review/www.amazon.com",
      "logo": null,
      "rating": 1.6,
      "stars": 1.5,
      "review_count": 48972,
      "categories": [
        {
          "category_id": "book_store",
          "name": "Book Store",
          "is_primary": false
        },
        {
          "category_id": "clothing_store",
          "name": "Clothing Store",
          "is_primary": false
        },
        {
          "category_id": "shoe_store",
          "name": "Shoe Store",
          "is_primary": false
        },
        {
          "category_id": "hobby_store",
          "name": "Hobby Store",
          "is_primary": false
        }
      ],
      "city": null,
      "country": "United Kingdom",
      "address": null,
      "zipcode": null,
      "is_recommended": false
    },
    {
      "business_unit_id": "46d72ac0000064000500e9bb",
      "name": "Amazon",
      "domain": "www.amazon.fr",
      "website": "https://www.amazon.fr",
      "url": "https://www.trustpilot.com/review/www.amazon.fr",
      "logo": null,
      "rating": 1.6,
      "stars": 1.5,
      "review_count": 19281,
      "categories": [
        {
          "category_id": "events_entertainment",
          "name": "Events & Entertainment",
          "is_primary": false
        }
      ],
      "city": null,
      "country": "France",
      "address": null,
      "zipcode": null,
      "is_recommended": false
    }
  ],
  "count": 10,
  "page": 1,
  "total_pages": 56,
  "total_results": 557,
  "query": "amazon",
  "categories": [
    {
      "category_id": "book_store",
      "name": "Book Store"
    },
    {
      "category_id": "e_commerce_agency",
      "name": "e-Commerce Agency"
    },
    {
      "category_id": "e_commerce_service",
      "name": "e-Commerce Service"
    }
  ]
}
```

## Notes

- `country` on each company is a country name, not a code; the company profile returned by Company Reviews carries the ISO code.
