# Facebook Search Events

Search public Facebook events by keyword. Returns event names, event IDs, and direct event page links. Filter by date range or location.

## Endpoint

```
GET /v1/facebook/events
```

**Price:** $0.008 per page
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `pages` | No | Number of pages to fetch (1-15, default 1). Billed per page. |
| `start_date` | No | Filter events from this date onward (format: `YYYY-MM-DD`) |
| `end_date` | No | Filter events up to this date (format: `YYYY-MM-DD`) |
| `location_id` | No | Facebook location ID to scope results to a place. Resolve one from a place name with the [Search Locations](/docs/facebook-search-locations) endpoint. |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `events` | array | Array of matching events |
| `events[].event_id` | string | Unique event identifier |
| `events[].title` | string | Event name |
| `events[].url` | string | Direct link to the event page |
| `count` | integer | Number of events returned |
| `pages` | integer | Number of pages fetched |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/events?query=music%20festival" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/events",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "music festival"
    }
)
print(response.json())
```

## Example Response

```json
{
  "events": [
    {
      "event_id": "1613570396584259",
      "title": "3rd Island Music Festival",
      "url": "https://www.facebook.com/events/1613570396584259/"
    },
    {
      "event_id": "947635377782868",
      "title": "Outlaw Festival: Willie Nelson, Wilco, Sheryl Crow & More!",
      "url": "https://www.facebook.com/events/947635377782868/"
    }
  ],
  "count": 2,
  "pages": 1
}
```
