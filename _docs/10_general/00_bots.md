---
title: Bots
hidden: true
category: general
permalink: /bots
---

We have a few bots that work for us :)

A few use-cases where we use our bots:
- When a customer adds a website we check if the script is installed correctly
- If a website doesn't have traffic anymore, we send a fake page view to detect our (missing) script<br />_(it's blocked by most analytics tools because we add `bot` in the User-Agent string)_
- We also check which technologies are used on their website so we can show the best plugin for their needs
- We generate screenshots of public referral pages

> You can to disable alerts for your missing script in [your website settings](https://simpleanalytics.com/select-website/settings#alerts).

The bots are usually identified with this User-Agent string:

```
Mozilla/5.0 (compatible; SimpleAnalyticsBot/1.0; +https://docs.simpleanalytics.com/bots)
```

Do you think this bot is causing noise? Please [let us know](https://simpleanalytics.com/contact)!
