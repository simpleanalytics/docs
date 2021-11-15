---
title: Create plugin for Simple Analytics
hidden: true
category: integrations
permalink: /create-plugin
---

To create a plugin for Simple Analytics we have a few requirements that need to work within that plugin. The goal of the plugin is to make is as easy as possible to implement Simple Analytics. There are two types of plugins: System plugins and Framework plugins.

## System plugins

A few examples: Wordpress, Drupal, Google Tag Manager, and CloudFlare.

The settings below should be changable via the UI of the plugin. All changed settings need to be passed to the `<script>`-tag. For example:

```html
<script data-mode="hash" data-collect-dnt="true" src="..." />
```

Settings that require an `array` would preferably have an UI element that adds items to a list. But in the script will be passed like this:

```html
<script data-ignore-pages="/search/*,/account/*,/vouchers" src="..." />
```

### Collapse settings

To keep the plugin simple and understandable, hide as many settings as possible.

For example, collapse an advanced settings block and let users click on it to unfold. Or add a checkbox with advanced settings, which is off by default, and when a users clicks on it, open advanced settings. The same goes for events. There are quite some settings related to events. Just hide them behind a toggle (checkbox or `<details>`-tag).

## Framework plugins

A few examples: React, Vue, Gridsome, and Gatsby.

The settings below should be changable via the plugin settings. Usually as a settings object passed to the plugin. There settings will be passed to the `<script>`-tag. For example:

```html
<script data-mode="hash" data-collect-dnt="true" src="..." />
```

Settings that require an `array` will be passed like this in the plugin settings:

```js
{
  ignorePages: ["/search/*", "/account/*", "/vouchers"]
}
```

But end up in the HTML script like this:

```html
<script data-ignore-pages="/search/*,/account/*,/vouchers" src="..." />
```

The plugin should collect page views without specifying any settings/options.

## Settings

For both System plugins and Framework plugins the following settings need to be changable:

### Advanced settings

|Setting|Description|Type|Default|Required|Example|
|:---|:---|:---|:---|:---:|:---|
|custom domain|[Custom domain](https://docs.simpleanalytics.com/bypass-ad-blockers)|string|undefined|no|`simple.example.com`|
|mode|[Change mode](https://docs.simpleanalytics.com/hash-mode)|string|undefined|no|`hash`|
|collect dnt|[Collect DoNotTrack visits](https://docs.simpleanalytics.com/dnt)|boolean|`false`|no|`true`|
|ignore pages|[Ignore pages](https://docs.simpleanalytics.com/ignore-pages)|array|undefined|no|`/search/*,/account/*,/vouchers`|
|auto collect page views|[Auto collect](https://docs.simpleanalytics.com/trigger-custom-page-views#use-custom-collection-anyway)|boolean|`true`|no|`false`|
|onload callback|[Onload function](https://docs.simpleanalytics.com/trigger-custom-page-views#use-custom-collection-anyway)|string|undefined|no|`onloadCallback()`|
|hostname|[Overwrite hostname](https://docs.simpleanalytics.com/overwrite-domain-name)|string|undefined|no|`otherdomain.com`|
|enabled|Enable the script|boolean|`true`|no|`false`|

### Event settings

|Setting|Description|Type|Default|Required|Example|
|auto collect downloads|[Auto collect downloads](https://docs.simpleanalytics.com/automated-events)|boolean|`false`|no|`true`|
|download extensions|[Download file extensions](https://docs.simpleanalytics.com/automated-events)|array|`pdf,csv,docx,xlsx,zip`|if "auto collect downloads" is `true`|`pdf,txt`|
|auto collect links|[Auto collect outbound links](https://docs.simpleanalytics.com/automated-events)|boolean|undefined|no|`true`|
|sa global|[Override event global](https://docs.simpleanalytics.com/events#the-variable-sa_event-is-already-used)|string|`sa_event`|no|`ba_event`|
