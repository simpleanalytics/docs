---
title: Overwrite domain name
category: script
permalink: /overwrite-domain-name
---

Sometimes you want to link multiple domains into one domain in your dashboard. Or you want to use a different domain than people see in their browser address bar. You can overwrite the default domain name by specifying its hostname.

Make sure to include the our <code>simpleanalytics<strong>cdn</strong>.com</code> script. Include these two lines at the end of your `<body>`:

<!-- prettier-ignore -->
```html
<script async defer data-hostname="" src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif?hostname=" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
```

You see that we added an attribute (`data-hostname=""`) to the script tag and `hostname` param to the `img` tag. If you add your domain to it (eg `example.com`) it will look like this:

<!-- prettier-ignore -->
```html
<script async defer data-hostname="example.com" src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif?hostname=example.com" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
```

## Add used domain to your dashboard

Now all the visits you collect with this script are collected under the name `example.com`. Make sure you [add the new used domain name](https://simpleanalytics.com/websites/add) (`example.com`) to your dashboard.
