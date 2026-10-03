# LinkedIn Person Details

Get a LinkedIn person's profile by profile URL, public slug, or member URN. Returns name, headline, about, location, follower and connection counts, open-to-work status, and the experience, education, skills, certifications, languages, honors, publications, volunteering, and projects sections.

## Endpoint

```
GET /v1/linkedin/person
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | Yes | LinkedIn profile URL, public slug, or member URN, e.g. `https://www.linkedin.com/in/reidhoffman`, `reidhoffman`, or `ACoAAAAABL0B3SGhqeNX998wiOuk_8hYA6ojLwg` (max 500 characters) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `urn` | string | LinkedIn member URN |
| `public_identifier` | string | Public profile slug |
| `url` | string | Profile URL |
| `first_name` | string | First name |
| `last_name` | string | Last name |
| `full_name` | string | Full name |
| `headline` | string | Profile headline |
| `about` | string | About section |
| `location` | string | Location as shown on the profile |
| `country_code` | string | Two-letter country code |
| `profile_picture` | string | Profile photo URL |
| `cover_image` | string | Cover image URL |
| `followers` | integer | Number of followers |
| `connections` | integer | Number of connections |
| `is_premium` | boolean | Has LinkedIn Premium |
| `is_creator` | boolean | Has creator mode on |
| `open_to_work` | boolean | Shows the Open to Work badge |
| `experience` | array | Positions, in profile order |
| `experience[].title` | string | Job title |
| `experience[].company` | string | Company name |
| `experience[].company_id` | string | LinkedIn company ID (empty when the company has no LinkedIn page, as are `company_url` and `company_logo`) |
| `experience[].company_url` | string | Company page URL |
| `experience[].company_logo` | string | Company logo URL |
| `experience[].location` | string | Position location |
| `experience[].employment_type` | string | `full_time`, `part_time`, `contract`, `freelance`, `self_employed`, `internship`, `seasonal`, ... (empty when not set) |
| `experience[].description` | string | Position description |
| `experience[].start_date` | object/null | `{"year", "month"}`; `month` is null when only the year is set |
| `experience[].end_date` | object/null | Same shape; null for a current position |
| `experience[].is_current` | boolean | Current position |
| `education` | array | Schools |
| `education[].school` | string | School name |
| `education[].school_id` | string | LinkedIn school ID |
| `education[].school_url` | string | School page URL |
| `education[].school_logo` | string | School logo URL |
| `education[].degree` | string | Degree |
| `education[].field_of_study` | string | Field of study |
| `education[].description` | string | Description |
| `education[].start_date` | object/null | `{"year", "month"}` |
| `education[].end_date` | object/null | `{"year", "month"}` |
| `skills` | array | Skills |
| `skills[].name` | string | Skill name |
| `skills[].endorsements` | integer | Number of endorsements (a skill with one endorsement may show 0) |
| `certifications` | array | Licenses and certifications |
| `certifications[].name` | string | Certification name |
| `certifications[].authority` | string | Issuing organization |
| `certifications[].issued_date` | object/null | `{"year", "month"}` |
| `languages` | array | Languages |
| `languages[].name` | string | Language |
| `languages[].proficiency` | string | `elementary`, `limited_working`, `professional_working`, `full_professional`, or `native_or_bilingual` (empty when not set) |
| `honors` | array | Honors and awards |
| `honors[].title` | string | Award title |
| `honors[].issuer` | string | Issuer |
| `honors[].issued_date` | object/null | `{"year", "month"}` |
| `honors[].description` | string | Description |
| `publications` | array | Publications |
| `publications[].title` | string | Title |
| `publications[].publisher` | string | Publisher |
| `publications[].published_date` | object/null | `{"year", "month"}` |
| `publications[].url` | string | Publication URL |
| `volunteering` | array | Volunteer experience |
| `volunteering[].role` | string | Role |
| `volunteering[].organization` | string | Organization |
| `volunteering[].start_date` | object/null | `{"year", "month"}` |
| `volunteering[].end_date` | object/null | `{"year", "month"}`; null when ongoing |
| `projects` | array | Projects |
| `projects[].title` | string | Project title |
| `projects[].description` | string | Description |
| `projects[].start_date` | object/null | `{"year", "month"}` |
| `projects[].end_date` | object/null | `{"year", "month"}` |
| `source` | string | `"LinkedIn"` |
| `domain` | string | `"linkedin.com"` |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/linkedin/person?url=reidhoffman" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/linkedin/person",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "reidhoffman"}
)
print(response.json())
```

## Example Response

```json
{
  "urn": "ACoAAAAABL0B3SGhqeNX998wiOuk_8hYA6ojLwg",
  "public_identifier": "reidhoffman",
  "url": "https://www.linkedin.com/in/reidhoffman",
  "first_name": "Reid",
  "last_name": "Hoffman",
  "full_name": "Reid Hoffman",
  "headline": "Co-Founder, LinkedIn, Manas AI & Inflection AI. Founding Team, PayPal.  Author of Superagency.  Podcaster of Possible and Masters of Scale.",
  "about": "My current priority is investing in and building with AI to benefit humanity...",
  "location": "United States",
  "country_code": "US",
  "profile_picture": "https://media.licdn.com/dms/image/...",
  "cover_image": "https://media.licdn.com/dms/image/...",
  "followers": 2795262,
  "connections": 4324,
  "is_premium": true,
  "is_creator": true,
  "open_to_work": false,
  "experience": [
    {
      "title": "Co-Founder, Executive Board Chair",
      "company": "Manas AI",
      "company_id": "106067845",
      "company_url": "https://www.linkedin.com/company/manas-ai",
      "company_logo": "https://media.licdn.com/dms/image/...",
      "location": "",
      "employment_type": "",
      "description": "Manas AI leverages proprietary AI, generative computational chemistry...",
      "start_date": {"year": 2025, "month": 1},
      "end_date": null,
      "is_current": true
    }
  ],
  "education": [
    {
      "school": "Università degli Studi di Perugia",
      "school_id": "2052604",
      "school_url": "https://www.linkedin.com/school/universit-degli-studi-di-perugia/",
      "school_logo": "https://media.licdn.com/dms/image/...",
      "degree": "Honorary Doctorate",
      "field_of_study": "Human Sciences",
      "description": "",
      "start_date": {"year": 2024, "month": 5},
      "end_date": {"year": 2024, "month": 5}
    }
  ],
  "skills": [{"name": "CEOs", "endorsements": 2}],
  "certifications": [],
  "languages": [],
  "honors": [
    {"title": "Sigillum Magnum", "issuer": "University of Bologna", "issued_date": {"year": 2023, "month": 9}, "description": "Sigillum Magnum is a silver-bronze medal realized in 1888..."}
  ],
  "publications": [
    {"title": "Superagency", "publisher": "Authors Equity", "published_date": {"year": 2025, "month": 1}, "url": "https://www.superagency.ai/"}
  ],
  "volunteering": [
    {"role": "Chair, Board of Directors", "organization": "Opportunity@Work", "start_date": {"year": 2016, "month": 6}, "end_date": null}
  ],
  "projects": [],
  "source": "LinkedIn",
  "domain": "linkedin.com"
}
```
