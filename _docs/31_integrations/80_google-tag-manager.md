---
title: Install Simple Analytics via Google Tag Manager
menu: Google Tag Manager
category: integrations
permalink: /install-simple-analytics-with-google-tag-manager
last_modified_at: 2022-06-22
---

You can embed our script via Google Tag Manager. We have an official Community Tag. Here is how to install this tag.

<blockquote class="red" markdown="1">

Our official tag fails to install due to changes in a Google account. We recommend to use this tag for now: [datastudio.google.com/.../create?connectorId=AKfyc...4B7QQ](https://datastudio.google.com/u/0/datasources/create?connectorId=AKfycbyswyUWn2yxh69Xd9yitZpPB8RtRKla7nf_5avHmEB2-1wE3kA5GlmoipJ9WRAt74B7QQ)

</blockquote>

Start at [the Google Tag Manager homepage](https://tagmanager.google.com) and follow the instructions:

{%
  include video.html
  controls="true"
  slug="google-tag-manager-integration"
  formats="mov,mp4,ogg,webm,wmv"
  poster="poster.png"
%}

If you prefer text instructions, follow this guide:

1. Click "Add a new Tag"
1. Click "Choose a tag type to begin setup..."
1. Click the blue bar "Discover more tag types in the Community Template Gallery"
1. Search for "Simple Analytics"
1. Click "Add to workspace"
1. Click "Add" in the popup
1. Change some settings if needed
   - [Custom domain](/bypass-ad-blockers) ([see extra instructions below](#custom-domain))
   - [Collect DoNotTrack](/dnt)
   - [Events](/events)
1. Click "Choose a trigger to make this tag fire..."
1. Select "Initialization - All Pages"
1. Click "Save" to save the tag

Now you added the Simple Analytics Tag with a trigger. Next, you can preview or submit the changes and your page views will be collected in Simple Analytics. Make sure to have a website set up in Simple Analytics to collect the data.

## Custom domain

To set up our tag with a custom domain, you will need to add your custom domain to your permissions. In this video we explain how to do this:

{%
  include video.html
  controls="true"
  slug="google-tag-manager-custom-domain"
  formats="mov,mp4,ogg,webm,wmv"
  poster="poster.png"
%}

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact).
