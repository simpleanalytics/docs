---
title: SRI version
category: script
permalink: /sri
---

If you want to use SRI you can do this by using specific scripts. The default scripts are changing to reflect new features or code optimizations. You want to use SRI if you consider it a risk when our scripts change. You can also host our SRI script on your own server or CDN.

When you want to use our SRI version of our script you will need to update your script to `https://scripts.simpleanalyticscdn.com/sri/v4.js`. The full embed script becomes:

```html
<script async defer src="https://scripts.simpleanalyticscdn.com/sri/v4.js" integrity="sha256-rmG3YnEIWDH4256MHh72YNw5EkCpXs4YdUxffKqYU1M= sha384-BV6pfT+M7+ULjTQRwkZA/rEheyrnNSRaoCSdDuzFI3GJrDAgI4ZBFlN3AWAgGLY0 sha512-Jb6whXeacnlX7+d2sFJGYjBTlHWgJMg7M7IgmGl7GSi50YR/mDMtlcwMhgOxTypdtKv6gT75HrBtxvMdFw8P0A==" crossorigin="anonymous"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt=""
/></noscript>
```

When using a [custom domain](/bypass-ad-blockers) you need to use this script: `https://CUSTOM.DOMAIN/v4/app.js`. Replace the `CUSTOM.DOMAIN` with your custom domain. To generate an SRI hash for your custom domain you can use [report-uri.com](https://report-uri.com/home/sri_hash) or [srihash.org](https://www.srihash.org/).

To verify if our script is an SRI version you can always check for `SRI-version` in the first line.
