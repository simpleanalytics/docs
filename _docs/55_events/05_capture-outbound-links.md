---
title: Capture outbound links with events
menu: Capture outbound links
category: events
permalink: /capture-outbound-links
---

To capture outbound links you need a function that saves the outbound link as an event. We have two ways to create outbound events from those links. One where the page opens in a new tab (easiest) and one where you can replace the current page with the links.

## Track all external links and open in new tabs

Just copy and paste this code into your HTML:

```html
<script>
(function createEvents() {
  // Get all links on the page
  var a = document.getElementsByTagName("a");

  // Loop over all links on the page
  for (var i = 0; i < a.length; i++) {
    var link = a[i];

    // Test is a link does start with http
    if (/^http/i.test(link.href)) {

      // Set event name with host of link without the www
      var event = "outbound_" + link.host.replace(/^(www|l|m)\./, "");
      link.setAttribute("target", "_blank");
      link.setAttribute("onclick", "sa_event('" + event + "');");
    }
  }
})();
</script>
```

It will track all links with our events and it will open those links in a new tab. Easy, right?

## Do not open links in a new tab

If you do not want to open links in a new tab you can use this function. We created the `captureOutboundLink`-function for this purpose. Copy this code into your HTML:

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

Or run this for all your links on the page:

```html
<script>
(function createEvents() {
  // Get all links on the page
  var a = document.getElementsByTagName("a");

  // Loop over all links on the page
  for (var i = 0; i < a.length; i++) {
    var link = a[i];

    // Test is a link does start with http
    if (/^http/i.test(link.href)) 
      link.setAttribute("onclick", "captureOutboundLink(this); return false;");
    }
  }
})();
</script>
```

> Out current implementation of events does not support callbacks yet, so that's why we use the 250ms timeout at the moment. It means that there is no guarantee that events will be saved before the user navigates away.

We love to improve capturing outbound links. Please let us know if you need any help! We don't mind getting our hands dirty.
