---
title: Server side tracking
category: script
permalink: /server-side-tracking
---

When you send data from your server to Simple Analytics you need to provide a few fields:

| Field       | Type    | Example                 | Required  | Explanation                                                                                        |
| ----------- | ------- | ----------------------- | --------- | -------------------------------------------------------------------------------------------------- |
| url         | string  | https://example.com/    | yes       | The current URL of the page                                                                        |
| ua          | string  | Mozilla/5.0 ...         | sometimes | We use this if there is no User Agent present in the headers                                       |
| width       | number  | 1440                    | no        | The viewport width of the device (not possible via server)                                         |
| unique      | boolean | true                    | no        | This tells us if this visit is unique. Don't send this field if you don't detect unique page views |
| timezone    | string  | Europe/Amsterdam        | no        | The time zone of the current user so we can detect the country                                     |
| referrer    | string  | https://duckduckgo.com/ | no        | The referrer of the current page (if any)                                                          |
| urlReferrer | string  | blog                    | no        | The value of `?ref=...` in the URL ([more info](/how-to-use-url-parameters))                       |

> If we find a User Agent in the headers, we will use that.

Please strip all sensitive data from your URLs. We do this at our end as well, but it's better to have this done on your server.

<style>
  table td, table th {
    white-space: nowrap;
  }
  @media screen and (min-width: 768px) {
    table tr td:last-of-type, table tr th:last-of-type {
      white-space: inherit;
    }
  }
</style>

Our API is located at `https://queue.simpleanalyticscdn.com/post`.

The request should be a POST with JSON like this:

```json
{
  "url": "https://example.com/",
  "ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:70.0) Gecko/20100101 Firefox/70.0",
  "width": 1440,
  "unique": true,
  "timezone": "Europe/Amsterdam"
}
```

<details markdown="1">
  <summary>Send request in Node.js</summary>

```js
const https = require("https");

const data = JSON.stringify({
  url: "https://example.com/",
  ua:
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:70.0) Gecko/20100101 Firefox/70.0",
  width: 1440,
  unique: true,
  timezone: "Europe/Amsterdam",
});

const options = {
  hostname: "queue.simpleanalyticscdn.com",
  path: "/post",
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Content-Length": data.length,
  },
};

const req = https
  .request(options, (res) => {
    let data = "";

    console.log("Status Code:", res.statusCode);

    res.on("data", (chunk) => {
      data += chunk;
    });

    res.on("end", () => {
      console.log("Body: ", JSON.parse(data));
    });
  })
  .on("error", (err) => {
    console.log("Error: ", err.message);
  });

req.write(data);
req.end();
```

</details>

The response for this request will look like this:

```json
{
  "success": true,
  "duration_ms": 1,
  "message": "Thank you",
  "location": "Reykjavík, Iceland"
}
```

[Let us know](https://simpleanalytics.com/contact) if we can help you with anything!
