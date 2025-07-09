---
title: Export API
category: api
permalink: /api/export-data-points
redirect_from:
  - /api/csv-export-visits
  - /api/export-pageviews
  - /api/export-page-views
  - /api/export-events
last_modified_at: 2025-07-04
fields: added_iso,country_code,datapoint,device_type,path,query,query_and_path,session_id,utm_source,utm_campaign,utm_content,utm_medium
---

With this API you can export raw data points (without sampling). Data points are both page views and events combined. Define a date range and it pulls out the data. The response will only include the selected fields.

> Want to use a simple interface to export your data? [See our video on exporting data](/export-data).

When using the API, it's recommended [to generate the export URL](/api/helpers#generate-export-url) via [the export your data interface](/export-data). It has a simple UI where fields can be selected without any coding or technical knowledge.

<details>
<summary>Available fields in export</summary>
<div markdown="1">

| Field               | Type    | Description                                                                                                                                                |
| ------------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| added_unix          | number  | The time of the page view in unix time format                                                                                                              |
| added_iso           | date    | The time of the page view in ISO8601 format                                                                                                                |
| hostname            | string  | The hostname of the website                                                                                                                                |
| hostname_original   | string  | When the hostname is overwritten, we store the original hostname                                                                                           |
| path                | string  | The path of the page view                                                                                                                                  |
| query               | string  | The query parameters of the URL                                                                                                                            |
| is_unique           | boolean | Is this page view unique                                                                                                                                   |
| is_robot            | boolean | Is page view visited by a robot or crawler                                                                                                                 |
| document_referrer   | string  | The [JavaScript `document.referrer`](https://developer.mozilla.org/en-US/docs/Web/API/Document/referrer) of the page                                       |
| utm_source          | string  | UTM source (specify via `ref=` or `utm_source` in your URL)                                                                                                |
| utm_medium          | string  | UTM medium (specify via `utm_medium` in your URL)                                                                                                          |
| utm_campaign        | string  | UTM campaign (specify via `utm_campaign` in your URL)                                                                                                      |
| utm_content         | string  | UTM content (specify via `utm_content` in your URL)                                                                                                        |
| utm_term            | string  | UTM term (specify via `utm_term` in your URL)                                                                                                              |
| scrolled_percentage | number  | How far did a visitor scroll on the page (in steps of 5%)                                                                                                  |
| duration_seconds    | number  | How many seconds did a visitor stay on this page (we stop the counter when a page is hidden)                                                               |
| viewport_width      | number  | Viewport width in pixels                                                                                                                                   |
| viewport_height     | number  | Viewport height in pixels                                                                                                                                  |
| screen_width        | number  | Screen width in pixels                                                                                                                                     |
| screen_height       | number  | Screen height in pixels                                                                                                                                    |
| user_agent          | string  | The [`navigator.userAgent`](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorID/userAgent) of a browser (in case of a fake one we don't store it. |
| device_type         | string  | Either desktop, mobile, tablet, or tv.                                                                                                                     |
| country_code        | string  | 2 letter country code                                                                                                                                      |
| browser_name        | string  | Browser name                                                                                                                                               |
| browser_version     | string  | Browser version (do note this is a string)                                                                                                                 |
| os_name             | string  | OS name                                                                                                                                                    |
| os_version          | string  | OS version (do note this is a string)                                                                                                                      |
| lang_region         | string  | The region part of [navigator.language](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorLanguage/language)                                       |
| lang_language       | string  | The language part of [navigator.language](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorLanguage/language)                                     |
| uuid                | string  | A UUID v4 of the page view (this is not always unique)                                                                                                     |
| metadata.\*\*\*     | N/A     | Metadata are your own specified fields followed by a type (e.g. `project_text`)                                                                            |

Data like `scrolled_percentage` and `duration_seconds` is not always added because it depends on the browser features of the visitor. [Metadata](/metadata) is found in `metadata.***` fields. They will only be exported when specified by key (e.g.: `metadata.dark_mode_bool`).

</div>
</details>

<details>
<summary>Deprecated fields</summary>
<div markdown="1">

These fields are deprecated but we keep them for backward compatibility. It's recommended to not use it for new projects.

| Field               | Description                                                           |
| ------------------- | --------------------------------------------------------------------- |
| url                 | Please use hostname and path to get the full URL                      |
| referrer            | We replaced this with document_referrer                               |
| referrer_raw        | We replaced this with document_referrer                               |
| device_width_pixels | We replaced this with viewport_width                                  |
| device_width        | We replaced this with viewport_width                                  |
| source              | What is the source of this page view, mostly `js` from our JavaScript |

</div>
</details>

## Authenticate

For this API features you'll need to authenticate. See the [authenticate page](/api/authenticate) on how to authenticate.

In short: apply an `Api-Key`-header where the key starts with `sa_api_key_...` and a `User-Id` header starting with `sa_user_id_...`.

## Selecting fields

You can specify all fields you like to export. Add them as a comma seperated list (e.g.: `&fields=added_iso,hostname,path`).

<details>
<summary>Request example (for developers)</summary>
<div markdown="1">

To test if your API key works correctly you can replace the example values of this cURL example with your own.

```bash
# Export daily data
curl "https://simpleanalytics.com/api/export/datapoints?version={{ site.api_version }}&format=csv&hostname=simpleanalytics.com&start={{ "now" | date: '%s' | minus: 2592000 | date: '%Y-%m-%d' }}&end={{ "now" | date: '%Y-%m-%d' }}&robots=false&timezone=Europe%2FAmsterdam&fields=added_iso,path&type=pageviews" \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'Content-Type: text/csv'

# Export hourly data (for 3PM today in Amsterdam)
curl "https://simpleanalytics.com/api/export/datapoints?version={{ site.api_version }}&format=csv&hostname=simpleanalytics.com&start={{ "now" | date: '%Y-%m-%d' }}T15&end={{ "now" | date: '%Y-%m-%d' }}T15&robots=false&timezone=Europe%2FAmsterdam&fields=added_iso,path&type=pageviews" \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'Content-Type: text/csv'
```

</div>
</details>

If you choose to export in the CSV format, it will export something like this:

| added_iso | country_code | datapoint    | device_type                       | path | session_id     | utm_campaign | utm_content | utm_medium                           | utm_source |
| --------- | ------------ | ------------ | --------------------------------- | ---- | -------------- | ------------ | ----------- | ------------------------------------ | ---------- | --- | ---------- | ---------- |
| {{ "now"  | date: '%s'   | minus: 83325 | date: '%Y-%m-%dT%H:%M:%S.100Z' }} | US   | visit_homepage | desktop      | /           | 1e5aad53-c734-40ac-b060-426a70d1c104 | ads1       |     |            | duckduckgo |
| {{ "now"  | date: '%s'   | minus: 2580  | date: '%Y-%m-%dT%H:%M:%S.100Z' }} | UK   | visit_homepage | desktop      | /           | 7b03aa29-612d-4aa8-b147-72c13986c4ae |            |     | newsletter |            |
| {{ "now"  | date: '%s'   | minus: 2340  | date: '%Y-%m-%dT%H:%M:%S.200Z' }} | UK   | popup_show     | desktop      | /           | 7b03aa29-612d-4aa8-b147-72c13986c4ae |            |     |            |            |
| {{ "now"  | date: '%s'   | minus: 55    | date: '%Y-%m-%dT%H:%M:%S.100Z' }} | NL   | visit_homepage | desktop      | /           | 928e4f2f-1f16-4900-9ad8-0a1965e689a3 |            |     |            | google     |
| {{ "now"  | date: '%s'   | minus: 35    | date: '%Y-%m-%dT%H:%M:%S.200Z' }} | NL   | popup_show     | desktop      | /           | 928e4f2f-1f16-4900-9ad8-0a1965e689a3 |            |     |            |            |
| {{ "now"  | date: '%s'   | minus: 5     | date: '%Y-%m-%dT%H:%M:%S.300Z' }} | NL   | popup_close    | desktop      | /           | 928e4f2f-1f16-4900-9ad8-0a1965e689a3 |            |     |            |            |

<details class="csv">
<summary>The above export in CSV format</summary>
<div markdown="1">

```
added_iso,country_code,datapoint,device_type,path,session_id,utm_campaign,utm_content,utm_medium,utm_source
{{ "now" | date: '%s' | minus: 83325 | date: '%Y-%m-%dT%H:%M:%S.100Z' }},US,visit_homepage,desktop,/,1e5aad53-c734-40ac-b060-426a70d1c104,ads1,,,duckduckgo
{{ "now" | date: '%s' | minus: 2580 | date: '%Y-%m-%dT%H:%M:%S.100Z' }},UK,visit_homepage,desktop,/,7b03aa29-612d-4aa8-b147-72c13986c4ae,,,newsletter,
{{ "now" | date: '%s' | minus: 2340 | date: '%Y-%m-%dT%H:%M:%S.200Z' }},UK,popup_show,desktop,/,7b03aa29-612d-4aa8-b147-72c13986c4ae,,,,
{{ "now" | date: '%s' | minus: 55 | date: '%Y-%m-%dT%H:%M:%S.100Z' }},NL,visit_homepage,desktop,/,928e4f2f-1f16-4900-9ad8-0a1965e689a3,,,,google
{{ "now" | date: '%s' | minus: 35 | date: '%Y-%m-%dT%H:%M:%S.200Z' }},NL,popup_show,desktop,/,928e4f2f-1f16-4900-9ad8-0a1965e689a3,,,,
{{ "now" | date: '%s' | minus: 5 | date: '%Y-%m-%dT%H:%M:%S.300Z' }},NL,popup_close,desktop,/,928e4f2f-1f16-4900-9ad8-0a1965e689a3,,,,
```

</div>
</details>

### Metadata fields

Because metadata fields are defined by the user, we don't know the fields upfront. The [export UI](/api/helpers#generate-export-url) gives a good overview of all metadata fields available for a certain period. Use those fields in the export API.

Fields in the API and exporter have a type appended to them. You can see fields like `metadata.fieldname_text`, `metadata.fieldname_date`, `metadata.fieldname_bool`, or `metadata.fieldname_int` (where fieldname is a user-defined name). Some metadata fields can have both, for example, `metadata.projectID_text` and `metadata.projectID_int`. If a text looks like a number, we convert it to an integer and we keep the text version.

When you see something prefixed with `metadata.sa_urlparam_`, it's a paramter from the [allowed URL parameters feature](/allow-params).

## Event counts

If you are only interested in how many certain events happened, you can use our [Stats API](/api/stats#events). It has a simple request and response with event totals.

```
https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&start=yesterday&end=today&timezone=Europe/Amsterdam&events=visit_pricing
```

[See live example](https://simpleanalytics.com/simpleanalytics.com.json?version={{ site.api_version }}&start=yesterday&end=today&timezone=Europe/Amsterdam&events=visit_pricing) of output.

## Hourly data export

You can now export data for specific hours of a day. This allows for more granular data analysis when you need to understand traffic patterns within a single day.

To export hourly data, append the hour to your date in the format `YYYY-MM-DDTHH` where `HH` is the hour in 24-hour format (00-23).

**Important constraints for hourly exports:**

- Both `start` and `end` parameters must include the hour
- The start and end dates must be the same (you can only export hourly data for a single day at a time)
- Hours must be between 00 and 23
- The hours are in the timezone you specify in the `timezone` parameter

**Example:**

```bash
# Export data for 2PM on July 4th, 2025
curl "https://simpleanalytics.com/api/export/datapoints?version={{ site.api_version }}&format=csv&hostname=example.com&start=2025-07-04T14&end=2025-07-04T14&fields=added_iso,path" \
     -H 'User-Id: sa_user_id_...' \
     -H 'Api-Key: sa_api_key_...'
```

## Performance

For us it does not matter how much data you export. We stream the data directly out of our database to your server or computer. No heavy load required.

To make the export size smaller only select the fields you need.

If you have any problems, drop us a line via [our contact page](https://simpleanalytics.com/contact).

<style>
  .content div.table-wrapper td {
    white-space: nowrap;
    font-feature-settings: "tnum";
    font-variant-numeric: tabular-nums;
  }

  /* Apply styling to first table */
  .content details div.table-wrapper:nth-of-type(1) td:nth-of-type(3) {
    white-space: inherit;
  }

  .content table td,
  .content table th {
    font-size: 14px;
  }

  details.csv pre.highlight {
    white-space: pre;
  }
</style>
