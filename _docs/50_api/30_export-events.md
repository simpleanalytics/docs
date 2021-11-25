---
title: Export events API
category: api
permalink: /api/export-events
redirect_from:
  - /api/csv-export-events
---

If you want to export raw events you can do so via our CSV export. You can define a date range and it pull out the data via streaming (very fast).

> Want to use a simple interface to export your data? [See our video on how to export data](/export-data).

For this API features you'll need to authenticate. You can do this with an `Api-Key`-header where the key starts with `sa_api_key_...` and with a `User-Id` header starting with `sa_user_id_...`. You can create them in [your account settings](https://simpleanalytics.com/account).

To test if your API key works correctly you can replace the example values of this cURL example with your own:

```bash
curl "https://simpleanalytics.com/api/export/events?hostname=example.com&start=2020-01-01&end=2020-01-02" \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'Content-Type: text/csv'
```

> Unlike the visits export you can't specify a time zone with the events export. Because of privacy reasons we store events with only a date (`YYYY-MM-DD`) in the UTC time zone. The time zone will always be UTC and can't be changed.

The export will look like this:

```bash
date,events,referrer
2020-06-05,visit_homepage.open_signup_modal,duckduckgo.com
2020-06-05,visit_homepage
2020-06-05,visit_homepage.open_signup_modal,twitter.com
```

> Do note that the events are exported per session. If two events happen in the same session (the same page or the session in a single page application) they are stored in one row. This way you can calculate conversions between events. We separate them with a dot (e.g.: `visit_homepage.open_signup_modal`).

For privacy reasons we hide events when they only happen once per day. To get all events in your export, [ask us](https://simpleanalytics.com/contact) to whitelist your events. We manually make sure personal identifiers in events are excluded.

If you have any problems, drop us a line via [our contact page](https://simpleanalytics.com/contact).
