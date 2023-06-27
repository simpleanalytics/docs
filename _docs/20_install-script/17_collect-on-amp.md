---
title: Collect in AMP
category: install-script
permalink: /collect-in-amp
last_modified_at: 2023-06-27
---

AMP is a web component framework by Google that you can use to create websites. It's loading last because it's cached on the servers of Google. Learn more about [how it works](https://amp.dev/about/how-amp-works/). To collect page views via AMP you can use [our collect pixel without JavaScript](/without-javascript) or use the default [`<amp-analytics>` component]().

## Use `<amp-analytics>` component

According to the [AMP docs](https://amp.dev/documentation/components/amp-analytics), include the `<amp-analytics>` script in the `<head>` of your AMP file:

```html
<script async custom-element="amp-analytics" src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js"></script>
```

Then in the `<body>` of the page, include the `<amp-analytics>` component:

```html
<amp-analytics>
  <script type="application/json">
    {
      "vars": {
        "dataHostname": "example.com"
      },
      "requests": {
        "pageview": "https://queue.simpleanalyticscdn.com/events"
      },
      "extraUrlParams": {
        "hostname": "$DEFAULT(${dataHostname}, ${sourceHostname})",
        "hostname_original": "$IF($EQUALS(${dataHostname}, ${sourceHostname}), , ${sourceHostname})",
        "path": "${sourcePath}",
        "referrer": "${documentReferrer}",
        "ua": "${userAgent}",
        "timezone": "${timezoneCode}",
        "screen_width": "${screenWidth}",
        "screen_height": "${screenHeight}",
        "viewport_width": "${viewportWidth}",
        "viewport_height": "${viewportHeight}",
        "utm_source": "QUERY_PARAM(utm_source)",
        "utm_medium": "QUERY_PARAM(utm_medium)",
        "utm_campaign": "QUERY_PARAM(utm_campaign)",
        "utm_content": "QUERY_PARAM(utm_content)",
        "utm_term": "QUERY_PARAM(utm_term)"
      },
      "triggers": {
        "trackPageview": {
          "on": "visible",
          "request": "pageview",
          "extraUrlParams": {
            "type": "pageview"
          }
        }
      },
      "transport": {
        "beacon": true,
        "xhrpost": true,
        "image": false,
        "useBody": true
      }
    }
  </script>
</amp-analytics>
```

Make sure to rename `example.com` with your own hostname.

## Use our pixel tag

It requires more coding on your side, so we recommend to use the `<amp-analytics>` component.

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

> We do not recommend using AMP for your website as it's very platform (Google) specific. Optimize your website for all platforms so everybody enjoys the (speed) improvements. On top of that, [Google hints](https://developers.google.com/search/blog/2021/04/more-details-page-experience#details) towards AMP not being important anymore.
