# Place Details

Get full details for a single Google Maps place by `place_id`. Returns everything Places Search returns, plus Plus Codes, a menu link, and an `emails_and_contacts` scrape of the place's official website (emails, phone numbers and links to 10 social platforms).

## Endpoint

```
GET /v1/places/details
```

**Price:** $0.003 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `place_id` | Yes | Google `place_id` (e.g. `ChIJifIePKtZwokRVZ-UdRGkZzs`), as returned by the [Places Search](/docs/places-search) endpoint |
| `country` | No | 2-letter ISO 3166-1 alpha-2 region code (default: `us`) |
| `language` | No | 2-letter ISO 639-1 language code (default: `en`) |

## Response Fields

The `place` object has the same schema as items in [Places Search](/docs/places-search), plus the fields below.

| Field | Type | Description |
|-------|------|-------------|
| `place` | object | Full place object (see [Places Search](/docs/places-search) for the shared schema) |
| `place.global_plus_code` | string \| null | Global Plus Code (e.g. `87G8Q237+V5`) |
| `place.compound_plus_code` | string \| null | Compound Plus Code (e.g. `Q237+V5 New York`) |
| `place.menu_link` | string \| null | Menu URL if the place has one |
| `place.emails_and_contacts` | object | Scrape of the place's official website |
| `place.emails_and_contacts.emails` | array | Email addresses found on the site |
| `place.emails_and_contacts.phone_numbers` | array | Phone numbers found on the site (raw, not normalized to E.164) |
| `place.emails_and_contacts.facebook` | string \| null | Facebook profile URL |
| `place.emails_and_contacts.instagram` | string \| null | Instagram profile URL |
| `place.emails_and_contacts.linkedin` | string \| null | LinkedIn profile URL |
| `place.emails_and_contacts.twitter` | string \| null | Twitter/X profile URL |
| `place.emails_and_contacts.tiktok` | string \| null | TikTok profile URL |
| `place.emails_and_contacts.youtube` | string \| null | YouTube channel URL |
| `place.emails_and_contacts.pinterest` | string \| null | Pinterest profile URL |
| `place.emails_and_contacts.snapchat` | string \| null | Snapchat profile URL |
| `place.emails_and_contacts.yelp` | string \| null | Yelp listing URL |
| `place.emails_and_contacts.github` | string \| null | GitHub profile URL |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/places/details?place_id=ChIJifIePKtZwokRVZ-UdRGkZzs" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/places/details",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"place_id": "ChIJifIePKtZwokRVZ-UdRGkZzs"}
)
print(response.json())
```

## Example Response

```json
{
  "place": {
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
    "working_hours": {"Monday": ["10 AM–3 AM"]},
    "opening_date": null,
    "address": "1435 Broadway, New York, NY 10018",
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
        "photo_id": "CIABIhAViB6GuQB0Czq6u1UIyD60",
        "type": "photo",
        "photo_url": "https://lh3.googleusercontent.com/gps-cs-s/APNQkAH...",
        "photo_url_large": "https://lh3.googleusercontent.com/gps-cs-s/APNQkAH...=w4280-h3407-k-no",
        "video_thumbnail_url": null,
        "latitude": 40.7546469,
        "longitude": -73.9868158,
        "photo_datetime_utc": "2026-05-30T00:00:00.000Z",
        "photo_timestamp": 1780099200
      }
    ],
    "place_link": "https://www.google.com/maps/place/...",
    "reviews_link": "https://search.google.com/local/reviews?placeid=ChIJifIePKtZwokRVZ-UdRGkZzs",
    "booking_link": "https://www.google.com/searchviewer/42?...",
    "reservations_link": "https://www.fooddiscoveryapp.com/new-york-city/joes-pizza",
    "order_link": "https://www.google.com/searchviewer/42?...",
    "owner_name": "Joe's Pizza Broadway",
    "owner_link": "https://maps.google.com/maps/contrib/103877821925204408966",
    "cid": "4280570365733019477",
    "global_plus_code": "87G8Q237+V5",
    "compound_plus_code": "Q237+V5 New York",
    "menu_link": null,
    "emails_and_contacts": {
      "emails": [],
      "phone_numbers": ["2123661182", "7183882216", "2122670860", "2123889474"],
      "facebook": null,
      "instagram": "https://www.instagram.com/joespizzanyc",
      "linkedin": null,
      "twitter": null,
      "tiktok": null,
      "youtube": null,
      "pinterest": null,
      "snapchat": null,
      "yelp": null,
      "github": null
    }
  }
}
```

## Notes

- The website scrape runs on every call and adds ~0.5–1s to the response time.
- If the site is unreachable or has no contact info, `emails_and_contacts` is returned with empty arrays and `null` social links.
- A 404 with `code: "not_found"` is returned when the `place_id` doesn't match any place; `not_found` responses are not charged.
