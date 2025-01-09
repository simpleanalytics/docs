---
title: Unique visits explained
menu: Unique visits
category: explained
permalink: /explained/unique-visits
redirect_from:
  - /uniques
last_modified_at: 2022-04-14
---

At Simple Analytics, we approach things differently. Our priority is to protect the privacy of your visitors while staying compliant with strict (and necessary) privacy laws. This means some of our statistics, like unique visits, work differently.

We record page views because it’s easy to do without compromising privacy. Tracking unique visits, however, can be more invasive. Traditional analytics tools use cookies to identify unique visits, storing them on a visitor’s computer. This allows tracking over long periods, which is highly intrusive.

Some privacy-focused tools improve this slightly by using hashes of a visitor’s IP address combined with a date. While better for privacy, it’s still not ideal. At Simple Analytics, we take it a step further.

## No cookies or fingerprinting

> We **do not** use cookies (or any kind of storage), fingerprinting, or PII data.

Under a European court ruling, pre-ticked cookie consent forms are no longer allowed under GDPR. In the UK, PECR (the privacy directive) already made this clear. Both laws also explicitly forbid visitor fingerprinting.

Many analytics providers rely on fingerprinting techniques, like using IP addresses, to track users. Although this may appear privacy-friendly, it’s considered fingerprinting and requires consent.

## No consent needed

> With Simple Analytics you don't need consent. It's one of our core values.

We don’t think you should ever have to ask for consent. Our service is designed for companies that care about the big picture, not tracking individual customers. That’s why we developed our own unique way of tracking unique visits.

## How it works

When a visitor moves from one website to another, their browser sends a [referrer](https://en.wikipedia.org/wiki/HTTP_referer). For example, if someone visits `randomwebsite.com` and then navigates to `yourwebsite.com`, the browser sends `randomwebsite.com` as the referrer to `yourwebsite.com`. This information helps identify where traffic is coming from, and we use it to determine if a visit is unique. When the referrer doesn't match your website, we count the first pageview as a new visitor.

![](/images/referrer-visit.jpg)

A direct visit occurs when a user lands on your website by typing the URL into their browser or when the previous page does not send a referrer. In that case, we also count the first pageview as a visitor.

![](/images/direct-visit.jpg)

## Some pages have pageviews but (almost) no visitors

This happens when users navigate within your website. After the first visitor is recorded, any additional pageviews during the session are counted as pageviews, not visitors. For example, if someone clicks through multiple pages on your site, those are additional pageviews but not visitors.

## SPAs

If you have a single-page application we automatically see all visits after the first visit as a non unique visit. For the first visit we use above functionality to detect if a visit is unique.

> If you have any questions about legal aspects or anything else, please [shoot us a message](https://simpleanalytics.com/contact).

[Follow Simple Analytics](https://twitter.com/SimpleAnalytic) or [the founder](https://twitter.com/adriaandotcom) on Twitter to see how we approach our challenges.
