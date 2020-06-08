---
title: Install Simple Analytics with the Analytics library
menu: Install via `analytics`
category: script
hidden: true
permalink: /install-simple-analytics-via-analytics-package
---

You can install Simple Analytics using the open source Analytics library ([website](https://getanalytics.io), [npm](https://www.npmjs.com/package/analytics)). It's a pluggable library designed as an abstraction layer to easily customize the analytics requirements of your app.

## Install via npm

```
npm install analytics analytics-plugin-simple-analytics
```

## Using the Analytics library

The Analytics library works with any frontend framework including `react`, `vue`, `angular` or static `html`.

To use it:

1. Import the `analytics` library and `analytics-plugin-simple-analytics`
2. Initialize the `analytics` library
3. Page views get tracked automatically
4. Include the non javascript fallback in your `html`

Example code:

```js
/* src/analytics.js */
import Analytics from "analytics";
import simpleAnalyticsPlugin from "analytics-plugin-simple-analytics";

const analytics = Analytics({
  app: "awesome-app",
  plugins: [
    // Load simple analytics! 🎉
    simpleAnalyticsPlugin(),
  ],
});

/* All page views are now tracked by simple analytics */
```

Make sure to include this file in the entry point of your application. This will ensure the Analytics library and Simple Analytics scripts load correctly.

When the Analytics library initialized it will automatically load the simple analytics script onto the page.

For additional instructions on how to use with other frontend frameworks, checkout the [Analytics library docs](https://getanalytics.io/tutorial/getting-started/)

## Include Non JS enabled browser fallback

Remember to include the `noscript` image tag in your HTML for JS disabled browsers.

Include this line at the end of your `<body>`

```
<noscript><img src="https://queue.simpleanalyticscdn.com/hello.gif" alt=""></noscript>
```

## View the source

You can view the source code of this plugin on [GitHub](https://github.com/DavidWells/analytics/tree/master/packages/analytics-plugin-simple-analytics)

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact?ref={{ site.hostname }}).
