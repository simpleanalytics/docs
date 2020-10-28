---
title: CSV export visits
category: api
permalink: /api/csv-export-visits
---

If you want to export raw visits without aggregations you can do so via our CSV export. You can define a date range and it pull out the data via streaming (very fast).

For this API features you'll need to authenticate. You can do this with an `Api-Key`-header where the key starts with `sa_api_key_...` and with a `User-Id` header starting with `sa_user_id_...`. You can create them in [your account settings](https://simpleanalytics.com/account).

To test if your API key works correctly you can replace the example values of this cURL example with your own:

```bash
curl "https://simpleanalytics.com/api/export/visits?version=1&hostname=example.com&start=2020-09-01&end=2020-09-02&timezone=Europe/Amsterdam" \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'Content-Type: text/csv'
```

The export will look like this:

```bash
added_unix,added_iso,url,referrer_raw,referrer,hostname,source,is_unique,utm_source,utm_medium,utm_campaign,utm_content,utm_term,scrolled_percentage,duration_seconds,device_width_pixels,device_width,viewport_width,viewport_height,screen_width,screen_height,uuid
1598927168,2020-09-01T02:26:08.000Z,https://blog.simpleanalytics.com/,simpleanalytics.com,simpleanalytics.com,blog.simpleanalytics.com,js,true,simpleanalytics.com,,,,,,,1461,1461,1461,849,1920,1080,f2dbec14-c8c1-4191-92da-d408fc7b7e1c
1598959428,2020-09-01T11:23:48.000Z,https://blog.simpleanalytics.com/practical-privacy-tips-for-your-business,hackernewsletter,,blog.simpleanalytics.com,js,true,hackernewsletter,email,,,fav,,,396,396,396,685,396,814,23f52505-9c1e-449e-bc84-97650f03c4df
1598968423,2020-09-01T13:53:43.000Z,https://blog.simpleanalytics.com/,simpleanalytics.com,simpleanalytics.com,blog.simpleanalytics.com,js,true,simpleanalytics.com,,,,,,,1366,1366,1366,616,1366,768,1b69a6fb-dbbf-4871-a4f6-6b81edf753cb
```

We included `added_unix` with a unix time stamp and `added_iso` with an ISO 8601 encoded date. `device_width_pixels` and `device_width` are deprecated and are now replaced by `viewport_width`. All sizes (`viewport_width`, `viewport_height`, `screen_width`, `screen_height`) are in pixels. Data like `scrolled_percentage` and `duration_seconds` is not always added because it depends on the browser features of the user.

If you have any problems, drop us a line via [our contact page](https://simpleanalytics.com/contact?ref={{ site.hostname }}).
