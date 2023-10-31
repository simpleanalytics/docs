---
title: Do Not Track
category: script-settings
permalink: /dnt
last_modified_at: 2023-10-31
---

> This page is about the DNT setting in browsers. We don't track your visitors, [read more on what we collect](/what-we-collect).

DNT stands for Do Not Track. It means that visitors can enable this setting and basically ask the websites they visit to not track them. This is great, but it's not very well supported. The organization behind our internet (W3C) disbanded its DNT working group in January 2018, citing insufficient support and adoption. Apple discontinued support for DNT the following month.

The [Do Not Track](https://en.wikipedia.org/wiki/Do_Not_Track) setting requests that a web application disables either its tracking or cross-site user tracking of an individual user. [We don't do that ever](/what-we-collect), but by default we do not collect visits from devices that have Do Not Track enabled. By default the data will not include visitors with the Do Not Track enabled.

To also record DNT visitors you can add `data-collect-dnt="true"` to the script tag:

<!-- prettier-ignore -->
```html
<script data-collect-dnt="true" async defer src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/hello.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
```

If you don't add the `data-collect-dnt` attribute we will not record visits from users who have DNT enabled.

## Enable collecting DNT visits for noscript.gif pixel

If you use our [noscript.gif](/without-javascript) to collect page views you can also enable collecting DNT visits. Just append `collect-dnt=true` to the pixel. Read more on [the collect without JavaScript page](/without-javascript).

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact).

## Legacy

Before this setting was called `data-skip-dnt`. Although both version will work, we advise you to only use `data-collect-dnt`.
