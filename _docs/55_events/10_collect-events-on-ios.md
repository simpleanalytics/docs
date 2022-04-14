---
title: Collect events on iOS with Swift
menu: Collect events on iOS
category: events
permalink: /events/ios
last_modified_at: 2022-04-14
---

This is a draft of how to track events with iOS. If you know how to improve it, please let us know.

```swift
import Foundation

@objc
class Analytics: NSObject {

    private struct EventData: Encodable {
        let v: Int = 1
        let ua: String = "ios"
        let platform: String = "ios"
        let hostname: String = "your.hostname.com"
        let date: Date = Date()
        let events: [String]
    }

    private static let encoder: JSONEncoder = {
        let encoder = JSONEncoder()
        encoder.keyEncodingStrategy = .convertToSnakeCase
        encoder.dateEncodingStrategy = .formatted(dateFormatter)
        return encoder
    }()

    private static let dateFormatter: DateFormatter = {
        let formatter = DateFormatter()
        formatter.dateFormat = "yyyy-MM-dd"
        return formatter
    }()

    @objc
    static func log(eventName: String) {
        Analytics.log(eventNames: [eventName])
    }

    @objc
    static func log(eventNames: [String]) {
        let eventData = EventData(events: eventNames)

        guard let jsonData = try? encoder.encode(eventData) else {
            print("Error while logging event: unable to convert event to JSON")
            return
        }

        let url = URL(string: "https://api.simpleanalytics.io/events")!
        var request = URLRequest(url: url)
        request.httpMethod = "POST"
        request.httpBody = jsonData
        request.addValue("application/json", forHTTPHeaderField: "Content-Type")
        request.addValue("application/json", forHTTPHeaderField: "Accept")

        let task = URLSession.shared.dataTask(with: request) { (data, response, error) in
            if let error = error {
                print("Error while logging event: \(error)")
            }
        }
        task.resume()
    }

}
```

Make sure to include a user agent in the headers of the request. This is not included in the example above.

Thanks to Rutger Bresjer from [Woost Technologies](https://woost.tech/) for providing above code example.
