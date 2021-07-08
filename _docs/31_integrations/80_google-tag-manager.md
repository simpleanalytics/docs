---
title: Install Simple Analytics via Google Tag Manager
menu: Google Tag Manager
category: integrations
permalink: /install-simple-analytics-with-google-tag-manager
---

You can embed our script via Google Tag Manager. Before our Tag is approved customers of Simple Analytics can import our tag manually.

1. Download our template: [simple-analytics-tag-template.tpl](https://assets.simpleanalytics.com/files/simple-analytics-tag-template.tpl)
1. Open [Google Tag Manager](https://tagmanager.google.com)
1. Select your container
1. Click on "Templates" in the sidebar
1. Click on "New" button in the "Tag Templates" section
1. Click on the 3 dots in the top right corner
1. Select "Import"
1. Open the download file named `simple-analytics-tag-template.tpl`
1. Optionally change the "Tag Configuration"
1. Save the template and close the "Template Editor"

Now you added the Tag to your Tag Manager container. Next you want to trigger the tag on "Initialization".

1. Click on "Tags" in the sidebar
1. Click on "New" button in the "Tags" section
1. Click on "Tag Configuration" to add a tag
1. An popover opens on the right, select "Simple Analytics"
1. Click on "Triggering" to add a trigger
1. Select "Initialization - All Pages"
1. Click "Save" to save the tag

Now you added the Simple Analytics Tag with a trigger. Next you can preview or submit the changes and your page views will be collected in Simple Analytics. Make sure to have a website setup in Simple Analytics to collect the data.

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact).
