# Quickstart

Get up and running with API Direct in three steps.

## Step 1: Create an Account

Sign up at [apidirect.io/signup](https://apidirect.io/signup). No credit card required — you get 50 free requests per endpoint every month.

## Step 2: Create an API Key

After signing in, go to the [API Keys](https://apidirect.io/dashboard/keys) page in your dashboard and create a new key. Your key will look like `ak_live_...`. Copy it — you'll need it for the next step.

## Step 3: Make Your First Request

### Using cURL

```bash
curl "https://api.apidirect.io/v1/reddit/posts?query=programming&page=1" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Using Python

```python
import requests

response = requests.get(
    "https://api.apidirect.io/v1/reddit/posts",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={
        "query": "programming",
        "page": 1
    }
)

data = response.json()
for post in data["posts"]:
    print(post["title"], "-", post["url"])
```

### Example Response

```json
{
  "posts": [
    {
      "title": "Best resources for learning programming",
      "url": "https://reddit.com/r/learnprogramming/...",
      "date": "2024-06-15 10:30:00",
      "author": "dev_learner",
      "source": "Reddit",
      "subreddit": "learnprogramming",
      "snippet": "I've compiled a list of the best free resources..."
    }
  ],
  "page": 1,
  "count": 20
}
```

## What's Next

- Learn about [Authentication](/docs/authentication) and managing API keys
- Understand the [Response Format](/docs/response-format) shared across all endpoints
- Browse the full [endpoint reference](/docs/linkedin-posts)
