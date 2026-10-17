---
title: Server-side
category: events
permalink: /events/server-side
last_modified_at: 2026-10-17
---

Server-side and mobile app data submissions are supported, allowing for the transmission of standard data points along with [metadata](/metadata). Access and analyze this data through the [Events Explorer](/events-explorer) or create [goals](/goals) for frequent event monitoring.

We created a video explaining how server side tracking works with Simple Analytics. [Here you go](https://www.youtube.com/watch?v=0W8typnKPSs)

## Data submission

Developers can submit data to `https://queue.simpleanalyticscdn.com/events` using JSON format.

### User agent guidelines

To prevent misidentification as a robot, avoid using default user agents from request libraries. We mark a data point as a robot when its user agent contains `bot`, `spider`, `crawl`, or `agent` (so a placeholder like `User Agent` is marked as a robot too), or matches a list of known tools like `python-requests/...`, `curl/...`, `node-fetch/...`, or `axios/...`. Instead, use the real user agent of the user, or use a custom user agent format, such as `ServerSide/1.0 (+https://www.yourwebsite.com/)`.

If you send screen and viewport sizes, don't send the same size for both on a landscape screen. We mark those data points as robots as well.

### Event data structure

For event tracking, structure your payload as follows:

```json
{
  "type": "event",
  "hostname": "example.com",
  "event": "event_name",
  "ua": "ServerSide/1.0 (+https://www.example.com/)"
}
```

We store event names exactly as you send them. To match events collected with [our script](/events#valid-event-names), only use letters, numbers, and underscores.

### Page view data structure

Page view data uses the same endpoint, structured like this:

```json
{
  "type": "pageview",
  "hostname": "example.com",
  "event": "pageview",
  "path": "/page-name",
  "ua": "ServerSide/1.0 (+https://www.example.com/)"
}
```

## Testing with cURL

To send test data, use the following cURL command:

Data should appear on your dashboard within minutes. You can always [export the raw latest data](/export-data) from our dashboard, or use the [Events Explorer](/events-explorer) to find your events.

### Testing events

```bash
curl -X POST -H "Content-Type: application/json" -d '{
  "type": "event",
  "hostname": "mobile-app.example.com",
  "event": "consent",
  "metadata": {
    "button": "yes"
  },
  "ua": "ServerSide/1.0 (+https://www.example.com/)"
}' https://queue.simpleanalyticscdn.com/events
```

### Testing page views

```bash
curl -X POST -H "Content-Type: application/json" -d '{
  "type": "pageview",
  "hostname": "mobile-app.example.com",
  "event": "pageview",
  "path": "/my-page-name", 
  "ua": "ServerSide/1.0 (+https://www.example.com/)"
}' https://queue.simpleanalyticscdn.com/events
```

## Additional data fields

Expand your data submission with additional fields:

```json
{
  "type": "event",
  "hostname": "example.com",
  "event": "event_name",
  "path": "/",
  "unique": true,
  "https": true,
  "ua": "ServerSide/1.0 (+https://www.example.com/)",
  "referrer": "https://www.anotherexample.com/page-1",

  "viewport_width": 1440,
  "viewport_height": 310,
  "screen_width": 1440,
  "screen_height": 900,

  "language": "en-US",
  "timezone": "Europe/Amsterdam",

  "source": "source",
  "campaign": "campaign",
  "medium": "medium",
  "content": "content",
  "term": "term",

  "timestamp": "2026-10-17T12:00:00.000Z",

  "metadata": {
    "button": "yes"
  }
}
```

- `unique` defaults to `true` when you don't send it. Read more about [unique visits](/explained/unique-visits).
- `timestamp` is optional and defaults to the time we receive the request. It must be an ISO 8601 date in UTC, like `2026-10-17T12:00:00.000Z` or `2026-10-17T12:00:00Z`.
- We derive the country from `timezone`.
