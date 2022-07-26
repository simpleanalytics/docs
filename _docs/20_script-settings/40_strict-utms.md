---
title: Strict UTMs
category: script-settings
permalink: /strict-utms
created_at: 2022-07-26
last_modified_at: 2022-07-26
---

When collecting UTM codes, we allow to skip the `utm_` part:

- `utm_source` / `source` / `ref`
- `utm_medium` / `medium`
- `utm_campaign` / `campaign`
- `utm_content` / `content`
- `utm_term` / `term`

In our dashboard `utm_source`, `source`, `ref` will be stored as `utm_source`. But sometimes both parameters are used. To give you control over which parameter we should store you can enable strict UTMs.

```html
<script
  data-strict-utm="true"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
></script>
```

This will only allow for the following UTMs to be used:

- `utm_source`
- `utm_medium`
- `utm_campaign`
- `utm_content`
- `utm_term`

The parameters `source`, `ref`, and more will not be collected.

Want to collect more URL parameters? [Learn how to allow more parameters](/allow-params).
