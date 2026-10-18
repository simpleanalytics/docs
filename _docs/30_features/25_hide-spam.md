---
title: Hide referral SPAM
category: features
permalink: /hide-referral-spam
redirect_from:
  - /delete-spam-from-your-analytics
  - /remove-referral-spam
last_modified_at: 2026-10-17
---

Simple Analytics lets you hide referral spam with a filter on your website's view. You don't need to set up complex rules or delete any data.

The filter applies to your dashboard and to the data you get through our APIs, including future page views. Filters don't delete data. If you remove the filter later, the hidden page views show up again.

Let's say you have referral SPAM from _"free-traffic.example"_. To hide it from your dashboard:

1. Click on the _"free-traffic.example"_ referrer in your dashboard and scroll down to the top referral pages. Below them, click on _"Hide visits from free-traffic.example"_:

   <img class="border" src="/images/hide-spam-referrer-link.png" alt="Hide visits from a referrer link in the Simple Analytics dashboard">

1. This opens the **Add filters** step of your website's view. Add a filter on the referrer, choose **is not**, and enter the spam domain.

1. Check the number of page views below the filters. It shows how many page views match your filters, so you can see the result before you save.

   <img class="border" src="/images/hide-spam-view-filter.png" alt="Referrer filter in the view editor with the number of matching page views">

1. Go through the next step and click **Update view**.

> You can also hide page views based on other fields, like the page path or UTM codes. Go to [the filters of your view](https://simpleanalytics.com/select-website/edit), add a filter, and save the view.
