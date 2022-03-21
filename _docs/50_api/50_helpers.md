---
title: API helpers
menu: Helpers
category: api
permalink: /api/helpers
version: 5
---

We added a few helpers to make it easier to work with our API.

## Time zones

In all requests you can specify your time zone. In the Stats API we default to your website setting, in the Export APIs we default to UTC. Speficy your time zone to always get the same results.

A list of valid time zones can be found at the Wikipedia page ["List of tz database time zones"](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List). For example, `Europe/Amsterdam` is a valid time zone. You should specify the time zone like this in your requests: `timezone=UTC`.

## Date placeholders

When working with time series data you need to specify a time period. You specify those in our APIs with `start`, and `end`, and `timezone` query parameters. Usually you would use a dates in the format of `YYYY-MM-DD`: `&start={{ "now" | date: '%s' | minus: 2592000 | date: '%Y-%m-%d' }}&end={{ "now" | date: '%Y-%m-%d' }}&timezone=UTC`.

To specify the date as today, use `today`. You can also use `yesterday` or `today-1d` to specify yesterday. To get the data from the last 30 days, use `&start=today-30d&end=yesterday` in your API requests. To get data for only today, use `&start=today&end=today`.

```
https://simpleanalytics.com/simpleanalytics.com.json?version={{ page.version }}&fields=histogram&start=yesterday&end=today&timezone=UTC
```

## Generate export URL

We created a simple interface where you can generate the export URL for events (and page views).

{%
  include video.html
  slug="get-event-api-url"
  formats="mp4,ogg,webm,wmv,mov"
  poster="video.png"
%}

If you need any help(er), [just shoot us a message](https://simpleanalytics.com/contact).
