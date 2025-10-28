---
title: Install Simple Analytics with Nuxt
hidden: true
category: integrations
permalink: /install-simple-analytics-with-nuxt
last_modified_at: 2025-10-24
---

Easily add privacy-friendly pageview and event tracking to your Nuxt 3 or 4 app with the Simple Analytics Nuxt module.

## Installation

```bash
npm i @simpleanalytics/nuxt
```

## Environment Variables

Set your website domain (the same as in your [Simple Analytics dashboard](https://dashboard.simpleanalytics.com/)):

```bash
SIMPLE_ANALYTICS_HOSTNAME=example.com
```

> Omit `www.` Use only the root domain, or include the subdomain if applicable, like `sub.example.com`.

## Configuration

Add the module to your `nuxt.config.ts` and optionally define your hostname:

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  // ...
  modules: ["@simpleanalytics/nuxt"],
  simpleAnalytics: {
    // optional, uses SIMPLE_ANALYTICS_HOSTNAME if not set
    // hostname: "example.com",
  },
});
```

## Usage

### Client-side analytics

The module automatically injects the Simple Analytics script through the `simple-analytics-vue` plugin.

### Tracking events in client components

To track custom events, use the injected `saEvent` function:

```vue
<script setup>
import { inject } from "vue";

const saEvent = inject("saEvent");

// e.g.: send event when liking a comment
const likeComment = (comment) => {
  saEvent(`comment_like_${comment.id}`);
};
</script>
```

### Server-side tracking (SSR & API)

You can track pageviews and events from the server during SSR or within Nitro API routes.

#### In server-rendered pages

```vue
<script setup lang="ts">
if (import.meta.server) {
  await trackPageview({
    some_extra_metadata: "homepage"
  });
}
</script>
```

#### In Nitro API routes

```ts
// server/api/signup.post.ts
export default defineEventHandler(async (event) => {
  await trackEvent(event, "user_signup", {
    source: "registration_form",
    user_type: "new",
  });

  // ...
});
```

## API Reference (Nuxt)

### `trackPageview(options)`

Tracks a pageview on the server.

#### Parameters

- `metadata` (object): Additional metadata to track (optional)

### `trackEvent(eventName, options)`

Tracks a custom event on the server.

#### Parameters

- `eventName` (string): Name of the event to track
- `metadata` (object): Additional metadata to track (optional)

## API Reference (Nitro)

### `trackEvent(event, eventName, options)`

Tracks a custom event in a Nitro API route.

#### Parameters

- `event` (H3Event): Nitro request event
- `eventName` (string): Name of the event to track
- `metadata` (object): Additional metadata to track (optional)