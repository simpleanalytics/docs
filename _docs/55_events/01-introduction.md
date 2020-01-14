---
title: Introduction to events
menu: Introduction
category: events
category_order: 10
order: 1
permalink: /events
---

<blockquote class="red">
  <p>The event feature is highly experimental, expect issues and please report them! To access this feature in your dashboard go to simpleanalytics.com<b>/events/[YOUR WEBSITE]</b>. In the previous version we used cookies, this is now removed. We want to stay a cookie-less solution to be GDPR, CCPA, and PECR complient out-of-the-box.</p>
</blockquote>

## Install embed script

To start working with events you need to have a recent version of our script. This script includes the normal page view functionality and the events feature.

<!-- prettier-ignore -->
```html
<script>window.sa=window.sa||function(){a=[].slice.call(arguments);sa.q?sa.q.push(a):sa.q=[a]};</script>
<script async defer src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
```

Or if you use our [custom domain feature](/bypass-ad-blockers):

<!-- prettier-ignore -->
```html
<script>window.sa=window.sa||function(){a=[].slice.call(arguments);sa.q?sa.q.push(a):sa.q=[a]};</script>
<script async defer src="https://[YOUR SUBDOMAIN LINKING TO US]/latest.js"></script>
```

> **Developers:** place this script in the `<head>` or top part of your `<body>` in your html. The second script (`latest.js`) can be placed elsewhere on the page if you like.

This little snippet creates a simple function called `sa`. After that it loads the Simple Analytics script asynchronously (it does not have any effect on your page load).

## `sa`-function

The `sa`-function is the function you'll need to use to create events. To track an event it's as simple as this:

```js
sa("click_signup");
```

In the background we add the events to the current page view. With the page view is a referrer saved, this referrer is also saved with the event.

### Valid event names

We want to keep events very simple. That's why we only allow alphanumeric characters and underscores (`_`). We convert events to lower case and invalid names to a version which is valid. This way your events are always saved.

## Tracking over multiple pages

We don't store anything on the computer of your visits so naturally events will not be linked when a visitor navigates between page. Unless it's a SPA (Single Page App) which does not reload the whole page but only a part of the page. If you don't have a SPA you can use [Pjax](https://github.com/MoOx/pjax/) to convert your website to a SPA website.

## The variable `sa` is already used

If the `sa` variable is already in use you can change it with the `data-sa-global` attribute:

<!-- prettier-ignore -->
```html
<script>window.ba=window.ba||function(){a=[].slice.call(arguments);ba.q?ba.q.push(a):ba.q=[a]};</script>
<script async defer data-sa-global="ba" src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
```
