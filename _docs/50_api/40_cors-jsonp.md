---
title: CORS and JSONP
category: api
hidden: true
permalink: /api/cors-jsonp
last_modified_at: 2026-10-17
---

We have support for JSONP and CORS. Here are two examples with jQuery:

```js
$.ajax({
  url: "https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=pageviews,visitors&callback=?",
  dataType: "jsonp",
  success: function (data) {
    console.log(data);
  },
});

$.ajax({
  url: "https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=pageviews,visitors",
  success: function (data) {
    console.log(data);
  },
});
```

We append the `Access-Control-Allow-Origin`-header with the `*`-value, so any modern browser should accept the request without any effort.

JSONP requests can't send an `Api-Key` header, so only use JSONP for public websites.
