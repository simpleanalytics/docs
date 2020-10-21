---
title: Embed graph on your site
category: features
skip_pjax: true
permalink: /embed-graph-on-your-site
---

Simple Analytics has a script which you can use to embed public website statistics.

> Do you want to access your stats with even more freedom? Use our [API](/api) for that!

```html
<p>
  This website has <span id="pageviews"></span> page views in the last month.
</p>
<div
  data-sa-graph-url="https://simpleanalytics.com/example.com?color=75b5aa"
  data-sa-page-views-selector="#pageviews"
>
  <p>
    Ad blockers don't like the Simple Analytics embed, disable yours to view
    this graph.
  </p>
</div>
<script src="https://scripts.simpleanalyticscdn.com/embed.js"></script>
```

> Change `example.com` to your own website

## Example

<p>Simple Analytics has <span id="pageviews">...</span> page views in the last month.</p>
<div data-sa-graph-url="https://simpleanalytics.com/simpleanalytics.com?color=FF4F64" data-sa-page-views-selector="#pageviews">
  <p>Ad blockers don't like the Simple Analytics embed, disable yours to view this graph.</p>
</div>
<script src="https://scripts.simpleanalyticscdn.com/embed.js"></script>

## Customize

You can give the graphs different colors by adding `?color=75b5aa` to the url of the `data-sa-graph-url` attribute. If you like to show the total page views you can use the `data-sa-page-views-selector` attribute. It will be filled via JavaScript `textContent` attribute (so it only works on text tags like `span`, `p`, `h2`).

You can just copy paste links from the normal dashboard, like these:

- `https://simpleanalytics.com/example.com`
- `https://simpleanalytics.com/example.com/contact` (stats of contact page)
- `https://simpleanalytics.com/example.com/` (stats of home page)
- `https://simpleanalytics.com/example.com?color=ff6600`
- `https://simpleanalytics.com/example.com?start=2018-09-17&end=2018-09-23`

> If you include multiple graphs on your website make sure you include `<script src="https://scripts.simpleanalyticscdn.com/embed.js"></script>` only once.

## Spikes

It happens that some data has huge spikes. This is great traffic wise, but you might want to cut off the spike in the graph to make more sense out of your data before and after the spikes. You can change this with the `y-limit` parameter. To limit your graph to – let's say 50,000 page views – you can add it like this: `https://simpleanalytics.com/example.com?y-limit=50000` .

## Scaling issues

Sometimes the graph does not stretch to the full page width. This can be caused by adding the `div` with the `data-sa-graph-url`-attribute in a flex element with `align-items: center`. This makes the div not stretch to the full width anymore. It can be solved by adding `align-self: stretch` to the `div` with the `data-sa-graph-url`-attribute. See this example:

```html
<div class="your-parent-class">
  <p>
    This website has <span id="pageviews"></span> page views in the last month.
  </p>
  <div
    class="your-graph-class"
    data-sa-graph-url="https://simpleanalytics.com/example.com?color=75b5aa"
    data-sa-page-views-selector="#pageviews"
  >
    <p>
      Ad blockers don't like the Simple Analytics embed, disable yours to view
      this graph.
    </p>
  </div>
</div>

<script src="https://scripts.simpleanalyticscdn.com/embed.js"></script>

<style>
  .your-parent-class {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .your-graph-class {
    align-self: stretch; /* This is the needed styling */
  }
</style>
```

If you have other issues, <a href="https://simpleanalytics.com/contact?ref=docs.simpleanalytics.com">please let us know</a> because we love to help you! Do you want to access your stats with even more freedom? Use our [API](/api) for that.
