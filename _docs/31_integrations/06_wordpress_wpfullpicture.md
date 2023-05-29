---
title: WP Full Picture plugin
category: integrations
hidden: true
permalink: /wordpress-full-picture-plugin
last_modified_at: 2023-05-29
---

[WP Full Picture](https://wordpress.org/plugins/full-picture-analytics-cookie-notice/) is a WordPress plugin with more features than [the official Simple Analytics plugin](/install-simple-analytics-on-wordpress).

WP Full Picture lets you:

* Load Simple Analytics only in specific countries. Simply enable geolocation module and choose countries that you want to use SA in
* Do not track page views until pages are actually viewed (e.g. when they are opened in tabs). This works out-of-the-box with no extra setup.
* Turn off tracking for specific user roles and users who are not logged in ([more information](https://wpfullpicture.com/support/documentation/how-to-exclude-users-from-tracking/))
* See traffic from some Android applications ([requires extra setup](https://wpfullpicture.com/support/documentation/how-to-get-better-traffic-sources-information/))
* Use custom domain for bypassing ad-blockers (after setting it up as [described here](https://docs.simpleanalytics.com/bypass-ad-blockers))
* Join traffic data from multiple websites under one domain without the need to [modify the script](https://docs.simpleanalytics.com/overwrite-domain-name)
* Run on localhost without having to modify the script
* Track single-page websites (clicks on navigation links that scroll to different parts of the page will be counted as different page views)

> See the plugin in action on a temporary Wordpress website on tastewp.com. Simply [click this link to generate a new test site](https://tastewp.com/new?pre-installed-plugin-slug=full-picture-analytics-cookie-notice&redirect=plugins.php&ni=true).

This is how the settings page looks:

<img class="border" src="/images/wp-full-picture-simple-analytics-settings.png" alt="Simple Analytics settings menu in WordPress' WP Full Picture plugin" />

## How to install Simple Analytics with the WP Full Picture plugin

1. Go to your WordPress admin
1. Go to **Plugins** in your WordPress admin and click on **Add new**:
1. Click on **Search Plugins** and type `wp full picture`
1. Click on **Install Now**

   ![](/images/wp-full-picture-simple-analytics-installation.png)

1. After this click on **Activate**
1. On WP Full Picture page click on **Choose modules**
1. Choose **Simple Analytics** and (optionally) **Geolocation** modules and save the changes

   ![](/images/wp-full-picture-simple-analytics-installation-2.png)

1. This will install Simple Analytics on your website. If you want to change other settings mentioned above click on "Configure" in the Simple Analytics block.
