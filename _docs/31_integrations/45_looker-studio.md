---
title: Google Looker Studio connector
menu: Google Looker Studio
category: integrations
permalink: /google-data-studio
redirect_from:
  - /google-looker-studio
last_modified_at: 2026-08-13
---

Use the Simple Analytics connector to build Google Looker Studio reports from
your website's aggregated pageview and event data.

## Before you start

You need:

- A [Simple Analytics account](https://www.simpleanalytics.com/signup).
- An active trial or a plan that includes API access. See our
  [current plans](https://www.simpleanalytics.com/pricing).
- A website in Simple Analytics that you are allowed to access.
- A Simple Analytics API key. Create or copy one from
  [API access in your account](https://dashboard.simpleanalytics.com/account#api).

API keys belong to individual users. If a user loses access to a website, that
user's key can no longer retrieve the website's data.

## Connect Simple Analytics to Looker Studio

1. Open the
   [Looker Studio connector gallery](https://datastudio.google.com/u/0/datasources/create),
   search for **Simple Analytics**, and select the connector.
2. Authorize the connector when Google asks for permission to connect to an
   external service. This permission lets the connector request your data from
   `simpleanalytics.com`; it does not give Simple Analytics access to other
   Google products or Google account data.
3. Enter your Simple Analytics API key when prompted.
4. Enter the website hostname without a protocol or path. For example, use
   `example.com`, not `https://example.com/about`.
5. Select a dataset:
   - **Pageviews** for website traffic, acquisition, device, and engagement
     reporting.
   - **Events** for event names and event totals.
6. Select the timezone to use for date grouping.
7. Click **Connect**, review the available fields, and create your report.

The connector requires a date range. The date range selected in Looker Studio
is sent with each query.

## Data available in the connector

The **Pageviews** dataset includes:

- Date by hour, day, week, month, or year.
- Path, referrer hostname, country, device, browser, operating system, and UTM
  dimensions.
- Pageviews, unique visitors, average visit duration, and average scroll depth.

The **Events** dataset includes:

- Date by hour, day, week, month, or year.
- Event name.
- Events and unique visitors.

### Metadata fields

The connector discovers recent metadata keys for the selected dataset and adds
them as dimensions named `Meta: ...`.

- Discovery looks back up to 365 days.
- Up to 100 safe text metadata dimensions are returned.
- URL-parameter metadata is excluded.
- Metadata dimensions support exact, list, and not-equal filters. They do not
  support contains filters.

Looker Studio caches data-source fields. In an existing data source, refresh
the fields when you want newly collected metadata to appear.

## Query limits

A chart can request up to ten metrics and five dimensions. It must include at
least one metric and can include at most one date dimension. A chart can use
one sort field.

Supported filters depend on the field:

- Path, referrer hostname, and UTM fields support equals, list, contains, and
  not-equals filters.
- Country, device, browser, and operating system support equals, list, and
  not-equals filters.
- Event name and metadata fields support equals, list, and not-equals filters.

## Data access and security

For each query, the connector sends your API key, website hostname, selected
date range, timezone, fields, filters, sorting, and row limit to Simple
Analytics over HTTPS. Simple Analytics returns the requested aggregated data to
Looker Studio.

The API key is stored per Google user using Apps Script user properties. It is
not stored as a Looker Studio data-source configuration field. You can revoke a
key at any time from
[API access in your account](https://dashboard.simpleanalytics.com/account#api).

Use of the connector is subject to the Simple Analytics
[General Terms and Conditions](https://www.simpleanalytics.com/general-terms-and-conditions)
and [Privacy Policy](https://www.simpleanalytics.com/privacy-policy).

## Troubleshooting

### Invalid credentials

Confirm that the key starts with `sa_api_key_` and still appears under API
access in your account. If needed, create a new key and reconnect the Looker
Studio data source.

### No permission to access a website

Confirm that the hostname is correct and that the Simple Analytics user who
created the API key can access that website.

### Numbers differ from the Simple Analytics dashboard

Use the same date range and timezone in both products. Different timezone
settings can move traffic into a different hour or day.

### New metadata is missing

Refresh the data-source fields in Looker Studio. Only safe text metadata seen
within the last 365 days is discoverable.

For further help, contact [Simple Analytics support](https://dashboard.simpleanalytics.com/contact).

The connector's source code is available on
[GitHub](https://github.com/simpleanalytics/google-data-studio/).
