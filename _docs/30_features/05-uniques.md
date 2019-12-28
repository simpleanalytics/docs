---
title: Unique visits
category: features
category_order: 3
order: 1
permalink: /uniques
---

At Simple Analytics we do things a bit differently. We put the privacy of your visitors first. At the same time we comply with strict (and necessary) privacy laws. This has an impact on our statistics, like unique visits. We record page views (which is very easy to do without invading the privacy of your visitors). With unique visits it's slightly difficult to invade. Traditional analytics tools will show you unique visits based on a cookie they place on the visitors computer. This can be extremely invasive to privacy because a visitor can be tracked for a longer period of time.

## No cookies or fingerprinting

> We **do not** use cookies (or any kind of storage), fingerprinting, or PII data.

With the new ruling of the European court it's forbidden to have pre-ticked cookie consent forms under GDPR. In the UK it's already clear in PECR (the UK's privacy directive). In these directives it's also forbidden to fingerprint a visitor. Other analytics businesses use this technique (for example based on IP address). This seems privacy friendly but is considered fingerprinting. For which, you need consent.

## No consent needed

> With Simple Analytics you don't need consent. It's one of our core values.

We don't want you to ask for consent ever. Our service is targeted at companies that want to get the big picture. Tracking customers is not part of that. That's why we came up with our unique way of tracking unique visits.

## How it works

When a visitor navigates from website to website the browser sends a [referrer](https://en.wikipedia.org/wiki/HTTP_referer) along. If you for example visit website `randomwebsite.com` and navigate to `yourwebsite.com` it sends the referrer `randomwebsite.com` to `yourwebsite.com`. This referrer is very useful to figure out where traffic is coming from. We use the referrer to calculate if a visit is unique.

![](/images/referrer-visit.jpg)

When a user lands on your website without visiting another website (direct visit) we record it as a unique visit:

![](/images/direct-visit.jpg)

## SPAs

If you have a single-page application we automatically see all visits after the first visit as a non unique visit. For the first visit we use above functionality to detect if a visit is unique.

> If you have any questions about legal aspects or anything else, please [shoot us a message](https://simpleanalytics.com/contact?ref={{ site.hostname }}).

[Follow Simple Analytics](https://twitter.com/SimpleAnalytic) or [the founder](https://twitter.com/adriaanvrossum) on Twitter to see how we approach our challenges.
