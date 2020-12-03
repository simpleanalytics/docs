---
title: Stats API
category: api
permalink: /api/stats
redirect_from:
  - /api/json-api
version: 4
---

To get aggregated statistics out of our API we created a JSON API. Basically it's the data your see in our dashboard. This API is useful for when you want to integrate Simple Analytics into your own systems. For example when embedding your data into a customized dashboard within your own website.

> The data you get through this API is aggregated. If you are looking for raw data you can use our [Export page views API](/api/export-page-views).

For this API you need to be [autenticated with an API key](/api/authenticate). If your website is set to public you can get the JSON data without any credentials.

You can find the JSON API by adding `.json` to the URL of your dashboard in Simple Analytics. For example for our website it will be [`https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}`](https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}).

## Query parameters

We have a list of query parameters that you can use with this API:

- `version` the version of the API (the latest version is `{{ page.version }}`)
- `start` the start date with this format `YYYY-MM-DD` (defaults to 1 month ago)
- `end` the end data with above format (defaults to today)
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
- `limit` a limit for the fields (1-1000)
- `timezone` a valid time zone like `Europe/Amsterdam` (with capitals)
- `info` shows more information about fields in the response (defaults to true)
- `callback` wraps the response in a callback for [JSONP](https://en.wikipedia.org/wiki/JSONP)

## Get data for specific pages

With the Stats API you can also retrieve data for a specific page of your website. You can specify this via the `pages` parameter: [`https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}&fields=histogram&pages=/contact`](https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}&fields=histogram&pages=/contact)).

You can also add the path to the URL and Simple Analytics returns the data for only that path. For example if you want to know how many visits you got on `simpleanalytics.com/contact`, you can get the JSON with this URL: [`https://simpleanalytics.com/simpleanalytics.com/contact.json?version={{ page.version }}&fields=histogram`](https://simpleanalytics.com/simpleanalytics.com/contact.json?version={{ page.version }}&fields=histogram)).

## CORS and JSONP

By default we allow requests from any website. Some customers want to use JSONP for their requests. Learn more about how to use [JSONP with Simple Analytics](/api/cors-jsonp).
