---
title: Hash mode
menu: Hash mode &#35;
category: script
permalink: /hash-mode
---

Some websites don't really navigate to other pages but us the hash (`#`) in the URL. Normally Simple Analytics removes everything from the URLs after a `?` or a `#`. We don't want to collect this information because it could contain private information like search keywords.

To allow the script to detect those hash changes you can add `data-mode="hash"` to the script tag:

<!-- prettier-ignore -->
```html
<script data-mode="hash" async defer src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
```

This way the Simple Analytics script knows it should detect hash changes and records them as page views. We still drop everything after the question mark, but we keep the hash.

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact).
