# Spending Limits

Spending limits let you cap your API costs on a daily and monthly basis. Configure them on your [billing page](https://apidirect.io/dashboard/billing).

## Daily Limit

Set a maximum dollar amount you're willing to spend per day. Once your daily spend reaches this limit, all API requests will be blocked until the next day (UTC midnight).

## Monthly Limit

Set a maximum dollar amount you're willing to spend per calendar month. Once your monthly spend reaches this limit, all API requests will be blocked until the next month.

## What Happens When a Limit Is Exceeded

When you hit a spending limit, the API returns a `429` error:

```json
{
  "error": "Daily spending limit reached",
  "code": "daily_limit_exceeded",
  "limit": 5.00,
  "current": 4.98
}
```

Or for monthly limits:

```json
{
  "error": "Monthly spending limit reached",
  "code": "monthly_limit_exceeded",
  "limit": 50.00,
  "current": 49.97
}
```

Requests will resume automatically when the next period begins (next day for daily limits, next month for monthly limits).

## Setting Limits

1. Go to your [Billing page](https://apidirect.io/dashboard/billing)
2. Find the Spending Limits section and click **Edit limits**
3. Enter your desired daily and/or monthly limit
4. Save your changes

## Threshold Alerts

You can be emailed before a limit is reached. In **Edit limits**, turn on the email alert and choose a percentage (for example 85%). When your daily or monthly spend reaches that percentage of the matching limit, an email goes to the account owner and to any extra addresses you add, such as a finance or ops inbox.

- One alert is sent per limit per period (daily alerts reset at UTC midnight, monthly alerts on the 1st)
- Changing a limit or the percentage re-arms the alert
- A separate email is always sent when a limit is actually reached and requests start being blocked

## Tips

- Start with conservative limits while you're testing and increase them as needed
- Use daily limits to protect against runaway scripts or unexpected spikes
- Use monthly limits to set a hard budget cap
- You can change or remove limits at any time from the dashboard
