---
title: Import Google Analytics data
category: features
permalink: /import-google-analytics-data
last_modified_at: 2022-07-08
---

With Simple Analytics you can import Google Analytics 4 properties.

> We filter the imported data heavily to ensure your users' privacy. First we remove tracking events from the imported events. We then discard all user data collected by Google from the events we keep.

## Import Google Analytics 4 data

We filter the Google Analytics 4 data based on a match on `eventName`. When this `eventName` is [`page_view`](https://support.google.com/analytics/answer/9356037), we import that event. All other events are discarded. Another filter we apply is a hostname filter. When you have multiple hostnames in your data, we ask you which hostnames to import. For example you might have `www.example.com` and `m.example.com`. You can pick the hostnames you want [in our UI](https://simpleanalytics.com/select-website/import).

### Dimensions

- `dateHour` – The combined values of date and hour formatted as YYYYMMDDHH.
- `fullPageUrl` – The hostname, page path, and query string for web pages visited; for example, the `fullPageUrl` portion of `https://www.example.com/store/contact-us?query_string=true` is `www.example.com/store/contact-us?query_string=true`.
- `sessionSource` – The source that initiated a session on your website or app.
- `deviceCategory` – The type of device: Desktop, Tablet, or Mobile.
- `countryId` – The geographic ID of the country from which the user activity originated, derived from their IP address. Formatted according to ISO 3166-1 alpha-2 standard.
- `browser` – The browsers used to view your website.
- `operatingSystem` – The operating systems used by visitors to your app or website. Includes desktop and mobile operating systems such as Windows and Android.
- `eventName` – The name of the event. For example, `page_view`.
- `hostname` – Includes the subdomain and domain names of a URL; for example, the Host Name of `www.example.com/contact.html` is `www.example.com`.

### Metrics

- `screenPageViews` – The number of app screens or web pages your users viewed. Repeated views of a single page or screen are counted. (`screen_view` + `page_view` events).
- `totalUsers` – The number of distinct users who have logged at least one event, regardless of whether the site or app was in use when that event was logged.
- `userEngagementDuration` – The total amount of time (in seconds) your website or app was in the foreground of users' devices.

> Use the [GA4 query explorer](https://ga-dev-tools.web.app/ga4/query-explorer/?d=dateHour%2CfullPageUrl%2CsessionSource%2CdeviceCategory%2CcountryId%2Cbrowser%2CoperatingSystem%2CeventName%2ChostName&e=totalUsers%2CscreenPageViews%2CuserEngagementDuration) to see which data we can import from Google Analytics 4. We prefilled the dimensions and metrics if you use our link to the [query explorer](https://ga-dev-tools.web.app/ga4/query-explorer/?d=dateHour%2CfullPageUrl%2CsessionSource%2CdeviceCategory%2CcountryId%2Cbrowser%2CoperatingSystem%2CeventName%2ChostName&e=totalUsers%2CscreenPageViews%2CuserEngagementDuration).

Go to [our Google Analytics importer](https://simpleanalytics.com/select-website/import) in our dashboard to import your Google Analytics data.
