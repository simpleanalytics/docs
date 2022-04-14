---
title: Install Simple Analytics with Gridsome
hidden: true
category: integrations
permalink: /install-simple-analytics-with-gridsome
last_modified_at: 2022-04-14
---

Install our Gridsome package:

```bash
npm install gridsome-plugin-simple-analytics
```

### Usage

```js
module.exports = {
  plugins: [
    {
      use: "gridsome-plugin-simple-analytics",
    },
  ],
};
```

### Bypass Ad Blockers

You can also optionally specify a custom domain to bypass ad blockers. Read more about this in [our documentation](https://docs.simpleanalytics.com/bypass-ad-blockers).

```js
module.exports = {
  plugins: [
    {
      use: "gridsome-plugin-simple-analytics",
      options: {
        domain: "api.example.com",
      },
    },
  ],
};
```
