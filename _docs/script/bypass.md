---
title: Bypass ad-blockers
category: script
category_order: 3
order: 4
permalink: /bypass-ad-blockers
---

Simple Analytics never collects any personal identifiable information. Ad-blockers see us just any other analytics company and some of the ad-blockers are blocking our domain as a result. To prevent your stats being blocked as a result we allow you to setup a bypass. This basically hides Simple Analytics' server name from the browser by redirecting a subdomain to our domain.

## Setup a custom subdomain

You only need access to your DNS to set this up. Add a CNAME record to your DNS pointing to `external.simpleanalytics.io.` _(including the last dot `.`)_ and fill in your own full domain here. We advise to choose a domain like `api.example.com` instead of `track.example.com` _(tracking, analytics, collect, and similar keywords are usually blocked)_.

You will need to enable the record in your website settings on Simple Analytics. We need to know this to request a certificate with <a href="https://letsencrypt.org/" target="_blank">Let's Encrypt</a>. This means your analytics will travel safe via HTTPS to our servers.

> If you are using <img src="https://cdn.simpleanalytics.io/images/cloudflare-icon.png" style="height: 10px; margin: 0 3px;" alt=""> CloudFlare, make sure to disable the orange cloud.
