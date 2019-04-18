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

### Forbidden characters

Certain character are not allowed in the URL parameters. Letter and numbers are always okay. If you want to use special characters (like spaces, `;`, `/`, `?`, `:`, `@`, `&`, `=`, `+`, `$`, or `,`) you need to escape your URL parameter. A good website that does this for you is [urlencoder.io](https://www.urlencoder.io/?ref={{ site.hostname }}).

Valid examples of URL parameters:

```
https://example.com/?ref=email-button
https://example.com/?ref={{ site.hostname }}
https://example.com/?ref=android%3A%2F%2Fcom.example.app%2Fpath
https://example.com/?ref=exister%2C%20avoir%20une%20r%C3%A9alit%C3%A9
```

> The referrer URL is only used the there are no URL parameters found

## Using the referrer URL

If there is no parameter found we save the URL of the referrer. We only save the part before any `?` or `#`. So for example if the referrer URL is `https://app.referrer.com/search?query=sensitive+information` we only store `app.referrer.com/search`. Note that the protocol (`https://`) is gone. We also delete common subdomains like `www.`, `m.`, `l.`, and `www2.` from the URL.

> You don't have to do anything to make this work.



Go to [what we collect](/what-we-collect) if you want to know more about what we collect and store of your visitors.

<img class="undraw-svg" src="/images/undraw_segment.svg" alt="">
