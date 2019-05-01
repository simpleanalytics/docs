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
<script>window.sa=window.sa||function(){a=arguments;sa.q?sa.q.push(a):sa.q=[a]};</script>
<script async defer src="https://www.simpleanalyticscdn.com/app.js"></script>
```

> **Developers** place this script right in the `<head>` or top part of your `<body>` in your html.

This little snippet creates a simple function called `sa`. After that it loads the Simple Analytics script asynchronously (it does not have an effect on your page load).

The `sa`-function is the function you'll need to use to create events. To track an event it's as simple as this:

```js
sa('click_signup')
```

In the background we add the referrer to every event. So in the tool you can select the referrer with every event. We also save the day of the first event, which we will use to match the events with the previous events.

## What we store about a visitor

When you use events (this is completely optional) we use a cookie. Make sure to have permission to use this cookie from the user before running our script.

<details>
  <summary>How to wait for cookie permissions of the visitor</summary>

  <div markdown="1">
If you're using a cookie permission (and you are required to do so in the EU), you tell us not set a cookie until you have permission.

Here is an example code of that:

```html
<script>window.sa=window.sa||function(){a=arguments;sa.q?sa.q.push(a):sa.q=[a]};</script>
<script async defer src="https://www.simpleanalyticscdn.com/app.js"></script>
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

When a user came from Google on May 18, 2019 and clicked on the FAQ and after that signed up the cookie would look like this:

```js
[
  { ref: 'google.com', date: '2019-05-18' },
  { name: 'click_faq' },
  { name: 'click_signup' }
]
```

There is no personally identifiable information in the cookie whatsoever. We want to keep it that way. After every event we send the contents of the cookie to our server and update the row that matches the path of events (minus the last event). This way we don't need to have any personal identifiable information.

<details markdown="1">
<summary>Read more in depth how our matching works</summary>
<div markdown="1">
lalalal
</div>
</details>

## The variable `sa` is already used

If the `sa` variable is already in use you can change it with the `data-sa-global` attribute:

```html
<script>window.ba=window.ba||function(){a=arguments;ba.q?ba.q.push(a):ba.q=[a]};</script>
<script async defer data-sa-global="ba" src="https://www.simpleanalyticscdn.com/app.js"></script>
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
