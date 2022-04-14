---
title: Install Simple Analytics with Vue
hidden: true
category: integrations
permalink: /install-simple-analytics-with-vue
last_modified_at: 2022-04-14
---

Run this command to install Simple Analytics for Vue:

```bash
npm install simple-analytics-vue
```

## Import Vue in your app

Import the plugin and add it to `Vue.use`. You can add a `skip` option which will define when page views should be skipped. This can be useful if you want to skip page views from yourself when developing your app.

```js
import SimpleAnalytics from "simple-analytics-vue";
import Vue from "vue";

Vue.use(SimpleAnalytics, { skip: process.env.NODE_ENV !== "production" });
```

You can also pass a function or promise to `skip`, which will be validated before injecting the Simple Analytics embed code:

```js
import auth from "lib/auth";
Vue.use(SimpleAnalytics, { skip: auth.isAdminPromise });
```

You can also optionally specify a custom domain to bypass ad blockers. Read more about this in [our documentation](https://docs.simpleanalytics.com/bypass-ad-blockers).

```js
Vue.use(SimpleAnalytics, { domain: "api.example.com" });
```

### Events

To send an event, use the globally available `saEvent` method.

```js
// ~/src/components/Comment.vue
{
  methods: {
    likeComment (comment) {
      // code to like comment
      this.saEvent(`comment_like_${comment.id}`)
    }
  }
```

Note: Simple Analytics does not run on localhost. You can still fire events, but they will be captured and logged in the console for debugging purposes.

## Nuxt.js

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

If you need any additional configuration options (as mentioned above), you need to apply them to your plugin.
