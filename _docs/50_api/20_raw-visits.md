---
title: CSV export
category: api
permalink: /api/csv-export
---

If you want to export raw visits without aggregations you can do so via our CSV export. You can define a date range and it pull out the data via streaming (very fast).

For this API features you'll need to authenticate. You can do this with an `Api-Key`-header where the key starts with `sa_api_key_...` and with a `User-Id` header starting with `sa_user_id_...`. You can create them in [your account settings](https://simpleanalytics.com/account).

To test if your API key works correctly you can replace the example values of this cURL example with your own:

```bash
curl "https://simpleanalytics.com/api/export/visits?hostname=example.com&start=2020-01-01&end=2020-01-02&timezone=Europe/Amsterdam" \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'Content-Type: text/csv'
```

The export will look like this:

```bash
added_unix,added_iso,url,referrer_raw,referrer,hostname,source,is_unique,scrolled_percentage,duration_seconds,device_width_pixels,device_width
1577867423,2020-01-01T08:30:23.343Z,https://simpleanalytics.com/example.com,https://simpleanalytics.com/example.com?start=2019-12-30&amp;end=2019-12-30,simpleanalytics.com,simpleanalytics.com,js,false,,,375,375
1577887745,2020-01-01T14:09:05.066Z,https://simpleanalytics.com/,twitter-bio,twitter,simpleanalytics.com,js,true,,,375,375
1577887760,2020-01-01T14:09:20.156Z,https://simpleanalytics.com/,https://simpleanalytics.com/?ref=twitter-bio,simpleanalytics.com,simpleanalytics.com,js,false,,,375,375
```

We included `added_unix` with a unix time stamp and `added_iso` with an ISO 8601 encoded date. `device_width` is deprecated and is now replaced by `device_width_pixels`. Data like `scrolled_percentage` and `duration_seconds` is not always added because it depends on the browser features of the user.

If you have any problems, drop us a line via [our contact page](https://simpleanalytics.com/contact?ref={{ site.hostname }}).
