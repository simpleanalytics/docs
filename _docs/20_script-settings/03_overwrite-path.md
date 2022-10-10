---
title: Overwrite path
category: script-settings
permalink: /overwrite-path
last_modified_at: 2022-07-26
created_at: 2022-07-26
---

Let's say you want to change the path of your page views (and events). You have profiles of users on your website (`https://example.com/profiles/@adriaan`), but don't want to see the profile name in your dashboard. But you do want to record that profiles did get visits.

This is how you set up a `myPathOverwriter`-function for that usecase:

```html
<script>
  function myPathOverwriter({ path }) {
    if (path.startsWith("/profiles/")) path = "/profiles/***";
    return path;
  }
</script>
<script
  data-path-overwriter="myPathOverwriter"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
></script>
```

You can specify the path callback function via `data-path-overwriter`, in the example above, you specify the `myPathOverwriter`-function. The function gets an object as argument in which you find the `path` key. If the function errors or it returns a falsy value, we keep the original path.

If you want to omit those page views completely, you can use our [ignore pages](/ignore-pages) feature.
