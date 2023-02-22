---
title: How to use Dailytics with your Simple Analytics account
menu: Dailytics
category: integrations
permalink: /get-powerful-email-reports-with-dailytics
canonical_url: https://dailytics.com/simple-analytics/
last_modified_at: 2022-04-14
---

In this tutorial, we are going to generate an email report to share with your team or clients using Dailytics.com.

[Dailytics](https://dailytics.com) is a very simple tool that allows you to create a powerful report with custom charts and lists (with many filters being applied to them). It integrates with different analytics providers and Simple Analytics is now one of them.

You will need to start by creating an account at [dailytics.com](https://dailytics.com) (they offer a free trial). Once you are ready with your account, you'll get straight to the "Choose the Source" screen: Select "Simple Analytics".

## Create your first report

At this point, you will need to have a valid `user_id` and `api_key` at Simple Analytics. You can get them at your [Account Settings](https://simpleanalytics.com/account#api), in the "API Access" section. It's a good practice to create a new `api_key` specially for Dailytics.

In the first half of the form, you will need to set a report name (it will be used as the subject of your report), the periodicity of the email (daily, weekly or monthly), a logo url (optional, but will make your email report look nicer), and the email address(es) you want to send the report to.

<img class="border" src="/images/dailytics-form-01.png" alt="Create a report at Dailytics - form, first part" />

In the second part, you will need to start by including your `user_id` (the one that starts with `sa_user_id_...`) and your `api_key` (the one that starts with `sa_api_key_...`). Once you put them, Dailytics will load automatically the list of all the websites that they can get with those credentials. Choose the right one and the time of the day you want your report to be sent.

<img class="border" src="/images/dailytics-form-02.png" alt="Create a report at Dailytics - form, second part" />

That's it! By default a few widgets will be generated automatically for you (top articles list, charts with your traffic, and a chart with your traffic from Google). The true power from Dailytics comes when you customise those widgets to add your own filters to get stats from different section of your website, or a chart with the main sources of traffic.

## Customise your widgets

This is a common example of a customised email report:

<img class="border" src="/images/dailytics-final-result.gif" alt="Dailytics example" />

You will be able to add any filter that is currently supported by the [Simple Analytics Stats API](https://docs.simpleanalytics.com/api/stats) but the easiest thing to do is to add filters by `page_path` and `referrals`. For this, you need to edit each Widget and add all your filters there. This is how you can edit each widget:

<img class="border" src="/images/dailytics-form-03.png" alt="Create a report at Dailytics - form, second part" />

The best part of the Simple Analytics integration is that we support wildcards in these filters, so you can filter by `/blog/*` and that will include any page path that "starts with `/blog/`".

That's it! you can now start sending these reports to your team or clients. They are very useful to start casual conversations related to the performance of some articles or editors (dailytics will try to fetch the `author` of any article), products or any new source of traffic. They will also let you know if you broke your traffic record yesterday!

You can find more details of the integration at [dailytics.com/simple-analytics](https://dailytics.com/simple-analytics/).

[Get started with Dailytics](https://dailytics.com).
