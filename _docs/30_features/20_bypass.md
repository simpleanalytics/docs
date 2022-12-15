---
title: Bypass ad-blockers
category: features
permalink: /bypass-ad-blockers
last_modified_at: 2022-04-14
---

Simple Analytics never collects any personal identifiable information. Ad-blockers see us just any other analytics company and some of the ad-blockers are blocking our domain as a result. To prevent your stats being blocked as a result we allow you to setup a bypass. This basically hides Simple Analytics' server name from the browser by redirecting a subdomain to our domain.

## Setup a custom subdomain

You only need access to your DNS to set this up. Add a CNAME record to your DNS pointing to `simpleanalyticsexternal.com` and fill in your full domain in [your website settings](https://simpleanalytics.com/select-website/settings#bypass-ad-blockers). We advise to choose a domain like `api.example.com` instead of `track.example.com` _(tracking, analytics, collect, and similar keywords are usually blocked)_.

You will need to enable the record in [your website settings](https://simpleanalytics.com/select-website/settings#bypass-ad-blockers) on Simple Analytics. We need to know this to request a certificate with <a href="https://letsencrypt.org/" target="_blank">Let's Encrypt</a>. This means your analytics will travel safe via HTTPS to our servers.

<img class="border" src="/images/cloudflare-dns-custom-domain.png" alt="Add Simple Analytics custom domain to CloudFlare DNS">

> If you are using <img src="https://cdn.simpleanalytics.com/images/cloudflare-icon.png" style="height: 10px; margin: 0 3px;" alt=""> CloudFlare, make sure to disable the orange cloud.

## Check if SSL works

Check if your custom domain page shows at `https://custom.domain.com`. It should show something like this:

<img class="border" src="https://assets.simpleanalytics.com/docs/custom-domain/custom-domain-page.png" alt="Placeholder page for custom domain">

If you get an SSL error, please hit refresh in your [website settings](https://simpleanalytics.com/select-website/settings#bypass-ad-blockers):

<img class="border" src="https://assets.simpleanalytics.com/docs/custom-domain/check-ssl-certificate.png" alt="Check SSL certificate in website settings">

## Update your script

Include these two lines at the end of your `<body>` (or anywhere else):

<!-- prettier-ignore -->
```html
<script async defer src="https://custom.domain.com/latest.js"></script>
<noscript><img src="https://custom.domain.com/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
```

Make sure to replace `custom.domain.com` with your own custom domain.

## Multiple websites

You can use one custom subdomain for all your websites. Make sure to link it to at least one domain via [your website settings](https://simpleanalytics.com/select-website/settings#bypass-ad-blockers). If you add the custom domain to one website we know which SSL certificates need renewal and which ones we can delete. Using one custom domain for multiple websites does not effect performance. It will be running through the same infrastructure.
