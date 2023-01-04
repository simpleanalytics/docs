---
title: What we do (and don't) collect
menu: What we do (and don't) collect
category: legal
permalink: /what-we-do-and-dont-collect
last_modified_at: 2023-01-04
---

Not collecting any information would be silly and unrealistic for an analytics tool. We collect information necessary to show you simple analytics, but unlike other analytics tools, we don’t collect more than is absolutely necessary. Here is a list of what we **do and don’t** collect from your visitors.

With every page view, we collect some metrics. We never track visitors, so the data below is never linked to one specific visitor.

You can limit the metrics we collect via our [ignore metrics](https://docs.simpleanalytics.com/ignore-metrics)\-feature.

## Metrics we collect

### URL of the page

Very important

For example, `https://simpleanalytics.com/contact`

We store this URL in parts in our database.

### Referrer

Very important

To know where customers come from, we store the page’s referrer. This means that a customer can see where a visitor is coming from—for example, `duckduckgo.com`.

### UTM codes

Somewhat important

For example, https://simpleanalytics.com/?utm\_source=newsletter

The part after the `?` is called [URL parameters](https://docs.simpleanalytics.com/how-to-use-url-parameters). We only keep the UTM codes (`utm_source`/`ref`, `utm_medium`, `utm_content`, `utm_campaign`) and drop all other URL parameters. The UTM codes are something that the customer adds to the URLs. By nature, these UTM codes don’t include personal data. They are generic terms like “newsletter\_may” or “twitter\_campaign\_2”. [See below](https://docs.simpleanalytics.com/metrics#utm-codes-explained).

### Time zone

In contrast with most services that collect countries based on IP address, we collect them based on the visitors' time zone. This way, we don’t have to touch their IP address and still can define their country. Every country has its own time zone, and modern devices automatically update the time zone when the device travels. The time zone is limited to a country, so we can’t get data about a city or region within a country. [Test this for yourself](https://simpleanalytics.com/timezone).

### IDs

We collect three IDs:

1. ID of the data point <span class="rating scaled"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> Somewhat important</span>
1. ID of the page <span class="rating scaled"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> Less important</span>
1. ID of the session <span class="rating scaled"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> Less important</span>

These IDs are not linked to a person or personal data. It’s linked to only a page view, page, or session. IDs are also not stored on the device. Meaning, that if a visitor reloads the page (with F5, for example), the IDs will all be reset.

### Scrolled percentage

Somewhat important

We collect scrolled percentage to know how far visitors scrolled (for example, 80%).

### User-agent

Somewhat important

To know which type of device the visitor used, we store the user agent. This is a metric that is the same for many visitors. It shows the browser used, the operating system, and the type of device.

### Device Dimensions

Less important:

We collect the device's screen dimensions. There are two dimensions: the viewport and the screen. The viewport is the part where the website runs in; the screen is the dimensions of the complete screen of the device.

### Language

Less important

The language of the browser, for example, `en-US`.


## What we don't collect

### Cookies

> We **do NOT set** any cookies (or use similar technologies)

<img loading="lazy" src="https://assets.simpleanalytics.com/images/drawings/cookie.png" style="float: right; margin-left: 1rem; transform: rotate(260deg); width: 150px;">

We care a great deal about the privacy of your visitors. Cookies are something that can track visitors across multiple pages or even multiple websites. For us this is a hard no. This goes for all similar technologies like (but not limited to) [local storage](https://en.wikipedia.org/wiki/Web_storage#Local_and_session_storage), [session cookies](https://en.wikipedia.org/wiki/HTTP_cookie#Session_cookie), [fingerprinting](<https://en.wikipedia.org/wiki/Fingerprint_(computing)>), and IP address hashing.

### IP addresses

> We \*\*do NOT collect or store\*\* IP addresses

We drop the IP address from every single request. Period. We don't save or collect them. We don't hash them with cryptography.

### Do Not Track

> By default we **do NOT collect or store** any data **if a visitor has Do Not Track** enabled

<img loading="lazy" src="https://assets.simpleanalytics.com/images/drawings/cctv.png" style="float: right; margin-left: 2rem; width: 150px;">

The <a href="https://en.wikipedia.org/wiki/Do_Not_Track">Do Not Track</a> browser setting asks a web application to disable either its own tracking or third-party tracking of an individual user. <a href="https://simpleanalytics.com/no-tracking">We never track</a> your users anyway, but by default we also ignore visits with Do Not Track enabled and do not add them to your dashboard. Read more on [how to disable](/dnt) this behavior.
