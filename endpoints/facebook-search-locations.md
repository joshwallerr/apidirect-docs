# Facebook Search Locations

Resolve a place name (city, region, or country) to Facebook location IDs. Use a returned `id` as the `location_id` filter on the [Search Posts](/docs/facebook-search-posts) or [Search Events](/docs/facebook-search-events) endpoint to scope a search to that place.

## Endpoint

```
GET /v1/facebook/locations
```

**Price:** $0.004 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Place name to resolve, e.g. `London` or `Paris, France` (max 500 characters) |

> **Tip:** Place names are often ambiguous — "London" matches London in the UK as well as London, Ontario and London, Texas. Use the `label` field to pick the right match, and add a country or region to your query to narrow results (e.g. `query=London, United Kingdom`).

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `results` | array | Array of matching locations |
| `results[].id` | string | Facebook location ID. Pass this to Search Posts or Search Events as `location_id`. |
| `results[].label` | string | Human-readable location name (use this to disambiguate matches) |
| `results[].timezone` | string | IANA timezone of the location (e.g. `Europe/London`) |
| `count` | integer | Number of locations returned |

## Using a location ID to filter posts

Filtering posts by location is a two-step flow. First resolve the place name to an ID:

```bash
curl "https://apidirect.io/v1/facebook/locations?query=London,%20United%20Kingdom" \
  -H "X-API-Key: YOUR_API_KEY"
```

Then pass the `id` from the result you want to [Search Posts](/docs/facebook-search-posts) as `location_id`:

```bash
curl "https://apidirect.io/v1/facebook/posts?query=coffee&location_id=106078429431815" \
  -H "X-API-Key: YOUR_API_KEY"
```

Location filtering biases results toward the chosen place rather than applying a strict geofence, so an occasional out-of-area post may still appear.

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/locations?query=London" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/locations",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"query": "London"}
)
print(response.json())
```

## Example Response

```json
{
  "results": [
    {
      "id": "106078429431815",
      "label": "London, United Kingdom",
      "timezone": "Europe/London"
    },
    {
      "id": "107624535933778",
      "label": "London, Ontario",
      "timezone": "America/Toronto"
    },
    {
      "id": "108364785855057",
      "label": "London, Kentucky",
      "timezone": "America/New_York"
    }
  ],
  "count": 3
}
```
