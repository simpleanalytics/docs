---
title: Automated events
category: events
permalink: /automated-events
redirect_from:
  - /capture-outbound-links
---

[Normal events](/events) need to be added into your code. To make it easier we created a separate automated events script. This script has to be installed once, and it will track outbound links, email addresses clicks, and amount of download for certain files. Events will appear on [your events page](https://simpleanalytics.com/select-website/events).

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

> This script is additional to the normal embed script. Make sure to also include [that script](/script).

If you are a developer or you know your way around HTML it's easy to embed this script on your website. If you need help with that, we are happy to help. Just [contact us](https://simpleanalytics.com/contact).

<!-- prettier-ignore -->
```html
<script>
(function(a){
  var options = {
    // What to collect
    outbound: true,
    emails: true,
    downloads: true,
    // Downloads: enter file extensions you want to collect
    downloadsExtensions: ["pdf", "csv", "docx", "xlsx"],

    // All: use title attribute if set for event name (for all events)
    // THIS TAKES PRECEDENCE OVER OTHER SETTINGS BELOW
    title: true,
    // Outbound: use full URL of the links? false for just the hostname
    outboundFullUrl: false,
    // Downloads: if taking event name from URL, use full URL or just filename (default)
    downloadsFullUrl: false,
  };

  function b(){try{for(var b,e=document.getElementsByTagName("a"),f=0;f<e.length;f++)if(b=e[f],!b.getAttribute("onclick")){var g;if(d.downloads&&/^https?:\/\//i.test(b.href)&&new RegExp(".("+(d.downloadsExtensions||[]).join("|")+")","i").test(b.pathname)?g="download":d.outbound&&/^https?:\/\//i.test(b.href)&&b.hostname!==a.location.hostname?g="outbound":d.emails&&/^mailto:/i.test(b.href)&&(g="email"),g)var h="saAutomatedLink(this, '"+g+"');";b.hasAttribute("target")&&"_self"!==b.hasAttribute("target")||(h+=" return false;"),b.setAttribute("onclick",h)}}catch(a){c(a.message,"warn")}}if("undefined"!=typeof a){var c=function(a,b){var c="warn"===b?console.warn:console.log;return c("Simple Analytics automated events: "+a)},d=options;"undefined"==typeof d&&c("options object not found, please specify","warn"),a.saAutomatedLink=function(b,e){try{if(!b)return c("no element found");var f=!1,g=function(){f||b.hasAttribute("target")||(document.location=b.getAttribute("href")),f=!0};if(a.sa_event){var h=b.hostname,i=b.pathname,j=!1;if(d.title&&b.hasAttribute("title")){var k=b.getAttribute("title").trim();""!=k&&(j=!0)}var l;if(j)l=k;else switch(e){case"outbound":{l=h+(d.outboundFullUrl?i:"");break}case"download":{l=d.downloadsFullUrl?h+i:i.split("/").pop();break}case"email":{var m=b.getAttribute("href");l=(m.split(":")[1]||"").split("?")[0];break}}var n=e+"_"+l.replace(/[^a-z0-9]+/gi,"_").replace(/(^_+|_+$)/g,"");return sa_event(n,g),c("collected "+n),a.setTimeout(g,5e3)}return c("sa_event is not defined","warn"),g()}catch(a){c(a.message,"warn")}},a.addEventListener("DOMContentLoaded",b)}
})(window);
</script>
```

The script is compressed with the public tool [jscompress.com](https://jscompress.com/).

<details markdown="1">
<summary>The non-minified version of the above script</summary>

```html
<script>
  (function saAutomatedEvents(window) {
    // Skip server side rendered pages
    if (typeof window === "undefined") return;

    var options = {
      // What to collect
      outbound: true,
      emails: true,
      downloads: true,
      // Downloads: enter file extensions you want to collect
      downloadsExtensions: ["pdf", "csv", "docx", "xlsx"],

      // All: use title attribute if set for event name (for all events)
      // THIS TAKES PRECEDENCE OVER OTHER SETTINGS BELOW
      title: true,
      // Outbound: use full URL of the links? false for just the hostname
      outboundFullUrl: false,
      // Downloads: if taking event name from URL, use full URL or just filename (default)
      downloadsFullUrl: false,
    };

    var log = function (message, type) {
      var logger = type === "warn" ? console.warn : console.log;
      return logger("Simple Analytics automated events: " + message);
    };

    // For minifying the script
    var optionsLink = options;

    if (typeof optionsLink === "undefined")
      log("options object not found, please specify", "warn");

    window.saAutomatedLink = function saAutomatedLink(element, type) {
      try {
        if (!element) return log("no element found");
        var sent = false;

        var callback = function () {
          if (!sent && !element.hasAttribute("target"))
            document.location = element.getAttribute("href");
          sent = true;
        };

        if (window.sa_event) {
          var hostname = element.hostname;
          var pathname = element.pathname;
          var useTitle = false;
          if (optionsLink.title && element.hasAttribute("title")) {
            var theTitle = element.getAttribute("title").trim();
            if (theTitle != "") useTitle = true;
          }

          var event;

          if (useTitle) {
            event = theTitle;
          } else {
            switch (type) {
              case "outbound": {
                event =
                  hostname + (optionsLink.outboundFullUrl ? pathname : "");
                break;
              }
              case "download": {
                event = optionsLink.downloadsFullUrl
                  ? hostname + pathname
                  : pathname.split("/").pop();
                break;
              }
              case "email": {
                var href = element.getAttribute("href");
                event = (href.split(":")[1] || "").split("?")[0];
                break;
              }
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

          // We don't want to overwrite website behaviour so we check for the onclick attribute
          if (!link.getAttribute("onclick")) {
            var collect;

            // Collect download clicks
            if (
              optionsLink.downloads &&
              /^https?:\/\//i.test(link.href) &&
              new RegExp(
                "\.(" + (optionsLink.downloadsExtensions || []).join("|") + ")",
                "i"
              ).test(link.pathname)
            ) {
              collect = "download";

              // Collect outbound links clicks
            } else if (
              optionsLink.outbound &&
              /^https?:\/\//i.test(link.href) &&
              link.hostname !== window.location.hostname
            ) {
              collect = "outbound";

              // Collect email clicks
            } else if (optionsLink.emails && /^mailto:/i.test(link.href)) {
              collect = "email";
            }

            if (collect)
              var onClickAttribute =
                "saAutomatedLink(this, '" + collect + "');";

            if (
              !link.hasAttribute("target") ||
              link.hasAttribute("target") === "_self"
            )
              onClickAttribute += " return false;";

            link.setAttribute("onclick", onClickAttribute);
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

> When you test with this script, note that it uses the `DOMContentLoaded` event. This event only fires when the script has been added before the page has loaded. If you want to test the script in your console make sure to replace <code>window.addEventListener("DOMContentLoaded", onDOMContentLoaded);</code> with `onDOMContentLoaded()`.

It takes care of sending it as an event to Simple Analytics. As events can only be letters, numbers, and underscores we already convert this name.

We love to improve our automated events. Please let us know if you need any help! We don't mind getting our hands dirty.
