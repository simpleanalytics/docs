---
title: Install Simple Analytics with Next.js
hidden: true
category: integrations
permalink: /install-simple-analytics-with-next
last_modified_at: 2022-04-14
---

Next.js has a lovely [Script component](https://nextjs.org/docs/basic-features/script).

In your app, you can add this Script component:

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
