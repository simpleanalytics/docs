---
title: Hash mode
category: script
category_order: 2
order: 3
permalink: /hash-mode
---

Some websites don't really navigate to other pages but us the hash (`#`) in the URL. Normally Simple Analytics removes everything from the URLs after a `?` or a `#`. We don't want to collect this information because it could contain private information like search keywords.

To allow the script to detect those hash changes you can add `data-mode="hash"` to the script tag:

```html
<script data-mode="hash" async defer src="https://cdn.simpleanalytics.io/hello.js"></script>
<noscript><img src="https://api.simpleanalytics.io/hello.gif" alt=""></noscript>
```

This way the Simple Analytics script knows it should detect hash changes and records them as page views.
