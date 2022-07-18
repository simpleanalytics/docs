---
title: Ignore metrics
category: script
permalink: /ignore-metrics
hidden: true
last_modified_at: 2022-07-18
---

Our script does only collect non-personal data. But some customers might want to limit [what we collect](/what-we-collect) even more. That's why we created the ignore metrics feature.

| Metric              | Slug           | Inferrered metric      |
| ------------------- | -------------- | ---------------------- |
| Referrer            | `referrer`     |                        |
| UTM codes           | `utm`          | [`ref` param][0]       |
| Country / time zone | `country`      |                        |
| Session IDs         | `session`      |                        |
| Time on page        | `timeonpage`   | Data point ID, Page ID |
| Scrolled            | `scrolled`     | Data point ID, Page ID |
| User Agent          | `useragent`    |                        |
| Screen size         | `screensize`   |                        |
| Viewport size       | `viewportsize` |                        |
| Language            | `language`     |                        |

[0]: /how-to-use-url-parameters#using-a-url-parameter

<style>
  /* Apply styling to first table */
  .content div.table-wrapper {
    overflow: auto;
  }
  .content div.table-wrapper td {
    white-space: nowrap;
  }

  .content table td,
  .content table th {
    font-size: 14px;
  }
</style>

[See page](/metrics) where we explain those metrics.

## Script setting `data-ignore-metrics`

You can enable this feature by adding `data-ignore-metrics=...` to our script embed:

```html
<script
  data-ignore-metrics="session"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
/>
```

In this case, it will not collect [a Session ID](/metrics#ids).

## Comma separated

If you have multiple metrics you want to ignore you can separate them with a comma:

```html
<script
  data-ignore-metrics="timeonpage,scrolled"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
/>
```

## Ignore all metrics

To ignore all metrics that you can ignore, you can use this embed script:

```html
<script
  data-ignore-metrics="referrer,utm,country,session,timeonpage,scrolled,useragent,screensize,viewportsize,language"
  src="https://scripts.simpleanalyticscdn.com/latest.js"
/>
```

Need any help? We love to help you set up your script. Don't hesitate to [contact us](https://simpleanalytics.com/contact). Silly questions don't exist.
