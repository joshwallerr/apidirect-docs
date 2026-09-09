# Trustpilot Category Search

Search Trustpilot categories by keyword to find category IDs at any level of the taxonomy.

## Endpoint

```
GET /v1/trustpilot/categories
```

**Price:** $0.005 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Keyword, e.g. bank or shop (max 200 characters) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `categories` | array | Matching categories |
| `categories[].category_id` | string | Category ID (slug) — pass to [Category Companies](/docs/trustpilot-category-companies) or [Category Details](/docs/trustpilot-category) |
| `categories[].name` | string | Display name |
| `count` | integer | Number of categories returned |
| `query` | string | Echo of the search query |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/trustpilot/categories?query=bank" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/trustpilot/categories",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "bank"}
)
print(response.json())
```

## Example Response

```json
{
  "categories": [
    {
      "category_id": "bank",
      "name": "Bank"
    },
    {
      "category_id": "savings_bank",
      "name": "Savings Bank"
    },
    {
      "category_id": "private_sector_bank",
      "name": "Private Sector Bank"
    },
    {
      "category_id": "investment_bank",
      "name": "Investment Bank"
    },
    {
      "category_id": "central_bank",
      "name": "Central Bank"
    },
    {
      "category_id": "trust_bank",
      "name": "Trust Bank"
    }
  ],
  "count": 6,
  "query": "bank"
}
```

## Notes

- The search is fuzzy and always returns up to 6 closest matches, even for a keyword that matches nothing well — check the names before using an ID.
- The full two-level taxonomy is on the [Category IDs](/docs/trustpilot-category-ids) page.
