---
title: Allow URL parameters
category: script-settings
permalink: /allow-params
created_at: 2022-07-26
last_modified_at: 2022-07-26
---

By default, we collect all UTM parameters (with and without the `utm_` prefix) and the `ref` (which is short for `utm_source`) parameter:

- `utm_source` / `source` / `ref`
- `utm_medium` / `medium`
- `utm_campaign` / `campaign`
- `utm_content` / `content`
- `utm_term` / `term`

> If your use [strict UTMs](/strict-utms), you can only use the query parameters that start with `utm_`.

We don't store the rest of the query parameters. But some customers have non-personal data in their query parameters—for example, `product-id` or `article-slug`. We allow collecting those parameters as long as they are specified via our script settings.

If you want to capture `product-id` and `article-slug` from your website's URLs, you can specify the following `data-allow-params`-setting:

```html
<script
  data-allow-params="product-id,article-slug"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
></script>
```

> **Warning:** Defined parameters in `data-allow-params` are case-sensitive.

Read more on [how to use URL parameters](/how-to-use-url-parameters) on your website.
