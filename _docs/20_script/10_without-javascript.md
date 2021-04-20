---
title: Collect without JavaScript
category: script
permalink: /without-javascript
---

Normally you would collect page view via our [open source JavaScript](/script). But there are other way to collect those. You can either send data via [your own server](/server-side-tracking) or send it through a pixel (a small GIF image).

> By default we already include a pixel (image) with our `<noscript>` tag. This tag gets executed when a visitor disabled JavaScript in their browser. The pixel inside the tag will still record that page view. The data connected to that page view is limited, but still useful for the overal picture.

To collect page views with our pixel you can add parameters to the URL of the image:

```html
<img
  src="https://queue.simpleanalyticscdn.com/noscript.gif?timezone=Europe%2FAmsterdam&unique=false"
  referrerpolicy="no-referrer-when-downgrade"
  alt=""
/>
```

In the example above we send a time zone and unique boolean with the pixel.

By default it will take the referrer of the pixel. This is the URL for the page the pixel is displayed on. It is **not** the referrer of the page, that is inaccessible from the pixel.

We automatically fetch this information via the referrer if you don't provide anything as pixel parameters: \*

- `hostname` (for example `example.com`)
- `https` (boolean `true` if protocol of the website is https)
- `path` (path including the `/`)
- `ua` (user agent)
- `utm_source`
- `utm_medium`
- `utm_campaign`
- `utm_content`
- `utm_term`

You can overwrite those via the pixel parameters.

These are the values we can't get with the pixel alone:

- timezone ([a valid JS time zone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones))
- referrer (the [document.referrer](https://developer.mozilla.org/en-US/docs/Web/API/Document/referrer) of the page)
- unique (if a visit is unique; true or false)
- collect-dnt (boolean to tell if it should collect [DNT visits](/dnt#enable-collecting-dnt-visits-for-noscriptgif-pixel))

> \* We advice to always include the `hostname` and `path` parameters if possible. Some times the browser does not send a referrer with the image and then we can't store a page view.

This way you are more in control what you are sending to our servers. It's also a great way if you need to avoid JavaScript for example within Google AMP environments.

> We don't record visitors that have DNT enabled. If you want to record those visits add `ignore-dnt=true` to the pixel parameters.

## Validate your implementation

If you want to validate your implementation you can test this in your browser. Open the page you implemented the pixel on.

1. Right click with your mouse somewhere on the page
1. Click "inspect" or sometimes "inspect element" in the menu that pops up
1. Click the "network" tab
1. Search for a request that ends with "noscript.gif"
1. In the sidebar you will see the headers of that request. Look for the "simple-analytics-feedback" header and check the value. It should say something like: "Thanks for sending this page view!"

<img src="/images/pixel-check-feedback.jpg" alt="Validate pixel feedback in browser" class="border">
