---
title: Install Simple Analytics with React
hidden: true
category: integrations
permalink: /install-simple-analytics-with-react
last_modified_at: 2026-10-17
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

Most React component options map directly to Simple Analytics script settings. Boolean options are passed as `"true"` or `"false"`, and array options are joined with commas before they are added to the script.
The script is injected once. Add these options when you render `<SimpleAnalytics />`; changing them after the script has loaded will not reconfigure the existing script.
For example, you can collect visits from browsers with Do Not Track enabled, ignore a few metrics, and allow extra URL parameters:

{% raw %}
```tsx
<SimpleAnalytics
  collectDnt
  ignoreMetrics={{
    referrer: true,
    screensize: true,
  }}
  allowParams={["product-id", "article-slug"]}
/>
```
{% endraw %}

### Available options

| Prop              | Script setting           | Description                                                                                                                                                            |
| ----------------- | ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `domain`          | Script source            | Load the script from a [custom domain](/bypass-ad-blockers), for example `stats.example.com`.                                                                          |
| `autoCollect`     | `data-auto-collect`      | Automatically collect pageviews. Set this to `false` if you want to send pageviews manually.                                                                           |
| `collectDnt`      | `data-collect-dnt`       | Also collect visits from browsers with [Do Not Track](/dnt) enabled.                                                                                                   |
| `hostname`        | `data-hostname`          | [Overwrite the hostname](/overwrite-domain-name) used in your Simple Analytics dashboard.                                                                              |
| `mode`            | `data-mode`              | Sets the script mode. The script only supports `hash` ([hash mode](/hash-mode)). The package's TypeScript type currently only accepts `"dash"`, which has no effect.       |
| `ignoreMetrics`   | `data-ignore-metrics`    | [Ignore metrics](/ignore-metrics) such as `referrer`, `utm`, `country`, `session`, `timeonpage`, `scrolled`, `useragent`, `screensize`, `viewportsize`, or `language`. |
| `ignorePages`     | `data-ignore-pages`      | [Ignore pages](/ignore-pages), including wildcard paths like `/account/*`.                                                                                             |
| `allowParams`     | `data-allow-params`      | [Allow extra URL parameters](/allow-params) to be collected.                                                                                                           |
| `nonUniqueParams` | `data-non-unique-params` | Has no effect, because the script doesn't support this setting. To count visits from specific referrers as non-unique, add [our script](/script) with [`data-non-unique-hostnames`](/non-unique-hostnames) instead. |
| `strictUtm`       | `data-strict-utm`        | Only collect URL parameters with the `utm_` prefix. See [strict UTMs](/strict-utms).                                                                                   |

Note: `trackPageview` requires `<SimpleAnalytics />` to be present in your app.

## Send events

```tsx
import { trackEvent } from "@simpleanalytics/react";

function Button() {
  return <button onClick={() => trackEvent("clicked")}>Track event</button>;
}
```

Note: `trackEvent` requires `<SimpleAnalytics />` to be present in your app.

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact).
