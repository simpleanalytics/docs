---
title: Install Simple Analytics with Gatsby
hidden: true
category: integrations
permalink: /install-simple-analytics-with-gatsby
last_modified_at: 2022-04-14
---

Run the following command:

```bash
npm install gatsby-plugin-simple-analytics --save-dev
```

## What does it do

It tracks page views with support for `pushState` navigation. It sends the data to [Simple Analytics](https://simpleanalytics.com) and it will be available in your dashboard. You need to have a paid subscription for it to work.

## How to use

1. Add our plugin to `gatsby-config.js`

   ```js
   plugins: [
     {
       resolve: "gatsby-plugin-simple-analytics",
       options: {
         trackPageViews: true,
       },
     },
   ];
   ```

1. If you want to set a custom domain, use this config:

   ```js
   plugins: [
     {
       resolve: "gatsby-plugin-simple-analytics",
       options: {
         domain: "custom.example.com",
         eventsGlobal: "sa",
         events: true,
         trackPageViews: true,
         ignorePages: ["pathname"],
       },
     },
   ];
   ```

   [Read our docs](https://docs.simpleanalytics.com/bypass-ad-blockers) on the custom domain feature.

## Use with Confirmic

[Confirmic](https://confirmic.com/) provides a privacy-by-design API to ethically manage your users' data. It's pretty cool.

If you want to use it with Confirmic's `data-micropolicy` use this config:

```js
plugins: [
  {
    resolve: "gatsby-plugin-simple-analytics",
    options: {
      metomic: "POLICY-SLUG",
    },
  },
];
```

It will result in something like this:

```html
<script src="https://scripts.simpleanalyticscdn.com/latest.js" async="" defer="" type="text/x-metomic" data-micropolicy="POLICY-SLUG">
```
