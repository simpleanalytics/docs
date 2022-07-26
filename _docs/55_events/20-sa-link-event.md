---
title: Collect events for link clicks
category: events
permalink: /events/custom-link-clicks
menu: Custom link clicks
last_modified_at: 2022-07-18
---

The [automated events script](/automated-events) does collect events for outbound links. It does not require any coding, just adding a script. You probably want to use [that script](/automated-events).

If you want to collect events for other links or control a bit more on how it works, you can use the code below. Let's say you have a HTML page with this content:

```html
<p>This is <a href="/">a link</a>.</p>
```

Then you can use this code to add a `data-sa-link-event`-helper that will collect an event for link clicks:

```html
<script>
  (function () {
    function saLoadedLinkEvents() {
      document
        .querySelectorAll("a[data-sa-link-event]")
        .forEach(function (element) {
          var href = element.getAttribute("href");
          var eventName = element.getAttribute("data-sa-link-event");
          if (!href || !window.sa_event || !window.sa_loaded) return;

          element.addEventListener("click", function (event) {
            var target = element.getAttribute("target");
            if (target === "_blank") {
              event.preventDefault();
              window.sa_event(eventName, function () {
                window.location.href = href;
              });
              return false;
            } else {
              window.sa_event(eventName);
              return true;
            }
          });
        });
    }

    if (document.readyState === "ready" || document.readyState === "complete") {
      saLoadedLinkEvents();
    } else {
      document.addEventListener("readystatechange", function (event) {
        if (event.target.readyState === "complete") saLoadedLinkEvents();
      });
    }
  })();
</script>
```

After your installed the helper, somewhere on the page, you can change your HTML like this:

```html
<p>This is <a href="/" data-sa-link-event="link_name_text">a link</a>.</p>
```

It will then collect an events called "link_name_text" every time a visitor clicks on that link.
