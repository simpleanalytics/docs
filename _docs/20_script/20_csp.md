---
title: Content Security Policy version
menu: CSP version
category: script
permalink: /csp
---

Content Security Policy (CSP) is an added layer of security that helps to detect and mitigate certain types of attacks, including Cross Site Scripting (XSS) and data injection attacks. These attacks are used for everything from data theft to site defacement to distribution of malware. [Read more on CSP at MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP).

For Simple Analytics you want to add the following Content Security Policy header (we included `'self'` for all as well):

<!-- prettier-ignore -->
```
Content-Security-Policy: script-src 'self' https://scripts.simpleanalyticscdn.com; connect-src 'self' https://queue.simpleanalyticscdn.com; img-src 'self' https://queue.simpleanalyticscdn.com;
```

Alternatively, the <meta> element can be used to configure a policy, for example:

```
<meta http-equiv="Content-Security-Policy" content="script-src 'self' https://scripts.simpleanalyticscdn.com; connect-src 'self' https://queue.simpleanalyticscdn.com; img-src 'self' https://queue.simpleanalyticscdn.com;">
```

Basically we use `https://scripts.simpleanalyticscdn.com` for our public script, `https://queue.simpleanalyticscdn.com` to send Beacon API data and error requests, and we use `https://queue.simpleanalyticscdn.com` also for sending data through our pixel.

Don't forget to add your own assets to the above Content Security Policy.
