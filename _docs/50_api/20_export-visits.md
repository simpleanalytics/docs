---
title: CSV export visits
category: api
permalink: /api/csv-export-visits
---

Simple Analytics does not own your data. That's why we care a lot about the interoperability of your data. This API is a good example of that. Most analytics companies do not give you access to their raw data. We believe it should be easy for our customers to get their raw data our of our database. What you do with that data is totally up to you.

With this API you can export raw visits (without sampling). Define a date range and it pull out the data via streaming. For us it does not matter how much data you export. We stream the data directly out of our database to your server or computer. No heavy load required. To make the export size smaller you can select the fields you want. The response will only include the fields you selected in the order you provided.

<details markdown="1">
<summary>Available fields in export</summary>

| Field               | Type    | Description |
|---------------------|---------|--------------------------------------|
| added_unix          | number  | The time of the page view in unix time format |
| added_iso           | date    | The time of the page view in ISO8601 format   |
| hostname            | string  | The hostname of the website |
| hostname_original   | string  | When the hostname is overwritten, we store the original hostname |
| path                | string  | The path of the page view |
| is_unique           | boolean  | Is this page view unique |
| is_robot            | boolean | Is page view visits by a robot or crawler |
| document_referrer   | string  | The [JavaScript `document.referrer`](https://developer.mozilla.org/en-US/docs/Web/API/Document/referrer) of the page |
| utm_source          | string  | UTM source |
| utm_medium          | string  | UTM medium |
| utm_campaign        | string  | UTM campaign |
| utm_content         | string  | UTM content |
| utm_term            | string  | UTM term |
| scrolled_percentage | number  | How far did a visitor scroll on the page (in steps of 5%) |
| duration_seconds    | number  | How many seconds did a visitor stay on this page (we stop the counter when a page is hidden) |
| viewport_width      | number  | Viewport width in pixels|
| viewport_height     | number  | Viewport height in pixels |
| screen_width        | number  | Screen width in pixels |
| screen_height       | number  | Screen height in pixels |
| user_agent          | string  | The [`navigator.userAgent`](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorID/userAgent) of a browser (in case of a fake one we don't store it. |
| device_type         | string  | Either desktop, mobile, tablet, or tv. |
| country_code        | string  | 2 letter country code |
| browser_name        | string  | Browser name |
| browser_version     | string  | Browser version (do note this is a string) |
| os_name             | string  | OS name |
| os_version          | string  | OS version (do note this is a string) |
| lang_region         | string  | The region part of [navigator.language](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorLanguage/language) |
| lang_language       | string  | The language part of [navigator.language](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorLanguage/language) |
| uuid                | string  | A UUID v4 of the page view (this is not always unique) |

Data like `scrolled_percentage` and `duration_seconds` is not always added because it depends on the browser features of the visitor.

</details>

<details markdown="1">
<summary>Deprecated fields</summary>

These fields are deprecated but we keep them for backward compatibility. It's recommended to not use it for new projects.

| Field               | Description                                      |
|---------------------|--------------------------------------------------|
| url                 | Please use hostname and path to get the full URL |
| referrer            | We replaced this with document_referrer          |
| referrer_raw        | We replaced this with document_referrer          |
| device_width_pixels | We replaced this with viewport_width             |
| device_width        | We replaced this with viewport_width             |
| source              | What is the source of this page view, mostly `js` from our JavaScript |

</details>

## API

For this API features you'll need to authenticate. You can do this with an `Api-Key`-header where the key starts with `sa_api_key_...` and with a `User-Id` header starting with `sa_user_id_...`. You can create them in [your account settings](https://simpleanalytics.com/account).

You can specify all fields you like to export. Add them as a comma seperated list (e.g.: `&fields=added_iso,hostname,path`).

To test if your API key works correctly you can replace the example values of this cURL example with your own:

```bash
curl "https://simpleanalytics.com/api/export/visits?version=2&fields=added_iso,hostname,path&hostname=example.com&start=2020-12-01&end=2021-01-01" \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'Content-Type: text/csv'
```

<details markdown="1">
<summary>Deprecated API</summary>
     
If you don't specify any `fields` we return all the basic fields.

```bash
curl "https://simpleanalytics.com/api/export/visits?version=1&hostname=example.com&start=2020-12-01&end=2021-01-01&timezone=Europe/Amsterdam" \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'Content-Type: text/csv'
```

This is how the API worked before and we don't want to add breaking changes to our APIs. A response when you don't specify any `fields` looks like this:
     
```bash
added_unix,added_iso,url,referrer_raw,referrer,hostname,source,is_unique,utm_source,utm_medium,utm_campaign,utm_content,utm_term,scrolled_percentage,duration_seconds,device_width_pixels,device_width,viewport_width,viewport_height,screen_width,screen_height,uuid
1598927168,2020-09-01T02:26:08.000Z,https://blog.simpleanalytics.com/,simpleanalytics.com,simpleanalytics.com,blog.simpleanalytics.com,js,true,simpleanalytics.com,,,,,,,1461,1461,1461,849,1920,1080,f2dbec14-c8c1-4191-92da-d408fc7b7e1c
1598959428,2020-09-01T11:23:48.000Z,https://blog.simpleanalytics.com/practical-privacy-tips-for-your-business,hackernewsletter,,blog.simpleanalytics.com,js,true,hackernewsletter,email,,,fav,,,396,396,396,685,396,814,23f52505-9c1e-449e-bc84-97650f03c4df
1598968423,2020-09-01T13:53:43.000Z,https://blog.simpleanalytics.com/,simpleanalytics.com,simpleanalytics.com,blog.simpleanalytics.com,js,true,simpleanalytics.com,,,,,,,1366,1366,1366,616,1366,768,1b69a6fb-dbbf-4871-a4f6-6b81edf753cb
```

This functionality is deprecated but we keep it for backward compatibility. It's recommended to not use it for new projects.
     
</details>

If you have any problems, drop us a line via [our contact page](https://simpleanalytics.com/contact?ref={{ site.hostname }}).

<style>
     /* Apply styling to first table */
     .content div.table-wrapper:nth-of-type(1) td:nth-of-type(1),
     .content div.table-wrapper:nth-of-type(1) td:nth-of-type(2) {
         white-space: nowrap;
     }

     /* Apply styling to second table */
     .content div.table-wrapper:nth-of-type(2) td:nth-of-type(1) {
         white-space: nowrap;
     }
</style>
