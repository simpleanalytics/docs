---
title: Google Looker Studio connector
menu: Google Looker Studio
category: integrations
permalink: /google-looker-studio
redirect_from: 
  - /google-data-studio
last_modified_at: 2023-01-07
---

> Google Data studio has been renamed to Google Looker Studio.

Some customers use [Google Looker Studio](https://datastudio.google.com/) for building reports. Because we care about privacy, we don't store any personal data. That's why we are comfortable enough to let customers choose to connect with Looker Studio while Google can't abuse our customers' data or their visitors.

<img class="border-radius" src="https://assets.simpleanalytics.com/docs/google-data-studio/connector.jpg" alt="Simple Analytics connector for Google Looker Studio" />

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
