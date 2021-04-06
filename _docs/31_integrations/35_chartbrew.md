---
title: How to visualize Simple Analytics data with Chartbrew
menu: Chartbrew
category: integrations
permalink: /import-simple-analytics-data-in-chartbrew
canonical: https://chartbrew.com/blog/how-to-visualize-simple-analytics-data-with-chartbrew/
---

In this tutorial, we are going to connect Simple Analytics' API, get different datasets, and create a dashboard in Chartbrew to show all this data.

[Chartbrew](https://chartbrew.com/) allows you to connect all your databases and APIs to create beautiful live charts and visualize your data. It supports public dashboards and helps you connect multiple data sources into one dashboard.

The part we're going to focus on here is creating a Chartbrew dashboard with data from the Simple Analytics API. In this tutorial, we are going to go through how to connect to the API, and then we are going to create a chart and a table view to display the data inside [Chartbrew](https://chartbrew.com/). For this tutorial, we are going to use the public data from the [simpleanalytics.com](https://simpleanalytics.com/simpleanalytics.com) site itself, but you can use your own website if you wish.

Grab your favorite brew, create a new project in Chartbrew and let's get started!

<img class="border" src="/images/chartbrew-create-new-dashboard.png" alt="Create new dashboard in Chartbrew" />

## Connect to the Simple Analytics API

We are going to follow the [Stats API](https://docs.simpleanalytics.com/api/stats) documentation to fetch the data we need for the charts. The documentation gives us the main URL that we can use to fetch the data:

```
https://simpleanalytics.com/simpleanalytics.com.json?version=4&fields=histogram
```

Head over to the connections menu in your new project in Chartbrew and create a new API connection. Fill in the details like in the screenshot below.

- Name: **SA API** (can be anything)
- Hostname: **https://simpleanalytics.com** (without any path)

<img class="border" src="/images/chartbrew-create-connection.png" alt="Create connection in Chartbrew" />

Note that for the hostname we only need to use https://simpleanalytics.com and you'll see why later. You can ignore the **Header** part if your data is public. In case you are using your own website and its data is private in Simple Analytics, you will have to add an authentication header. [Follow the documentation](https://docs.simpleanalytics.com/api/authenticate) to generate an API key if you don't already have one and then add a header to the Chartbrew connection like above.

Now that we have a connection, it's time to brew some charts!

## Create a time-series chart

Next, we are going to create a time-series chart showing the number of visitors and page views for the website. Head over to the dashboard of the new project and add a new chart called "Site stats" and then create a dataset called "Page views".

<img class="border" src="/images/chartbrew-create-data-set.png" alt="Create data set in Chartbrew" />

Once we have the first dataset, we can connect it to the Simple Analytics connection that we created earlier.

<img class="border" src="/images/chartbrew-make-request.png" alt="Make request in Chartbrew" />

<p class="caption">Click on "Make request" to configure the first API call</p>

In the next window, we can configure the API call we're making to the Simple Analytics connection. Copy the following in the **route** field and them press on "Make the request":

```
/simpleanalytics.com.json?version=4&fields=histogram
```

<img class="border" src="/images/chartbrew-test-request.png" alt="Test request in Chartbrew" />

<p class="caption">Making the first request to the API</p>

The data we get gives us a **histogram** array that contains the page views and visitors. The first dataset we created is for the Page Views so let's display this on the chart.

When you press "Done", you will see a straight line on the chart. This is because Chartbrew tries to do a **count** operation by default. Change the operation on the **Y-Axis** with "No operation" and the chart will show all the page views like in the API response.

<img class="border" src="/images/chartbrew-y-axis.png" alt="Y-axis in Chartbrew" />

<p class="caption">And we have a time-series that shows the page views</p>

To display the number of visitors we need to create a new dataset. Click on "Add a new dataset" and name it **Visitors**. We need to make the same API call we did previously, but instead of selecting **pageviews** as the **Y-Axis**, we select the **visitors**.

<img class="border" src="/images/chartbrew-add-visitors.png" alt="Add visitors as an extra dataset in Chartbrew" />

<p class="caption">Added Visitors as an extra dataset</p>

Here we go, a time-series chart that shows the page views and visitors. You can further customize the colors in the **Appearance** tab if you wish.

## Creating a table to show the referrals

Chartbrew can also show data in table views and this is useful for things like referrals, UTM sources, browsers, and more. You'll see more examples as we progress through the tutorial.

For starters, let's focus on getting the referrers. Create a new chart like we did previously and name this one **Referrals** and then a dataset with the same name. You should have something like this:

<img class="border" src="/images/chartbrew-make-request-again.png" alt="Make request again in Chartbrew" />

Click on "Make request" and add the following route in the field:

```
/simpleanalytics.com.json?version=4&fields=referrers
```

Proceed to send the request to the API and then click on the "table view" button like shown in the screenshot below. The table should load quickly after and we'll get another type of view.

<img class="border" src="/images/chartbrew-select-table.png" alt="Select table in Chartbrew" />

Like with the time-series chart above, we can add multiple datasets to the table view as well. For example, we can get useful insights from the UTM sources, so let's create a new dataset and call it **UTM sources**.

Repeat all the steps above, but change the route to the following:

```
/simpleanalytics.com.json?version=4&fields=utm_sources
```

<img class="border" src="/images/chartbrew-select-utm-sources.png" alt="Select UTM sources in Chartbrew" />

<p class="caption">Added two more datasets to the table view - UTM Sources and Pages</p>

## Sharing, embedding, and auto-updating

There are extra things you can do with the charts after you created them in Chartbrew. Head over to the dashboard and click on the individual chart menu to see all the options:

<img class="border" src="/images/chartbrew-chart-options.png" alt="Select chart options in Chartbrew" />

For example, you can embed charts on other websites. Here's a demo that you can interact with:

<iframe class="border" src="https://chartbrew.com/chart/362/embedded" allowTransparency="true" width="100%" height="400" scrolling="no" frameborder="0" style="background-color: #fff"></iframe>

That's it for this tutorial! You can go ahead and create more charts using Simple Analytics's [API documentation](https://docs.simpleanalytics.com/api/stats). Check which fields you can query for and put the data in other charts.

> [I created more charts and you can see them in the public dashboard here.](https://app.chartbrew.com/b/Simple_Analytics_305)

<img class="border" src="/images/chartbrew-dashboard.png" alt="Dashboard with Simple Analytics data in Chartbrew" />

## Next steps

Chartbrew becomes more powerful when you mix data from different data sources. On top of website analytics data that comes from Simple Analytics, you can have financial data, marketing campaigns data, or even data from your own custom APIs and databases.

- Connect Stripe's API to the dashboard and query for your finance data ([see tutorial](https://chartbrew.com/blog/how-to-create-a-stripe-dashboard-in-chartbrew/))
- Connect any PostgreSQL, MySQL, MongoDB database and see how your content evolves

This post was originally posted [at the Chartbrew blog](https://chartbrew.com/blog/how-to-visualize-simple-analytics-data-with-chartbrew/).

[Get started with Chartbrew](https://chartbrew.com).
