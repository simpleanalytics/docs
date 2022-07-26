---
title: Non-unique hostnames
category: script-settings
permalink: /non-unique-hostnames
created_at: 2022-07-26
last_modified_at: 2022-07-26
---

Suppose you redirect your visitors to a payment provider, and after they complete the payment, they return to your website. Because of the nature of not tracking visitors in Simple Analytics, we count those "returning" visitors as new visitors. To prevent this from happening, you can specify the hostname of that payment provider to tell us we should register this visit as non-unique.

You can specify a list of hostnames (without `https://`) in the `data-non-unique-hostnames` setting of our embed script:

```html
<script
  data-non-unique-hostnames="checkout.stripe.com"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
/>
```

In the above example, visitors coming from `checkout.stripe.com` will be counted a non-unique.
