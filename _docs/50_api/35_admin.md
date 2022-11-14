---
title: Admin API
category: api
permalink: /api/admin
last_modified_at: 2022-04-14
---

Use this if you want to administer your account. With this API you can do a few things, for example, list all websites and add websites to your dashboard.

## List websites

> `GET` [https://simpleanalytics.com/api/websites](https://simpleanalytics.com/api/websites)

The only Admin API endpoint that is available for all plans.

```bash
curl "https://simpleanalytics.com/api/websites" \
     -H 'Content-Type: application/json' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000'
```

Your user ID and API key are shown in [your account settings](https://simpleanalytics.com/account).

## Add a website

> `POST` [https://simpleanalytics.com/api/websites/add](https://simpleanalytics.com/api/websites/add)

<blockquote class="red">
  <p>For this endpoint you need a Business plan. You will be upgraded automatically when using this endpoint.</p>
</blockquote>

You can specify a time zone via `timezone` and set the website to public or private via the `public` boolean. [See wikipedia](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) for a list of valid time zones. If you don't specify a time zone we will set it to UTC.

```bash
curl -X "POST" "http://localhost:3000/api/websites/add" \
     -H 'Content-Type: application/json' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000' \
     -d $'{
  "public": false,
  "hostname": "example.com",
  "timezone": "Europe/Amsterdam"
}'
```

### Labels

If you want to keep track of your websites in a different way. A label could help. This is how that looks at the websites overview page:

<img loading="lazy" src="https://assets.simpleanalytics.com/docs/dashboard/labels-in-website-overview.png" alt="Simple Analytics websites overview with custom labels" class="border">

Add `"label": "customer note"` to your request body to set a label. Only strings are allowed.

## Custom endpoints

For bigger customers we make custom endpoints. If you are in the need of a custom endpoint, [let us know](https://simpleanalytics.com/contact).
