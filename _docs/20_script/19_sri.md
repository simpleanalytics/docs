---
title: SRI version
category: script
permalink: /sri
sriVersion: 8
sriHash: sha256-cT9x5SqW9l5tHekepcFmRA/OGD9BqpNjFfUbQN5/xhU= sha384-Ctlr4fGZ2vC/YG88I+6MX6HY7TSS4RS0sDUpAwJm5qytQPEAvEA1Tl+GvJ9hL4Kw sha512-y3S+Gb/NJYXLQEiLuQ+gCpID6yDrSsplgubNIqtvm9BcmNOkMvym1CyYa82WcS5rNKLn0pTUu3eXQ+tgCGXQrA==
last_modified_at: 2022-04-14
---

If you want to use SRI you can do this by using specific scripts. The default scripts are changing to reflect new features or code optimizations. You want to use SRI if you consider it a risk when our scripts change. You can also host our SRI script on your own server or CDN.

When you want to use our SRI version of our script you will need to update your script to `https://scripts.simpleanalyticscdn.com/sri/v{{ page.sriVersion }}.js`. The full embed script becomes:

<!-- prettier-ignore -->
```html
<script async defer src="https://scripts.simpleanalyticscdn.com/sri/v{{ page.sriVersion }}.js" integrity="{{ page.sriHash }}" crossorigin="anonymous"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
```

When using a [custom domain](/bypass-ad-blockers) you need to use this script: `https://CUSTOM.DOMAIN/v{{ page.sriVersion }}/app.js`. Replace the `CUSTOM.DOMAIN` with your custom domain. To generate an SRI hash for your custom domain you can use [report-uri.com](https://report-uri.com/home/sri_hash) or [srihash.org](https://www.srihash.org/).

To verify if our script is an SRI version you can always check for `SRI-version` in the first line:

<img class="border" src="https://user-images.githubusercontent.com/1079135/147767570-1f7d86bb-b824-4e22-87e3-fbe2757e01c1.png" alt="SRI script viewed in a browser" />
