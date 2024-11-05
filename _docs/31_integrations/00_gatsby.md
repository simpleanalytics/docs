---
title: Install Simple Analytics with Gatsby
hidden: true
category: integrations
permalink: /install-simple-analytics-with-gatsby
last_modified_at: 2024-11-05
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
   ]
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
   ]
   ```

   [Read our docs](https://docs.simpleanalytics.com/bypass-ad-blockers) on the custom domain feature.
