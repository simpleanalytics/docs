---
title: Hide referral SPAM
category: features
permalink: /hide-referral-spam
redirect_from:
  - /delete-spam-from-your-analytics
  - /remove-referral-spam
last_modified_at: 2022-04-14
---

Simple Analytics has a feature where you can hide referral spam. Not by setting up complex filters, but just with a click on a button.

Hiding spam in your dashboard works by creating a filter. We have some logic in place where you can see how many page views are found with a certain referral so you know how many page views you are hiding. Do note that this filter will also be used in all other Simple Analytics features. You don't see the filtered referrals anywhere anymore. This is also the case for future page views.

> You can hide page views based on UTM codes as well. Go to [the cleaning feature](https://simpleanalytics.com/select-website/clean) to try it out.

Let's say you have referral SPAM from _"buy-my-product-now"_ as shown in this dashboard:

<img class="border" src="/images/spam-overview.jpg" alt="Overview of a SPAM referral">

This is annoying and make your stats inaccurate. If you want to remove this SPAM please follow these steps to remove it from your dashboard:

1. Click on the _"buy-my-product-now"_ referral and scroll down the page

1. Click on this link at the bottom of that page:

   <img class="border" src="/images/spam-click-on-link.jpg" alt="Click on this link to go to SPAM referral screen">

1. On the next page check if the amount of visits seems correct:

   <img class="border" src="/images/spam-verify.jpg" alt="Verify amount of visits">

1. Download a copy of your data

   <img class="border" src="/images/spam-download-a-copy.jpg" alt="Download a copy of your data first">

1. Remove the visits by clicking the button.

   <img class="border" src="/images/spam-confirm.jpg" alt="Confirm the removal of SPAM referrals">

1. The hiding of the visits starts and should be finished in a few seconds.

> You can also remove SPAM based on the page. This is uncommon, but if you want you can ask us for help or try it yourself. Use this URL (`https://simpleanalytics.com/clean?hostname=example.com&type=path&path=/page`) and replace `example.com` with your domain and `/page` with the page you like to remove. It will ask you to confirm because removing.
