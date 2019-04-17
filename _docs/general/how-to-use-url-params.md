---
title: How to use URL parameters
menu: How to use URL params
category: general
category_order: 1
order: 3
permalink: /how-to-use-url-parameters
---

When you want to know where visitors are coming from you can add certain parameters to your URL. Browsers send the previous page (referrer) to the next page so you can see where a visitor did come from. There are a few ways how we determine where a visitor comes from.

## Using an URL parameter

First we check the referrer for the parameters `ref`, `source`, and `utm_source`. So if you link your website in your email it's wise to add something like this:

```
https://example.com/path?ref=email
```

This way Simple Analytics knows where the visitor did come from (email) and will save this information and show it in the dashboard (as a referrer).

## Using the referrer URL

If there is no parameter found we save the URL of the referrer. We only save the part before any `?` or `#`. So for example if the referrer URL is `https://referrer.com/search?query=sensitive+information` we only store `referrer.com/search`. You don't have to do anything to make this work.

Go to [what we collect](/what-we-collect) if you want to know more about what we collect and store of your visitors.
