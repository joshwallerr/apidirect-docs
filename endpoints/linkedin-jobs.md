# LinkedIn Jobs

Search LinkedIn job listings by keyword. Returns job title, company, location, posting date, job type, experience level, workplace type, industry, salary, benefits, full description, and company logo. Supports filtering by recency, job type, company, and location.

## Endpoint

```
GET /v1/linkedin/jobs
```

**Price:** $0.006 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | Yes | Search keyword (max 500 characters) |
| `page` | No | Page number for pagination (default: 1) |
| `sort_by` | No | Sort order: `most_recent` or `relevance` (default: `relevance`) |
| `posted_ago` | No | Maximum job age: `1h`, `24h`, `7d`, or `30d` (default: all time) |
| `job_type` | No | Job type filter: `full_time`, `part_time`, `contract`, `temporary`, `volunteer`, `internship`, `other`. Comma-separated for multiple. |
| `company_ids` | No | Filter by company. Comma-separated LinkedIn company IDs (get IDs from the Search Companies endpoint). |
| `location_id` | No | Filter by location. A numeric LinkedIn location ID (see [Job Location IDs](/docs/linkedin-job-locations) for a full list). |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `jobs` | array | Array of matching job listings |
| `jobs[].title` | string | Job title |
| `jobs[].url` | string | Direct link to the job posting |
| `jobs[].company` | string | Company name |
| `jobs[].company_id` | string | LinkedIn company ID |
| `jobs[].company_url` | string | Link to the company's LinkedIn page |
| `jobs[].company_logo` | string | URL to the company logo |
| `jobs[].location` | string | Job location |
| `jobs[].date` | string | Date the job was posted |
| `jobs[].job_type` | string | Employment type (e.g., `full_time`, `contract`, `part_time`) |
| `jobs[].experience_level` | string | Required experience level (e.g., `entry_level`, `mid_senior`, `director`) |
| `jobs[].workplace_type` | string | Workplace arrangement: `on_site`, `remote`, or `hybrid` |
| `jobs[].industry` | string | Industry classification (when available) |
| `jobs[].job_functions` | string | Job function codes (e.g., `ENG, IT`) |
| `jobs[].description` | string | Full job description text |
| `jobs[].salary` | string | Salary information (when available) |
| `jobs[].benefits` | string | Inferred benefits (when available) |
| `jobs[].apply_url` | string | External application URL (when available) |
| `jobs[].applicants` | string | Number of applicants (when available) |
| `page` | integer | Current page number |
| `count` | integer | Number of results returned |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/linkedin/jobs?query=software%20engineer&page=1&sort_by=relevance" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/linkedin/jobs",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "software engineer",
        "page": 1,
        "sort_by": "relevance"
    }
)
print(response.json())
```

## Example Response

```json
{
  "jobs": [
    {
      "title": "Senior Software Engineer",
      "url": "https://www.linkedin.com/jobs/view/4417833240/",
      "company": "Stripe",
      "company_id": "2135371",
      "company_url": "https://www.linkedin.com/company/stripe",
      "company_logo": "https://media.licdn.com/dms/image/.../company-logo.jpg",
      "location": "San Francisco, CA",
      "date": "2026-05-20 14:30:00",
      "job_type": "full_time",
      "experience_level": "mid_senior",
      "workplace_type": "hybrid",
      "industry": "Technology, Information and Internet",
      "job_functions": "ENG, IT",
      "description": "We are looking for a Senior Software Engineer to join our team...",
      "salary": "$180,000 - $250,000",
      "benefits": "",
      "apply_url": "https://stripe.com/jobs/listing/senior-software-engineer/1234",
      "applicants": "200+ applicants"
    }
  ],
  "page": 1,
  "count": 25
}
```
