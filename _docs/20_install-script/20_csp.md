---
title: Content Security Policy
category: install-script
permalink: /csp
last_modified_at: 2022-07-14
---

Content Security Policy (CSP) is an added layer of security that helps to detect and mitigate certain types of attacks, including Cross Site Scripting (XSS) and data injection attacks. These attacks are used for everything from data theft to site defacement to distribution of malware. [Read more on CSP at MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP).

## Content-Security-Policy header

For Simple Analytics you want to add the following Content Security Policy header (we included `'self'` for all as well):

<!-- prettier-ignore -->
```
Content-Security-Policy: script-src 'self' 'unsafe-inline' https://scripts.simpleanalyticscdn.com; connect-src 'self' https://queue.simpleanalyticscdn.com; img-src 'self' https://queue.simpleanalyticscdn.com https://simpleanalyticsbadges.com;
```

## Content-Security-Policy meta tag

Alternatively, a `<meta>` element can be used to configure a policy, for example:

```
<meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline' https://scripts.simpleanalyticscdn.com; connect-src 'self' https://queue.simpleanalyticscdn.com; img-src 'self' https://queue.simpleanalyticscdn.com https://simpleanalyticsbadges.com;">
```

Basically we use `https://scripts.simpleanalyticscdn.com` for our public script, `https://queue.simpleanalyticscdn.com` to send Beacon API data and error requests, and we use `https://queue.simpleanalyticscdn.com` also for sending data through our "pixel". If you show our badge, you need to have `https://simpleanalyticsbadges.com`.

## Why `script-src 'unsafe-inline'`?

If you use the automated events, make sure to have `'unsafe-inline'` in your `script-src`, otherwise you can remove that from the examples above. We use `'unsafe-inline'` to add [`onClick`](https://developer.mozilla.org/en-US/docs/Web/API/Element/click_event) event listeners to your download buttons, email links, and outbound links.

Don't forget to add your own assets to the above Content Security Policy.
