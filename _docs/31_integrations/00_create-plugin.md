---
title: Create plugin for Simple Analytics
hidden: true
category: integrations
permalink: /create-plugin
last_modified_at: 2022-04-14
---

To create a plugin for Simple Analytics, we have a few requirements that need to work within that plugin. The goal of the plugin is to make it as easy as possible to implement Simple Analytics. There are two types of plugins: System plugins and Framework plugins.

## System plugins

A few examples: WordPress, Drupal, Google Tag Manager, and Cloudflare.

The settings below should be changable via the UI of the plugin. All changed settings need to be passed to the `<script>`-tag. For example:

<!-- prettier-ignore -->
```html
<script data-mode="hash" data-collect-dnt="true" src="..." />
```

Settings that require an `array` would preferably have an UI element that adds items to a list. But in the script will be passed like this:

<!-- prettier-ignore -->
```html
<script data-ignore-pages="/search/*,/account/*,/vouchers" src="..." />
```

### Hide admins

If possible, do not collect data from admins. Let's say you are an admin and logged in to Drupal. If the plugin can detect it's an admin to the current site, do not collect data for that user. Make this optional in the UI.

### Scripts

We have two scripts that need to be embedded into the page: Embed script (to collect data), Events script (to queue events before the Embed script is loaded).

#### Embed script

The following HTML should be added to the `<body>` of the page:

