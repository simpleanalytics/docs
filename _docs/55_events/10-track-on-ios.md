---
title: Track events in iOS via Swift or Objective-C
menu: Track events in iOS
category: events
order: 10
permalink: /events/ios
---

> This is a draft of how to track events with iOS. If you know how to improve it, please let us know.

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
