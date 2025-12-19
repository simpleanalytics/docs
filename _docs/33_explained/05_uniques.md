---
title: Unique visits explained
menu: Unique visits
category: explained
permalink: /explained/unique-visits
redirect_from:
  - /uniques
last_modified_at: 2024-12-19
---

At Simple Analytics, we approach things differently. Our priority is protecting your visitors' privacy while staying compliant with strict privacy laws. This means some of our statistics work differently than traditional analytics tools.

## What we actually measure

Strictly speaking, Simple Analytics doesn't track "unique visitors" in the traditional sense. Instead, we track **unique pageviews**, which we call "visitors" in our dashboard. We chose this terminology because showing both "unique pageviews" and "pageviews" can be confusing for most users.

So when you see "visitors" in Simple Analytics, you're looking at unique pageviews, not individual people tracked across sessions.

## How we detect unique pageviews

We use the [referrer](https://en.wikipedia.org/wiki/HTTP_referer) to determine whether a pageview should be counted as unique. Here's how it works:

**A pageview is counted as unique (visitor) when:**

- There is no referrer (direct traffic)
- The referrer's hostname is different from your website's hostname (traffic from external sources)

**A pageview is NOT counted as unique when:**

- The referrer's hostname matches your website's hostname (internal navigation)
- The user navigates using browser history (back/forward buttons)
- The user reloads the page

For example, if someone visits `randomwebsite.com` and clicks a link to `yourwebsite.com`, the referrer (`randomwebsite.com`) is different from your site, so we count this as a unique pageview (visitor).

If that same person then clicks a link to `yourwebsite.com/page`, the referrer is now `yourwebsite.com` (which matches), so this second pageview is not counted as unique.

![](/images/referrer-visit.jpg)

The same logic applies to direct visits. When someone types `yourwebsite.com` directly into their browser or clicks a link that doesn't send a referrer, there's no referrer available, so we count this as a unique pageview (visitor).

If they then navigate to `yourwebsite.com/page`, the referrer is now `yourwebsite.com`, so this second pageview is not counted as unique.

![](/images/direct-visit.jpg)

## Why some pages have pageviews but (almost) no visitors

This happens naturally with internal navigation. Once someone enters your site (counted as a visitor on their entry page), any subsequent pages they visit during that session only add to pageviews, not visitors. Only pages that users land on directly (with no referrer or a referrer from an external site) can be counted as visitors.

## Single-page applications (SPAs)

For single-page applications, we automatically detect all navigation after the initial page load as non-unique. Only the first pageview uses the referrer-based detection described above.

## No cookies or fingerprinting

> We **do not** use cookies (or any kind of storage), fingerprinting, or PII data.

Traditional analytics tools use cookies to identify unique visitors, storing them on a visitor's computer to track them over long periods. Some privacy-focused tools use hashes of IP addresses combined with dates, but this is still considered fingerprinting and requires consent under GDPR and PECR.

We don't do any of this. Our referrer-based approach requires no storage on the visitor's device and doesn't identify or track individuals.

## No consent needed

> With Simple Analytics you don't need consent. It's one of our core values.

Because we don't use cookies, fingerprinting, or any form of visitor identification, you don't need to ask for consent to use Simple Analytics. Our service is designed for companies that care about aggregate insights, not tracking individual users.

> If you have any questions about how we count visitors or anything else, please [shoot us a message](https://dashboard.simpleanalytics.com/contact).

[Follow Simple Analytics](https://x.com/SimpleAnalytic) or [the founder](https://x.com/adriaandotcom) on X to see how we approach our challenges.
