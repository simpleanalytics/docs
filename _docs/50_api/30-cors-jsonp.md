---
title: CORS and JSONP
category: api
category_order: 9
order: 3
permalink: /api/cors-jsonp
---

We have support for JSONP and CORS. Here are two examples with jQuery:

```js
$.ajax({
  url: "https://simpleanalytics.com/simpleanalytics.com.json?callback=?",
  dataType: "jsonp",
  success: function(data) {
    console.log(data);
  }
});

$.ajax({
  url: "https://simpleanalytics.com/simpleanalytics.com.json",
  success: function(data) {
    console.log(data);
  }
});
```

We append the `Access-Control-Allow-Origin`-header with the `*`-value , so any modern browser should accept the request without any effort.
