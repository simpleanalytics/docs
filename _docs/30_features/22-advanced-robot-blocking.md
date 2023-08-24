---
title: Advanced robot blocking
menu: Robot blocking
category: features
permalink: /robot-blocking
last_modified_at: 2023-08-24
---

By default, we block robots based on their user agent and some traces they leave in the browser by default. For most robots, this works great, but some slip through the cracks. We added *advanced robot blocking* to prevent those robots from polluting your data.

It works by having an extensive list of known IPs of data centers (from Udger, Google Cloud, Amazon AWS,  Microsoft Azure). This list does not contain the IPs of your visitors. Before we store a data point, we check if the IP matches this list of IPs of data centers. If it does, we tag the datapoint as being from a robot. We never store (not even a hashed version of) the IPs of your visitors.

Advanced robot blocking settings works for all of your websites in your account.

Here is how it looks in your account settings when it's enabled:

<img class="border" src="https://assets.simpleanalytics.com/docs/account/advanced-robot-blocking.png" alt="Advanced robot blocking in Simple Analytics account settings" />

Go to [your account](https://simpleanalytics.com/account#advanced-robot-blocking) to enable *Advanced robot blocking*.
