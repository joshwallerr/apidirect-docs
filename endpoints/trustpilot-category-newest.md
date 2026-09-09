# Trustpilot Category Newest

Get the newest companies added to a Trustpilot category — the short list shown on the category page, plus the category's size and subcategories.

## Endpoint

```
GET /v1/trustpilot/category/newest
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `category_id` | Yes | Category slug, e.g. bank. See [Category IDs](/docs/trustpilot-category-ids). A trustpilot.com/categories/... URL also works |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `companies` | array | Newest companies in the category, newest first |
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
| `category` | object | The category |
| `category.category_id` | string | Category ID (slug) |
| `category.name` | string \| null | Display name |
| `category.business_count` | integer \| null | Number of businesses in the category |
| `category.parent_id` | string \| null | Parent category ID, `null` for a top-level category |
| `category.url` | string | Category page URL on Trustpilot |
| `category.subcategories` | array | Direct subcategories: `category_id`, `name`, `business_count` |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/trustpilot/category/newest?category_id=bank" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/trustpilot/category/newest",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"category_id": "bank"}
)
print(response.json())
```

## Example Response

```json
{
  "companies": [
    {
      "business_unit_id": "6a7e73aed75f36cab8924224",
      "name": "Lutonsavings",
      "domain": "www.lutonsavings.com",
      "website": null,
      "url": "https://www.trustpilot.com/review/www.lutonsavings.com",
      "logo": null,
      "rating": 2.9,
      "stars": 3.0,
      "review_count": 2,
      "categories": [
        {
          "category_id": "savings_bank",
          "name": "Savings Bank",
          "is_primary": true
        },
        {
          "category_id": "bank",
          "name": "Bank",
          "is_primary": false
        },
        {
          "category_id": "non_bank_finance",
          "name": "Non-Bank Financial Service",
          "is_primary": false
        },
        {
          "category_id": "financial_consultant",
          "name": "Financial Consultant",
          "is_primary": false
        }
      ],
      "city": "",
      "country": "United States",
      "address": null,
      "zipcode": null,
      "is_recommended": null
    },
    {
      "business_unit_id": "6a8bf26af4ba0eb8dbbfe55c",
      "name": "Trustbankonline",
      "domain": "trustbankonline.com",
      "website": null,
      "url": "https://www.trustpilot.com/review/trustbankonline.com",
      "logo": null,
      "rating": 3.2,
      "stars": 3.0,
      "review_count": 1,
      "categories": [
        {
          "category_id": "financial_institution",
          "name": "Financial Institution",
          "is_primary": false
        },
        {
          "category_id": "cryptocurrency_service",
          "name": "Cryptocurrency Service",
          "is_primary": true
        },
        {
          "category_id": "bank",
          "name": "Bank",
          "is_primary": false
        },
        {
          "category_id": "financial_consultant",
          "name": "Financial Consultant",
          "is_primary": false
        },
        {
          "category_id": "currency_exchange_service",
          "name": "Currency Exchange Service",
          "is_primary": false
        }
      ],
      "city": "",
      "country": "United States",
      "address": null,
      "zipcode": null,
      "is_recommended": null
    }
  ],
  "count": 10,
  "category": {
    "category_id": "bank",
    "name": "Bank",
    "business_count": 1861,
    "parent_id": "banking_money",
    "url": "https://www.trustpilot.com/categories/bank",
    "subcategories": []
  }
}
```

## Notes

- This is Trustpilot's own "newest companies" list for the category, typically 0-10 entries; many categories have none at a given moment.
- For the full, paginated list of companies in a category use [Category Companies](/docs/trustpilot-category-companies).
