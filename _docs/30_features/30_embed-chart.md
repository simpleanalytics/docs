---
title: Embed chart on your site
category: features
skip_pjax: true
permalink: /embed-chart-on-your-site
redirect_from:
  - /embed-graph-on-your-site
  - /embed
---

Simple Analytics allows you to embed a chart of your public website statistics on your website. In this chart we show you the visitors (<span id="visitors">...</span>) and page views (<span id="pageviews">...</span>) of simpleanalytics.com:

<div
  id="chart-id"
  data-hostname="simpleanalytics.com"
  style="aspect-ratio: 2/1"
  data-types="visitors,pageviews"
  data-page-views-selector="#pageviews"
  data-visitors-selector="#visitors">
  <p style="margin: 0;">Chart is not loading. It might be blocked by an ad-blocker.</p>
</div>
<script
  async
  src="https://scripts.simpleanalyticscdn.com/embed.js"
  data-chart-selectors="#chart-id,#chart-colors"
></script>

The chart above is highly customizable. You can overwrite colors, which data types to show, period to show, and much more.

> Want to built your own dashboard with your website data? Check out our [APIs](/api).

## Embed chart script

To include this chart, you'll need to add a script and some HTML to your website. The minimal working version of this code that you can copy into the HTML of your page:

```html
<div id="chart" data-hostname="example.com" style="aspect-ratio: 2/1">
  <p style="margin: 0">Loading chart...</p>
</div>
<script
  async
  data-chart-selectors="#chart"
  src="https://scripts.simpleanalyticscdn.com/embed.js"
></script>
```

> Make sure to replace `example.com` with your own website.

## Customize

The following parameters are customizable:

```html
<div
  id="chart"
  style="aspect-ratio: 2/1"
  data-hostname="example.com"
  data-start="2020-11-11"
  data-end="2021-11-11"
  data-types="visitors"
  data-page-views-selector="#pageviews"
  data-visitors-selector="#visitors"
  data-y-max="60000"
  data-timezone="Europe/Amsterdam"
  data-border-width="1"
  data-text-color="#ff6600"
  data-page-views-color="#ff6600"
  data-visitors-color="#cc2200"
  data-area-opacity="10"
  data-show-logo="true"
></div>
```

We recommend to keep the `style="aspect-ratio: 2/1"` to prevent the page from jumping when the chart is loading.

### Colors

If you leave the `data-text-color` empty, the chart will grab the text color from a paragraph and use that. It even works after you change your website to dark mode.

`data-area-opacity` is the opacity in percent of the areas below the line charts.

<div
  id="chart-colors"
  data-hostname="simpleanalytics.com"
  style="aspect-ratio: 2/1"
  data-types="visitors,pageviews"
  data-text-color="#ff6600"
  data-page-views-color="#ff6600"
  data-visitors-color="#cc2200"
  data-area-opacity="10">
  <p style="margin: 0;">Chart is not loading. It might be blocked by an ad-blocker.</p>
</div>

### Others

If you leave `data-timezone` empty, it will grab the time zone from the visitor.

The `border-width` is the width in pixels of the data lines in the chart.

You can hide the logo by adding `data-show-logo="false"`.

## Include multiple charts

```html
<!-- Chart 1 with data from simpleanalytics.com -->
<div
  id="chart-id-1"
  data-hostname="simpleanalytics.com"
  style="aspect-ratio: 2/1"
>
  <p style="margin: 0;">
    Chart is not loading. It might be blocked by an ad-blocker.
  </p>
</div>

<!-- Chart 2 with data from blog.simpleanalytics.com -->
<div
  id="chart-id-2"
  data-hostname="blog.simpleanalytics.com"
  style="aspect-ratio: 2/1"
>
  <p style="margin: 0;">
    Chart is not loading. It might be blocked by an ad-blocker.
  </p>
</div>

<!-- One script tag for multiple charts -->
<script
  async
  data-chart-selectors="#chart-id-1,#chart-id-2"
  src="https://scripts.simpleanalyticscdn.com/embed.js"
></script>
```

You can apply the `data-` settings from [customize](#customize) on the `<script>` as well to apply settings to all charts.

> When you include multiple charts on your website make sure you include `<script src="https://scripts.simpleanalyticscdn.com/embed.js"></script>` only once.

## Spikes

It happens that some data has huge spikes. This is great traffic-wise, but you might want to cut off the spike in the chart to make more sense out of your data before and after the spikes. You can change this with the `y-limit` parameter. To limit your chart to – let's say 50,000 page views – you can add it like this to your `<div>`-tag: `data-y-max="50000"`.

## Onload callback

```html
<script>
  function onLoad(ok) {
    if (ok) console.log("All charts loaded successfully");
    else {
      // Hide all elements that show charts
      // ...
    }
  }
</script>
<div id="chart" style="aspect-ratio: 2/1" data-hostname="example.com"></div>
<script
  async
  src="https://scripts.simpleanalyticscdn.com/embed.js"
  data-chart-selectors="#chart"
  data-onload="onLoad"
></script>
```

If you have other issues, <a href="https://simpleanalytics.com/contact">please let us know</a> because we love to help you! Do you want to access your stats with even more freedom? Use our [API](/api) for that.
