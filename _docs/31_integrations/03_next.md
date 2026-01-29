---
title: Install Simple Analytics with Next.js
menu: Next.js
category: integrations
permalink: /install-simple-analytics-with-next
last_modified_at: 2024-01-15
---

We recommend using the official **Simple Analytics for Next.js** plugin (`@simpleanalytics/next`). It provides cookie-less analytics, request proxying to avoid ad blockers, and event tracking on both client and server.

Documentation source: [simpleanalytics-next-docs.vercel.app](https://simpleanalytics-next-docs.vercel.app/docs).

## Quick Start

### Introduction

Simple Analytics for Next.js lets you add privacy first web analytics and event tracking to your Next.js site in a few steps.

The library provides:

- **No cookie banner required** — Cookie-less analytics, no personal data about visitors is stored.
- **Proxying analytics requests** — Analytics requests are proxied to prevent interference by ad blockers.
- **Track events** — Track custom events with metadata, both on the client and server.
- **Server-side tracking support** — Track pageviews on the server without client code using Middleware.

### Install the package

```bash
npm i @simpleanalytics/next
```

### Configure environment variables

Add the website domain you use in the [Simple Analytics dashboard](https://dashboard.simpleanalytics.com/) as environment variables:

```env
NEXT_PUBLIC_SIMPLE_ANALYTICS_HOSTNAME=example.com
SIMPLE_ANALYTICS_HOSTNAME=example.com
```

### Update Next.js config

The `withSimpleAnalytics` plugin enables proxying of client-side tracking requests and improves accuracy for server-side tracking.

In your project root, update `next.config.ts` (or `next.config.mjs` / `next.config.js`):

```js
import type { NextConfig } from "next";
import withSimpleAnalytics from "@simpleanalytics/next/plugin";

const nextConfig = {
  /* your existing config */
};

export default withSimpleAnalytics(nextConfig);
```

### Add the SimpleAnalytics component in your layout (optional)

The `SimpleAnalytics` component is required for **client-side** tracking. For **server-side** tracking only, see [Tracking Pageviews](#tracking-pageviews) and [Tracking Events](#tracking-events).

The component injects the Simple Analytics script so pageviews are collected:

```jsx
// app/layout.js
import { SimpleAnalytics } from "@simpleanalytics/next";

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        {children}
        <SimpleAnalytics />
      </body>
    </html>
  );
}
```

You should then see visitor metrics in the [Simple Analytics dashboard](https://dashboard.simpleanalytics.com/).

---

## Tracking Pageviews

The `trackPageview` function lets you track pageviews manually, e.g. to add metadata such as whether the user is signed in.

### Disabling automatic pageview collection

The `SimpleAnalytics` component collects pageviews automatically. For manual tracking, disable auto collection to avoid duplicate pageviews by setting `autoCollect` to `false`:

```jsx
<SimpleAnalytics autoCollect={false} />
```

### Tracking pageviews server-side

Simple Analytics infers the visitor’s country from their time zone. On the server you don’t have that by default, but some hosts (e.g. [Vercel](https://vercel.com/docs/edge-network/headers/request-headers), [Cloudflare](https://developers.cloudflare.com/rules/transform/managed-transforms/reference/), [Amazon CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/adding-cloudfront-headers.html)) send the visitor’s time zone in request headers. If present, it is included in the data sent to Simple Analytics unless you ignore it.

#### Usage in Edge Middleware

Tracking pageviews in middleware is **experimental** and does not support the same functionality as client-side tracking.

You can add pageview tracking app-wide with `trackPageview` and Next.js Edge Middleware:

```js
// middleware.js
import { NextResponse } from "next/server";
import { trackPageview } from "@simpleanalytics/next/server";

export function middleware(request, event) {
  event.waitUntil(trackPageview({ request }));
  return NextResponse.next();
}

export const config = {
  matcher: [
    /*
     * Match all request paths except:
     * - api (API routes)
     * - _next/static (static files)
     * - _next/image (image optimization)
     * - favicon.ico, apple-icon.(jpg|jpeg|png), icon.(ico|jpg|jpeg|png|svg), sitemap.xml, robots.txt
     */
    "/((?!api|_next/static|_next/image|favicon.ico|sitemap.xml|robots.txt|apple-icon\\.(?:jpg|jpeg|png)|icon\\.(?:ico|jpg|jpeg|png|svg)).*)",
  ],
};
```

#### Usage in Server Components

You can track pageviews manually in React Server Components with `trackPageview`, giving per-page control and optional metadata.

**Note:** In Server Components there is no request object; you use request headers and must pass the path explicitly. The `headers()` function [cannot be called](https://nextjs.org/docs/app/api-reference/functions/after#with-request-apis) inside the `after` callback when used in a Server Component.

```jsx
// app/blog/page.js
import { after } from "next/server";
import { headers } from "next/headers";
import { trackPageview } from "@simpleanalytics/next/server";

export default async function Page() {
  const headerList = await headers();

  after(async () => {
    await trackPageview("/blog", { headers: headerList });
  });

  return <>{/* ... */}</>;
}
```

#### Handling parameters in dynamic routes

For dynamic segments (e.g. `app/blog/posts/[id]/page.js`), build the path from the segment and pass it to `trackPageview`:

```jsx
// app/blog/posts/[id]/page.js
import { after } from "next/server";
import { headers } from "next/headers";
import { trackPageview } from "@simpleanalytics/next/server";

export default async function Page({ params }) {
  const headerList = await headers();
  const { id } = await params;

  after(async () => {
    await trackPageview(`/blog/posts/${id}`, { headers: headerList });
  });

  // ...
}
```

---

## Tracking Events

Use the `trackEvent` function to track events (e.g. button clicks, form submissions) in your app. See the [Simple Analytics events docs](https://docs.simpleanalytics.com/events) for more on events.

### Tracking client-side events

Client-side `trackEvent` requires the `SimpleAnalytics` component to be used.

```jsx
"use client";

import { trackEvent } from "@simpleanalytics/next";

export default function Page() {
  function addToCart() {
    // ...
    trackEvent("added_to_cart");
  }

  return <>{/* ... */}</>;
}
```

### Adding metadata to events

You can attach metadata to events for extra context:

```jsx
"use client";

import { trackEvent } from "@simpleanalytics/next";

export default function Page() {
  function purchase() {
    trackEvent("addToCart", {
      product_id: "123",
      currency: "EUR",
    });
  }

  return <>{/* ... */}</>;
}
```

### Tracking server-side events

Events can be tracked in Server Actions and Route Handlers. You must pass the `request` object or the request headers to `trackEvent`.

#### Usage in Server Actions

```js
"use server";

import { after } from "next/server";
import { headers } from "next/headers";
import { trackEvent } from "@simpleanalytics/next/server";

export async function purchaseAction() {
  // ...

  after(async () => {
    await trackEvent("purchase", {
      headers: await headers(),
      metadata: {
        product_id: "123",
        currency: "EUR",
      },
    });
  });

  return { success: true };
}
```

#### Usage with Route Handlers

```js
import { after, NextResponse } from "next/server";
import { trackEvent } from "@simpleanalytics/next/server";

export async function POST(request) {
  // ...

  after(async () => {
    await trackEvent("purchase", {
      request,
      metadata: {
        product_id: "123",
        currency: "EUR",
      },
    });
  });

  return NextResponse.json({ success: true });
}
```

---

## Alternative: manual script (without plugin)

If you prefer not to use the plugin, you can load the script yourself with Next.js’s [Script component](https://nextjs.org/docs/pages/building-your-application/optimizing/scripts).

### App Router

```jsx
// app/layout.js
import Script from "next/script";

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>{children}</body>
      <Script src="https://scripts.simpleanalyticscdn.com/latest.js" />
    </html>
  );
}
```

### Pages Router

```jsx
// pages/_app.js
import Script from "next/script";

export default function MyApp({ Component, pageProps }) {
  return (
    <>
      <Component {...pageProps} />
      <Script src="https://scripts.simpleanalyticscdn.com/latest.js" />
    </>
  );
}
```

### Before Next.js 13

```jsx
// _app.js
import Script from "next/script";

function MyApp({ Component, pageProps }) {
  return (
    <>
      <Component {...pageProps} />
      <Script src="https://scripts.simpleanalyticscdn.com/latest.js" />
      <noscript>
        <img
          src="https://queue.simpleanalyticscdn.com/noscript.gif"
          alt=""
          referrerPolicy="no-referrer-when-downgrade"
        />
      </noscript>
    </>
  );
}

export default MyApp;
```

The script uses the `afterInteractive` strategy. The `<noscript>` tag is optional; most visitors without JavaScript are bots.

### Send events with JavaScript (manual script)

```js
export const saEvent = (eventName) => {
  if (typeof window !== "undefined" && window.sa_event)
    return window.sa_event(eventName);
};
```

### Send events with TypeScript (manual script)

```ts
declare function sa_event(eventName: string);

export const saEvent = (eventName: string) => {
  if (typeof window !== "undefined" && window.sa_event)
    return window.sa_event(eventName);
};
```
