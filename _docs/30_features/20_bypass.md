---
title: Bypass ad-blockers
category: features
permalink: /bypass-ad-blockers
last_modified_at: 2026-09-10
---

Simple Analytics never collects any personal identifiable information. Ad-blockers see us just any other analytics company and some of the ad-blockers are blocking our domain as a result. To prevent your stats being blocked as a result we allow you to setup a bypass. This basically hides Simple Analytics' server name from the browser by redirecting a subdomain to our domain.

We created a video showing how to bypass adblockers in Simple Analytics. [Here you go](https://www.youtube.com/watch?v=C8pVceioNi0).

## Proxy

We cannot stress this enough, if you want the best ad-blocker bypass, set up [our proxy](/proxy). It requires technical knowledge, but is the least detectable by ad-blockers.

## Setup a custom subdomain

You only need access to your DNS to set this up. Add a CNAME record to your DNS pointing to `simpleanalyticsexternal.com` and fill in your full domain in [your website settings](https://simpleanalytics.com/select-website/settings#bypass-ad-blockers). We advise to choose a domain like `api.example.com` instead of `track.example.com` _(tracking, analytics, collect, and similar keywords are usually blocked)_.

Add the CNAME record before you save the domain in [your website settings](https://simpleanalytics.com/select-website/settings#bypass-ad-blockers). We check that the record points to `simpleanalyticsexternal.com` and show a warning if it does not. If you see the warning, check the CNAME target, wait for the DNS change to propagate, and save the domain again to retry the check. DNS changes can take a few minutes to propagate.

Existing CNAME records pointing to `external.simpleanalytics.com` or `external.simpleanalytics.io` are also supported.

<img class="border" src="https://assets.simpleanalytics.com/docs/instructions/custom-domain-cloudflare-dns.png" alt="Add Simple Analytics custom domain to Cloudflare DNS">

> If you are using <img src="https://cdn.simpleanalytics.com/images/cloudflare-icon.png" style="height: 10px; margin: 0 3px;" alt=""> Cloudflare, set the record to **DNS only** (the gray cloud). Proxied records hide the CNAME target, so our check cannot verify it.

## Check if SSL works

After you save the domain and the DNS check passes, we automatically make an HTTPS request to your custom domain to start certificate issuance with <a href="https://letsencrypt.org/" target="_blank">Let's Encrypt</a>. Certificates are issued on the first HTTPS connection that needs one, so this first request can take a few seconds. This keeps your analytics traffic encrypted via HTTPS.

Check if your custom domain page shows at `https://custom.domain.com`. It should show something like this:

<img class="border" src="https://assets.simpleanalytics.com/docs/custom-domain/custom-domain-page.png" alt="Placeholder page for custom domain">

If you get an SSL error, try opening the domain again after a few seconds. You can inspect the certificate with our [SSL checker](https://simpleanalytics.com/check-ssl), also linked as **Check SSL certificate** in your website settings. If the error persists, verify your DNS record and save the domain again in your website settings to retry.

## Update your script

Replace your existing Simple Analytics script with this script at the end of your `<body>` (or anywhere else):

<!-- prettier-ignore -->
```html
<script async src="https://custom.domain.com/latest.js"></script>
```

Make sure to replace `custom.domain.com` with your own custom domain.

## Multiple websites

You can use one custom subdomain for all your websites. Keep it linked to at least one website via [your website settings](https://simpleanalytics.com/select-website/settings#bypass-ad-blockers) so we can authorize certificate issuance for that domain. Certificates are renewed automatically. Using one custom domain for multiple websites does not affect performance. It will be running through the same infrastructure.
