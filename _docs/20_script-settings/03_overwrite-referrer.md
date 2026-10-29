---
title: Overwrite referrer
category: script-settings
permalink: /overwrite-referrer
last_modified_at: 2026-10-29
created_at: 2026-10-29
---

From script version 12, you can overwrite the referrer of the first page view. This helps when the browser doesn't pass the original referrer but you know where the visitor came from, for example after a redirect through your own server.

Add the referrer URL to `data-referrer`:

```html
<script
  async
  data-referrer="https://example.com/newsletter"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
></script>
```

We clean this referrer the same way as [the referrer from the browser](/how-to-use-url-parameters#using-the-referrer-url). Later page views in a single page app still use the previous page as their referrer. If you [ignore the `referrer` metric](/ignore-metrics), we don't send it.

You can also set it with `referrer` in [`sa_settings`](/script#settings-via-javascript).
