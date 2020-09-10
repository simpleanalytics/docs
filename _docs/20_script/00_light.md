---
title: Light version script
category: script
hidden: true
permalink: /light
---

Our script is already very light, but some customers love it even lighter. That's why we always create two versions of our script: normal and light.

Just replace `latest.js` with `light.js` in your embed script. It will look similar to this:

<!-- prettier-ignore -->
```html
<script async defer src="https://scripts.simpleanalyticscdn.com/light.js"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt=""
/></noscript>
```

We support both Brotli and Gzip compression depending on the browser capabilities. To get an idea of our file sizes:

Script | Compressed size (Gzip) | Compressed size (Brotli) | Uncompressed size
-- | --| --| --
light.js | 1.6 KB | 1.7 KB | 2.7 KB
latest.js | 2.9 KB | 2.9 KB | 5.3 KB 

Source: [giftofspeed.com](https://www.giftofspeed.com/gzip-test/) (for Brotli)

## Features

Obviously not all features are available in our light script. Here an comparison of both versions:

Feature                                             | `latest.js` | `light.js` 
:---------------------------------------------------|:-----------:|:----------:
Page views                                          |      x      |      x     
Referrer                                            |      x      |      x     
UTM codes                                           |      x      |      x     
[Uniques](/uniques)                                 |      x      | (will be added)
Time on page                                        |      x      |  
[Events](/events)                                   |      x      |     
[Hash navigation](/hash-mode)                       |      x      |     
Scroll depth                                        |      x      |     
[SPA](/trigger-custom-page-views)                   |      x      |     
Screen sizes                                        |      x      |     
[Ignore pages](/ignore-pages)                       |      x      |    
[Overwrite domain name](/overwrite-domain-name)     |      x      |     
Bot detection                                       |      x      |     
Error reporting                                     |      x      |     
Show warnings                                       |      x      |     
[Ignore DNT](/dnt)                                  |      x      |     
