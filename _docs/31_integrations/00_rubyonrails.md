---
title: Install Simple Analytics with Ruby on Rails
hidden: true
category: integrations
permalink: /install-simple-analytics-with-ruby-on-rails
last_modified_at: 2022-04-14
---

This gem adds the [JavaScript Tracking Script](https://docs.simpleanalytics.com/script) to the `<head>` & `<body>` tag of your Ruby on Rails applications.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'simple_analytics_rails'
```

And then execute:

```bash
bundle install
```

Or install it yourself as:

```bash
gem install simple_analytics_rails
```

## Usage

After the gem is installed, it will automatically append the Simple Analytics JavaScript snippet before the `</head>` tag on your HTML pages.

However, you can also configure it via an initializer:

```ruby
# config/initializers/simple_analytics.rb
SimpleAnalyticsRails.configure do |configuration|
  # ==> Overwrite domain name
  # https://docs.simpleanalytics.com/overwrite-domain-name
  #
  # Default is ""
  configuration.hostname = "example.com"
  # ==> Hash mode
  # https://docs.simpleanalytics.com/hash-mode
  #
  # Default is ""
  configuration.mode = "hash"
  # ==> Do not track
  # https://docs.simpleanalytics.com/dnt
  #
  # Default is false
  configuration.collect_dnt = false
  # ==> Ignore pages
  # https://docs.simpleanalytics.com/ignore-pages
  #
  # Default is ""
  configuration.ignore_pages = "/search/*,/account/*,/vouchers"
  # ==> Override variable used for JavaScript Events
  # https://docs.simpleanalytics.com/events#the-variable-sa_event-is-already-used
  #
  # Default is "sa_event"
  configuration.sa_global = "sa_event"
  # ==> Trigger custom page views
  # https://docs.simpleanalytics.com/trigger-custom-page-views#use-custom-collection-anyway
  #
  # Default is true
  configuration.auto_collect = true
  # ==> Onload Callback
  # https://docs.simpleanalytics.com/trigger-custom-page-views#use-custom-collection-anyway
  #
  # Default is ""
  configuration.onload_callback = "onloadCallback()"
  # ==> Custom Domain
  # https://docs.simpleanalytics.com/bypass-ad-blockers
  #
  # Default is ""
  configuration.custom_domain = "custom.domain.com"
  # ==> Inject JavaScript To Head
  # You can disable the automatic JavaScript injection if you'd like.
  #
  # Default is true
  configuration.enabled = Rails.env.production?
end
```
