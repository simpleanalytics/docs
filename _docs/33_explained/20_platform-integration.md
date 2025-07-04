---
title: Platform integration
category: explained
permalink: /explained/platform-integration
last_modified_at: 2025-07-04
---

Add an **Enable Simple Analytics** checkbox in your settings page.

- When the user checks the box, inject the embed script below into their pages.
- When the user unchecks, remove the script.

<img class="border" src="https://assets.simpleanalytics.com/docs/explained/platform-integration.png" alt="Simple Analytics integration in your platform" />

Usually it's just a user or team setting in your platform.

## Embed script

The only thing that's required, is enabling this script somewhere in the `<body>` (or `<head>`) of your platform when your user enables the *Simple Analytics Enabled* checkbox. They don't need to enter a website ID and don't need to create a Simple Analytics account before this checkbox can be enabled. We use the domain as an identifier.

```html
<!-- Simple Analytics platform integration -->
<script async data-hostname="<customer_domain>" data-platform="<your-platform-name>" data-affiliate="<affiliate-code>" src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
```

- *`<customer_domain>`* (required) is the stable identifier you create for that site on day one. Usually this is `customerxxx.yourplatform.com`, or `customerdomain.com`. Keep it even if the user changes domains later. It's also the hostname the Simple Analytics users will see in their dashboard.
- *`<your-platform-name>`* (required) is a unique name of your platform (eg.: `netlify`, `partner.com`, `kennis.shop`). This helps us linking all domains to your platform. Allowing us to give your users tailored instructions.
- *`<affiliate-code>`* (optional) is a unique code you can get from us which we use to attach it to every hit so new sign ups are credited to your account. This is optional.

## Optional event tracking

This part is completely optional, but some users like it when implemented. You can track clicks on buttons, submitting of forms, or clicks on download links.

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

<details markdown="1">

<summary>How to implement thisServer side</summary>

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

</details>

## Testing

1. Spin up a test site.
2. Enable the checkbox.
3. Visit the test site.
4. Check if there are requests to Simple Analytics in the Network tab of the Developer Tools.

## Support

[Contact us](https://dashboard.simpleanalytics.com/contact) and we will help you.
