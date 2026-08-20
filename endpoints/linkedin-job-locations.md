# LinkedIn Job Location IDs

The [Search Jobs](/docs/linkedin-jobs) endpoint supports filtering results by location using the `location_id` parameter. This parameter accepts a LinkedIn location ID (also known as a geo URN).

## Using the location_id parameter

Pass a numeric location ID to the `location_id` parameter to filter job results to that location. Location IDs can represent countries, states/provinces, metro areas, or cities.

### Example: Jobs in the United States

```bash
curl "https://apidirect.io/v1/linkedin/jobs?query=software%20engineer&location_id=103644278" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Example: Jobs in London, United Kingdom

```bash
curl "https://apidirect.io/v1/linkedin/jobs?query=data%20analyst&location_id=102257491" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Example: Jobs in the San Francisco Bay Area

```bash
curl "https://apidirect.io/v1/linkedin/jobs?query=product%20manager&location_id=90000084" \
  -H "X-API-Key: YOUR_API_KEY"
```

## Common location IDs

### Countries

| Location | ID |
|----------|----|
| United States | 103644278 |
| United Kingdom | 101165590 |
| Canada | 101174742 |
| Germany | 101282230 |
| France | 105015875 |
| India | 102713980 |
| Australia | 101452733 |
| Netherlands | 102890719 |
| Singapore | 102454443 |
| Japan | 101355337 |
| Spain | 105646813 |
| Italy | 103350119 |
| Sweden | 105117694 |
| Switzerland | 106693272 |
| Ireland | 104738515 |
| Israel | 101620260 |
| South Korea | 105149562 |
| Mexico | 103323778 |
| Poland | 105072130 |

### US States

| Location | ID |
|----------|----|
| California | 102095887 |
| New York | 105080838 |
| Texas | 102748797 |
| Florida | 101318387 |
| Illinois | 101949407 |
| Pennsylvania | 102986501 |
| Georgia | 103950076 |
| Ohio | 106981407 |
| North Carolina | 103255397 |
| Virginia | 101630962 |
| New Jersey | 101651951 |
| Massachusetts | 101098412 |
| Washington | 103977389 |
| Colorado | 105763813 |
| Arizona | 106032500 |
| Michigan | 103051080 |
| Tennessee | 104629187 |

### Major US Cities

| Location | ID |
|----------|----|
| New York City, New York | 102571732 |
| Los Angeles, California | 102448103 |
| San Francisco, California | 102277331 |
| Chicago, Illinois | 103112676 |
| Seattle, Washington | 104116203 |
| Austin, Texas | 104472865 |
| Denver, Colorado | 103736294 |
| Washington, DC | 104383890 |
| Atlanta, Georgia | 106224388 |
| Dallas, Texas | 104194190 |
| Houston, Texas | 103743442 |
| Miami, Florida | 102394087 |
| San Diego, California | 103918656 |
| Portland, Oregon | 104727230 |
| Minneapolis, Minnesota | 103039849 |
| Nashville, Tennessee | 105573479 |
| Raleigh, North Carolina | 100197101 |
| Phoenix, Arizona | 100219842 |
| Philadelphia, Pennsylvania | 104937023 |

### US Metro Areas

| Location | ID |
|----------|----|
| San Francisco Bay Area | 90000084 |
| Greater Chicago Area | 90000014 |
| Dallas-Fort Worth Metroplex | 90000031 |
| Greater Houston | 90000042 |
| Greater Los Angeles Area | 90000049 |
| Atlanta Metropolitan Area | 90000052 |
| Miami-Fort Lauderdale Area | 90000056 |
| Austin, Texas Metropolitan Area | 90000064 |
| Greater New York City Area | 90000070 |
| Greater Philadelphia | 90000077 |
| Portland, Oregon Metropolitan Area | 90000079 |
| Washington DC-Baltimore Area | 90000097 |
| Greater Minneapolis-St. Paul Area | 90000512 |
| Nashville Metropolitan Area | 90000536 |
| Greater Phoenix Area | 90000620 |
| Raleigh-Durham-Chapel Hill Area | 90000664 |

### Canadian Cities

| Location | ID |
|----------|----|
| Toronto, Ontario | 100025096 |
| Montreal, Quebec | 101728226 |
| Vancouver, British Columbia | 103366113 |
| Calgary, Alberta | 102199904 |
| Ottawa, Ontario | 106234700 |
| Edmonton, Alberta | 106535873 |
| Greater Toronto Area | 90009551 |

### European Cities

| Location | ID |
|----------|----|
| London, England, United Kingdom | 102257491 |
| Berlin, Germany | 103035651 |
| Amsterdam, Netherlands | 102011674 |
| Paris, France | 106383538 |
| Dublin, Ireland | 105178154 |
| Barcelona, Spain | 105088894 |
| Munich (District), Germany | 105264689 |
| Stockholm, Sweden | 100907646 |
| Zurich, Switzerland | 102436504 |
| Madrid, Spain | 100994331 |
| Milan, Italy | 102873640 |
| Copenhagen, Denmark | 106743989 |
| Frankfurt am Main, Germany | 106150090 |
| Düsseldorf, Germany | 104008204 |
| Cologne, Germany | 102426246 |
| Stuttgart, Germany | 102473731 |
| Lyon, France | 103815258 |
| Marseille, France | 103857854 |
| Toulouse, France | 105073465 |
| Bordeaux, France | 104787182 |
| London Area, United Kingdom | 90009496 |
| Greater Munich Metropolitan Area | 90009735 |
| Greater Paris Metropolitan Region | 90009659 |
| Greater Barcelona Metropolitan Area | 90009761 |
| Greater Madrid Metropolitan Area | 90009790 |

### Asia-Pacific Cities

| Location | ID |
|----------|----|
| Singapore | 102454443 |
| Tokyo, Japan | 103925994 |
| Sydney, Australia | 104769905 |
| Melbourne, Australia | 100992797 |
| Bengaluru (Bangalore), India | 105214831 |
| Mumbai, India | 106164952 |
| Hong Kong | 103291313 |
| Seoul, South Korea | 103588929 |
| Dubai, United Arab Emirates | 106204383 |
| Delhi, India | 106187582 |
| Hyderabad, India | 105556991 |
| Greater Tokyo Area | 90009987 |
| Greater Sydney Area | 90009524 |
| Greater Melbourne Area | 90009521 |

## Full location list

The complete list of location IDs is available as a JSON file:

**[Download linkedin-job-locations.json](/static/linkedin-job-locations.json)**

The JSON file contains thousands of locations with the following format:

```json
[
  {
    "id": "103644278",
    "name": "United States"
  },
  {
    "id": "102095887",
    "name": "California, United States"
  },
  {
    "id": "102277331",
    "name": "San Francisco, California, United States"
  }
]
```

You can search this file for the location you need and use the `id` value as the `location_id` parameter.

## Finding location IDs from LinkedIn

If the location you need is not in the list above, you can find its ID directly from LinkedIn:

1. Go to [linkedin.com/jobs](https://www.linkedin.com/jobs/) and sign in
2. Enter any search term and click the **Location** filter
3. Type the location you want and select it from the dropdown
4. Run the search
5. Look at the URL in your browser's address bar. It will contain a `geoId` parameter:

```
https://www.linkedin.com/jobs/search/?geoId=103644278&keywords=...
```

The number after `geoId=` is the location ID. In this example, `103644278` is the ID for the United States.

If the URL contains `f_PP` instead of `geoId`, the value after `f_PP=` is the same location ID:

```
https://www.linkedin.com/jobs/search/?f_PP=103644278&keywords=...
```
