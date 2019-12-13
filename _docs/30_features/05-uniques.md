---
title: Unique visits
category: features
category_order: 3
order: 1
permalink: /uniques
---

At Simple Analytics we do things a bit differently. We put the privacy of your visitors first. At the same time we comply with strict (and necessary) privacy laws. This has effect on our statistics like unique visits. We record page views (which is very easy to do without invading the privacy of your visitors). With unique visits it's slightly difficult. Traditional analytics tools will show you unique visits based on a cookie they place on the visitors computer. This can be very privacy invasive because a visitor can be tracked for a period of time.

With the new ruling of the European court ruling it's forbidden to have pre-ticked cookie consent forms under GDPR. In the UK it's already very clear in PECR (the privacy directive of the UK). In these directives it's also forbidden to fingerprint a visitor. Other analytics businesses use this technique based on IP address for example. This seems privacy friendly but is considered fingerprinting. For which you need consent.

We don't want you to ask for consent ever. Our service is targeted at companies that want to get the big picture. Tracking customers is not part of that. That's why we came up with are unique way of tracking unique visits.

When a visitor navigates from website to website the browser sends a referrer along. If you for example visit website `randomwebsite.com` and navigate to `yourwebsite.com` it sends the referrer `randomwebsite.com` to `yourwebsite.com`. This is very useful to know where traffic comes from. We use the referrer to calculate if a visit is unique.

![](/images/referrer-visit.jpg)

When a user lands on your website without visiting another website we will record it as a non unique visit:

![](/images/direct-visit.jpg)

If you have any questions about legal aspects or anything else, please [shoot us a message](https://simpleanalytics.com/contact?ref={{ site.hostname }}).
