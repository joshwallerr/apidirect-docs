# LinkedIn Job Details

Get detailed information about a specific LinkedIn job listing by URL. Returns job title, company, location, posting date, job type, experience level, workplace type, industry, salary, benefits, full description, and company logo.

## Endpoint

```
GET /v1/linkedin/job
```

**Price:** $0.002 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | Yes | LinkedIn job URL (e.g., `https://linkedin.com/jobs/view/1234567890`) or numeric job ID |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `title` | string | Job title |
| `url` | string | Direct link to the job posting |
| `company` | string | Company name |
| `company_id` | string | LinkedIn company ID |
| `company_url` | string | Link to the company's LinkedIn page |
| `company_logo` | string | URL to the company logo |
| `location` | string | Job location |
| `date` | string | Date the job was posted |
| `job_type` | string | Employment type (e.g., `full_time`, `contract`, `part_time`) |
| `experience_level` | string | Required experience level (e.g., `entry_level`, `mid_senior`, `director`) |
| `workplace_type` | string | Workplace arrangement: `on_site`, `remote`, or `hybrid` |
| `industry` | string | Industry classification (when available) |
| `job_functions` | string | Job function codes (e.g., `ENG, IT`) |
| `description` | string | Full job description text |
| `salary` | string | Salary information (when available) |
| `benefits` | string | Inferred benefits (when available) |
| `apply_url` | string | External application URL (when available) |
| `applicants` | string | Number of applicants (when available) |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/linkedin/job?url=https://linkedin.com/jobs/view/4417833240" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/linkedin/job",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://linkedin.com/jobs/view/4417833240"}
)
print(response.json())
```

## Example Response

```json
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
```
