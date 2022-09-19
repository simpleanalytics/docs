---
title: Import Google Analytics data
category: features
permalink: /import-google-analytics-data
last_modified_at: 2022-07-08
---

[Google Analytics is shutting down](https://blog.simpleanalytics.com/google-to-sunset-universal-analytics-in-2023) its Universal Analytics properties. To keep this data you can choose to import it into Simple Analytics. We built a simple import tool where you can import your data in just a few clicks.

With Simple Analytics you can import Universal Analytics properties and Google Analytics 4 properties.

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

## Import Google Universal Analytics data

With Universal Analytics we have one filter we apply, which is the hostname filter. When you have multiple hostnames in your data, we ask you which hostnames to import. For example you might have `www.example.com` and `m.example.com`. You can pick the hostnames you want [in our UI](https://simpleanalytics.com/select-website/import).

### Dimensions

- `ga:dateHour` – The combined values of date and hour formatted as YYYYMMDDHH.
- `ga:pagePath` – A page on the website specified by path and/or query parameters. Use this with hostname to get the page's full URL.
- `ga:fullReferrer` – The full referring URL including the hostname and path.
- `ga:deviceCategory` – The type of device: desktop, tablet, or mobile.
- `ga:countryIsoCode` – Users' country's ISO code (in ISO-3166-1 alpha-2 format), derived from their IP addresses or Geographical IDs. For example, BR for Brazil, CA for Canada.
- `ga:browser` – The name of users' browsers, for example, Internet Explorer or Firefox.
- `ga:browserVersion` – The version of users' browsers, for example, 2.0.0.14.

### Metrics

- `ga:pageviews` – The total number of pageviews for the property.
- `ga:sessions` – The total number of sessions.
- `ga:timeOnPage` – Time (in seconds) users spent on a particular page, calculated by subtracting the initial view time for a particular page from the initial view time for a subsequent page. This metric does not apply to exit pages of the property.

> Use the [Universal Analytics Query Explorer](https://ga-dev-tools.web.app/query-explorer/) to see which data we can import from Universal Analytics. With Universal Analytics you have to manually copy and paste the dimensions and metrics from above into the Query Explorer.

### Data sampling

Google Universal Analytics uses data sampling. [They explain it like this](https://support.google.com/analytics/answer/2637192):

> In data analysis, sampling is the practice of analyzing a subset of all data in order to uncover the meaningful information in the larger data set. For example, if you wanted to estimate the number of trees in a 100-acre area where the distribution of trees was fairly uniform, you could count the number of trees in 1 acre and multiply by 100, or count the trees in a half acre and multiply by 200 to get an accurate representation of the entire 100 acres.

It happens for high-traffic websites or data older than one year. At Simple Analytics, we don't sample your data. You always get accurate metrics from our systems. But when you import from Google Analytics, Google might sample your data. We tell you in the confirmation email after your import is finished if Google has sampled data:

> **Important!** Google applied sampling and calculated the import results from 2,987,390 samples of a sampling space size of approximately 56,182,369 sessions. Sampling results in your data looking incomplete in a day-to-day view, but when viewed by month, the numbers do add up. We can't do anything about this.

Your dashboard can show spikes every x days while other days are empty. Sometimes it might be best to view the chart with page views instead of sessions for the periods of imported data. We recommend viewing this data on a multi-month basis. Daily and weekly can cause those spikes. Those spikes don't mean the totals aren't correct; it is just sampled.

Go to [our Google Analytics importer](https://simpleanalytics.com/select-website/import) in our dashboard to import your Google Analytics data.
