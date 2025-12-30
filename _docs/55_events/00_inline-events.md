---
title: Inline events helper
category: events
permalink: /events/inline
hidden: true
last_modified_at: 2025-04-22
---

This small script watches your page for any element with a `data-simple-event`-attribute and automatically sends events to Simple Analytics when the user interacts. You don’t need to write any extra JavaScript calls—just add the right attributes to your HTML.

<blockquote class="red">
  <p>Warning, this script is in beta and can change any time.</p>
</blockquote>

### Installation

Include the tracker snippet somewhere on your page, just before the closing `</body>` tag.

```html
<script async src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
<script async src="https://scripts.simpleanalyticscdn.com/inline-events.js"></script>
```

### Tracking button clicks

To track a click, add `data-simple-event="event_name"` to any clickable element. The script prevents the default action, sends your event, then continues with the click (including opening links).

```html
<a href="/pricing" data-simple-event="visit_pricing_page">See pricing</a>
```

Tracking form submissions

Simply put `data-simple-event="form_name"` on your form tag. When the user submits, the script sends an event with the name of the form and the text of the submit button, then submits the form.

```html
<form action="/signup" data-simple-event="signup_form">
  <input name="email" type="email" />
  <input name="password" type="password" />
  <button type="submit">Sign up</button>
</form>
```

### Adding custom metadata

Any attribute starting with `data-simple-event-` will be included as event metadata. Dashes convert to underscores.

```html
<button
  data-simple-event="select_plan"
  data-simple-event-plan="enterprise"
  data-simple-event-referrer="homepage"
>
  Choose Enterprise
</button>
```

### Manual event tracking

You can also fire events from code using `sa_event("event_name", { key: value })`. This works before or after the auto‑binding. For this you don't need this extra script.

```js
// custom event on newsletter popup
sa_event("newsletter_signup", { source: "modal" })
```

### 404 detection

On DOMContentLoaded the script checks for "404" in your page HTML. If it finds it and the server HEAD request confirms status 404, it will send a page_404 event with the URL and status code.
