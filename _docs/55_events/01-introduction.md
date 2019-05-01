---
title: Introduction to events
menu: Introduction
category: events
category_order: 10
order: 1
permalink: /events
---

> This page is not published yet and is a work in progress

To start working with events you need (or maybe already have) to install the embed script.


```html
<script>window.sa=window.sa||function(){a=arguments;sa.q?sa.q.push(a):sa.q=[a]};</script>
<script async defer src="https://www.simpleanalyticscdn.com/app.js"></script>
```

> For developers: Place this script right in the `<head>` or top part of your `<body>` in your html.

This little snipped creates a simple function called `sa`. After that it loads the Simple Analytics script asynchronously (it does not have an effect on your page load).

The `sa`-function is the function you'll need to use to create events. To track an event it's as simple as this:

```js
sa('click_signup')
```

In the background we add the referrer to every event. So in the tool you can select the referrer with every event. We also save the day of the first event, which we will use to match the events with the previous events.

## What we store about a visitor

When you use events (this is completely optional) we use a cookie. Make sure to have permission to use this cookie from the user before running our script.

...

## How to wait for cookie permissions of the visitor

If you're using a cookie permission (and you are required to do so in the EU), you tell us not set a cookie until you have permission.

Here is an example code of that:

```html
<script>window.sa=window.sa||function(){a=arguments;sa.q?sa.q.push(a):sa.q=[a]};</script>
<script async defer src="https://www.simpleanalyticscdn.com/app.js"></script>
<script>
  // Cookie is not yet set
  sa('sa_cookie', false)

  // Events happen (they are send to Simple Analytics)
  sa('signup')

  // User approves cookie (Simple Analytics will set a cookie)
  sa('sa_cookie', true)
</script>
```

## The variable `sa` is already used

If that is the case, you can change it with the `data-sa-global` attribute:

```html
<script>window.ba=window.ba||function(){a=arguments;ba.q?ba.q.push(a):ba.q=[a]};</script>
<script async defer data-sa-global="ba" src="https://www.simpleanalyticscdn.com/app.js"></script>
```


<details markdown="1">
  <summary>The embed script explained for developers</summary>

```js
(function(window, document, hostname, functionName, script, firstScript) {
  // Store the name of the Analytics object
  window.SimpleAnalyticsFunction = functionName

  // Check whether the Analytics object is defined
  if (!(functionName in window)) {

    // Define the Analytics object
    window[functionName] = window[functionName] || function() {

      // Add the tasks to the queue
      window[functionName].q.push(arguments)
    }

    // Create the queue
    window[functionName].q = []
  }

  // Create a new script element
  script   = document.createElement('script')
  script.src   = '//' + hostname + '/app.js'
  script.async = true

  // Insert the script element into the document
  firstScript = document.getElementsByTagName('script')[0]
  firstScript.parentNode.insertBefore(script, firstScript)

})(window, document, 'www.simpleanalyticscdn.com', 'sa')
```
</details>
