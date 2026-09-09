# Trustpilot Category Details

Get a Trustpilot category's display name, business count, parent, and subcategories. Works at any level of the taxonomy.

## Endpoint

```
GET /v1/trustpilot/category
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `category_id` | Yes | Category slug, e.g. electronics_technology. See [Category IDs](/docs/trustpilot-category-ids). A trustpilot.com/categories/... URL also works |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
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
curl "https://apidirect.io/v1/trustpilot/category?category_id=electronics_technology" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/trustpilot/category",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"category_id": "electronics_technology"}
)
print(response.json())
```

## Example Response

```json
{
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

- Third-level categories (e.g. `cell_phone_store`) have an empty `subcategories` array.
