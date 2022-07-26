---
title: Collect in AMP
category: install-script
permalink: /collect-in-amp
last_modified_at: 2022-04-14
---

AMP is a web component framework by Google that you can use to create websites. It's loading last because it's cached on the servers of Google. Learn more about [how it works](https://amp.dev/about/how-amp-works/). To collect page views via AMP you can use [our collect pixel without JavaScript](/without-javascript).

We built this feature for websites that want to collect page views but don't want to require JavaScript. This is great for websites that need to load fast. AMP is such a framework where speed matters and having less JavaScript helps.

You can embed the pixel via an image tag:

```html
<img
  src="https://queue.simpleanalyticscdn.com/noscript.gif?hostname=example.com&path=/page-one"
  referrerpolicy="no-referrer-when-downgrade"
  alt=""
/>
```

This way there is no JavaScript needed and you can still collect page views within environments like AMP. You can add more data to the pixel by adding parameters to its URL. [Read more about that here](/without-javascript).

> We do not recommend using AMP for your website as it's very platform (Google) specific. Optimize your website for all platforms so everybody enjoys the (speed) improvements.
