---
title: Automated events
category: events
permalink: /automated-events
redirect_from:
  - /capture-outbound-links
---

To make it easier for our customers we added automated events. You can collect a few different events automatically: outbound links, email clicks, and amount of downloads.

## Outbound

Outbound links are basically just links that go to a different website. For example you have a website with a few products listed on them. People pay you for listing those products on your website. Now you want to find a way to track the amount of visitors that go to that website. For this you'll need outbound events!

It's as easy as including the script below and making sure the `outbound` in config is set to `true`.

## Emails

Do you have links to email addresses on your website? Then it could make sense to see how many clicks you get on your `mailto` links.

It's as easy as including the script below and making sure the `emails` in config is set to `true`.

## Downloads

Do you have links to pdf's or other files? Collect the amount of downloads. You can specify the extensions of the files your want to collect downloads for.

It's as easy as including the script below and making sure the `downloads` in config is set to `true`. Feel free to add extensions to the list.

## Script

If you are a developer or you know your way around HTML it's easy to embed this script on your website. If you need help with that, we are happy to help. Just [contact us](https://simpleanalytics.com/contact).

<details markdown="1">
<summary>Copy and paste this code into your HTML</summary>

```html
<script>
  (function saAutomatedEvents(window) {
    if (!window || !document) return;

    var options = {
      // What to collect
      outbound: true,
      emails: true,
      downloads: true,

      // Outbound: get full paths of the links? false for just the hostname
      paths: false,

      // Downloads: enter extensions you want to collect
      extensions: ["pdf", "csv", "docx", "xlsx"],
    };

    var log = function (message, type) {
      var logger = type === "warn" ? console.warn : console.log;
      return logger("Simple Analytics automated events: " + message);
    };

    if (typeof options === "undefined")
      log("options object not found, please specify", "warn");

    window.saAutomatedLink = function saAutomatedLink(element, type) {
      try {
        if (!element) return log("no element found");
        var sent = false;

        var callback = function () {
          if (!sent) document.location = element.getAttribute("href");
          sent = true;
        };

        if (window.sa_event) {
          var hostname = element.hostname;
          var pathname = element.pathname;
          var event;

          switch (type) {
            case "outbound": {
              event = hostname + (options.paths ? pathname : "");
              break;
            }
            case "download": {
              event = hostname + pathname;
              break;
            }
            case "email": {
              var href = element.getAttribute("href");
              event = (href.split(":")[1] || "").split("?")[0];
              break;
            }
          }

          var clean =
            type +
            "_" +
            event.replace(/[^a-z0-9]+/gi, "_").replace(/(^_+|_+$)/g, "");

          sa_event(clean, callback);

          log("collected " + clean);

          return window.setTimeout(callback, 5000);
        } else {
          log("sa_event is not defined", "warn");
          return callback();
        }
      } catch (error) {
        log(error.message, "warn");
      }
    };

    function onDOMContentLoaded() {
      try {
        var a = document.getElementsByTagName("a");

        // Loop over all links on the page
        for (var i = 0; i < a.length; i++) {
          var link = a[i];

          // Test is a link does start with http:// or https://
          if (!link.getAttribute("onclick")) {
            var collect;
            if (
              options.downloads &&
              /^https?:\/\//i.test(link.href) &&
              new RegExp(
                "\.(" + (options.extensions || []).join("|") + ")",
                "i"
              ).test(link.pathname)
            ) {
              collect = "download";
            } else if (
              options.outbound &&
              /^https?:\/\//i.test(link.href) &&
              link.hostname !== window.location.hostname
            ) {
              collect = "outbound";
            } else if (options.emails && /^mailto:/i.test(link.href)) {
              collect = "email";
            }

            if (collect)
              link.setAttribute(
                "onclick",
                "saAutomatedLink(this, '" + collect + "'); return false;"
              );
          }
        }
      } catch (error) {
        log(error.message, "warn");
      }
    }

    window.addEventListener("DOMContentLoaded", onDOMContentLoaded);
  })(window);
</script>
```

> You can compress above code (after changing the options) via [jscompress.com](https://jscompress.com/).

</details>

It takes care of sending it as an event to Simple Analytics. As events can only be letters, numbers, and underscores we already convert this name.

We love to improve our automated events. Please let us know if you need any help! We don't mind getting our hands dirty.
