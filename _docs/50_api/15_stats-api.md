---
title: Stats API
category: api
permalink: /api/stats
redirect_from:
  - /api/json-api
last_modified_at: 2026-08-11
---

To get the aggregated statistics you see in our dashboard, use this Stats API. This API helps integrate Simple Analytics into your systems. For example, you can get KPIs out of your data or embed your data into a customized dashboard.

> If you are looking for raw data, you can use our [Export API](/api/export-data-points).

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
- `end` the end date with the above format (defaults to today)
- `limit` a limit for the fields (1-1000)
- `timezone` a valid time zone like `Europe/Amsterdam` (with capitals)
- `info` shows more information about fields in the response (defaults to true)
- `callback` wraps the response in a callback for [JSONP](https://en.wikipedia.org/wiki/JSONP)
- [`events` a list of specified events and how much they occurred](#events)
- `metadata.<key>` filters by an exact metadata value (version 6 and later)
- `interval` for histogram field: `hour`, `day`, `week`, `month`, or `year` (`hour` added in version 6)
- `fields` a comma separated list of fields you want to get returned:
  - `pageviews` the total amount of page views in the specified period
  - `visitors` the total amount of visitors (unique page views) in the specified period
  - `histogram` an array with page views and visitors per day
  - `pages` a comma separated list of pages you want to get stats for
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
- `os_name` filter by an OS name
- `device_type` filter by a device type (mobile, tablet, desktop, tv)
- `metadata.<key>` filter by an exact metadata value (version 6 and later)

These filters also apply to results selected with the `events` query parameter.

</div>
</details>

### Filter by metadata

Starting with version 6, you can filter Stats API results by [metadata](/metadata) with a `metadata.<key>` query parameter. The key can contain only letters, numbers, and underscores (`[a-zA-Z0-9_]+`). Use the normalized metadata key without its storage type suffix, such as `_text`, `_int`, `_bool`, or `_date`.

For example, this request only returns page views where the `app_id` metadata value is `nl-123`:

```
https://simpleanalytics.com/example.com.json?version=6&fields=histogram&metadata.app_id=nl-123
```

The Stats API automatically checks the stored metadata type. Numeric values match both number and text metadata, while boolean and date values also fall back to their exact text value. Matches are exact and wildcards are not supported. When you specify multiple metadata filters, all of them must match (AND).

## Get data for specific pages

With the Stats API, you can also retrieve data for a specific page of your website. You can specify this via the `pages` parameter: [`https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=histogram&pages=/contact`](https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=histogram&pages=/contact)).

You can also add the path to the URL, and Simple Analytics returns the data for only that path. For example, if you want to know how many visits you got on `simpleanalytics.com/contact`, you can get the JSON with this URL: [`https://simpleanalytics.com/simpleanalytics.com/contact.json?version={{ site.api_version }}&fields=histogram`](https://simpleanalytics.com/simpleanalytics.com/contact.json?version={{ site.api_version }}&fields=histogram)).

## Wildcards

The filtering parameters support trailing wildcards. Add an `*` to the end of a value to match everything that starts with it. For example, use [`pages=/web*`](https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&fields=pages&pages=/web*) to return pages whose paths start with `/web`.

Page filters also support a single leading-and-trailing wildcard pattern to match paths that contain a specific value. These searches are more resource intensive and therefore have the following requirements:

- Authenticate the request with an API key, including for public websites.
- Specify exactly one path pattern with `page` or `pages`.
- Start and end the pattern with `*`, with no additional wildcards in between.
- Include at least 12 non-slash characters between the wildcards.
- Only request the `pageviews`, `visitors`, and/or `histogram` fields.
- Do not request events.

For example, this request matches paths containing `/app/example-name/`:

```sh
curl "https://simpleanalytics.com/example.com.json?version={{ site.api_version }}&fields=pageviews,visitors,histogram&pages=*/app/example-name/*" \
  -H "Api-Key: sa_api_key_..."
```

Contains searches are rate limited. If a request returns HTTP `429`, wait for the number of seconds in the `Retry-After` response header before retrying.

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
