---
title: How to use URL parameters
menu: How to use URL params
category: general
permalink: /how-to-use-url-parameters
excerpt: "You can add URL parameters to see where your customers are coming from."
last_modified_at: 2022-04-14
---

There are a few ways we determine where a visitor comes from. We automatically detect the previous page (referrer) from the visitor's browser, but you can also add a URL parameter to override this and set a custom referrer.

## Using a URL parameter

If the current URL on your site includes a parameter named `ref` or `utm_source`, we use this value instead of the browser's previous page.

For example, if you were to include this link in an email newsletter, Simple Analytics records the referrer as `email` in your dashboard, no matter where user actually comes from:

```
https://example.com/landing-page?ref=email
```

### UTM codes

UTM codes are bits of text you can add to a link that tell Simple Analytics (as well as other analytics tools) a little bit more information about each link. Here's a sample of what one looks like:

```
https://example.com/landing-page?utm_source=company-x&utm_medium=newsletter&utm_campaign=march_01
```

We support the following codes:

- UTM source (e.g.: `utm_source=company-x`)
- UTM medium (e.g.: `utm_medium=newsletter`)
- UTM campaign (e.g.: `utm_campaign=march_01`)
- UTM content (e.g.: `utm_content=button_red`)
- UTM term (e.g.: `utm_term=shoes`, this param is deprecated as it is intended to contain user generated content)

The UTM codes will show up on the dashboard in the "Referrals" dropdown menu:

<img class="border" style="width: 583px" src="https://assets.simpleanalytics.com/docs/dashboard/utm-dropdown.png" />

[Read the UTM guide](https://buffer.com/library/utm-guide/) at Buffer to learn more about UTM codes.

### Forbidden characters

Certain character are not allowed in the URL parameter. Letters and numbers are always okay, but if you want to use special characters (like spaces, `;`, `/`, `?`, `:`, `@`, `&`, `=`, `+`, `$`, or `,`) you need to escape your URL parameter. A good website that does this for you is [urlencoder.io](https://www.urlencoder.io/).

Valid examples of URL parameters:

```
https://example.com/?ref=email-button
https://example.com/
https://example.com/?ref=android%3A%2F%2Fcom.example.app%2Fpath
https://example.com/?ref=exister%2C%20avoir%20une%20r%C3%A9alit%C3%A9
```

## Using the referrer URL

> The referrer URL is only used if there are none of the URL parameters mentioned above

If there is no referral parameter found, we save the URL of the referring page from the visitor's browser. We only save the part of the referrer before `?` or `#`, so if the referrer URL is `https://referrer.example.com/search?query=sensitive+information`, we only store `referrer.example.com/search`. Note that the protocol (`https://`) is also removed. We also ignore common subdomains like `www.`, `m.`, `l.`, and `www2.`.

> You don't have to do anything to make this work.

## Parsing of values

We parse the URL parameter differently than the referrer URL. Because you generate the URL parameters yourself, we don't want to touch these too much. Instead, we decode their values (so you can use forbidden characters) and convert hostnames to more general names. For example, we convert `www.google.com` to `google`. We still store the original value, but we show `google` as the referrer in the dashboard. We do this so we can combine similar referrers, such as `www.google.com`, `google.nl`, and `google.fr`, into simply `google`.

Referrer URLs contain the full URL that the browser gives us, such as `https://www.example.com/search?query=sensitive+information`. From this URL we store `example.com` as the referrer and keep `example.com/search` as the original URL. We drop the query (`?query=sensitive+information`), protocol (`https://`), and common subdomain (`www.`).
