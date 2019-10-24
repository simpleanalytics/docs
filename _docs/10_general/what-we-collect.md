---
title: What we collect
category: general
category_order: 1
order: 10
permalink: /what-we-collect
---

To say we don't collect any information would be silly for an analytics tool. We do collect information that is needed to show you the simple analytics. But unlike other analytics tools, we don't collect more than absolutely necessary. Here is a list of what we collect from your users.

<img class="undraw-svg" src="/images/undraw_collecting.svg" alt="">

### IP addresses

> We don't collect and store IPs

We drop the IP address from every request. So don't store them in the logs. We don't hash them with cryptography. We just don't save or collect them. Period.

### Timestamps

> We **collect** and **store** timestamps

We use timestamps to show you the graphs. We store this data because we want to be able to show the information of previous days as well.

### User agents

> We **collect** and **store** user agents for a maximum of **90 days**

We detect and exclude bots and spiders based on the User Agent. We don't believe this data is useful for any other function, but we keep it in our logs (not database) for 90 days. When an incoming request fails for some reason we store the request body in our logs. After 90 days the logs are deleted including the user agents. We don't use User Agents for fingerprinting, but only for showing the OS, device, and browser version

> Update: Jan 14, 2019. We didn't store the User Agents before, but now we save failed requests to our logs, so we added this as a clarification to the paragraph above.

### URLs

> We **partly collect** and **partly store** URL's

Too much information in the URL can be confusing and can make your stats messy. So we only collect and store the first part of the URL. If an URL looks like this `https://example.com/index.html?search=keyword#top` we will only store `https://example.com/index.html`. Also known as the protocol, hostname, and pathname.

### Referrers

> We **collect** and **partly store** referrer's

Referrers answer the question _"Where did the visitor come from?"_. We have 2 ways of checking from which source a user came to your website.

First of all; With most requests, browsers send the URL of the previous website as a referrer. Second; website owners can add a URL param (`utm_source=...`) in the links they post elsewhere. The URL param can also be called `ref=...` or `source=...`. In case we get the referrer via the browser (with full URL) we store it the same as URLs (see above). You can find a list of the most popular referrers in your analytics dashboard.

### Device dimensions

> We **collect** and **store** device dimensions

With the collection of dimensions of the browser window (`window.innerWidth`) we can show the most popular screen sizes. This is useful for you so you can make sure your website works great on all of those dimensions.

### Do Not Track

> We skip when Do Not Track is enabled

The <a href="https://en.wikipedia.org/wiki/Do_Not_Track">Do Not Track</a> setting requests that a web application disables either its tracking or cross-site user tracking of an individual user. <a href="https://simpleanalytics.com/no-tracking">We never track</a> your users, so we skip requests with the Do Not Track enabled. The stats will not include visitors with the Do Not Track enabled.

> We are thinking of making skipping of DNT visitors optional. We don't track or profile anyway. What do you think? Let us know [on Twitter](https://twitter.com/intent/user?screen_name=SimpleAnalytic).
