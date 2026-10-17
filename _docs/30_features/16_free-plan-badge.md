---
title: Free plan badge
category: features
permalink: /free-plan-badge
created_at: 2026-10-17
last_modified_at: 2026-10-17
---

From November 1, 2026, websites on the Free plan need to show a Simple Analytics badge. Paid plans don't require a badge. If you'd rather not show it, [upgrade to a paid plan](https://www.simpleanalytics.com/pricing).

Build your badge and copy the code on [our badges page](https://www.simpleanalytics.com/badges). Place it in a footer that shows on every page of your website.

## When we check

- The first check runs 14 days after the first visit to your website. Unfinished and inactive websites aren't checked.
- After that, we check about every 30 days.
- We don't check while your trial is active.
- We look for the badge on the most visited page of your website in the last 30 days. If that page no longer exists, we check your homepage.

Our scanner identifies itself as `SimpleAnalyticsBot`. See [our bots page](/bots) for the full user agent.

## What counts as a badge

The badge needs to be visible on the page. We find it when the page shows one of these:

- The badge image from `simpleanalyticsbadges.com`, like in the code from [our badges page](https://www.simpleanalytics.com/badges).
- An image that links to `simpleanalytics.com` with `utm_content=badge` in the link.
- An unchanged copy of the badge that you host yourself, in any image format browsers support (for example SVG, PNG, or WebP).

Keep the badge's link to Simple Analytics intact. Hidden elements, for example with `display: none` or `opacity: 0`, don't count.

If your website uses a [Content Security Policy](/csp), add `img-src simpleanalyticsbadges.com` to your policy.

## When the badge is missing

If we can't find the badge, we email the owners and admins of your team and show a notice in your dashboard. You then have 14 days to add the badge. After those 14 days, we check again.

If the badge is still missing, we lock dashboard data, API access, and exports for that website. API requests return HTTP status `423`. This also affects public dashboards and embedded charts. We keep collecting your page views and events while access is locked.

After you add the badge, an owner or admin needs to click **Check badge again** in the dashboard notice. We don't check locked websites again automatically. When we find the badge, access returns right away. You can run this check once every 10 minutes.

If your website blocks our scanner (for example with a captcha or a `401`, `403`, or `429` response) or can't be reached, we don't warn you or lock your website because of that check. We try again later.
