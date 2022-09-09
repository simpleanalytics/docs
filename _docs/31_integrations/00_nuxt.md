---
title: Install Simple Analytics with Nuxt 3
hidden: true
category: integrations
permalink: /install-simple-analytics-with-nuxt
last_modified_at: 2022-09-09
---

Run this command to install Simple Analytics for Vue:

```bash
npm install simple-analytics-vue
```

## Nuxt 3

```js
import SimpleAnalytics from 'simple-analytics-vue'

export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.vueApp.use(SimpleAnalytics, {
    skip: process.env.NODE_ENV !== "production",
    domain: "api.example.com"
  })
})
```

## Nuxt 2

Create a file in your plugin folder with the name `simple-analytics.js`:

```js
// ~/plugins/simple-analytics.js

import SimpleAnalytics from "simple-analytics-vue";
import Vue from "vue";

Vue.use(SimpleAnalytics, { skip: process.env.NODE_ENV !== "production" });
```

Then on your `nuxt.config.js`, make sure to include the plugin with `ssr: false` as we only want to run it on the client:

```js
// nuxt.config.js

export default {
  plugins: [{ src: "~/plugins/simple-analytics.js", ssr: false }],
};
```
