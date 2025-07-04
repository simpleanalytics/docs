---
title: Platform integration
category: explained
permalink: /explained/platform-integration
last_modified_at: 2025-07-04
---

Add an **Enable Simple Analytics** checkbox in your settings page.

* When the user checks the box, inject the embed script below into their pages.
* When the user unchecks, remove the script.

![](https://assets.simpleanalytics.com/docs/explained/platform-integration.png)

## Embed script

```html
<!-- Simple Analytics privacy first analytics -->
<script async data-affiliate="<affiliate-code>" data-hostname="<customer_subdomain>.example.com" src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
```

*`<customer_subdomain>`* is the stable identifier you create for that site on day one. Keep it even if the user changes domains later. It's also the hostname the Simple Analytics users will see in their dashboard.

*`<affiliate-code>`* is a unique code you can get from us which we use to attach it to every hit so new sign ups are credited to your account.

## Optional event tracking

Add this helper once in `<head>`. You can include it for every customer. If the Simple Analytics script is not enabled the events remain in the browser and are ignored. When the script is enabled they are automatically sent to Simple Analytics servers.

```html
<script>
window.sa_event = window.sa_event || function () {
  const a = [].slice.call(arguments);
  window.sa_event.q ? window.sa_event.q.push(a) : window.sa_event.q = [a];
};
</script>
```

Front end events send with this function:

```js
sa_event("click_signup");
```

Server side events:

```bash
curl -X POST https://queue.simpleanalyticscdn.com/events \
-H "Content-Type: application/json" \
-d '{
  "type": "event",
  "hostname": "<customer_subdomain>.example.com",
  "affiliate": "affiliate-code",
  "event": "click_signup",
  "ua": "<user_agent>"
}'
```

## Testing

1. Spin up a test site.
2. Enable the checkbox.
3. Load a page and confirm hits appear in your Simple Analytics dashboard under the `affiliate-code` affiliate tab.

## Support

[Contact us](https://dashboard.simpleanalytics.com/contact) and we will help you.
