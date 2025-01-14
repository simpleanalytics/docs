---
title: Install Simple Analytics in WordPress via Head & Footer Code Plugin
hidden: true
category: integrations
permalink: /install-simple-analytics-in-wordpress-with-head-footer-code-plugin
last_modified_at: 2023-09-27
---

Sometimes you want to use more script features then our official WordPress plugin offers.

You can easily embed Simple Analytics script into your WordPress website using the "Head & Footer Code" plugin. Follow the steps below to get started:

## Installing the Head & Footer Code Plugin

1. In your WordPress dashboard, navigate to the "Plugins" section.
2. Click on "Add New."
3. Search for "Head & Footer Code" in the plugin search bar.
4. Click "Install Now" next to the "Head & Footer Code" plugin.
5. After installation, activate the plugin by clicking "Activate."

## Adding the Simple Analytics Embed Script

1. In the WordPress dashboard, navigate to "Settings" and then "Head & Footer Code."
2. In the “Site-wide Head Code” section, paste the Simple Analytics embed script.
   - Example script that uses the [ignore pages](/ignore-pages) feature:
   ```html
   <script
     data-ignore-pages="/a-page-to-ignore,/another-page"
     async
     src="https://scripts.simpleanalyticscdn.com/latest.js"
   ></script>
   ```
3. Click "Save Settings" to apply the changes.

## Verify Installation

To ensure the script has been properly added:

1. Visit your WordPress site and view the page source code (Right-click on the page and select "View Page Source").
2. Search for the Simple Analytics script in the head section to confirm that it has been added successfully.

Congratulations! Now Simple Analytics will start collecting data from your WordPress website.

## Troubleshooting

If the Simple Analytics script does not appear in the source code or if data is not being collected, ensure the plugin is activated and the script is correctly pasted in the “Site-wide Head Code” section. Also, check for any script blockers or browser extensions that may prevent the script from loading. [Use our debug guide](https://www.simpleanalytics.com/blog/debug-simple-analytics-script) to debug issue with your script installation.

If you encounter any issues or need further assistance, feel free to reach out to us via [our support channels](https://simpleanalytics.com/contact).
