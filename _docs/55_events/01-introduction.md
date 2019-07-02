---
title: Introduction to events
menu: Introduction
category: events
category_order: 10
order: 1
permalink: /events
---

<blockquote class="red">
  <p>This page is not published yet and is a work in progress. <b>Please don't share.</b></p>
</blockquote>

If you haven't already done so, to start working with events you need to first install the embed script.

{% comment %}
```html
<script>
!function(s,i,m,p,l,e){(s.SimpleAnalyticsFunction=p)in s||(s.sa=s.sa||function(){
s.sa.q.push(arguments)},s.sa.q=[]),(l=i.createElement("script")).src=m,
l.async=!0,(e=i.getElementsByTagName('script')[0]).parentNode.insertBefore(l,e)
}(window,document,'//www.simpleanalyticscdn.com/app.js','sa');
</script>
```
{% endcomment %}

```html
<script>window.sa=window.sa||function(){a=[].slice.call(arguments);sa.q?sa.q.push(a):sa.q=[a]};</script>
<script async defer src="https://[YOUR SUBDOMAIN LINKING TO US]/e.js"></script>
```

> **Developers:** place this script in the `<head>` or top part of your `<body>` in your html.

This little snippet creates a simple function called `sa`. After that it loads the Simple Analytics script asynchronously (it does not have an effect on your page load).

The `sa`-function is the function you'll need to use to create events. To track an event it's as simple as this:

```js
sa('click_signup')
```

In the background we add the referrer to every event. So in the tool you can select the referrer with every event. We also save the date (`YYYY-MM-DD`) of the first event, which we will use to match the events with the previous events.

### Valid event names

We want to keep events very simple. That's why we only allow certain characters: alphanumeric, `.`, `_`, `-`. We convert events to lower case and invalid names to a version which is valid. This way your events are always saved.

## What we store about a visitor

When you use events (which is completely optional), we use [sessionStorage](https://en.wikipedia.org/wiki/Web_storage) to store the past events of a user. From now on we use the more general term cookie. Make sure to have permission from your visitor to use cookies before using events.

> The cookie will be cleared when a browser closes (session ends)

<details>
  <summary>How to wait for cookie permissions of the visitor</summary>

  <div markdown="1">
If you're using a cookie permission (which you are required to do in the EU), you can tell us not to set a cookie until you have permission.

Here is an example code:

```html
<script>window.sa=window.sa||function(){a=[].slice.call(arguments);sa.q?sa.q.push(a):sa.q=[a]};</script>
<script async defer src="https://[YOUR SUBDOMAIN LINKING TO US]/e.js"></script>
<script>
  // Cookie is not yet set
  sa('sa_cookie', false)

  // Events happen (they are sent to Simple Analytics)
  sa('signup')

  // User approves cookie (Simple Analytics will set a cookie)
  sa('sa_cookie', true)
</script>
```
  </div>
</details>

This way you can still have events before the approval of a visitor but they don't survive page reloads. So make sure to have permission on the first page the visitor lands.

For example, if a user came from Google on May 18, 2019, clicked on the FAQ, and the next day returned again to sign up, the cookie would look like this:

```js
[
  { v: 1, ref: 'google.com', date: '2019-05-18' },
  ['click_faq'],
  ['click_faq', 1],
  ['click_signup', 1]}
]
```

There is no personally identifiable information in the cookie whatsoever. We want to keep it that way. After every event we send the contents of the cookie to our server and update the row that matches the path of events (minus the last event). This way we don't need to have any personally identifiable information.

<details markdown="1">
<summary>Read more in depth how our matching works</summary>
<div markdown="1">
We will add more information here.
</div>
</details>

## The variable `sa` is already used

If the `sa` variable is already in use you can change it with the `data-sa-global` attribute:

```html
<script>window.ba=window.ba||function(){a=[].slice.call(arguments);ba.q?ba.q.push(a):ba.q=[a]};</script>
<script async defer data-sa-global="ba" src="https://[YOUR SUBDOMAIN LINKING TO US]/e.js"></script>
```


{% comment %}
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

{% endcomment %}
