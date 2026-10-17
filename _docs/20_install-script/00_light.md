---
title: Light version script
category: install-script
hidden: true
permalink: /light
last_modified_at: 2026-10-17
---

Our script is already very light, but some customers love it even lighter. That's why we always create two versions of our script: normal and light.

Just replace `latest.js` with `light.js` in your embed script. It will look similar to this:

<!-- prettier-ignore -->
```html
<script async src="https://scripts.simpleanalyticscdn.com/light.js"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
```

We support both Brotli and Gzip compression depending on the browser capabilities. To get an idea of our file sizes:

| Script    | Compressed size (Gzip) | Compressed size (Brotli) | Uncompressed size |
| --------- | ---------------------- | ------------------------ | ----------------- |
| light.js  | 2.0 KB                 | 1.9 KB                   | 3.5 KB            |
| latest.js | 3.8 KB                 | 3.8 KB                   | 7.3 KB            |

Sizes are approximate and measured on the current versions of both scripts.

## Features

Obviously not all features are available in our light script. Here is a comparison of both versions:

| Feature                                                                      | `latest.js` | `light.js` |
| :--------------------------------------------------------------------------- | :---------: | :--------: |
| Page views                                                                   |      x      |     x      |
| Referrer                                                                     |      x      |     x      |
| UTM codes                                                                    |      x      |     x      |
| [Strict UTMs](/strict-utms)                                                  |      x      |     x      |
| [Overwrite domain name](/overwrite-domain-name)                              |      x      |     x      |
| [Uniques](/uniques)                                                          |      x      |    x \*    |
| Bot detection                                                                |      x      |   x \*\*   |
| Show warnings                                                                |      x      |     x      |
| [Events](/events)                                                            |      x      |            |
| [Metadata](/metadata)                                                        |      x      |            |
| Error reporting                                                              |      x      |            |
| Time on page                                                                 |      x      |            |
| Scroll depth                                                                 |      x      |            |
| Screen sizes                                                                 |      x      |            |
| [Hash navigation](/hash-mode)                                                |      x      |            |
| [SPA](/trigger-custom-page-views)                                            |      x      |            |
| [Custom page views](/trigger-custom-page-views#use-custom-collection-anyway) |      x      |            |
| [Ignore pages](/ignore-pages)                                                |      x      |            |
| [Ignore metrics](/ignore-metrics)                                            |      x      |            |
| [Allow URL parameters](/allow-params)                                        |      x      |            |
| [Non-unique hostnames](/non-unique-hostnames)                                |      x      |            |
| [Overwrite path](/overwrite-path)                                            |      x      |            |
| [Collect DNT visits](/dnt)                                                   |      x      |            |

\* `light.js` only uses the referrer to detect unique visits. It doesn't detect reloads and back or forward navigation, so those can count as unique visits.

\*\* In the browser, `light.js` only checks the user agent. The checks on our servers apply to both scripts.

Because `light.js` doesn't support events, it doesn't define the `sa_event` function and doesn't send events, even if you added the placeholder function. Use `latest.js` if you want to collect events.
