---
title: Trigger custom page views
category: install-script
permalink: /trigger-custom-page-views
last_modified_at: 2026-10-29
---

Normally you want to trigger a custom page view for _Single Page Apps_ (SPAs) like React, Vue, and Angular. Because pages are not completely reloaded on navigation we need a way to track those navigations as page views.

For some analytics tools like Google Analytics you need to trigger a page view via their script. For Simple Analytics this is different.

> With Simple Analytics there is **no** need to implement anything to detect page views in SPAs. It all works out of the box.

<details>
<summary>Technical explanation</summary>
<div markdown="1">

We make this work by overwriting the native `pushState`-function of the browser. We also listen to the `popstate` event, so back and forward navigation in your app is collected as well.

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

There might be a situation where you don't want to auto collect page views. When you add the `data-auto-collect="false"` attribute, the script doesn't send page views by itself and you send them with the `sa_pageview` function. When you call this function, the script will send a page view with the path you give as a parameter. If you don't give a path it will use `window.location.pathname` as a default. This only works with `latest.js`, not with our [light script](/light).

```html
<script>
  function saLoaded() {
    // Always check for the function before using it.
    // The script might be blocked or not loaded for other reasons.
    if (window.sa_pageview) window.sa_pageview(window.location.pathname);
  }
</script>

<script
  async
  data-auto-collect="false"
  onload="saLoaded()"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
></script>
<noscript
  ><img
    src="https://queue.simpleanalyticscdn.com/noscript.gif"
    alt=""
    referrerpolicy="no-referrer-when-downgrade"
/></noscript>
```

You can add [metadata](/metadata) to the page view with a second argument:

```js
window.sa_pageview("/pricing", { plan: "pro" });
```

If you call `sa_pageview` with the same path as the previous page view, we don't send it again.

From script version 12:

- `sa_pageview` is also available when we collect page views automatically.
- You can pass a callback as the last argument. It runs after the page view is sent, and also when we skip it (for example, for the same path or an [ignored page](/ignore-pages)):

  ```js
  window.sa_pageview("/pricing", { plan: "pro" }, function () {
    window.location.href = "/checkout";
  });
  ```

- You can add a query string to the path, for example `/pricing?utm_source=newsletter`. We treat it like the query string of a normal page view. The same path with a different query string counts as a new page view.
- With a [custom namespace](/events#the-variable-sa_event-is-already-used), the function uses that namespace, for example `ba_pageview`. `sa_pageview` stays available unless your website already uses that name.

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact).
