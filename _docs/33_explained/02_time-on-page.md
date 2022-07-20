---
title: Time on page explained
menu: Time on page
category: explained
permalink: /explained/time-on-page
last_modified_at: 2022-04-14
---

_Time on page_ is an important metric to measure how engaged your visitors are with your content. But in most analytics tools, there is something very wrong with that metric. You might think when using Simple Analytics: "These numbers are lower than I'm used to", well, that's probably right.

We care about numbers being close to real-world scenarios. With _time on page_ for example it makes a lot of sense to exclude the duration when visitors are not interacting with the page.

## Google Analytics

Take Google Analytics for example. Let's say you have Google Analytics installed on `yourwebsite.com`. Google starts the timer on the first page you land on (like it should). After that, they keep the time running until the visitors navigate to a new page on the same website. If a visitor doesn't navigate to another page on the same website the _time on page_ will not be recorded at all:

![](/images/time-on-page-ga-stop.png)

In the illustration above you would expect to at least record the time for the first page (you see in browsers 1 & 3). But instead, you don't get any _time on page_ for this situation in Google Analytics. It's because, by default Google Analytics does not send a request at the end of the visit but only at the beginning. They have no way of knowing how long a visitor will be on the page at the beginning. They can however calculate the time between the first page and the following page (on the same domain). In that case, their flow works like this:

![](/images/time-on-page-ga.png)

In this case, the visitor visits 2 pages (`page1` and `page2`) on `yourwebsite.com` and 1 page on `otherwebsite.com`. Because the visitor now visits another page on the `yourwebsite.com` domain Google knows how much time there was between the first page and the second page. The time between the two pages is the _time on page_ for `page1`. In this situation, Google only knows the _time on page_ for the first page, not for the second. Google Analytics will show that a visitor was on `page1` for 35 seconds instead of 15 seconds. It will not show anything for `page2` which the visitor was on for 5 seconds.

### What does go wrong?

- It should record _time on page_ even if you only visit one page
- It should not record the 20 seconds of a different website
- It should record the _time on page_ of the last page visited as well

## Simple Analytics

Simple Analytics detects when a user navigates to a different website (in a new tab). We stop the timer when we detect that, so the duration of your visitors doesn't count towards the total duration on a page. Simple Analytics records _time on page_ for every page your visitors visit.

![](/images/time-on-page-sa.png)

In the above example, we get the expected result: a visitor was 15 seconds on `page1` and 5 seconds on `page2`. Nothing more, nothing less. That's what you can expect from Simple Analytics. We make sure your data is as close to real-world scenarios as possible.

{%
  include video.html
  slug="time-on-page"
  formats="mp4,ogg,webm,wmv"
  poster="video.png"
%}

## Median versus average

The dataset of _time on page_ can have a lot of outliers. There could be a visitor that keeps a website open before leaving the house. In this case, the _time on page_ will be very high. As a privacy-friendly company, we don't want to track mouse movement or other signs of webpage interaction to detect if the user is still consuming the content. This means that the _time on page_ can be very high. Let's say that the visitor comes back after 2 hours and closes the website. The dataset now contains a super high number. This usually happens with data like this. So what can you do about those outliers?

At Simple Analytics we researched what the best way would be to have an accurate number representing the _time on page_ without including those extreme outliers. Where other tools use average we calculate the median for all the _time on page_ entries.

| Page view #                 | 1   | 2   | 3   | 4   | 5    |
| --------------------------- | --- | --- | --- | --- | ---- |
| _Time on page_ (in seconds) | 10  | 20  | 15  | 10  | 1000 |

When you calculate the average you sum all numbers and divide it by the amount of page views. 10 + 20 + 15 + 10 + 1000 = 1055. 1055 / 5 = 211. **The average for _time on page_ for all 5 page views is 211 seconds.**

When calculating the median, you sort the numbers from low to high and pick the middle number. In this case, we sort the numbers like this: 10, 10, 15, 20, 1000. Then we pick the middle number: 15. **The median for all 5 page views is 15 seconds.**

We believe (and our customers with us) the more accurate number for the above dataset is 15 seconds. Those 1000 seconds represent likely somebody that left their computer running while not actively interacting with the website.

[Read the discussion](https://github.com/simpleanalytics/roadmap/issues/100) we had with our customers on GitHub.

### Bounce rate and bots

To make the _time on page_ more accurate, we exclude the page views with a _time on page_ **lower than 5 seconds**. We see those visits as bounced visits and don't include them in the _time on page_ metric. Page views that have a _time on page_ lower than 5 seconds will be visible all other metrics and charts. Just not included in the _time on page_ metric.

We exclude bots from all our stats (although you have the [ability to download them](/export-data)).

Have any questions? [Ask away!](https://simpleanalytics.com/contact)
