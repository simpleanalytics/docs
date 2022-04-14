---
title: Stats API
category: api
permalink: /api/stats
redirect_from:
  - /api/json-api
last_modified_at: 2022-04-14
---

To get the aggregated statistics you see in our dashboard, use this Stats API. This API helps integrate Simple Analytics into your systems. For example, you can get KPIs out of your data or embed your data into a customized dashboard.

> If you are looking for raw data, you can use our export [page views](/api/export-page-views) or [events](/api/export-events) API.

For this API, you need to be [authenticated with an API key](/api/authenticate). If your website is public, you can get the JSON data without credentials.

You can find the Stats API by adding `.json` to the URL of your dashboard in Simple Analytics. For example, for our website, it is:

```
https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=histogram&start=yesterday&end=today
```

[See the live response](https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=histogram&start=yesterday&end=today) to the above request.

## Query parameters

We have a list of query parameters that you can use with this API.

<details>
<summary>All query parameters</summary>
<div markdown="1">

The complete list of all query params you can use with the latest Stats API.

- `version` the version of the API (the latest version is `{{ site.api_version }}`)
- `start` the start date with this format `YYYY-MM-DD` (defaults to 1 month ago)
- `end` the end data with above format (defaults to today)
- `limit` a limit for the fields (1-1000)
- `timezone` a valid time zone like `Europe/Amsterdam` (with capitals)
- `info` shows more information about fields in the response (defaults to true)
- `callback` wraps the response in a callback for [JSONP](https://en.wikipedia.org/wiki/JSONP)
- [`events` a list of specified events and how much they occurred](#events)
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
  - `seconds_on_page` the median of seconds a visitor spent on the page ([see more](#time-on-page))

</div>
</details>

<details>
<summary>All filters</summary>
<div markdown="1">

You can filter the returned data. Here is the list of filters you can use.

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

These filters don't have effect on the `events` query parameter.

</div>
</details>

## Get data for specific pages

With the Stats API, you can also retrieve data for a specific page of your website. You can specify this via the `pages` parameter: [`https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=histogram&pages=/contact`](https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=histogram&pages=/contact)).

You can also add the path to the URL, and Simple Analytics returns the data for only that path. For example, if you want to know how many visits you got on `simpleanalytics.com/contact`, you can get the JSON with this URL: [`https://simpleanalytics.com/simpleanalytics.com/contact.json?version={{ site.api_version }}&fields=histogram`](https://simpleanalytics.com/simpleanalytics.com/contact.json?version={{ site.api_version }}&fields=histogram)).

## Wildcards

The filtering parameters support wildcard searches. It's as easy as adding an `*` at the end of your parameter value. If you want to search for pages with a path that starts with `/web`, you can get it via [`https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=pages&pages=/web*`](https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=pages&pages=/web*)). If you wish to get all pages that contain a word in its path, you should use [`https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=pages&pages=*terms*`](https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=pages&pages=*terms\*)).

## Time on page

To get the median of time on page you can use the field `seconds_on_page`. This field is a bit more special than the rest. It also includes the `seconds_on_page` within the results you select with other fields. For example, [when you choose](https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=pages,seconds_on_page&info=false&pages=/,/contact) some pages with the request:

```
https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=pages,seconds_on_page&pages=/,/contact
```

it embeds the time on page in those pages:

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

Note the `seconds_on_page` being part of the `pages` ánd part of the root of the JSON response. We have [an explainer on time on page](/explained/time-on-page), which goes into more detail about the metric and why we did choose to make it a median instead of average.

## Date placeholders

See [helpers](/api/helpers#date-placeholders) to learn how to use `&start=today-30d&end=yesterday`.

## Events

Get event counts by adding the `events=...`-param to your request. To get the counts of the events (`visit_homepage`, `popup_replace_show`, `popup_replace_close`), you can run this request:

```
https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&start=yesterday&end=today&timezone=Europe/Amsterdam&events=visit_homepage,popup_replace_show,popup_replace_close
```

```json
{
  "events": [
    {
      "name": "visit_homepage",
      "total": 233
    },
    {
      "name": "popup_replace_show",
      "total": 117
    },
    {
      "name": "popup_replace_close",
      "total": 61
    }
  ]
}
```

If you use `events=*`, all events are returned (limited to 1000 events).

## CORS and JSONP

By default, we allow requests from any website. Some customers want to use JSONP for their requests. Learn more about how to use [JSONP with Simple Analytics](/api/cors-jsonp).
