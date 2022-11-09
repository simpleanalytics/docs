---
title: Automated events
category: events
permalink: /automated-events
redirect_from:
  - /capture-outbound-links
last_modified_at: 2022-04-14
---

[Normal events](/events) need to be added into your code. To make it easier we created a separate automated events script. This script has to be installed once, and it will track outbound links, email addresses clicks, and amount of downloads for common files (pdf, csv, docx, xlsx). Events will appear on [your events page](https://simpleanalytics.com/select-website/events).

## Outbound

Outbound links are basically just links that go to a different website. For example you have a website with a few products listed on them. People pay you for listing those products on your website. Now you want to find a way to track the amount of visitors that go to that website. For this you'll need outbound events!

## Emails

Do you have links to email addresses on your website? Then it could make sense to see how many clicks you get on your `mailto` links.

## Downloads

Do you have links to pdf's or other files? Collect the amount of downloads. You can specify the extensions of the files your want to collect downloads for.

## Script

> This script is additional to the normal embed script. Make sure to also include [that script](/script).

If you are a developer or you know your way around HTML it's easy to embed this script on your website. If you need help with that, we are happy to help. Just [contact us](https://simpleanalytics.com/contact).

<!-- prettier-ignore -->
```html
<script async src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
<script async src="https://scripts.simpleanalyticscdn.com/auto-events.js"></script>
```

Or if you want to change some settings (these are the defaults):

<!-- prettier-ignore -->
```html
<script async src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
<script
  async
  data-collect="outbound,emails,downloads"
  data-extensions="pdf,csv,docx,xlsx,zip,doc,xls"
  data-use-title="true"
  data-full-urls="false"
  src="https://scripts.simpleanalyticscdn.com/auto-events.js"></script>
```

It takes care of sending it as an event to Simple Analytics. Events can only be letters, numbers, and underscores. We convert the event names directly in this script.

## Demo of the script

To see a live demo of the script implementation, go to [autoevents.simpleanalytics.com](https://autoevents.simpleanalytics.com/). It shows an example of the automated events script with a few links you can click.

We love to improve our automated events. Please let us know if you need any help! We don't mind getting our hands dirty.

## Open-source

The automated events script is open-source. Feel free to take a look at it [on GitHub](https://github.com/simpleanalytics/scripts/blob/main/src/auto-events.js).
