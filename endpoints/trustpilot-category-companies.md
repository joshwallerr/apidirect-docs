# Trustpilot Category Companies

List the companies in a Trustpilot category, ranked, 20 per page, along with the category's size and subcategories.

## Endpoint

```
GET /v1/trustpilot/category/companies
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

Each page returns up to 20 companies.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `category_id` | Yes | Category slug, e.g. bank or electronics_technology. See [Category IDs](/docs/trustpilot-category-ids). A trustpilot.com/categories/... URL also works |
| `page` | No | Page number, 1-500 (default: 1). Each page returns up to 20 companies |
| `sort_by` | No | recommended (default), recently_reviewed |
| `country` | No | 2-letter ISO 3166-1 country code (e.g. us, gb, de). Default: all countries |
| `min_rating` | No | Only companies with at least this TrustScore: 3, 3.5, 4, 4.5 |
| `claimed` | No | Set to true to return only companies that have claimed their Trustpilot profile |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `companies` | array | Companies in the category, in ranked order |
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
| `total_pages` | integer \| null | Total pages available (Trustpilot serves at most 500) |
| `total_companies` | integer \| null | Total companies matching the filters (capped at 10,000 by Trustpilot) |
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
curl "https://apidirect.io/v1/trustpilot/category/companies?category_id=electronics_technology&country=us&min_rating=4" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/trustpilot/category/companies",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "category_id": "electronics_technology",
        "country": "us",
        "min_rating": "4"
    }
)
print(response.json())
```

## Example Response

```json
{
  "companies": [
    {
      "business_unit_id": "4bdc9828000064000505dc60",
      "name": "Flashbay",
      "domain": "www.flashbay.com",
      "website": "https://www.flashbay.com",
      "url": "https://www.trustpilot.com/review/www.flashbay.com",
      "logo": "https://s3-eu-west-1.amazonaws.com/tpd/screenshotlogo-domain/4bdc9828000064000505dc60/198x149.png",
      "rating": 5.0,
      "stars": 5.0,
      "review_count": 19329,
      "categories": [
        {
          "category_id": "gift_shop",
          "name": "Gift Shop",
          "is_primary": false
        },
        {
          "category_id": "hobby_store",
          "name": "Hobby Store",
          "is_primary": false
        },
        {
          "category_id": "business_to_business_service",
          "name": "Business to Business Service",
          "is_primary": false
        },
        {
          "category_id": "promotional_items_store",
          "name": "Promotional Item Store",
          "is_primary": true
        },
        {
          "category_id": "computer_accessories_store",
          "name": "Computer Accessories Store",
          "is_primary": false
        },
        {
          "category_id": "drives_and_storage_service",
          "name": "Drives and Storage Service",
          "is_primary": false
        }
      ],
      "city": null,
      "country": "United States",
      "address": "Flashbay Inc. 569 Clyde Avenue, Unit 500, Mountain View, CA 94043",
      "zipcode": null,
      "is_recommended": true
    },
    {
      "business_unit_id": "4bdc7d56000064000505cb54",
      "name": "TadiBrothers",
      "domain": "www.tadibrothers.com",
      "website": "https://www.tadibrothers.com",
      "url": "https://www.trustpilot.com/review/www.tadibrothers.com",
      "logo": "https://s3-eu-west-1.amazonaws.com/tpd/screenshotlogo-domain/4bdc7d56000064000505cb54/198x149.png",
      "rating": 5.0,
      "stars": 5.0,
      "review_count": 3685,
      "categories": [
        {
          "category_id": "electronics_store",
          "name": "Electronics Store",
          "is_primary": true
        },
        {
          "category_id": "auto_repair_shop",
          "name": "Auto Repair Shop",
          "is_primary": false
        },
        {
          "category_id": "truck_parts_supplier",
          "name": "Truck Parts Supplier",
          "is_primary": false
        },
        {
          "category_id": "safety_equipment_supplier",
          "name": "Safety Equipment Supplier",
          "is_primary": false
        },
        {
          "category_id": "auto_body_parts_supplier",
          "name": "Auto Body Parts Supplier",
          "is_primary": false
        },
        {
          "category_id": "horsebox_specialist",
          "name": "Horse Transport Supplier",
          "is_primary": false
        }
      ],
      "city": "Reseda",
      "country": "United States",
      "address": "6924 Canby Ave, #107",
      "zipcode": "91335",
      "is_recommended": true
    }
  ],
  "count": 20,
  "page": 1,
  "total_pages": 500,
  "total_companies": 10000,
  "category": {
    "category_id": "electronics_technology",
    "name": "Electronics & Technology",
    "business_count": 59806,
    "parent_id": null,
    "url": "https://www.trustpilot.com/categories/electronics_technology",
    "subcategories": [
      {
        "category_id": "appliances_electronics",
        "name": "Appliances & Electronics",
        "business_count": 5569
      },
      {
        "category_id": "audio_visual",
        "name": "Audio & Visual",
        "business_count": 1807
      },
      {
        "category_id": "computers_phones",
        "name": "Computers & Phones",
        "business_count": 8342
      },
      {
        "category_id": "internet_software",
        "name": "Internet & Software",
        "business_count": 45334
      },
      {
        "category_id": "repair_services",
        "name": "Repair & Services",
        "business_count": 2857
      }
    ]
  }
}
```

## Notes

- Category IDs are listed on the [Category IDs](/docs/trustpilot-category-ids) page; deeper slugs (e.g. `cell_phone_store`) also work. Find them with [Category Search](/docs/trustpilot-categories) or a category's `subcategories`.
- `total_companies` is capped at 10,000 by Trustpilot even for larger categories; `category.business_count` carries the real size.
