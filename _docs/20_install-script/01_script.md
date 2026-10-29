---
title: How to add our script
category: install-script
permalink: /script
last_modified_at: 2026-10-29
---

Include these two lines on every page at the end of your `<body>` (or anywhere else):

<!-- prettier-ignore -->
```html
<!-- Simple Analytics - 100% privacy-first analytics -->
<script async src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
```

> To install the script on Wordpress, Ghost, WIX, Squarespace, Webflow, Gatsby, Vue, Django, Ruby, and others, go to [Install on other platforms](/install-on-other-platforms).

We have a website setup wizard to test if you installed your script correctly. If you still have problems installing it, please let us know! We helped a lot of people with setting up their script and we love to help you as well. Just [contact](https://simpleanalytics.com/contact) us.

## Server-side tracking

We support server-side tracking, [read more about it here](/events/server-side#page-view-data-structure).

## Non-JavaScript environments

While most people browse the internet with JavaScript enabled, there are still some users who disable it, fully aware that many websites may not function as intended. If you want to capture data from these visitors, consider adding our `noscript` tag. Be aware that this may also increase traffic from bots, as some don’t have JavaScript enabled.

<!-- prettier-ignore -->
```html
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
```

## Developers

With Simple Analytics you don't need to manually trigger page views in SPA. We automatically trigger page views in [_Single Page Apps_ (SPA's)](/trigger-custom-page-views) like React, Vue, and Angular. You can also use [hash navigation](/hash-mode) to trigger page views.

Some people like a very light script. All our scripts are heavily compressed and we have [an extra light](/light) version.

If you want to run the script on localhost, please use our dev (`https://scripts.simpleanalyticscdn.com/latest.dev.js`) version. Note the `.dev` part. You might want to [overwrite your hostname](/overwrite-domain-name) from localhost to something like `dev.example.com` (where `example.com` is your domain) to receive it in your dashboard. Make sure to remove the `.dev` part from the script on production.

We drop data from some shared preview and proxy domains, like `*.vercel.app`, `*.lovable.app`, and `*.translate.goog`, unless that exact hostname is added to your dashboard. To collect data on such a domain, add the hostname to your dashboard or [overwrite the hostname](/overwrite-domain-name).

When you are done implementing [go to your dashboard](https://simpleanalytics.com/websites).

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact).

### Javascript version

If you can't embed HTML, but you can embed JavaScript, here is the code you need to install Simple Analytics with just JavaScript.

```js
// Simple Analytics - 100% privacy-first analytics
const script = document.createElement("script");
script.setAttribute("src", "https://scripts.simpleanalyticscdn.com/latest.js");
document.head.appendChild(script);
```

### Settings via JavaScript

Instead of `data-` attributes, you can pass settings with a `window.sa_settings` object. Define it before the script loads. Settings in this object take precedence over `data-` attributes.

```html
<script>
  window.sa_settings = {
    hostname: "example.com",
    ignorePages: ["/search/*", "/account/*"],
    collectDnt: true,
  };
</script>
<script async src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
```

These settings are available:

| Setting              | Same as                          | Example                      |
| -------------------- | -------------------------------- | ---------------------------- |
| `hostname`           | [`data-hostname`][1]             | `"example.com"`              |
| `mode`               | [`data-mode`][2]                 | `"hash"`                     |
| `collectDnt`         | [`data-collect-dnt`][3]          | `true`                       |
| `autoCollect`        | [`data-auto-collect`][4]         | `false`                      |
| `ignorePages`        | [`data-ignore-pages`][5]         | `["/search/*", "/vouchers"]` |
| `ignoreMetrics`      | [`data-ignore-metrics`][6]       | `["timeonpage", "scrolled"]` |
| `allowParams`        | [`data-allow-params`][7]         | `["product-id"]`             |
| `nonUniqueHostnames` | [`data-non-unique-hostnames`][8] | `["checkout.stripe.com"]`    |
| `strictUtm`          | [`data-strict-utm`][9]           | `true`                       |
| `namespace`          | [`data-namespace`][10]           | `"ba"`                       |
| `pathOverwriter`     | [`data-path-overwriter`][11]     | `"myPathOverwriter"`         |
| `metadataCollector`  | [`data-metadata-collector`][12]  | `"myAddMetadataFunction"`    |
| `pings`              | [`data-pings`][13]               | `[5, 30, 60]`                |
| `detect404`          | [`data-detect-404`][14]          | `true`                       |
| `referrer`           | [`data-referrer`][15]            | `"https://example.com/"`     |

For `pathOverwriter` and `metadataCollector`, use the name of a function on `window`, not the function itself. The script logs the settings it received in the browser console.

[1]: /overwrite-domain-name
[2]: /hash-mode
[3]: /dnt
[4]: /trigger-custom-page-views#use-custom-collection-anyway
[5]: /ignore-pages
[6]: /ignore-metrics
[7]: /allow-params
[8]: /non-unique-hostnames
[9]: /strict-utms
[10]: /events#the-variable-sa_event-is-already-used
[11]: /overwrite-path
[12]: /metadata
[13]: /pings
[14]: /events/inline#404-pages
[15]: /overwrite-referrer

## Browser support

We test our script on a wide range of browsers and real devices with [BrowserStack](https://www.browserstack.com/). We support browser, OS, and device versions that their vendors still maintain, and we keep testing them for two years after their end of life. Older browser versions with more than 0.1% global usage stay covered.

## Open source

Our user facing scripts are [open source on GitHub](https://github.com/simpleanalytics/scripts).

<img class="drawing" src="https://assets.simpleanalytics.com/images/drawings/chart.png" alt="">
