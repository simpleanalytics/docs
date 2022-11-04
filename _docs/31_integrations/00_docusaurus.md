---
title: Install Simple Analytics with Docusaurus
hidden: true
category: integrations
permalink: /install-simple-analytics-with-docusaurus
last_modified_at: 2022-11-04
---

Docusaurus is an optimized site generator in React. Docusaurus helps users to move fast and write content. Build documentation websites, blogs, marketing pages, and more. To use it with Simple Analytics, you can use our Docusaurus plugin.

## Install

Run the following command to install the plugin:

```bash
npm install docusaurus-plugin-simple-analytics --save
```

Then, add the plugin to `docusaurus.config.js`:

```js
plugins: [
  ...
  ['docusaurus-plugin-simple-analytics', {}],
  ...
],
```

## Custom domain

The property `domain` lets you specify [your custom domain](https://docs.simpleanalytics.com/bypass-ad-blockers).

Example:

```js
plugins: [
  ...
  ['docusaurus-plugin-simple-analytics', {
    domain: 'custom.domain.com'
  }],
  ...
],
```

## Notes

The plugin has no effect in development.

## Special thanks

Developed by [Frédéric Massart](https://github.com/FMCorz) from [branchup.tech](https://www.branchup.tech/?utm_source=docs.simpleanalytics.com%2Finstall-simple-analytics-with-docusaurus) ([@branchup](https://github.com/branchup)).
