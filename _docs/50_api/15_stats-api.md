---
title: Stats API
category: api
permalink: /api/stats
redirect_from:
  - /api/json-api
version: 5
---

To get aggregated statistics out of our API we created a Stats API. Basically it's the data your see in our dashboard. This API is useful for when you want to integrate Simple Analytics into your own systems. For example when embedding your data into a customized dashboard within your own website.

> The data you get through this API is aggregated. If you are looking for raw data you can use our [Export page views API](/api/export-page-views).

For this API you need to be [autenticated with an API key](/api/authenticate). If your website is set to public you can get the JSON data without any credentials.

You can find the Stats API by adding `.json` to the URL of your dashboard in Simple Analytics. For example for our website it will be [`https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}&fields=histogram`](https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}&fields=histogram).

## Query parameters

We have a list of query parameters that you can use with this API:

- `version` the version of the API (the latest version is `{{ page.version }}`)
- `start` the start date with this format `YYYY-MM-DD` (defaults to 1 month ago)
- `end` the end data with above format (defaults to today)
- `limit` a limit for the fields (1-1000)
- `timezone` a valid time zone like `Europe/Amsterdam` (with capitals)
- `info` shows more information about fields in the response (defaults to true)
- `callback` wraps the response in a callback for [JSONP](https://en.wikipedia.org/wiki/JSONP)
- `fields` a comma seperated list of fields you want to get returned:
  - `pageviews` the total amount of page views in the specified period
  - `visitors` the total amount of visitors (unique page views) in the specified period
  - `histogram` an array with page views and visitors per day
  - `pages` a comma seperated list of pages you want to get stats for
  - `countries` a list of country codes
  - `referrers` a list of referrers (normalized)
  - `utm_sources` a list of UTM sources
  - `utm_mediums` a list of UTM mediums
  - `utm_campaigns` a list of UTM campaigns
  - `utm_contents` a list of UTM contents
  - `utm_terms` a list of UTM terms
  - `browser_names` a list of browser names
  - `os_names` a list of OS names
  - `device_types` a list of device types (mobile, tablet, desktop, tv)
  - `seconds_on_page` the median of seconds a visitor spent on the page ([see more](/explained/time-on-page))

For filtering you can use:

- `page` filter by a page
- `pages` filter by a comma separated list of pages (`/contact,/product/*`)
- `country` filter by a country code
- `referrer` filter by a referrer (normalized)
- `utm_source` filter by a UTM source
- `utm_medium` filter by a UTM medium
- `utm_campaign` filter by a UTM campaign
- `utm_content` filter by a UTM content
- `utm_term` filter by a UTM term
- `browser_name` filter by a browser name
- `os_name` filter by a OS name
- `device_type` filter by a device type (mobile, tablet, desktop, tv)

## Get data for specific pages

With the Stats API you can also retrieve data for a specific page of your website. You can specify this via the `pages` parameter: [`https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}&fields=histogram&pages=/contact`](https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}&fields=histogram&pages=/contact)).

You can also add the path to the URL and Simple Analytics returns the data for only that path. For example if you want to know how many visits you got on `simpleanalytics.com/contact`, you can get the JSON with this URL: [`https://simpleanalytics.com/simpleanalytics.com/contact.json?version={{ page.version }}&fields=histogram`](https://simpleanalytics.com/simpleanalytics.com/contact.json?version={{ page.version }}&fields=histogram)).

## Wildcards

The filtering parameters support wildcard searches. It's as easy as adding an `*` at the end of your parameter value. If you want to search for pages that have a path that starts with `/web` you can get it via [`https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}&fields=pages&pages=/web*`](https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}&fields=pages&pages=/web*)). If you want all pages that contains a word in their path you should use [`https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}&fields=pages&pages=*terms*`](https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}&fields=pages&pages=*terms*)).

## Time on page

To get the median of time on page you can use the field `seconds_on_page`. This field is a bit more special than the rest. It also includes the `seconds_on_page` within results you select with other fields. For example, [when you select](https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}&fields=pages,seconds_on_page&info=false&pages=/,/contact) some pages with it:

```
https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}&fields=pages,seconds_on_page&info=false&pages=/,/contact
```

It returns:

```js
{
  ...
  "seconds_on_page": 26,
  "pages": [
    {
      "value": "/",
      "pageviews": 100,
      "visitors": 50,
      "seconds_on_page": 25
    },
    {
      "value": "/contact",
      "pageviews": 60,
      "visitors": 30,
      "seconds_on_page": 20
    }
  ]
}
```

Note the `seconds_on_page` being part of the `pages` and part of the root of the JSON response.

## CORS and JSONP

By default we allow requests from any website. Some customers want to use JSONP for their requests. Learn more about how to use [JSONP with Simple Analytics](/api/cors-jsonp).
