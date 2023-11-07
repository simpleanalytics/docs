---
title: Install Simple Analytics on other platforms
menu: Install on other platforms
category: install-script
permalink: /install-on-other-platforms
last_modified_at: 2022-11-04
---

## Platform guides

We try to make installing Simple Analytics as simple as possible. We want privacy to be accessible as possible. We don't require the need for a developer if you use any of the following tools.

Read our guides on how to install Simple Analytics on:

- [Google Tag Manager](/install-simple-analytics-with-google-tag-manager) <small>(source on [GitHub](https://github.com/simpleanalytics/google-tag-manager#readme))</small>
- [Wordpress](/install-simple-analytics-on-wordpress) <small>(source on [GitHub](https://github.com/simpleanalytics/wordpress-plugin#readme))</small>
- [Ghost](/install-simple-analytics-on-ghost)
- [CloudFlare](/install-simple-analytics-on-cloudflare) <small>(source on [GitHub](https://github.com/simpleanalytics/cloudflare-app#readme))</small>
- [WIX](/install-simple-analytics-on-wix)
- [Squarespace](/install-simple-analytics-on-squarespace)
- [Webflow](/install-simple-analytics-on-webflow)
- [Jimdo Creator](/install-simple-analytics-on-jimdo-creator)
- [MailerLite](/install-simple-analytics-on-mailerlite)
- [GoDaddy](/install-simple-analytics-on-godaddy)

> Are you missing your favorite platform? [Let us know!](https://simpleanalytics.com/contact) Happy to create a guide or plugin for you.

## Framework plugins

For most frameworks, you can include the script. We magically track page views, so you don't have to change your app code. [Read on how we do that](/trigger-custom-page-views). For some, we got requests to create a plugin for them.

{% assign currentDate = 'now' | date: '%s' %}
{% assign threeMonthsLater = '2023-02-07' | date: '%s' | plus: 7884000 %}  {# 7884000 is approximately the number of seconds in 3 months #}

Get our official plugins for these frameworks:

- [React](/install-simple-analytics-with-react) <small>(guide only)</small>
- [Ruby on Rails](/install-simple-analytics-with-ruby-on-rails) <small>(source on [GitHub](https://github.com/simpleanalytics/rubyonrails-plugin#readme))</small>
- [Gatsby](/install-simple-analytics-with-gatsby) <small>(source on [GitHub](https://github.com/simpleanalytics/gatsby-plugin#readme))</small>
- [Vue](/install-simple-analytics-with-vue) <small>(source on [GitHub](https://github.com/simpleanalytics/vue-plugin#readme))</small>
- [VuePress](/install-simple-analytics-with-vuepress) <small>(source on [GitHub](https://github.com/simpleanalytics/vuepress-plugin#readme))</small>
- [Nuxt.js](/install-simple-analytics-with-nuxt) <small>(guide only)</small>
- [Gridsome](/install-simple-analytics-with-gridsome) <small>(source on [GitHub](https://github.com/simpleanalytics/gridsome-plugin#readme))</small>
- [Django](/install-simple-analytics-with-django) <small>(source on [GitHub](https://github.com/simpleanalytics/django-plugin#readme))</small>
- [Analytics library](/install-simple-analytics-via-analytics-package) <small>(source on [GitHub](https://github.com/DavidWells/analytics/tree/master/packages/analytics-plugin-simple-analytics))</small>
- [Hugo](/install-simple-analytics-with-hugo) <small>(guide only)</small>
- [Next.js](/install-simple-analytics-with-next) <small>(guide only)</small>
- [Docusaurus](/install-simple-analytics-with-docusaurus) <small>(source on [GitHub](https://github.com/simpleanalytics/docusaurus-plugin#readme))</small>
- [iOS (Swift)](/install-simple-analytics-with-swift) <small>(source on [GitHub](https://github.com/simpleanalytics/swift-package#readme))</small> {% if currentDate < threeMonthsLater %}NEW{% endif %}

> Are you missing your favorite framework? [Let us know!](https://simpleanalytics.com/contact) Happy to create a plugin for you.
