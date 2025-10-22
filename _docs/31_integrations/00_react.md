---
title: Install Simple Analytics with React
hidden: true
category: integrations
permalink: /install-simple-analytics-with-react
last_modified_at: 2025-10-22
---

Add Simple Analytics to React apps with our official React package.

## Install

Run this command to install Simple Analytics for React:

```bash
npm i @simpleanalytics/react
```

## Usage

Import the `<SimpleAnalytics />` to start tracking pageviews

```tsx
import { SimpleAnalytics } from "@simpleanalytics/react";

export function App() {
  return (
    <>
      {/* your app */}
      <SimpleAnalytics />
    </>
  );
}
```

## Options

- **Custom domain**: see [/bypass-ad-blockers](/bypass-ad-blockers)

```tsx
<SimpleAnalytics domain="custom.domain.com" />
```

## Send events

```tsx
import { trackEvent } from "@simpleanalytics/react";

function Button() {
  return (
    <button onClick={() => trackEvent("clicked")}>
      Track event
    </button>
  );
}
```

Note: `trackEvent` requires `<SimpleAnalytics />` to be present in your app.

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact).
