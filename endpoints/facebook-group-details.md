# Facebook Group Details

Get detailed information about a Facebook group by URL. Returns the group name, ID, description, privacy setting, member count, and more.

## Endpoint

```
GET /v1/facebook/group
```

**Price:** $0.008 per request
**Free tier:** 50 requests/month

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `url` | Yes | Facebook group URL (e.g. https://www.facebook.com/groups/example) |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `group` | object | Group data |
| `group.id` | string | Facebook group ID |
| `group.name` | string | Group name |
| `group.url` | string | URL of the group |
| `group.description` | string | Group description / about text |
| `group.privacy` | string | Privacy setting (e.g. "Public", "Private") |
| `group.members_count` | integer | Number of group members |
| `group.location` | string | Group location (if set) |
| `group.cover_photo` | string | URL to group cover photo |

## Example Request

### cURL

```bash
curl "https://apidirect.io/v1/facebook/group?url=https://www.facebook.com/groups/example" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Python

```python
import requests

response = requests.get(
    "https://apidirect.io/v1/facebook/group",
    headers={"X-API-Key": "YOUR_API_KEY"},
    params={"url": "https://www.facebook.com/groups/example"}
)
print(response.json())
```

## Example Response

```json
{
  "group": {
    "id": "482710394817253",
    "name": "Example Group",
    "url": "https://www.facebook.com/groups/example",
    "description": "A community for sharing tips, resources, and discussions about the latest trends. Join us to connect with like-minded people from around the world.",
    "privacy": "Public group",
    "members_count": 85600,
    "location": "New York, NY",
    "cover_photo": "https://scontent.xx.fbcdn.net/v/t39.30808-6/482710_..._n.jpg"
  }
}
```
