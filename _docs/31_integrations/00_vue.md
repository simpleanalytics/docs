---
title: Install Simple Analytics with Vue.js
hidden: true
category: integrations
permalink: /install-simple-analytics-with-vue
last_modified_at: 2026-11-13
description: "Installation document to get website traffic by Simple Analytics for Vue.js"
---

Run this command to install Simple Analytics for Vue 3:

```bash
npm install simple-analytics-vue
```

Are you using Vue 2? Install version 2 with `npm install simple-analytics-vue@2.x`. It doesn't get updates anymore.

## Add the plugin to your app

Import the plugin and add it to your app with `app.use`. You can add a `skip` option which will define when page views should be skipped. This can be useful if you want to skip page views from yourself when developing your app.

```js
import { createApp } from "vue";
import SimpleAnalytics from "simple-analytics-vue";
import App from "./App.vue";

const app = createApp(App);
app.use(SimpleAnalytics, { skip: process.env.NODE_ENV !== "production" });
app.mount("#app");
```

You can also pass a function or promise to `skip`, which will be validated before injecting the Simple Analytics embed code:

```js
import auth from "lib/auth";
app.use(SimpleAnalytics, { skip: auth.isAdminPromise });
```

You can also optionally specify a custom domain to bypass ad blockers. Read more about this in [our documentation](https://docs.simpleanalytics.com/bypass-ad-blockers).

```js
app.use(SimpleAnalytics, { domain: "api.example.com" });
```

### Events

To send an event, inject the `saEvent` function in your component:

```vue
<!-- ~/src/components/Comment.vue -->
<script setup>
import { inject } from "vue";

const saEvent = inject("saEvent");

// e.g.: send event when liking a comment
const likeComment = (comment) => {
  saEvent(`comment_like_${comment.id}`);
};
</script>
```

Note: Simple Analytics does not run on localhost. You can still fire events, but they will be captured and logged in the console for debugging purposes.

## Nuxt

Use our [Nuxt module](/install-simple-analytics-with-nuxt).
