---
title: Capture outbound links with events
menu: Capture outbound links
category: events
permalink: /capture-outbound-links
---

To capture outbound links you need a function that saves the outbound link as an event.

Just copy and paste this code into your HTML:

```html
<script>
(function saInitializeLinkCapture(window) {
  var log = function (message, type) {
    var logger = type === "warn" ? console.warn : console.log;
    return logger("Simple Analytics: " + message);
  };

  window.saCaptureOutboundLink = function saCaptureOutboundLink(element) {
    if (!element) return log("no element found in saCaptureOutboundLink");
    var sent = false;

    var callback = function () {
      if (!sent) document.location = element.getAttribute("href");
      sent = true;
    };

    if (window.sa_event) {
      var href = element.getAttribute("href");
      var hostname = href.indexOf("://") ? href.split("/")[2] : href;
      var event =
        "outbound_" +
        hostname.replace(/[^a-z0-9]+/gi, "_").replace(/(^_+|_+$)/g, "");
      sa_event(event, callback);
      log("captured outbound link as event: " + event);

      return window.setTimeout(callback, 5000);
    } else {
      log("sa_event is not defined", "warn");
      return callback();
    }
  };

  function onDOMContentLoaded() {
    var a = document.getElementsByTagName("a");

    // Loop over all links on the page
    for (var i = 0; i < a.length; i++) {
      var link = a[i];

      // Test is a link does start with http:// or https://
      if (
        /^https?:\/\//i.test(link.href) &&
        link.hostname !== window.location.hostname
      ) {
        link.setAttribute(
          "onclick",
          "saCaptureOutboundLink(this); return false;"
        );
      }
    }
  }

  window.addEventListener("DOMContentLoaded", onDOMContentLoaded);
})(window);
</script>
```

It will track all links with our events. Easy, right? It takes care of sending it as an event to Simple Analytics. As events can only be letters, numbers, and underscores we already convert this name.

We love to improve capturing outbound links. Please let us know if you need any help! We don't mind getting our hands dirty.
