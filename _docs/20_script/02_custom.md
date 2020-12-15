---
title: Trigger custom page views
category: script
permalink: /trigger-custom-page-views
---

Normally you want to trigger a custom page view for _Single Page Apps_ (SPA's) like React, Vue, and Angular. Because pages are not completely reloaded on navigation we need a way to track those navigations as page views.

For some analytics tools like Google Analytics you need to trigger a page view via their script. For Simple Analytics this is different.

> With Simple Analytics there is **no** need to implement anything to detect page views in SPA's. It all works out of the box.

<details markdown="1">
<summary>Technical explanation</summary>
<div markdown="1">

We make this work by overwriting the native `pushState`-function of the browser.

```js
// We check if the browser supports pushState
if (history.pushState && Event && dispatchEvent) {
  // We create a listener based on the original browser feature
  var stateListener = function (type) {
    var orig = history[type];
    return function () {
      var rv = orig.apply(this, arguments);
      var event = new Event(type);
      event.arguments = arguments;
      dispatchEvent(event);
      return rv;
    };
  };

  // We connect our own created a listener to the pushState feature
  history.pushState = stateListener("pushState");

  // Now we can listen for pushState events and keep the original feature of the browser working
  window.addEventListener("pushState", function () {
    // Here we trigger the page view
  });
}
```

You can read our source code [on GitHub](https://github.com/simpleanalytics/scripts/blob/4ad5c1b6cb4c42ae2e483dc43a578e25399d53a4/src/default.js#L120-L137).

</div>
</details>

## Use custom collection anyway

There might be situation where you don't want to auto collect page views. When you add the `data-auto-collect="false"` attribute you can expose a function called `sa_pageview`. When you call this fuction the script will send a page with the path you give as a parameter. If you don't give a path it will use `window.location.pathname` as a default.

```html
<script>
  function saLoaded() {
    // Always check for the function before using it.
    // The script might be blocked or not loaded for other reasons.
    if (window.sa_pageview) window.sa_pageview(window.location.pathname);
  }
</script>

<script async defer data-auto-collect="false" onload="saLoaded()" src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
```

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact).
