---
title: Custom views
category: features
permalink: /custom-views
last_modified_at: 2026-09-07
---

Custom views help you to have permanent filters on your dashboard, merge multiple domains into one dashboard, or give others access to a limited subset of the data.

> You need to have the Team subscription to use custom views.

1. Start by [creating a custom view](https://dashboard.simpleanalytics.com/views/create).
2. Select the websites you want to include in the view. If you are part of multiple teams, you can only include websites from the same team in one custom view.
   ![Custom Views - Select Websites](https://assets.simpleanalytics.com/docs/dashboard/custom-views-01-select-websites.png)
3. Optionally, you can add filters to custom views. This can be useful if you want to exclude some pages or give someone access to only a subset of the website data.
   ![Custom Views - Add Filters](https://assets.simpleanalytics.com/docs/dashboard/custom-views-02-add-filters.png)
4. Create a name for the view.
   ![Custom Views - Name View](https://assets.simpleanalytics.com/docs/dashboard/custom-views-03-name-view.png)
5. After a custom view exists, open `https://dashboard.simpleanalytics.com/views/<your-view-slug>/edit` and go to the **Settings** step. These settings only apply to the view itself. They do not change any of the websites included in it.
   - **Visibility**: set the view's dashboard to private or public. When it is public, you can also hide top pages and hide the public dashboard from search engines. You need to be an admin or developer to change visibility.
   - **Number rounding**: use the account default, round numbers (for example 12k), or show exact numbers (for example 12,193). This only changes how numbers are displayed, the underlying data is never rounded. Showing exact numbers requires a plan that includes exact numbers.
   - **Time zone**: pick the time zone used for the dates and times shown in this view. It does not modify the underlying data.
