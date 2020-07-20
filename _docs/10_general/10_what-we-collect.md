---
title: What we collect
category: general
permalink: /what-we-collect
---

Not collecting any information would be silly and unrealistic for an analytics tool. We do collect information that is necessary to show you _simple_ analytics, but unlike other analytics tools, we don't collect more than absolutely necessary. Here is a list of what we **do and don't** collect from your users.

### IP addresses

> We **do NOT collect or store** IP addresses

We drop the IP address from every single request. Period. We don't save or collect them. We don't hash them with cryptography.

<blockquote class="note">
  <p markdown="1">Update: Nov 21, 2019. Just to be completely transparent: we found IPs in our logs when requests on our server were failing. We fixed this by filtering all log messages and replacing IPs with zeros using [mmanon](https://www.rsyslog.com/doc/v8-stable/configuration/modules/mmanon.html). From now on, all IPs (like `1.1.1.1` or `2606:4700:4700::1111`) will become `0.0.0.0` or `0:0:0:0:0:0:0:0` before they enter our logs.</p>
</blockquote>

### Unique views

> We **do collect and store** whether visits are unique

Our unique detection of visits is quite unique itself. Most services use cookies or IP addresses to see if a visitor has visited the website in the past, except we don't use cookies or IP addresses at all. In the UK, for example, websites can't use IP addresses (even hashed) without an active opt-in from each user. This is why Simple Analytics is compatible with all existing privacy laws, including GDPR. You don't need an opt-in for our service.

We detect a unique visit based on the hostname of the _referrer_ of the page. When a user comes from one domain to another, their browser shares the previous domain with the next. If the current page's domain is the same as the one in the _referrer_, we know it's a non-unique visit.

[Read more](/uniques) on how we register unique page views.

### Timestamps

> We **do collect and store** timestamps

We use timestamps to generate the graphs you see on your dashboard, which allows you to analyze changes in your website's performance over various lengths of time.

### User agents

> We **do collect and store** user agents for a maximum of **90 days**

We detect and exclude bots and spiders based on the visitor's User Agent. We **don't** use User Agents for fingerprinting, only for counting **operating systems, device types, and browsers** in your dashboard. We don't believe this data is useful for any other function, but we keep it in our logs (not database) for a maximum of 90 days. When an incoming request fails for some reason, we store the request body in our logs, which includes a User Agent. After 90 days, these logs are deleted.

<blockquote class="note">
  <p>Update: Jan 14, 2019. Previously, we didn't store the User Agents, but now we save failed requests to our logs, so we added this as a clarification to the paragraph above.</p>
</blockquote>

### URLs

> We **partially collect** and **partially store** URLs

Too much information in the URL can be confusing and can make your stats messy. We only collect and store the first part of the URL. If an URL looks like this `https://example.com/index.html?search=keyword#top` we will only store `https://example.com/index.html`, also known as the protocol (`https`), hostname (`example.com`), and pathname (`/index.html`).

### Referrers

> We **do collect** and **partially store** referrers

Referrers answer the question _"Where did this visitor come from?"_. We have two ways of checking the source of a user visiting your website.

In most cases, browsers send the URL of the previous website as a referrer. We store the referrer the same as URLs (see above). You can find a list of the most popular referrers in your analytics dashboard.

Secondly we check the source of the customer with the UTM-parameters.

### UTM-parameters

> We **do collect** and **store** UTM-codes

We track these UTM codes:

- `utm_source` (e.g.: `duckduckgo.com`)
- `utm_medium` (e.g.: `search`)
- `utm_campaign` (e.g.: `get_customers_02`)
- `utm_content` (e.g.: `sidebar`)
- `utm_term` (e.g.: `privacy friendly analytics`)

Website owners can add a URL parameter to links to their website, like `ref=...`, `source=...` or `utm_source=...`. These are all saved as the `utm_source`. Read more on [using URL parameters](/how-to-use-url-parameters).

<blockquote class="note">
  <p>Added: July 20, 2020. We now store all UTM-parameters and not just the `utm_source`. UTM-parameters are not privacy invasive as they are being used for groups of visitors and not for individuals.</p>
</blockquote>

### Device dimensions

> We **do collect and store** device dimensions

Collecting the dimensions of a user's browser window (`innerWidth` and `innerHeigth` as viewport) and device dimensions (`screen.width` and `screen.height`) allows us to show you the most popular screen sizes. This is useful for making sure your website works great on all screens: phones, tablets, desktops, etc.

<blockquote class="note">
  <p>Updated: July 20, 2020. Previously, we didn't store the device dimensions, but we they are useful for certain and accessability design tools, so we added this as a clarification to the paragraph above.</p>
</blockquote>

### Do Not Track

> By default we **do NOT collect or store** any data **if a visitor has Do Not Track** enabled

The <a href="https://en.wikipedia.org/wiki/Do_Not_Track">Do Not Track</a> browser setting asks a web application to disable either its own tracking or third-party tracking of an individual user. <a href="https://simpleanalytics.com/no-tracking">We never track</a> your users anyway, but by default we also ignore visits with Do Not Track enabled and do not add them to your dashboard. Read more on [how to disable](/dnt) this behavior.
