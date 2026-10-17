---
title: Bots
hidden: true
category: general
permalink: /bots
last_modified_at: 2026-10-17
redirect_from:
  - /b
---

We have a few bots that work for us :)

A few use-cases where we use our bots:
- When a customer adds a website we check if the script is installed correctly
- If a website doesn't have traffic anymore, we send a fake page view to detect our (missing) script<br />_(it's blocked by most analytics tools because we add `bot` in the User-Agent string)_
- We also check which technologies are used on their website so we can show the best plugin for their needs
- We generate screenshots of public referral pages
- We check if websites on the Free plan show the [Simple Analytics badge](/free-plan-badge)

> You can to disable alerts for your missing script in [your website settings](https://simpleanalytics.com/select-website/settings#alerts).

The bots are usually identified with this User-Agent string:

```
Mozilla/5.0 (compatible; SimpleAnalytics/1.0; +https://docs.simpleanalytics.com/b)
Mozilla/5.0 (compatible; SimpleAnalyticsBot/1.0; +https://docs.simpleanalytics.com/bots)
```

Do you think this bot is causing noise? Please [let us know](https://simpleanalytics.com/contact)!

## How we detect bots on your website

We don't show visits from bots in your dashboard. You can still [download them](/export-data). We mark a page view or event as coming from a bot when:

- The User-Agent contains `bot`, `spider`, `crawl`, or `agent`, or matches our list of known crawlers
- Our script detects a browser that is controlled by automation software, like a headless browser
- The viewport has exactly the same size as a landscape screen (this happens with automated browsers, but also with browsers in full screen mode), or matches sizes that are known to come from bots
- The request comes from a known data center and you enabled [advanced robot blocking](/robot-blocking)
