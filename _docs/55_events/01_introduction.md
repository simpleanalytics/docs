---
title: Introduction to events
menu: Introduction
category: events
permalink: /events
---

With events in Simple Analytics you can collect counts of certain events. Let's say, you want to record a button click, you can fire an event for that. To make it easier for non-developers, we created [an automated events script](/automated-events). This script collects events for downloads, outbound links, and clicks on email links. You will need to install our separate script for it, but after that you don't need to modify any code.

If you want to get your hands dirty, you can collect events for all kinds of custom events. Like form submits, button clicks, and many more.

> The event UI is not that feature rich as you would expect from other Simple Analytics features. To access this feature in your dashboard go to [your events page](https://simpleanalytics.com/select-website/events). We are working on a new version where the posibilities are endless. Want to join that conversation? [Join our Slack channel](https://join.slack.com/t/simple-analytics/shared_invite/zt-ppfiaq04-LNDu5Cs4EOaJD0JhIFdkcg) to discuss the new events.

## Install embed script

To start working with events you need to have a recent version of our script. This script includes the normal page view functionality and the events feature.

Place this `<script>`-tag in the `<head>` of the page:

<!-- prettier-ignore -->
```html
<script>window.sa_event=window.sa_event||function(){var a=[].slice.call(arguments);window.sa_event.q?window.sa_event.q.push(a):window.sa_event.q=[a]};</script>
```

The script above is required for when events happen before our embed script is loaded. If your events only happen after the script is loaded, you don't really need it.

The next part is probably already on your page for collecting page views. If not, add it in your `<body>`-tag:

<!-- prettier-ignore -->
```html
<script async defer src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
```

If you **can't** add it to your `<body>` tag, place it in the `<head>` of the page. Don't place the `<noscript>` part in the `<head>`. If you can't add it to the body, just omit it.

If you use our [custom domain feature](/bypass-ad-blockers), make sure to replace `scripts.simpleanalyticscdn.com` and `queue.simpleanalyticscdn.com` with your custom domain.

### Developers

This little snippet creates a simple function called `sa_event`. After that it loads the Simple Analytics script asynchronously (it does not have any effect on your page load).

> Our scripts **do not send** data from localhost. We do this to prevent your localhost data to end up on our servers.

## `sa_event`-function

The `sa_event`-function is the function you'll need to use to create events. To track an event it's as simple as this:

```js
sa_event("click_signup");
```

> In previous versions we used `sa` instead of `sa_event`, but it caused too many issues because minifiers would use this variable name as well.
> If you use that old script (ending with `/e.js`) and you are updating to `/latest.js`, make sure to rename those functions or overwrite with `sa-global` (see below).

In the background we add the events to the current page view. With the page view is a referrer saved, this referrer is also saved with the event.

### Valid event names

We want to keep events very simple. That's why we only allow alphanumeric characters and underscores (`_`). We convert events to lower case and invalid names to a version which is valid. This way your events are always saved. If you return a function for an event we run this function and if the result is a string we will store the event. For example: `sa_event(function() { return "clicked_signup_on_" + window.document.location.pathname })`.

Event names are limited to 200 characters. If this exceeds we truncate the name to 200 characters.

## Tracking over multiple pages

We don't store anything on the computer of your visits so naturally events will not be linked when a visitor navigates between page. Unless it's a SPA (Single Page App) which does not reload the whole page but only a part of the page. If you don't have a SPA you can use [Pjax](https://github.com/MoOx/pjax/) to convert your website to a SPA website.

## Export events

To export events you can use [our API](/api/export-events).

## Event callbacks

In some cases you want to send an event before the visitor navigates away. For example to [capture outbound links](/capture-outbound-links). You can add a callback function as the second parameter of the `sa_event`-function:

```js
sa_event("outbound_link_to_affiliate", function () {
  window.location.href = "https://example.com/?affiliate=...";
});
```

The above example will capture the event before sending the visitor to `https://example.com/?affiliate=...`.

It's always smart to check if `sa_event` is available before using it:

```js
function callback() {
  window.location.href = "https://example.com/?affiliate=...";
}
if (window.sa_event_loaded) sa_event("outbound_link_to_affiliate", callback);
else callback();
```

## The variable `sa_event` is already used

If the `sa_event` variable is already in use you can change it with the `data-sa-global` attribute:

<!-- prettier-ignore -->
```html
<script>window.ba=window.ba||function(){var a=[].slice.call(arguments);window.ba.q?window.ba.q.push(a):window.ba.q=[a]};</script>
<script async defer data-sa-global="ba" src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
```
