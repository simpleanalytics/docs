---
title: Data points
category: general
permalink: /data-points
excerpt: "We never track visitors so the data below is never linked to one specific visitor. Here is a list of data points we collect."
last_modified_at: 2022-04-14
---

Here is a list of data points we collect.

> [Go to our general overview](/what-we-collect) of what we collect.

With every page view we collect some data points. We never track visitors so the data below is never linked to one specific visitor.

Everything is collected within the browser except for the data points with an \*

| Data point       | What is it?                                                                | Example               |
| :--------------- | :------------------------------------------------------------------------- | :-------------------- |
| Timestamp        | Time and date of the visit                                                 | 2021-04-14 12:31:00   |
| Referrer         | The URL of the previous page linked to the page view [wiki][3]             | https://google.com/   |
| Website          | The website of the visit                                                   | example.com           |
| Path             | Path of the page view                                                      | /contact              |
| Original website | In case the website [is overwritten by a customer][4] we save the original | orginal-example.com   |
| Country          | Country collected via the time zone of the visitor                         | The Netherlands       |
| Language         | Language of the browser                                                    | en_US                 |
| Unique page view | True of false for if [visit is unique][2]                                  | true                  |
| Robot            | True of false for if the visitor is a robot                                | false                 |
| Time on page     | How long is the visitor on a page                                          | 2 minutes 5 seconds   |
| How far scrolled | Scrolled percentage on the page by the visitor                             | 60%                   |
| Browser name     | Browser of the visitor                                                     | Safari                |
| Browser version  | Browser of the visitor                                                     | 14.4.1                |
| OS name          | Operating system of the visitor                                            | Mac OS X              |
| OS version       | Operating system version of the visitor                                    | 13.2                  |
| Device type      | Device type of visitor                                                     | desktop/tablet/mobile |
| Screen height    | Full-screen height of visitor's device in pixels                           | 1440px                |
| Screen width     | Full-screen width of visitor's device in pixels                            | 900px                 |
| Viewport height  | Window height of visitor's browser in pixels                               | 720px                 |
| Viewport width   | Window width of visitor's browser in pixels                                | 1200px                |
| User agent       | User-agent string of the browser                                           | [see below][6]        |
| UTM source       | URL utm_source parameter of the page view [see below][5]                   | company-x             |
| UTM medium       | URL utm_medium parameter of the page view                                  | newsletter            |
| UTM campaign     | URL utm_campaign parameter of the page view                                | march_01              |
| UTM content      | URL utm_content parameter of the page view                                 | button_red            |
| UTM term         | URL utm_term parameter of the page view                                    | shoes                 |
| Page view id     | Identifier of the page view                                                | 918291910             |
| Script id        | Identifier of the embed script                                             | script_1              |
| Server id \*     | Identifier of our server                                                   | server_1              |
| Ingest time \*   | Time and date when the visit is saved on our server                        | 2021-04-14 12:31:01   |

\* Not collected in the browser but on our server

## UTM codes

UTM codes are bits of text you can add to a link that tell Simple Analytics (as well as other analytics tools) a little bit more information about each link. Here's a sample of what one looks like:

```
https://example.com/landing-page?utm_source=company-x&utm_medium=newsletter&utm_campaign=march
```

[Read the UTM guide](https://buffer.com/library/utm-guide/) at Buffer.

## User agents strings

Browsers or devices identify themselves to websites. They give themselves some kind of name. For example, a user agent can look like this ([wiki][1]):

```
Mozilla/5.0 (iPad; U; CPU OS 3_2_1) AppleWebKit/531.21.10 (KHTML, like Gecko) Mobile/7B40598
```

This could potentially have user specific information in them so we annonymise these user-agent strings. We replace long numbers with zeros.

After cleanup, it looks like this:

```
Mozilla/5.0 (iPad; U; CPU OS 3_2_0) AppleWebKit/531.21.0 (KHTML, like Gecko) Mobile/7B40000
```

In some browsers we collect browser name and operating system name without the user agent but via the [user agent client hints](https://wicg.github.io/ua-client-hints/).

[1]: https://en.wikipedia.org/wiki/User_agent
[2]: /explained/unique-visits
[3]: https://en.wikipedia.org/wiki/HTTP_referer
[4]: /overwrite-domain-name
[5]: #utm-codes
[6]: #user-agents-strings
