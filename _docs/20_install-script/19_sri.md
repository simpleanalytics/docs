---
title: SRI version
category: install-script
permalink: /sri
sriVersion: 9
sriHash: sha256-wrULalJT03I+s3JjnJ72rhJk4YjDxqbtwMMyLc7uowY= sha384-2UfNPQId6M49occlZMgVy2iaMMC9rAE0KCqnhEBxLmlBu4o3gVwjcA8AKIgb/qMQ sha512-UqBsXbIOByTjAsluV2ruHqjoobyM0Md03uGeJVMMEpZHXV2UpmE0evS6sC4/wyrCb4DaLzcwFvwTU0GPVA1hTA==
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
