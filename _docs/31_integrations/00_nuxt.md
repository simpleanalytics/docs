---
title: Install Simple Analytics with Nuxt 3
hidden: true
category: integrations
permalink: /install-simple-analytics-with-nuxt
last_modified_at: 2023-03-03
---

We have a package that works with both Nuxt 2 and Nuxt 3.

## Nuxt 3

Run this command to install Simple Analytics for Vue:

```bash
npm install simple-analytics-vue --save-dev
```

Create a file called `plugins/simpleanalytics.client.js`:

```js
import SimpleAnalytics from "simple-analytics-vue";

export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.vueApp.use(SimpleAnalytics);
});
```

That's it! Continue only if you want to go advanced.

If you want to skip your own visits on development:

```js
import SimpleAnalytics from "simple-analytics-vue";

export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.vueApp.use(SimpleAnalytics, {
    skip: process.env.NODE_ENV !== "production",
  });
});
```

If you have a [custom domain for bypassing ad-blockers](/bypass-ad-blockers) set up, use this:

```js
import SimpleAnalytics from "simple-analytics-vue";

export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.vueApp.use(SimpleAnalytics, {
    skip: process.env.NODE_ENV !== "production",
    domain: "api.example.com"
  });
});
```

## Nuxt 2

Run this command to install Simple Analytics for Vue:

```bash
npm install simple-analytics-vue@2.x --save-dev
```

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
