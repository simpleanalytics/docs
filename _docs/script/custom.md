---
title: Trigger custom page views
category: script
category_order: 3
order: 2
permalink: /trigger-custom-page-views
---

Normally you want to trigger a custom page view for _Single Page Apps_ (SPA's) like React, Vue, and Angular. Because pages are not completely reloaded on navigation we need a way to track those navigations as page views.

For some analytics tools like Google Analytics you need to trigger a page view via their script. For Simple Analytics this is different.

> You **don't** have to implement anything to detect page views in SPA's

## Technical explanation

We make this work by overwriting the native `pushState`-function of the browser.

```js
// We check if the browser supports pushState
if (history.pushState && Event && dispatchEvent) {

  // We create a listener based on the original browser feature
  var stateListener = function(type) {
    var orig = history[type]
    return function() {
      var rv = orig.apply(this, arguments)
      var event = new Event(type)
      event.arguments = arguments
      dispatchEvent(event)
      return rv
    }
  }

  // We connect our own created a listener to the pushState feature
  history.pushState = stateListener('pushState')

  // Now we can listen for pushState events and keep the original feature of the browser working
  window.addEventListener('pushState', function() {
    // Here we trigger the page view
  })
}
```

You can read our source code [on GitHub](https://github.com/simpleanalytics/cdn/blob/849c8237ced90683b410d389ef6d114758e6d1db/hello.js#L81-L98).