<!-- prettier-ignore -->
```html
<script async defer src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
````

If that is not possible, add only the `<script>`-tag in the `<head>` of the page and ignore the `<noscript>` part.

#### Events script

Place this `<script>`-tag in the `<head>` of the page:

<!-- prettier-ignore -->
```html
<script>window.sa_event=window.sa_event||function(){var a=[].slice.call(arguments);window.sa_event.q?window.sa_event.q.push(a):window.sa_event.q=[a]};</script>
```

## UI

In the UI of the System plugin, we need to be able to change all settings. See here an example for the Drupal module:

| Settings                                                                               | Advanced settings                                                                               | Events                                                                               |
| -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| [full size](https://assets.simpleanalytics.com/docs/system-plugin/drupal-settings.png) | [full size](https://assets.simpleanalytics.com/docs/system-plugin/drupal-advanced-settings.png) | [full size](https://assets.simpleanalytics.com/docs/system-plugin/drupal-events.png) |
| ![](https://assets.simpleanalytics.com/docs/system-plugin/drupal-settings.png)         | ![](https://assets.simpleanalytics.com/docs/system-plugin/drupal-advanced-settings.png)         | ![](https://assets.simpleanalytics.com/docs/system-plugin/drupal-events.png)         |

### System plugin checklist

- [ ] [All settings](#settings) below are changable via the UI of the plugin
- [ ] Settings are hidden by default (if possible)
- [ ] Add ignore admins feature (if possible)
- [ ] Allow custom settings (key, value)
- [ ] Embed script is added to the body of the page (with the changed settings)
- [ ] Events script is added to the head of the page
- [ ] Auto deploy via GitHub Actions (if possible/needed)
- [ ] Change filename from `latest.js` to `plus.js` when automated events are enabled

### Collapse settings

To keep the plugin understandable and straightforward, hide as many settings as possible.

For example, collapse an advanced settings block and let users click on it to unfold. Or add a checkbox with advanced settings, which is off by default, and when a user clicks on it, open advanced settings. The same goes for events. There are quite some settings related to events. Just hide them behind a toggle (checkbox or `<details>`-tag).

## Framework plugins

A few examples: React, Vue, Gridsome, and Gatsby.

The settings below should be changeable via the plugin settings. Usually, as a settings object passed to the plugin. These settings will be passed to the `<script>`-tag. For example:

```html
<script data-mode="hash" data-collect-dnt="true" src="..." />
```

Settings that require an `array` will be passed like this in the plugin settings:

```js
{
  ignorePages: ["/search/*", "/account/*", "/vouchers"];
}
```

But end up in the HTML script like this:

```html
<script data-ignore-pages="/search/*,/account/*,/vouchers" src="..." />
```

### Custom settings

Custom settings should be specified like this: `customSettings: { collectDarkMode: true, ... }` which will be send to the script as `data-collect-dark-mode="true"`.

### System plugin checklist

- [ ] [All settings](#settings) below are changeable via the options object of the plugin
- [ ] The plugin should collect page views without specifying any settings/options
- [ ] `enabled` setting should allow async function that returns true or false
- [ ] Allow custom settings (key, value)
- [ ] Embed script is added to the body of the page (with the changed settings)
- [ ] Events script is added to the head of the page
- [ ] Expose framework event function that can be used on all pages
- [ ] Embed script URL changes when auto collect events is turned on
- [ ] Auto deploy via GitHub Actions (if possible/needed)
- [ ] Change filename from `latest.js` to `plus.js` when automated events are enabled

## Settings

For both System plugins and Framework plugins, the following settings need to be changeable:

### Advanced settings

<!-- prettier-ignore -->

|Setting|Description|Type|Default|Required|Example|
|:---|:---|:---|:---|:---:|:---|
|custom domain|[Custom domain](https://docs.simpleanalytics.com/bypass-ad-blockers)|string|undefined|no|`simple.example.com`|
|`data-mode`|[Change mode](https://docs.simpleanalytics.com/hash-mode)|string|undefined|no|`hash`|
|`data-collect-dnt`|[Collect DoNotTrack visits](https://docs.simpleanalytics.com/dnt)|boolean|`false`|no|`true`|
|`data-ignore-pages`|[Ignore pages](https://docs.simpleanalytics.com/ignore-pages)|array|undefined|no|`/search/*,/account/*,/vouchers`|
|`data-auto-collect` page views|[Auto collect](https://docs.simpleanalytics.com/trigger-custom-page-views#use-custom-collection-anyway)|boolean|`true`|no|`false`|
|`data-onload` callback|[Onload function](https://docs.simpleanalytics.com/trigger-custom-page-views#use-custom-collection-anyway)|string|undefined|no|`onloadCallback()`|
|`data-hostname`|[Overwrite hostname](https://docs.simpleanalytics.com/overwrite-domain-name)|string|undefined|no|`otherdomain.com`|
|`data-sa-global`|[Override global](https://docs.simpleanalytics.com/events#the-variable-sa_event-is-already-used)|string|`sa_event`|no|`ba_event`|
|enabled|Enable the script|boolean|`true`|no|`false`|

### Event settings

<!-- prettier-ignore -->

|Setting|Description|Type|Default|Required|Example|
|:---|:---|:---|:---|:---:|:---|
|`data-collect`|[Auto collect downloads](https://docs.simpleanalytics.com/automated-events)|array|undefined|no|`outbound,emails,downloads`|
|`data-extensions`|[Download file extensions](https://docs.simpleanalytics.com/automated-events)|array|`pdf,csv,docx,xlsx,zip`|if "auto collect downloads" is `true`|`pdf,txt`|
|`data-use-title`|[Use titles of page](https://docs.simpleanalytics.com/automated-events)|boolean|`false`|no|`true`|
|`data-full-urls`|[Use full URLs](https://docs.simpleanalytics.com/automated-events)|boolean|`false`|no|`true`|
|`data-sa-global`|[Override global](https://docs.simpleanalytics.com/events#the-variable-sa_event-is-already-used)|string|`sa_event`|no|`ba_event`|

### System plugins specific settings

<!-- prettier-ignore -->

|Setting|Description|Type|Default|Required|Example|
|:---|:---|:---|:---|:---:|:---|
|ignore admins|Ignore admin|boolean|`true`|no|`false`|

### Custom settings

The plugin should allow custom settings as well. In the future we will add more settings to our script. To be able to use those settings we want users to be able to add such a setting. For example a new setting could be named `collect-dark-mode` with the value `true`. In the plugin it should be possible to pass this value for that so it ends up in the script like this:

```html
<script data-collect-dark-mode="true" src="..." />
```

## Scripts

The scripts should be loaded into the HTML of the page.

<!-- prettier-ignore -->
```html
<script async defer src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
````

Or in case when a custom domain is enabled:

<!-- prettier-ignore -->
```html
<script async defer src="https://custom.domain/latest.js"></script>
<noscript><img src="https://custom.domain/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
````

When automated events are enabled the filename of the script changes from `latest.js` to `plus.js`.
