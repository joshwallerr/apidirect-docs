# Spending Limits

Spending limits let you cap your API costs on a daily and monthly basis. Configure them in your [dashboard settings](https://apidirect.io/dashboard/settings).

## Daily Limit

Set a maximum dollar amount you're willing to spend per day. Once your daily spend reaches this limit, all API requests will be blocked until the next day (UTC midnight).

## Monthly Limit

Set a maximum dollar amount you're willing to spend per calendar month. Once your monthly spend reaches this limit, all API requests will be blocked until the next month.

## What Happens When a Limit Is Exceeded

When you hit a spending limit, the API returns a `429` error:

```json
{
  "error": "Daily spending limit reached",
  "code": "daily_limit_exceeded"
}
```

Or for monthly limits:

```json
{
  "error": "Monthly spending limit reached",
  "code": "monthly_limit_exceeded"
}
```

Requests will resume automatically when the next period begins (next day for daily limits, next month for monthly limits).

## Setting Limits

1. Go to your [Dashboard Settings](https://apidirect.io/dashboard/settings)
2. Find the Spending Limits section
3. Enter your desired daily and/or monthly limit
4. Save your changes

## Tips

- Start with conservative limits while you're testing and increase them as needed
- Use daily limits to protect against runaway scripts or unexpected spikes
- Use monthly limits to set a hard budget cap
- You can change or remove limits at any time from the dashboard
