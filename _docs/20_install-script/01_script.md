---
title: How to add our script
category: install-script
permalink: /script
last_modified_at: 2022-04-14
---

Include these two lines on every page at the end of your `<body>` (or anywhere else):

<!-- prettier-ignore -->
```html
<!-- Simple Analytics - 100% privacy-first analytics -->
<script async src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
```

> To install the script on Wordpress, Ghost, WIX, Squarespace, Webflow, Gatsby, Vue, Django, Ruby, and others, go to [Install on other platforms](/install-on-other-platforms).

We have a website setup wizard to test if you installed your script correctly. If you still have problems installing it, please let us know! We helped a lot of people with setting up their script and we love to help you as well. Just [contact](https://simpleanalytics.com/contact) us.

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

## Open source

Our user facing scripts are [open source on GitHub](https://github.com/simpleanalytics/scripts).

<img class="drawing" src="https://assets.simpleanalytics.com/images/drawings/chart.png" alt="">
