---
title: Introduction to events
menu: Introduction
category: events
permalink: /events
last_modified_at: 2023-01-20
---

With events in Simple Analytics you can collect counts of certain events. Let's say, you want to record a button click, you can fire an event for that. To make it easier for non-developers, we created [an automated events script](/automated-events). This script collects events for downloads, outbound links, and clicks on email links. You will need to install our separate script for it, but after that you don't need to modify any code.

If you want to get your hands dirty, you can collect events for all kinds of custom events. Like form submits, button clicks, and many more. We created a simple video showing how to collect events in Simple Analytics. [Here you go](https://www.youtube.com/watch?v=CCvdgTReqms)

For specific platforms, we have integration guides. For example, if you're using [Circle paywalls](/install-simple-analytics-on-circle), you can track successful payments as conversion events.

You can [download your events](/export-data), use them in the [Events Explorer](/events-explorer), and use them in [Goals](/goals).

<img class="border" src="https://assets.simpleanalytics.com/docs/events/events-explorer.png" alt="Overview of the Events Explorer in Simple Analytics" />
<p class="caption" markdown="1">Overview of the [Events Explorer](/events-explorer) in Simple Analytics</p>

<img class="border" src="https://assets.simpleanalytics.com/docs/goals/goals-histogram.png" alt="A goal selected in Simple Analytics" />
<p class="caption" markdown="1">The histogram view of a [goal](/goals) in Simple Analytics</p>

## Placeholder event function

> If your events only happen after the script is loaded, you don't really need the placeholder events function. For example, when using automated events. Those events will happen way after the page (including the embed script) has finished loading. That script includes the final event function.

Events that can happen within seconds from page load should be queued when the embed script hasn't loaded yet.

To allow this, place this `<script>`-tag in the `<head>` of the page (best before other scripts):

<!-- prettier-ignore -->
```html
<script>window.sa_event=window.sa_event||function(){var a=[].slice.call(arguments);window.sa_event.q?window.sa_event.q.push(a):window.sa_event.q=[a]};</script>
```

This little snippet creates a simple function called `sa_event`. After that it loads the Simple Analytics script asynchronously (it does not have any effect on your page load).

## Install script

The next part is probably already on your page for collecting page views. If not, add it in your `<body>`-tag:

<!-- prettier-ignore -->
```html
<script async src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
```

If you **can't** add it to your `<body>` tag, place it in the `<head>` of the page.

Don't place the `<noscript>` part in the `<head>`.
If you can't add it to the body, just omit it.
We don't recommend adding a noscript tag, because it's mostly collecting data from robots.

If you use our [custom domain feature](/bypass-ad-blockers), make sure to replace `scripts.simpleanalyticscdn.com` and `queue.simpleanalyticscdn.com` with your custom domain.

## `sa_event`-function

The `sa_event`-function is the function you'll need to use to create events. To track an event it's as simple as this:

```js
sa_event("click_signup");
```

To send metadata with your event, [check our metadata page](/metadata).

## Inline events helper

We created a simple helper script that allows you to use data attributes for events:

```html
<a href="/pricing" data-simple-event="click_pricing_page">See pricing</a>
```

[Read more about it here](/events/inline).

## Snippets

First, check if the events you need are part of our [automated events script](/automated-events). If not, these snippets might help to get you started with custom events:

- [Button clicks](https://gist.github.com/adriaandotcom/aa00b4cdc85797a2f2ba715e82de85da#file-button-click-html)
- [Form submits](https://gist.github.com/adriaandotcom/aa00b4cdc85797a2f2ba715e82de85da#file-forms-submit-html)
- [Link clicks](https://gist.github.com/adriaandotcom/aa00b4cdc85797a2f2ba715e82de85da#file-links-click-html)
- [Form submits in Google Tag Manager](https://www.simpleanalytics.com/blog/how-to-track-form-submissions-using-google-tag-manager)
- [Video events in Google Tag Manager](https://www.simpleanalytics.com/blog/video-tracking)
- [Circle paywall conversions](/install-simple-analytics-on-circle) - Track successful payments

## Valid event names

We want to keep events very simple. That's why we only allow alphanumeric characters and underscores (`_`). We convert events to lower case and invalid names to a version which is valid. This way your events are always saved. If you return a function for an event we run this function and if the result is a string we will store the event. For example: `sa_event(function() { return "clicked_signup_on_" + window.document.location.pathname })`.

Event names are limited to 200 characters. If this exceeds we truncate the name to 200 characters.

## Tracking over multiple pages

We don't store anything on the computer of your visits so naturally events will not be linked when a visitor navigates between page. Unless it's a SPA (Single Page App) which does not reload the whole page but only a part of the page. If you don't have a SPA you can use [Pjax](https://github.com/MoOx/pjax/) to convert your website to a SPA website.

## Export events

To export events you can use [our API](/api/export-events).

## Event callbacks

> Do not track does not play nice with callbacks, please skip callbacks for Do Not Track visitors. Either [enable collecting DNT visitors](/dnt) or check for them in your code. See below.

In some cases you want to send an event before the visitor navigates away. For example to [capture outbound links](/capture-outbound-links). You can add a callback function as the second parameter of the `sa_event`-function:

```js
sa_event("outbound_link_to_affiliate", function () {
  window.location.href = "https://example.com/?affiliate=...";
});
```

The above example will capture the event before sending the visitor to `https://example.com/?affiliate=...`.

It's always smart to check if `sa_loaded` is available before using it:

<!-- prettier-ignore -->
```js
function callback() {
  window.location.href = "https://example.com/?affiliate=...";
}

/* Check for DoNotTrack visitors */
var dntActive = parseInt(navigator.msDoNotTrack || window.doNotTrack || navigator.doNotTrack, 10) === 1;

/* Check for sa_loaded boolean */
if (window.sa_loaded && !dntActive) sa_event("outbound_link_to_affiliate", callback);
else callback();
```

## The variable `sa_event` is already used

If the `sa_event` variable is already in use you can change it with the `data-namespace` attribute:

<!-- prettier-ignore -->
```html
<script>window.ba_event=window.ba_event||function(){var a=[].slice.call(arguments);window.ba_event.q?window.ba_event.q.push(a):window.ba_event.q=[a]};</script>
<script async data-namespace="ba" src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
```

Do note that the namespace will also change other functions as well. For example, `sa_metadata` becomes `ba_metadata`, `sa_loaded` becomes `ba_loaded`, and `sa_pageview` becomes `ba_pageview`.
