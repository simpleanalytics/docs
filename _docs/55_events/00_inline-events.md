---
title: Inline events
category: events
permalink: /events/inline
last_modified_at: 2026-10-29
---

From script version 12, our main script sends an event when a visitor interacts with an element that has a `data-simple-event` attribute. You don't need to write JavaScript or load an extra script.

```html
<script async src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
```

### Clicks

Add `data-simple-event="event_name"` to any clickable element:

```html
<a href="/pricing" data-simple-event="visit_pricing_page">See pricing</a>
```

The script never delays or cancels the click, so links, downloads and new tabs work as before.

### Form submissions

Put `data-simple-event="form_name"` on your `form` tag. The event is sent when the form is submitted and includes the text of the submit button as `button_text`. We never collect what visitors type into your form.

```html
<form action="/signup" data-simple-event="signup_form">
  <input name="email" type="email" />
  <button type="submit">Sign up</button>
</form>
```

### Metadata

Every inline event includes the element's tag name as `tag`. Attributes starting with `data-simple-event-` are added as [metadata](/metadata), with dashes converted to underscores:

```html
<button data-simple-event="select_plan" data-simple-event-plan="enterprise">
  Choose Enterprise
</button>
```

### 404 pages

Add `data-detect-404="true"` to the script to send a `page_404` event when a page contains "404" and a request to the same URL confirms the 404 status.

```html
<script
  async
  data-detect-404="true"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
></script>
```
