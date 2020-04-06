---
title: How to use URL parameters
menu: How to use URL params
category: general
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

## Parsing of values

We parse the URL parameters differently then the referrer URL. Because people generate the URL parameters themselves we don't want to touch those too much. What we do is we decode their values (so you can use forbidden characters) and convert hostnames to more general names. For example we convert `www.google.com` to `google`. We still store the original value, but we show google as a referrer in the dashboard. We do this so we can combine similar referrers into one. So we count `www.google.com`, `google.nl`, and `google.fr` as `google`.

Referrer URLs contain the full URL that the browser gives us. It's something like `https://www.referrer.com/search?query=sensitive+information`. From this URL we store only `referrer.com` as the referrer and we keep `referrer.com/search` as the original referrer. We drop the query, protocol, and common subdomain.

<img class="undraw-svg" src="/images/undraw_segment.svg" alt="">
