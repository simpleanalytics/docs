---
title: Collect events with Ruby
category: events
permalink: /events/ruby
hidden: true
last_modified_at: 2022-05-17
---

This is a draft of how to collect events with [Ruby](https://www.ruby-lang.org/en/). If you know how to improve it, please let us know.

> This is deprecated and only left for historical purposes.

Save below code as `simple_analytics_event.rb`:

```ruby
# simple_analytics_event.rb

require 'net/http'
require 'json'
require 'date'

class SimpleAnalyticsEvent
def self.trigger(event_name)
  new.trigger(event_name)
end

# EventData makes sure the data is corrent when sending to
# API endpoint
class EventData
  attr_reader: version,: ua,: platform,: hostname,: date,: events

  def initialize(events, user_agent = nil, platform = nil)
    @version = 1
    @ua = user_agent
    @platform = platform

    # use your own hostname here
    @hostname = "your.own.hostname.here"

    @date = Date.today
    @events = events
  end

  def to_h {
    version: version,
    ua: ua,
    platform: platform,
    hostname: hostname,
    date: date.strftime("%Y-%m-%d"),
    events: events
  }
  end
end
attr_reader: api_endpoint

def initialize
  @api_endpoint = "https://api.simpleanalytics.io/events"
end

def request_headers {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}
end

def post(data)
  uri = URI(api_endpoint)
  http = Net::HTTP.new(uri.host, uri.port)
  http.use_ssl = true
  request = Net::HTTP::Post.new(uri.path, request_headers)
  request.body = data.to_json

  begin
    response = http.request(request)
    puts "debug: #{response.body}"
    true
    rescue StandardError => e
      # net / http has notoriously hard exception handling,
      # read more: https: //stackoverflow.com/a/11802674
      puts e.inspect
      false
    end
  end

  def trigger(event, params = {})
    data = EventData.new([event])
    post(data.to_h)
  end
end
```

To test run this in your console:

```ruby
% irb
irb(main):001:0' require './simple_analytics_event'
=> true
irb(main):002:0> SimpleAnalyticsEvent.trigger('example_event')
debug: {"success":true,"duration_ms":1,"message":"Thank you","location":"Amsterdam"}
=> true
```

Make sure to include a user agent in the code because the request will fail otherwise.

Thanks to [Tuomas Jomppanen](https://www.tuomas.io/) for providing this example.
