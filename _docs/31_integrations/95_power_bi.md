---
title: Microsoft Power BI
menu: Power BI
category: integrations
permalink: /microsoft-power-bi
last_modified_at: 2022-04-14
---

Some customers use [Microsoft Power BI](https://powerbi.microsoft.com/) for building reports. Because we care about privacy, we don't store any personal data. No personal data from your visitors will end up on the servers of Microsoft.

This connector lets customers query data from the [API](/api/export-page-views) of [Simple Analytics](https://simpleanalytics.com/).

1. Before you start, you will need the export URL [from your Simple Analytics dashboard](https://simpleanalytics.com/select-website/export). Select the fields you want in the export and select "CSV":

   ![](https://assets.simpleanalytics.com/images/docs/power-bi/00-simple-analytics-export-dashboard.png)

1. Copy the URL with a right mouse, click on the "Export" button and select "Copy link" (or something like that). Save this link for a later step.

1. Add a data connector in Power BI by selecting the web connector:

   ![](https://assets.simpleanalytics.com/images/docs/power-bi/01-select-web-data.png)

1. After you hit "Connect" select the "Advanced" option

   ![](https://assets.simpleanalytics.com/images/docs/power-bi/02-advanced-web.png)

1. In the URL parts, you can add the URL you copy the link you copied from the "Export" button.

1. You can decide to break the URL up into parts by adding, for example, the dates programmatically

1. Finally, you have to fill in two headers (get from [your account page](https://simpleanalytics.com/account#api)):

   - `User-Id`: `sa_user_id_00000000-0000-0000-0000-000000000000`
   - `Api-Key`: `sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxx`

1. Hit "Ok" and on the next screen, click "Transform Data":

   ![](https://assets.simpleanalytics.com/images/docs/power-bi/03-transform.png)

1. You will have the Simple Analytics data in Microsoft Power BI. The possibilities are endless. That's why we stop the guide here for now.

We are planning to extend this guide to include an entire automatic updating data store in Power BI.

Let us know if you plan to implement that. Happy to help!
