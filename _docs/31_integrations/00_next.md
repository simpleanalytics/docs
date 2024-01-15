---
title: Install Simple Analytics with Next.js
hidden: true
category: integrations
permalink: /install-simple-analytics-with-next
last_modified_at: 2024-01-15
---

Next.js has a lovely [Script component](https://nextjs.org/docs/pages/building-your-application/optimizing/scripts).

In your app, you can add this Script component. You can use the App Router, the Pages Router, or the pre Next.js 13 way.

## App router

```jsx
// app/layout.js
import Script from 'next/script'
 
export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>{children}</body>
      <Script src="https://scripts.simpleanalyticscdn.com/latest.js" />
    </html>
  )
}
```

## Pages Router

```jsx
// pages/_app.js
import Script from 'next/script'
 
export default function MyApp({ Component, pageProps }) {
  return (
    <>
      <Component {...pageProps} />
      <Script src="https://scripts.simpleanalyticscdn.com/latest.js" />
    </>
  )
}
```

## Before Next.js 13

```jsx
// _app.tsx
import type { AppProps } from "next/app";
import React from "react";
import Script from "next/script";

function MyApp({ Component, pageProps }: AppProps) {
  return (
    <React.Fragment>
      <Component {...pageProps} />
      <Script src="https://scripts.simpleanalyticscdn.com/latest.js" />
      <noscript>
        {/* eslint-disable @next/next/no-img-element */}
        <img
          src="https://queue.simpleanalyticscdn.com/noscript.gif"
          alt=""
          referrerPolicy="no-referrer-when-downgrade"
        />
      </noscript>
    </React.Fragment>
  );
}

export default MyApp;
```

It will use the `afterInteractive` strategy to load the script. From the docs:

> For scripts that can fetch and execute after the page is interactive, such as tag managers and analytics. These scripts are injected on the client-side and will run after hydration.

## Noscript

You can use the `<noscript>`-tag, but it's not really needed. Most visitors without JavaScript are bots anyway.

## Send events with JavaSript

```ts
export const saEvent = (eventName) => {
  if (window && window.sa_event) return window.sa_event(eventName);
};
```

## Send events with TypeScript

```ts
declare function sa_event(eventName: string);

export const saEvent = (eventName: string) => {
  if (window && window.sa_event) return window.sa_event(eventName);
};
```
