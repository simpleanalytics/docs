---
title: What we collect
category: general
order: 10
permalink: /what-we-collect
---

Not collecting any information would be silly for an analytics tool. We do collect information that is necessary to show you the simple analytics. But unlike other analytics tools, we don't collect more than absolutely necessary. Here is a list of what we do collect from our users.

### IP addresses

> We don't collect and store IPs

We drop the IP address from request. We don't hash them with cryptography. We just don't save or collect them. Period.

<blockquote class="note">
  <p markdown="1">Update: Nov 21, 2019. Just to be completely transparent: we found IPs in our logs when requests on our server were failing. We fixed this by filtering all log messages and replace IPs with zero's using [mmanon](https://www.rsyslog.com/doc/v8-stable/configuration/modules/mmanon.html). Now all IPs (like `1.1.1.1` or `2606:4700:4700::1111`) will become `0.0.0.0` or `0:0:0:0:0:0:0:0` before it enters our logs.</p>
</blockquote>

### Unique views

> We **collect** and **store** if visits are unique

Our unique detection of visits is quite unique by itself. Most services use cookies or IP addresses to see if a visitor has visited the website. We don't use cookies or IP addresses, so not either for detecting unique visits. In the UK for example you can't use IP addresses (even hashed) without an active opt-in. This is why Simple Analytics is compatible with all existing privacy laws. You don't need an opt-in for our service.

We detect a unique visit based on the hostname of the _referrer_ of the page. If a user comes from one domain to another it shares the previous domain with the next via a so called _referrer_. If the domain is the same as the one in the _referrer_ we know it's a non-unique visit.

[Read more](/uniques) on how we register unique pages views.

### Timestamps

> We **collect** and **store** timestamps

We use timestamps to show you the graphs. We store this data because we want to be able to show the information of previous days as well.

### User agents

> We **collect** and **store** user agents for a maximum of **90 days**

We detect and exclude bots and spiders based on the User Agent. We don't believe this data is useful for any other function, but we keep it in our logs (not database) for 90 days. When an incoming request fails for some reason we store the request body in our logs. After 90 days the logs are deleted including the user agents. We don't use User Agents for fingerprinting, rather only for showing the OS, device, and browser version.

<blockquote class="note">
  <p>Update: Jan 14, 2019. Previously, we didn't store the User Agents, but now we save failed requests to our logs, so we added this as a clarification to the paragraph above.</p>
</blockquote>

### URLs

> We **partly collect** and **partly store** URL's

Too much information in the URL can be confusing and can make your stats messy. So we only collect and store the first part of the URL. If an URL looks like this `https://example.com/index.html?search=keyword#top` we will only store `https://example.com/index.html`. Also known as the protocol, hostname, and pathname.

### Referrers

> We **collect** and **partly store** referrer's

Referrers answer the question _"Where did the visitor come from?"_. We have two ways of checking the source of a user that visited your website.

First of all; With most requests, browsers send the URL of the previous website as a referrer. Second; website owners can add a URL param (`utm_source=...`) in the links they post elsewhere. The URL param can also be called `ref=...` or `source=...`. In case we get the referrer via the browser (with full URL) we store it the same as URLs (see above). You can find a list of the most popular referrers in your analytics dashboard.

### Device dimensions

> We **collect** and **store** device dimensions

With the collection of dimensions of the browser window (`window.innerWidth`) we can show the most popular screen sizes. This is useful for you so you can make sure your website works great on all of those dimensions.

### Do Not Track

> We skip when Do-Not-Track is enabled

The <a href="https://en.wikipedia.org/wiki/Do_Not_Track">Do Not Track</a> setting requests that a web application disables either its tracking or cross-site user tracking of an individual user. <a href="https://simpleanalytics.com/no-tracking">We never track</a> your users, but by default we also skip requests with Do-Not-Track enabled. The stats will not include visitors when Do-Not-Track is enabled. Read more on [how to disable](/dnt) this behavior.
