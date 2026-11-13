---
title: Filters
category: features
permalink: /filters
last_modified_at: 2026-11-13
---

How can we make it easy to find that data about that specific page/referrer/UTM code? Well, we created filters just for that. With a few clicks, you will find the data you are looking for.

{%
  include video.html
  slug="filters"
  formats="mp4,ogg,webm,wmv"
  poster="video.png"
%}

## Filter on values

Click a value in a list of your dashboard, like a page, referrer, country, UTM code, browser or device, to only see the stats for it. Click more values in the same list to add them. You then see the data that matches any of them, like visitors from Germany or France.

Filters in different lists work together. With Germany and your pricing page selected, you see the visitors from Germany on your pricing page.

Visits without a referrer show as _(direct)_ in the **Referrals** list. Click on _(direct)_ to filter your dashboard on those visits.

## Change your filters

Your filters show above the chart. For every filter you can:

- Click **=** to change it to **≠** (not equal). You then see everything except the values of that filter. Click again to change it back.
- Click its values to pause the filter, and click again to turn it back on. This way you can compare with and without a filter, without selecting everything again.
- Click the cross to remove it.

The **=** button on the right changes all your filters at once: it shows everything except these filters. **Clear** removes them all.

## Search in a list

Looking for values that have something in common, like all pages with `blog` in their path? Type it in the search box of a list. Your dashboard then only shows the data of the values that contain your search. A search shows next to your other filters, where you can change it to _does not contain_.

## Save your filters

Do you use the same filters often? Click the star on the right of your filters, give them a name and click **Save**. The same menu lists the filters you saved, to apply or delete them.

Saved filters are yours: other members of your team don't see them. You save them per website or [custom view](/custom-views). For filters that everybody sees and can't turn off, use a custom view.

## Paid and organic search

Click a search engine in the **Referrals** list, like Google or Bing, to see its **Paid** and **Organic** visits. Paid visits landed on your website with an ad click ID in the URL, like `gclid` for Google Ads or `msclkid` for Microsoft Advertising. Organic visits came from the search engine without one. Click **Paid** or **Organic** to filter your dashboard on those visits.

We only collect the names of these URL parameters, not their values, and only with [version 12 of our script](/script/v12) or `latest.js`. That's why the split starts on October 29, 2026. Visits we can't tell apart count as organic, for example from before that date or collected with the [light script](/light).

## Filters in the API and AI apps

AI apps that you [connect with MCP](/mcp) and the [Tools API](/api/tools) use the same filters, including the ones you saved. See [filters for tools](/tools#filters). The [Stats API](/api/stats) has [its own filters](/api/stats#query-parameters).

Go to [your dashboard](https://simpleanalytics.com/select-website) and start playing with filters.
