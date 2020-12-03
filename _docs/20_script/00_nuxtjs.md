---
title: Install Simple Analytics with Nuxt.js
category: script
hidden: true
permalink: /install-simple-analytics-with-nuxt
---

Run this command to install Simple Analytics for Vue:

```bash
npm install simple-analytics-vue
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

> If you need any additional configuration options (as the ones mentioned above), you just need to apply to your plugin.

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact).

Special thanks to [Joaquim Ley](https://github.com/simpleanalytics/vue-plugin/pull/8) for writing this guide.
