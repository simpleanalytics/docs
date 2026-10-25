---
title: Pings
category: script-settings
permalink: /pings
created_at: 2026-10-25
last_modified_at: 2026-10-25
---

We send the [time on page](/explained/time-on-page) when a page gets hidden. If a browser discards a page before that, for example on mobile, we don't get any time for that page view.

With pings, the script also sends the time on page when the visible time passes the thresholds you set, in seconds. Each ping replaces the time sent earlier for that page view, so seconds are never counted twice. Pings require script version 12.

```html
<script
  async
  data-pings="5,30,60"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
></script>
```

Or with the [settings object](/script#settings-via-javascript):

```html
<script>
  window.sa_settings = { pings: [5, 30, 60] };
</script>
```

There are no pings by default. Every threshold adds a request per page view, so only add the ones you need. When you ignore `timeonpage` with [ignore metrics](/ignore-metrics), pings only send how far visitors scrolled.
