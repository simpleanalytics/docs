---
title: API Introduction
menu: Introduction
category: api
permalink: /api
---

There are a few ways to interact with our API. We have the stats API for basic stats and the business API for changing users, websites and other settings.

## Stats API

Use this if you want to retrieve aggregated stats from your website. Basically the stats you see in your dashboard (for now we show page views, but referrals and others will be added later).

While some websites are set to public, others are set to private. You can manually adjust this in your website settings. If your website is set to public you can get the JSON data without any credentials.

You can set the JSON format by adding `.json` to the URL of Simple Analytics. For example for our website it will be [`https://simpleanalytics.com/simpleanalytics.com.json`](https://simpleanalytics.com/simpleanalytics.com.json). Alternatively, you can add _start_ and _end_ dates to the URL as well, for example: [`https://simpleanalytics.com/simpleanalytics.com.json?start=2019-01-01&end=2019-01-31`](https://simpleanalytics.com/simpleanalytics.com.json?start=2019-01-01&end=2019-01-31).

If you have your website set to private you can still export this data. You need to authenticate yourself. [See here how to authenticate](/api/authenticate).

### Get data for specific pages

With the stats API you can also retrieve data for a specific page of your website. By adding the path to the URL Simple Analytics returns the data for that path. For example if you want to know how many visits you got on `simpleanalytics.com/contact`, you can get the JSON with this URL: [`https://simpleanalytics.com/simpleanalytics.com/contact.json`](https://simpleanalytics.com/simpleanalytics.com/contact.json))

## Business API

Use this if you want to administer your account.

With this API you can do a few things, for example add websites to your dashboard. This API is only available on request because we want to know what the use case for the API will be. Just drop us a line via [our contact page](https://simpleanalytics.com/contact?ref={{ site.hostname }}).

### List websites

> `GET` [https://simpleanalytics.com/api/websites](https://simpleanalytics.com/api/websites)

The only Business API endpoint that is available for all plans.

```bash
curl "https://simpleanalytics.com/api/websites" \
     -H 'Content-Type: application/json' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000'
```

Your user ID and API key are shown in [your account settings](https://simpleanalytics.com/account).

### Add a website

> `POST` [https://simpleanalytics.com/api/websites/add](https://simpleanalytics.com/api/websites/add)

For this endpoint you will need a Business plan. You can specify a time zone via `timezone` and set the website to public or private via the `public` boolean. [See wikipedia](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) for a list of valid time zones. If you don't specify a time zone we will set it to UTC.

```bash
curl -X "POST" "http://localhost:3000/api/websites/add" \
     -H 'Content-Type: application/json' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000' \
     -d $'{
  "public": true,
  "hostname": "example.com",
  "timezone": "Europe/Amsterdam"
}'
```

### Custom endpoints

For bigger customers we make custom endpoints. If you are in the need of a custom endpoint, [let us know](https://simpleanalytics.com/contact?ref={{ site.hostname }}).
