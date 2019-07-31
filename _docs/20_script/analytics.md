---
title: Install Simple Analytics with the open source analytics package
menu: Install via `analytics`
category: script
category_order: 2
order: 5
hidden: true
permalink: /install-simple-analytics-via-analytics-package
---

You can install and using simple analytics using the open source [analytics](https://getanalytics.io) package.

[Analytics](https://www.npmjs.com/package/analytics) is a pluggable library designed as an abstraction layer to easily customize the analytics requirements of your app.

## Install via npm

```
npm install analytics
npm install analytics-plugin-simple-analytics
```

Or install via `yarn`

```
yarn add analytics
yarn add analytics-plugin-simple-analytics
```

## Using `analytics`

Analytics works with any frontend framework including `react`, `vue`, `angular` or static `html`. 

To use it: 

1. Import the `analytics` library and `analytics-plugin-simple-analytics`
2. Initialize the `analytics` library
3. Page views get tracked automatically 😎
4. Include the non javascript fallback in your `html`

Example code:

```js
/* src/analytics.js */
import Analytics from 'analytics'
import simpleAnalyticsPlugin from 'analytics-plugin-simple-analytics'

const analytics = Analytics({
  app: 'awesome-app',
  plugins: [
    // Load simple analytics! 🎉
    simpleAnalyticsPlugin(),
  ]
})

/* All page views are now tracked by simple analytics */
```

Make sure to include this file in the entry point of your application. This will ensure analytics & simple analytics scripts load correctly.

When the `analytics` library initialized it will automatically load the simple analytics script onto the page.

For additional instructions on how to use with other frontend frameworks, checkout the [analytics docs](https://getanalytics.io/tutorial/getting-started/)

## Include Non JS enabled browser fallback

Remember to include the `noscript` image tag in your HTML for JS disabled browsers.

Include this line at the end of your `<body>`

```
<noscript><img src="https://api.simpleanalytics.io/hello.gif" alt=""></noscript>
```
