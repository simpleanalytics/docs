---
title: Do Not Track
category: script
category_order: 2
order: 3
permalink: /dnt
---

> This page is about the DNT setting in browsers. We don't track your visitors, [read more on what we collect](/what-we-collect).

DNT stands for Do Not Track. It means that visitors can enable this setting and basically ask the websites they visit to not track them. This is great, but it's not very well supported. The organization behind our internet (W3C) disbanded its DNT working group in January 2018, citing insufficient support and adoption. Apple discontinued support for DNT the following month.

The [Do Not Track](https://en.wikipedia.org/wiki/Do_Not_Track) setting requests that a web application disables either its tracking or cross-site user tracking of an individual user. [We don't do that ever](/no-tracking), but by default we skip requests with the Do Not Track enabled. The stats will not include visitors with the Do Not Track enabled.

To also record DNT visitors you can add `data-skip-dnt="true"` to the script tag:

<!-- prettier-ignore -->
```html
<script data-skip-dnt="true" async defer src="https://cdn.simpleanalytics.io/hello.js"></script>
<noscript ><img src="https://api.simpleanalytics.io/hello.gif" alt=""/></noscript>
```

If you don't add the `data-skip-dnt` attribute we will not record visits from users where DNT is enabled.

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact?ref={{ site.hostname }}).
