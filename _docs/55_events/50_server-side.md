---
title: Server side
category: events
permalink: /events/server-side
last_modified_at: 2023-01-26
---

We allow data to be send server side or from mobile apps.

You can send us the regular data point fields and include [metadata](/metadata).

To view this data it's usually enough to use the [Events Explorer](/events-explorer), but you can also create [goals](/goals) for events you check often.

## Sending data

The following information is targeted at developers. Don't get scared away, they know what this means.

Customer can send their data to this endpoint: `https://queue.simpleanalyticscdn.com/events`. It should be JSON.

Example payload of the data:

```js
{
  type: "event",
  hostname: "example.com",
  event: "event-name",
  ua: "User Agent",
}
```

It's advised to include the user agent of the device, because the defaults could be detected as robots.

## Example

Sometimes you just want to send some test data. Here is an example with cURL to send data:

```bash
curl -X POST -H "Content-Type: application/json" -d '{
  "type": "event",
  "hostname": "mobile-app.example.com",
  "event": "consent",
  "metadata": {
    "button": "yes"
  },
  "ua": "Your User Agent"
}' https://queue.simpleanalyticscdn.com/events
```

If you want you can copy and paste the above cURL command into your terminal to test it. It shows up in your dashboard within a few minutes (usually way faster).

You can always [export the raw latest data](/export-data) from our dashboard, or use the [Events Explorer](/events-explorer) to find your events.

## Fields

Here is an example with many fields added:

```js
{
  type: "event",
  hostname: "example.com",
  event: "event-name",
  path: "/",
  viewport_width: 1440,
  viewport_height: 310,
  language: "en-US",
  screen_width: 1440,
  screen_height: 900,
  unique: true,
  https: true,
  timezone: "Europe/Amsterdam",
  metadata: {
    button: "yes",
  },
  ua: "User Agent",
}
```
