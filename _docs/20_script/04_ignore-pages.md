---
title: Ignore specified pages
menu: Ignore pages
category: script
permalink: /ignore-pages
---

Normally you install the script on all pages of your website. You add your script in the header or footer so you don't have to copy it to every page. But sometimes you don't want to record all pages on your website. That's why we have a feature where you can ignore pages easily.

## `ignore-pages`

Let's say you have pages that you want to ignore:
- `https://example.com/search/keyword` (where `keyword` kan be any keyword)
- `https://example.com/account/@profilename` (where `profilename` kan be any name)
- `https://example.com/vouchers` (only one page)

Then you can define these with the `ignore-pages` attribute in your embed script. Every page you want to ignore starts with a slash (`/`) and is only the page of the page, not the full link. For `https://example.com/vouchers` it would be `/vouchers`:

```html
<script ignore-pages="/vouchers" src="..." />
```

## Comma separated

If you have multiple pages you want to block you can separate them with a comma.

```html
<script ignore-pages="/search/keyword,/account/@profilename,/vouchers" src="..." />
```

## Wildcard search

Note that if you need to match a part of a string you need to add an asterisk (`*`). To match `/search/1` and `/search/2` you can use `/search/*`. If you use `/search/` it will only ignore that page and still collects ``/search/1` and `/search/2`.

To block all above pages you can use the following code:

```html
<script ignore-pages="/search/*,/account/*,/vouchers" src="..." />
```
