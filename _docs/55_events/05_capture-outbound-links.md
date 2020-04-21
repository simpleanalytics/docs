---
title: Capture outbound links with events
menu: Capture outbound links
category: events
permalink: /capture-outbound-links
---

To capture outbound links you need a function that saves the outbound link as an event.

We created the `captureOutboundLink`-function for this purpose. Copy this code into your HTML:

```html
<script>
  function captureOutboundLink(element) {
    var timeout = 0;
    if (element && window.sa_event) {
      var href = element.getAttribute("href");
      var hostname = href.indexOf("://") ? href.split("/")[2] : href;
      var event = "outbound_" + hostname.replace(/[^a-z0-9]+/gi, "_");
      sa_event(event);
      console.info(
        "Simple Analytics: captured outbound link as event: " + event
      );
      timeout = 250;
    }
    window.setTimeout(function () {
      document.location = href;
    }, timeout);
  }
</script>
```

It takes care of sending it as an event to Simple Analytics. As events can only be letters, numbers, and underscores we already convert this name.

To use this function in your HTML you can add `onclick="captureOutboundLink(this); return false;"` to your links:

```html
<a
  href="http://www.example.com"
  onclick="captureOutboundLink(this); return false;"
  >Check out example.com</a
>
```

> Out current implementation of events does not support callbacks yet, so that's why we use the 250ms timeout at the moment. It means that there is no guarantee that events will be saved before the user navigates away.

We love to improve capturing outbound links. Please let us know if you need any help! We don't mind getting our hands dirty.
