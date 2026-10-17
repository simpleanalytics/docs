---
title: Install Simple Analytics on WordPress
menu: WordPress
category: integrations
permalink: /install-simple-analytics-on-wordpress
last_modified_at: 2026-10-17
---

You can embed our script in WordPress using a plugin. On this page we will explain how to download this plugin and help you installing the Simple Analytics plugin on WordPress.

We created a video showing how to install Simple Analytics on a WordPress website. [Here you go](https://www.youtube.com/watch?v=x_w0uiWlNwM)

The WordPress plugin is ready to roll right from install—no setup needed. But for the adventurers out there:

<details markdown="1">
   <summary>Explore and customize every setting to make it yours!</summary>

| General | Ignore Rules |
|:-------:|:------------:|
| ![](/images/wordpress-settings-general.png) | ![](/images/wordpress-settings-ignore-rules.png) |

| Advanced | Events |
|:--------:|:------:|
| ![](/images/wordpress-settings-advanced.png) | ![](/images/wordpress-settings-events.png) |

</details>

## Requirements

- PHP 7.4 or higher
- A recent version of WordPress 7. See [our plugin on wordpress.org](https://wordpress.org/plugins/simpleanalytics/) for the exact minimum version.

## Install official plugin via WordPress dashboard

1. Go to your WordPress admin (likely on /wp-admin or [wordpress.com/log-in](https://wordpress.com/log-in))
1. Go to **Plugins** in your WordPress admin and click on **Add Plugin**:

   ![](/images/wordpress-click-add-new-plugin.jpg)

1. Click on Search Plugins and type `simpleanalytics` _(do not use a space)_
1. Click on **Install Now**
1. After this click on **Activate** and our plugin is installed

<details>
   <summary>Manual installation</summary>
   <div markdown="1">

Follow these steps to add Simple Analytics to your WordPress website:

1. First download our plugin via WordPress: [wordpress.org/plugins/simpleanalytics](https://wordpress.org/plugins/simpleanalytics/)
1. Go to your WordPress admin (likely on /wp-admin or [wordpress.com/log-in](https://wordpress.com/log-in))
1. Next click on **Plugins** > **Add Plugin** in the sidebar menu:

   ![](/images/wordpress-click-add-new-plugin.jpg)

1. Click on the **Upload Plugin** button:

   ![](/images/wordpress-click-upload-plugin.jpg)

1. Click on **Browse** to select a file _(this button can have different text depending on your browser)_:

   ![](/images/wordpress-click-browse.jpg)

1. Browse and select the file that you downloaded in the first step.

1. Click on the button **Install Now**:

   ![](/images/wordpress-click-install-now.jpg)

1. Click on **Activate Plugin**:

   ![](/images/wordpress-click-activate-plugin.jpg)

1. If the Simple Analytics plugin is successfully installed it shows a screen like this:

   ![](/images/wordpress-installed-plugins.jpg)

</div>
</details>

Make sure to have your website added in your [Simple Analytics dashboard](https://dashboard.simpleanalytics.com/) to see your stats.

## Settings

You find the settings of the plugin in your WordPress admin under **Settings** > **Simple Analytics**. The **General** tab confirms that the plugin is active and links to your dashboard. The other tabs have these settings:

**Ignore Rules**

- **Ignore Pages**: a comma-separated list of [pages to ignore](/ignore-pages), for example `/contact, /category/*`.
- **Specific User Roles to Exclude**: by default, the plugin doesn't collect visits from any logged-in user. Select one or more roles, for example **Administrator**, to only exclude those roles and collect visits from other logged-in users, like customers or members.
- **Exclude IP Addresses**: IP addresses to exclude, one per line.

> IP and role exclusion only works when your pages are not cached. With page caching, visitors can get a cached page that was created for someone else.

**Advanced**

- **Custom Domain**: the domain you set up to [bypass ad-blockers](/bypass-ad-blockers), for example `api.example.com`. Leave it empty to use our default domain.
- **Collect Do Not Track**: also collect visitors that have [Do Not Track](/dnt) enabled.
- **Hash mode**: turn this on if your website uses [hash navigation](/hash-mode). Most WordPress websites don't.
- **Manually collect page views**: turns off automatic page views, so you can [send them yourself](/trigger-custom-page-views#use-custom-collection-anyway) with `sa_pageview`.
- **Support no JavaScript mode**: adds our [`noscript` tag](/script#non-javascript-environments) to collect visitors without JavaScript.
- **Onload Callback**: JavaScript to run when our script has loaded, for example `sa_event("my_event")`. Only users who are allowed to save unfiltered HTML can save this setting. On multisite, those are super admins. If you change the security keys (salts) of your WordPress site, save the callback again.
- **Overwrite domain name**: the domain that is sent to Simple Analytics, useful for [multi-domain setups](/overwrite-domain-name).
- **Global variable name**: [change the name](/events#the-variable-sa_event-is-already-used) of the `sa_event` function.

**Events**

- **Collect automated events**: adds our [automated events](/automated-events) script, which collects clicks on outbound links, email addresses, and downloads.
- **Auto collect downloads**: which automated events to collect, as a comma-separated list of `outbound`, `emails`, and `downloads`. Leave it empty to collect all three.
- **Download file extensions**: the file extensions to collect as downloads, for example `pdf, zip`. Leave it empty to use [the defaults](/automated-events#script).
- **Use titles of page**: use the `title` attribute of a link as event name, when the link has one.
- **Use full URLs**: use the full URL in event names for outbound links and downloads, instead of only the hostname or file name.
- **Override global**: the name of the `sa_event` function for automated events, if you changed it.

Deactivating the plugin keeps your settings. Deleting the plugin removes them.

## Upgrading to version 1.110 or later

Version 1.110 fixed a few settings that didn't work as intended before. Check these settings after you upgrade:

- **Manually collect page views** now turns off automatic page views. If you turned it on but don't call `sa_pageview` yourself, turn it off to keep collecting page views.
- **Onload Callback** now runs your JavaScript. A callback saved in an earlier version stays inactive until you save the **Advanced** tab again.
- **Use titles of page** is now respected when it's turned off, which is the default. Automated events then no longer use the `title` attribute of links as event name. Turn it on to keep using link titles.
- **Use full URLs** now works when it's turned on. Event names for outbound links and downloads then include the full URL instead of only the hostname or file name.

## Troubleshooting

Don't see your own visits? By default, the plugin doesn't collect visits from logged-in users. Log out or use a private window to test.

To check if the plugin added our script, open the source code of a page on your website and search for "Simple Analytics". When the script is added, you see this comment above it:

```html
<!-- Simple Analytics - 100% privacy-first analytics (official WordPress plugin) -->
```

When you are excluded by your IP address or user role, the plugin doesn't add our script and shows which rule excluded you:

```html
<!-- Simple Analytics: Script not included because this visitor is excluded by tracking rule: Exclude User Role -->
```

## Others

> See our plugin in action by [creating a temporary Wordpress website on tastewp.com in one click](https://tastewp.com/new?pre-installed-plugin-slug=simpleanalytics&redirect=plugins.php&ni=true). Do note that by default we don't collect visits from logged-in users. Log out to see the requests to Simple Analytics.

<details markdown="1">
   <summary>Non-official plugins</summary>

There are two non-official plugins made by others:
 - [WordPress plugin by Refined Practice](/wordpress-plugin-by-refined-practice)
 - [WP Full Picture plugin](/wordpress-full-picture-plugin)

</details>

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact).
