# Places Search

Search Google Maps places — local businesses, restaurants, hotels, shops and points of interest — by free-text query. Returns name, address, phone, website, rating, review count, opening hours, and coordinates for each result. Optionally bias results by geographic center.

## Endpoint

```
GET /v1/places/search
```

**Price:** $0.01 per page
**Free tier:** 20 requests/month

Each page returns up to 10 places.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters). E.g. `coffee shops brooklyn`, `dentists 90210`, `hilton hotels paris` |
| `pages` | No | Number of pages to fetch, 1-20 (default: 1). Each page returns up to 10 results and is billed as one request |
| `lat` | No | Center latitude for geographic bias (provide with `lng`) |
| `lng` | No | Center longitude for geographic bias (provide with `lat`) |
| `zoom` | No | Map zoom level 1-20 (default: 13). Smaller values widen the search radius |
| `country` | No | 2-letter ISO 3166-1 alpha-2 region code (default: `us`) |
| `language` | No | 2-letter ISO 639-1 language code (default: `en`) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `places` | array | Array of matching places |
| `places[].place_id` | string | Google place_id (`ChIJ...`) |
| `places[].name` | string | Place display name |
| `places[].type` | string | Primary category (e.g. `Pizza restaurant`) |
| `places[].subtypes` | array | All Google categories |
| `places[].phone_number` | string \| null | Phone number in E.164 format |
| `places[].website` | string \| null | Official website URL |
| `places[].domain` | string \| null | Website apex domain (e.g. `joespizzanyc.com`) |
| `places[].rating` | number \| null | Average rating, 0.0–5.0 |
| `places[].review_count` | integer | Total number of reviews |
| `places[].reviews_per_rating` | object | Count of reviews per star (`{"1": N, "2": N, ...}`) |
| `places[].price_level` | string \| null | Price indicator (e.g. `$`, `$10–20`) |
| `places[].verified` | boolean | Whether the listing is verified by Google |
| `places[].business_status` | string | `OPEN`, `CLOSED_TEMPORARILY`, `CLOSED_PERMANENTLY` |
| `places[].opening_status` | string \| null | Human-readable status (e.g. `Open · Closes 3 AM`) |
| `places[].working_hours` | object \| null | Hours by day-of-week |
| `places[].opening_date` | string \| null | First listing date if known |
| `places[].address` | string | Full address |
| `places[].street_address` | string \| null | Street component only |
| `places[].district` | string \| null | District / neighborhood |
| `places[].city` | string \| null | City |
| `places[].state` | string \| null | State / region |
| `places[].zipcode` | string \| null | Postal code |
| `places[].country` | string \| null | Country code |
| `places[].latitude` | number | Latitude |
| `places[].longitude` | number | Longitude |
| `places[].timezone` | string \| null | IANA timezone (e.g. `America/New_York`) |
| `places[].summary` | string \| null | Short editorial summary |
| `places[].about` | object \| null | Structured About panel (`summary` plus a `details` object of categorised attributes) |
| `places[].photo_count` | integer | Total photos available |
| `places[].photos_sample` | array | Sample of recent photos (same shape as [Place Photos](/docs/places-photos) items) |
| `places[].place_link` | string | Google Maps URL |
| `places[].reviews_link` | string \| null | Google reviews URL |
| `places[].booking_link` | string \| null | Booking URL if available |
| `places[].reservations_link` | string \| null | Reservation URL if available |
| `places[].order_link` | string \| null | Online order URL if available |
| `places[].owner_name` | string \| null | Listing owner name |
| `places[].owner_link` | string \| null | Listing owner profile URL |
| `places[].cid` | string | Google CID identifier |
| `count` | integer | Number of places returned |
| `query` | string | Echo of the search query |
| `pages` | integer | Echo of the requested pages |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/places/search?query=pizza%20new%20york&pages=2" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/places/search",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "pizza new york",
        "pages": 2,
        "lat": 40.7549,
        "lng": -73.9870,
        "zoom": 14,
    }
)
print(response.json())
```

## Example Response

```json
{
  "places": [
    {
      "place_id": "ChIJifIePKtZwokRVZ-UdRGkZzs",
      "name": "Joe's Pizza Broadway",
      "type": "Pizza restaurant",
      "subtypes": ["Pizza restaurant", "Pizza delivery", "Restaurant"],
      "phone_number": "+16465594878",
      "website": "https://www.joespizzanyc.com",
      "domain": "joespizzanyc.com",
      "rating": 4.5,
      "review_count": 25433,
      "reviews_per_rating": {"1": 753, "2": 604, "3": 2107, "4": 4946, "5": 17023},
      "price_level": "$10–20",
      "verified": true,
      "business_status": "OPEN",
      "opening_status": "Open · Closes 3 AM",
      "working_hours": {"Monday": ["10 AM–3 AM"], "Sunday": ["10 AM–3 AM"]},
      "opening_date": null,
      "address": "Joe's Pizza Broadway, 1435 Broadway, New York, NY 10018",
      "street_address": "1435 Broadway",
      "district": "Manhattan",
      "city": "New York",
      "state": "New York",
      "zipcode": "10018",
      "country": "US",
      "latitude": 40.75468,
      "longitude": -73.98703,
      "timezone": "America/New_York",
      "summary": "Modern outpost of a longtime counter-serve pizza joint prepping New York-style slices and pies.",
      "about": {
        "summary": "Modern outpost of a longtime counter-serve pizza joint prepping New York-style slices and pies.",
        "details": {
          "Accessibility": {
            "Wheelchair accessible entrance": true,
            "Wheelchair accessible parking lot": false,
            "Wheelchair accessible seating": false
          }
        }
      },
      "photo_count": 22117,
      "photos_sample": [
        {
          "photo_id": "CIABIhBpKlqRIOpwhdI384bUAF4L",
          "type": "photo",
          "photo_url": "https://lh3.googleusercontent.com/gps-cs-s/APNQkAH...",
          "photo_url_large": "https://lh3.googleusercontent.com/gps-cs-s/APNQkAH...=w3000-h4000-k-no",
          "video_thumbnail_url": null,
          "latitude": 40.7546469,
          "longitude": -73.9868158,
          "photo_datetime_utc": "2026-06-16T00:00:00.000Z",
          "photo_timestamp": 1781568000
        }
      ],
      "place_link": "https://www.google.com/maps/place/data=...",
      "reviews_link": "https://search.google.com/local/reviews?placeid=ChIJifIePKtZwokRVZ-UdRGkZzs",
      "booking_link": "https://www.google.com/searchviewer/42?...",
      "reservations_link": "https://www.fooddiscoveryapp.com/new-york-city/joes-pizza",
      "order_link": "https://www.google.com/searchviewer/42?...",
      "owner_name": "Joe's Pizza Broadway",
      "owner_link": "https://maps.google.com/maps/contrib/103877821925204408966",
      "cid": "4280570365733019477"
    }
  ],
  "count": 1,
  "query": "pizza new york",
  "pages": 2
}
```

## Notes

- The `place_id` field is the standard Google identifier. Pass it to [Place Details](/docs/places-details), [Place Reviews](/docs/places-reviews) and [Place Photos](/docs/places-photos) to fetch more data about a result.
- When you provide `lat` and `lng`, results are biased to that area. Without coordinates, results use a default center; for accurate local results, always pass coordinates.
- The `zoom` level mirrors Google Maps zoom — `13` covers roughly a city, `15` a neighborhood, `10` a metro area.
