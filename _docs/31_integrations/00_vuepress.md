---
title: Install Simple Analytics with VuePress
hidden: true
category: integrations
permalink: /install-simple-analytics-with-vuepress
---

Run this command to install Simple Analytics for [VuePress](https://vuepress.vuejs.org/):

```bash
npm install vuepress-plugin-simple-analytics --save-dev
```

## Add the plugin

Add the plugin to your plugins in `.vuepress/config.js`.

```js
module.exports = {
  plugins: ["vuepress-plugin-simple-analytics"],
};
```

## More features

We have more features like a [custom domain](https://docs.simpleanalytics.com/bypass-ad-blockers) to bypass ad-blockers, [events](https://docs.simpleanalytics.com/events), and [allow the collect from DNT users](https://docs.simpleanalytics.com/dnt). Events are enabled by default.

```js
module.exports = {
  plugins: [
    [
      "vuepress-plugin-simple-analytics",
      {
        customDomain: "data.example.com", // You custom domain
        eventsGlobal: "sa", // The global events object for sa("click_button")
        skipDnt: true, // When set to true you track the DNT users
      },
    ],
  ],
};
```
