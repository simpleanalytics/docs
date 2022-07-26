---
title: Light version script
category: script
hidden: true
permalink: /light
last_modified_at: 2022-04-14
---

Our script is already very light, but some customers love it even lighter. That's why we always create two versions of our script: normal and light.

Just replace `latest.js` with `light.js` in your embed script. It will look similar to this:

<!-- prettier-ignore -->
```html
<script async defer src="Check Gzip/Brotli Compression"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
```

We support both Brotli and Gzip compression depending on the browser capabilities. To get an idea of our file sizes:

| Script    | Compressed size (Gzip) | Compressed size (Brotli) | Uncompressed size |
| --------- | ---------------------- | ------------------------ | ----------------- |
| light.js  | 1.9 KB                 | 2.0 KB                   | 3.3 KB            |
| latest.js | 3.7 KB                 | 3.8 KB                   | 6.9 KB            |

Source: [giftofspeed.com](https://www.giftofspeed.com/gzip-test/) for Brotli, [adresults.nl/tools/gzip-compression-test](https://adresults.nl/tools/gzip-compression-test) for Gzip.

## Features

Obviously not all features are available in our light script. Here an comparison of both versions:

| Feature                                         | `latest.js` |   `light.js`    |
| :---------------------------------------------- | :---------: | :-------------: |
| Page views                                      |      x      |        x        |
| Referrer                                        |      x      |        x        |
| UTM codes                                       |      x      |        x        |
| [Uniques](/uniques)                             |      x      |        x        |
| [Events](/events)                               |      x      |        x        |
| Bot detection                                   |      x      |        x        |
| Error reporting                                 |      x      |        x        |
| Show warnings                                   |      x      |        x        |
| Time on page                                    |      x      |                 |
| [Hash navigation](/hash-mode)                   |      x      |                 |
| Scroll depth                                    |      x      |                 |
| [SPA](/trigger-custom-page-views)               |      x      |                 |
| Screen sizes                                    |      x      |                 |
| [Ignore pages](/ignore-pages)                   |      x      |                 |
| [Overwrite domain name](/overwrite-domain-name) |      x      |                 |
| [Ignore DNT](/dnt)                              |      x      |                 |
