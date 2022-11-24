---
title: Ignore pages
menu: Ignore pages
category: script-settings
permalink: /ignore-pages
last_modified_at: 2022-11-24
---

Normally you install the script on all pages of your website. You add your script in the header or footer so you don't have to copy it to every page. But sometimes you don't want to record all pages on your website. That's why we have a feature where you can ignore pages easily.

## `ignore-pages`

Every page you want to ignore starts with a slash (`/`) and is only the path after the domain name, not the full link. For `https://example.com/vouchers` it would be `/vouchers`:

```html
<script
  data-ignore-pages="/vouchers"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
></script>
```

## Comma separated

Let's say you have these pages that you want to ignore:

- `https://example.com/contact`
- `https://example.com/accounts/@adriaan`
- `https://example.com/vouchers`

If you want to block all these pages you can separate them with a comma:

```html
<script
  data-ignore-pages="/search/contact,/accounts/@adriaan,/vouchers"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
></script>
```

## Wildcards

If you need to match a part of a string you need to add an wildcard asterisk (`*`).

Let's say you have these pages:

- `https://example.com/search/keyword` (where `keyword` kan be any keyword)
- `https://example.com/accounts/@profilename` (where `profilename` can be any name)
- `https://example.com/vouchers` (only one page)

To match `/search/1` and `/search/2` you can use `/search/*`. If you use `/search/` it will only ignore that page and still collects `/search/1` and `/search/2`.

To block all above pages you can use the following code:

```html
<script
  data-ignore-pages="/search/*,/accounts/*,/vouchers"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
></script>
```

Need any help? We love to help you set up your script. Don't hesitate to [contact us](https://simpleanalytics.com/contact). Silly questions don't exist.
