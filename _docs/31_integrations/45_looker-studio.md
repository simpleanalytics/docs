---
title: Google Data Studio connector
menu: Google Data Studio
category: integrations
permalink: /google-data-studio
redirect_from:
  - /google-looker-studio
last_modified_at: 2026-07-28
---

> Data studio has been renamed to Looker Studio and then back to Data Studio.

Some customers use [Google Data Studio](https://datastudio.google.com/) for building reports. Because we care about privacy, we don't store any personal data. That's why we are comfortable enough to let customers choose to connect with Data Studio while Google can't abuse our customers' data or their visitors.

<img class="border-radius" style="aspect-ratio: 1440/810" src="https://assets.simpleanalytics.com/docs/google-data-studio/connector.jpg" alt="Simple Analytics connector for Google Data Studio" />

This connector lets customers query data from the [API](/api) of [Simple Analytics](https://simpleanalytics.com/). It does need access to your Simple Analytics data. We need the Google scope "connect to an external service" for that.

1. Go to [https://datastudio.google.com/datasources/create?connectorId=AKf...eEg](https://datastudio.google.com/datasources/create?connectorId=AKfycbxtZ_DIGiEd-fEVo5j2rjiAUVMUvCUz26oiYSnGYzSzMnNiXTdZoE0L9lOWrKYOXTteEg)
1. Follow the steps in the video:

{%
  include video.html
  controls="true"
  red="true"
  slug="connect-google-data-studio"
  formats="mp4,ogg,webm,wmv"
%}

When using this connector you are subjected to our [general terms and conditions](https://simpleanalytics.com/general-terms-and-conditions) and [privacy policy](https://simpleanalytics.com/privacy).

The source code for the connector is hosted on [GitHub](https://github.com/simpleanalytics/google-data-studio/).

## Compare Simple Analytics data with Google Data Studio

Some customers reported that the data in Google Data Studio wasn't equal with the data they saw in the Simple Analytics dashboard. Follow this guide on how to get the exact numbers in Google Data Studio as in the Simple Analytics dashboard.

To keep data consistent it's recommended to use the UTC timezone in all reports.

Let's take one day from our dashboard, in our case 27th of April. It shows 1019 visitors:

<img class="border" style="aspect-ratio: 1440/1075" src="https://assets.simpleanalytics.com/docs/google-data-studio/simple-analytics-dashboard.png" alt="Simple Analytics dashboard for comparing with Google Data Studio" />

To set up your Google Data Studio it would require these changes:

1. Set your Simple Analytics dashboard to UTC (at the bottom of the date picker).
2. Set data source time zone to UTC in Google Data Studio.
3. Select "count" for aggregation on the "Unique" metric.
4. Select the same dates as your did in the Simple Analytics dashboard.
5. Create a filter on "Unique" is "True".

It should show the same amount of visitors as in your Simple Analytics dashboard:

<img class="border" style="aspect-ratio: 1440/1090" src="https://assets.simpleanalytics.com/docs/google-data-studio/instructions.png" alt="Set up dashboard in Google Data Studio" />
