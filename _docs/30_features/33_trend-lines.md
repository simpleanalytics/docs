---
title: Trend lines
category: features
permalink: /trend-lines
redirect_from:
  - /trendlines
last_modified_at: 2022-10-21
---

Trend lines give you a quick overview of how your numbers are changing in the period shown in the charts.

### Curved trend lines with outliers excluded

The default in Simple Analytics is to show these curved trend lines, excluding outliers. It gives a bit more information than linear instead of curved trend lines. Curved trend lines use a [polynomial regression](https://en.wikipedia.org/wiki/Polynomial_regression) with an order of 2. It does not always play nice with outliers. To exclude them, we use an [interquartile range (IQR) x 1.5](https://en.wikipedia.org/wiki/Interquartile_range).

<img src="https://assets.simpleanalytics.com/docs/trend-lines/curved-excluding-outliers.png" alt="Curved trend lines with outliers excluded" class="border">

The dashed line shows which data is excluded. At the start and the end, the data is incomplete. We never include that data for the trend line. In the chart above, you see another dashed line; the month of July. That's an excluded outlier. It will not be included in the trend line (unless you change this [in your account settings](https://simpleanalytics.com/account#trendlines)).

### Curved trend lines with outliers included

Curved trend lines don't always play nice with outliers. By default, we exclude them. If you include them, you see a trend line like this:

<img src="https://assets.simpleanalytics.com/docs/trend-lines/curved-including-outliers.png" alt="Curved trend lines with outliers included" class="border">

### Linear trend lines with outliers included

The more basic trend line is linear. Just disable curved if you want to see these types of trend lines.

<img src="https://assets.simpleanalytics.com/docs/trend-lines/linear-including-outliers.png" alt="Linear trend lines with outliers included" class="border">

### Account settings

In [your account settings](https://simpleanalytics.com/account#trendlines), you can change the settings of your trend lines.

<img src="https://assets.simpleanalytics.com/docs/trend-lines/account-settings.png" alt="Account settings in Simple Analytics for trend lines" class="border">
